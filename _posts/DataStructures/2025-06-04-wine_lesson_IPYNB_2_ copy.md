---
layout: post
title: Wine Lesson
categories: ['AP CSA']
description: Wine ML Lesson Lesson
permalink: /wine_lesson
toc: False
comments: True
---

# Using Tablesaw, Smile, and Weka to Drink Tasty Wine 🍷

Many say that wine is very good. Some people make a profession out of tasting the best wine. But the objectivity of computers trumps the fickle and subjective nature of human taste buds. Let us now find what is objectively the best wine.

## Prerequisites

### Dataset

We first need to download our dataset. Run the following set of commands in your terminal, or run the Java code in the next code cell.
```bash
# Change these variables if you want!
$DATA_DIR=~/wine-quality-dataset
$WINE_ZIP_DOWNLOAD=/tmp/wine-quality-dataset.zip

# Download and extract the wine dataset
curl -L -o $WINE_ZIP_DOWNLOAD https://www.kaggle.com/api/v1/datasets/download/yasserh/wine-quality-dataset
mkdir -p $DATA_DIR
unzip -o $WINE_ZIP_DOWNLOAD -d $DATA_DIR
```


```Java
import java.io.*;
import java.net.*;
import java.nio.file.*;
import java.util.zip.*;

public class DownloadWine {
    public static void main(String[] args) {
        // Change these variables if you want!
        String wineDir = System.getProperty("user.home") + "/wine-dataset";
        String wineZipDownload = "/tmp/wine.zip";

        try {
            // Download and extract the Wine dataset
            downloadFile("https://www.kaggle.com/api/v1/datasets/download/yasserh/wine-quality-dataset", wineZipDownload);
            Files.createDirectories(Paths.get(wineDir));
            unzipFile(wineZipDownload, wineDir);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void downloadFile(String urlStr, String dest) throws IOException {
        URL url = new URL(urlStr);
        HttpURLConnection httpConn = (HttpURLConnection) url.openConnection();
        httpConn.setRequestProperty("User-Agent", "Mozilla/5.0");
        httpConn.setRequestMethod("GET");

        try (InputStream in = httpConn.getInputStream();
             FileOutputStream out = new FileOutputStream(dest)) {
            byte[] buffer = new byte[4096];
            int bytesRead;

            while ((bytesRead = in.read(buffer)) != -1) {
                out.write(buffer, 0, bytesRead);
            }
        }
    }

    private static void unzipFile(String zipFilePath, String destDirectory) throws IOException {
        try (ZipInputStream zipIn = new ZipInputStream(new FileInputStream(zipFilePath))) {
            ZipEntry entry;

            while ((entry = zipIn.getNextEntry()) != null) {
                File filePath = new File(destDirectory, entry.getName());

                if (entry.isDirectory()) {
                    // Create directory if it doesn't exist
                    if (!filePath.isDirectory() && !filePath.mkdirs()) {
                        throw new IOException("Failed to create directory " + filePath);
                    }
                } else {
                    // Ensure parent directories exist
                    File parent = filePath.getParentFile();
                    if (parent != null && !parent.exists()) {
                        if (!parent.mkdirs()) {
                            throw new IOException("Failed to create directory " + parent);
                        }
                    }

                    // Write file content
                    try (BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(filePath))) {
                        byte[] bytesIn = new byte[4096];
                        int read;
                        while ((read = zipIn.read(bytesIn)) != -1) {
                            bos.write(bytesIn, 0, read);
                        }
                    }
                }
                zipIn.closeEntry();
            }
        }
    }
}

DownloadWine.main(null);
```

### Dependencies

Let's start by installing the necessary dependencies (our three lovely libraries: tablesaw, smile, and weka).

What do they do?
- Tablesaw -> Loads and stores data as **dataframes** (comparable to the pandas library in Python)
- SMILE -> Provides powerful **machine learning algorithms** and tools for data analysis in Java
  - SMILE stands for Statistical Machine Intelligence and Learning Engine (crazy yap name) 
- Weka -> Another popular **machine learning toolkit** with a focus on easy-to-use interfaces and classic algorithms
  - More high-level than smile and slightly less features but it's easier to use

These let us load and analyze data in Java, and train ML models to predict data too.


```Java
// Add Tablesaw (Java data analysis library)
%maven tech.tablesaw:tablesaw-core:0.43.1
%maven tech.tablesaw:tablesaw-jsplot:0.43.1
```


```Java
// Add Smile (because I want you to smile :))
%maven com.github.haifengl:smile-core:3.0.1
%maven com.github.haifengl:smile-data:2.6.0

// Add Weka (machine learning library)
%maven nz.ac.waikato.cms.weka:weka-stable:3.8.6
```

## Time to Do Stuff

### Tablesaw - Loading and Analyzing Data

Let's start by using tablesaw to load our wine quality dataset and output some information about it. 

> Why use tablesaw? When you have **structured data** (basically just things where you know the format of the data beforehand), libraries like tablesaw make it super easy to work with the data. In this case, we have structured data because we have a specific set of properties of the wine every time, unlike in something like an image, which is **unstructured**.


```Java
import tech.tablesaw.api.*;
import tech.tablesaw.io.csv.CsvReadOptions;

CsvReadOptions options = 
	CsvReadOptions.builder(System.getProperty("user.home") + "/wine-dataset/WineQT.csv")
		.separator(';')
		.build();

Table wine = Table.read().usingOptions(options);

System.out.println(wine.structure());
System.out.println(wine.shape());
wine.first(5);
```

In our code, we loaded the file at `~/wine-dataset/WineQT.csv` (open the file and see for yourself!) and we converted it to a **tablesaw table**.

Tablesaw can output a lot of information about the table, as we saw above, like the structure and shape.

We can also output some plots to show some information!


```Java
// Remove the second parameter if you want it to show directly rather than to a file, it doesn't work in WSL
Figure hist = Histogram.create("Alcohol", wine.numberColumn("alcohol"));
Figure scatter = ScatterPlot.create("Alcohol vs Quality", wine, "alcohol", "quality");

// uncomment to show directly in a GUI
Plot.show(hist);
Plot.show(scatter);
```

From these graphs, we can get a little information, like the fact that alcohol content doesn't seem to be the greatest predictor of wine quality.

### Smile - Predicting Wine Quality from Wine Data

Now we can solve the million dollar question - how can we ensure that we never have to taste terrible wine ever again?

We can use SMILE to train a **random forest**, a type of machine learning model.

However, SMILE doesn't take in tablesaw tables. It instead takes in its own class called DataFrame, so we need to first convert our data to that format.

> Note: we'll call the information about the wine **features**, and we'll say that these would be along our x-axis. We can call the quality of the wine our **target**, since that is what we want to know about it.


```Java
import smile.classification.*;
import smile.data.*;

String[] featureNames = wine.columnNames().toArray(String[]::new);
double[][] data = wine.as().doubleMatrix();
DataFrame df = DataFrame.of(data, featureNames);

// we want our quality to be an integer prediction for SMILE because it is a classification task
IntVector quality = IntVector.of("quality", df.doubleVector("quality").stream()
    .mapToInt(d -> (int) d)
    .toArray());
df = df.drop("quality").merge(quality);
```

Now, we need to split our dataset into two parts: one for training our model and one for testing our model. We'll set 80% of our data as training data and 20% as testing.


```Java
int n = df.nrow();
int[] indices = IntStream.range(0, n).toArray();
MathEx.permutate(indices); 

int splitIndex = (int)(n * 0.75);
int[] trainIdx = Arrays.copyOfRange(indices, 0, splitIndex);
int[] testIdx = Arrays.copyOfRange(indices, splitIndex, n);

DataFrame trainDf = df.select(trainIdx);
DataFrame testDf = df.select(testIdx);
```

Now we can finally train the model!


```Java
RandomForest rf = RandomForest.fit(Formula.lhs("quality"), trainDf);
```

Now let's test how accurate our model is!


```Java
int[] yTrue = testDf.stream().mapToInt(r -> r.getInt("quality")).toArray();
int[] yPred = testDf.drop("quality")
    .stream()
    .mapToInt(rf::predict)
    .toArray();


double accuracy = Accuracy.of(yTrue, yPred);
System.out.printf("Model Accuracy: %.2f%%%n", accuracy * 100);

```

`yTrue` represents the actual qualities, while `yPred` represents our model's prediction of the wine quality.

### Weka - Another Way to Make Classification Models

The weka library also allows us to make machine learning models. We ultimately do many of the same steps.

Let's start by converting our Tablesaw `Table` to a Weka `Instance`, just like how we had converted `Table` to `DataFrame` earlier.


```Java
import weka.core.*;
import weka.classifiers.trees.RandomForest;
import weka.classifiers.Evaluation;
import java.util.ArrayList;


ArrayList<Attribute> attributes = new ArrayList<>();
for (String col : wine.columnNames()) {
    if (!col.equals("quality")) {
        attributes.add(new Attribute(col));
    }
}

// we make an int column for the quality bc it is the classification
IntColumn qualityCol = (IntColumn) wine.intColumn("quality");
int minQuality = qualityCol.min();
int maxQuality = qualityCol.max();
ArrayList<String> qualityVals = new ArrayList<>();
for (int i = minQuality; i <= maxQuality; i++) {
    qualityVals.add(String.valueOf(i));
}
attributes.add(new Attribute("quality", qualityVals));

Instances wData = new Instances("Wine", attributes, wine.rowCount());
wData.setClassIndex(wData.numAttributes() - 1); // ok so this sets the last attribute (quality) as the target variable during classification

for (int i = 0; i < wine.rowCount(); i++) {
    double[] vals = new double[wData.numAttributes()];
    for (int j = 0; j < wine.columnCount() - 1; j++) {
        vals[j] = wine.column(j).getDouble(i);
    }
    vals[wData.numAttributes() - 1] = qualityVals.indexOf(String.valueOf(qualityCol.get(i)));
    wData.add(new DenseInstance(1.0, vals));
}
```

This code does the same thing as before: converts the table into a different format and turns the quality column into a column of integers.

Now, let's split the data into our training and testing data, just like last time.


```Java
// same 80/20 split as before
int trainSize = (int) Math.round(wData.numInstances() * 0.8);
int testSize = wData.numInstances() - trainSize;
Instances train = new Instances(wData, 0, trainSize);
Instances test = new Instances(wData, trainSize, testSize);
```

Now, let's finally train our random forest model, except this time it'll be using weka instead of smile.

> Should you use Weka or SMILE? For the most part, this is just personal preference. You can create powerful ML models with both libraries, and for the most part, they have relatively similar features and work pretty similarly. Note that SMILE is also an application which can be used to train models more easily, and has some more features, but Weka is also pretty straightforward to use. For the most part just try using both and see which one you like better.


```Java
RandomForest wekaRf = new RandomForest();
wekaRf.buildClassifier(train);
```

Now, let's see how well our model did!


```Java
Evaluation eval = new Evaluation(train);
eval.evaluateModel(wekaRf, test);

System.out.printf("Weka RandomForest Accuracy: %.2f%%%n", eval.pctCorrect());
```
