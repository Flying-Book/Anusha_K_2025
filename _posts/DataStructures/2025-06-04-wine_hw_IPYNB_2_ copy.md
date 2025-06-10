---
layout: post
title: Wine HW
categories: ['AP CSA']
description: Wine ML Lesson HW
permalink: /wine_hw
toc: False
comments: True
---

# Wine Quality Analysis - Homework Assignment 🍷📊

In this homework, you'll analyze wine quality data and build machine learning models. You'll use Tablesaw for data analysis and both SMILE and Weka for machine learning.

## Learning Objectives
- Load and explore wine quality datasets
- Create visualizations to understand data patterns
- Build and compare machine learning models
- Make predictions on wine quality

## Setup
Make sure you have the wine dataset at `~/wine-dataset/WineQT.csv`


```python
// Dependencies
%maven tech.tablesaw:tablesaw-core:0.43.1
%maven tech.tablesaw:tablesaw-jsplot:0.43.1
%maven com.github.haifengl:smile-core:3.0.1
%maven com.github.haifengl:smile-data:2.6.0
%maven nz.ac.waikato.cms.weka:weka-stable:3.8.6

// Imports
import tech.tablesaw.api.*;
import tech.tablesaw.io.csv.CsvReadOptions;
import tech.tablesaw.plotly.api.*;
import tech.tablesaw.plotly.components.Figure;
import tech.tablesaw.aggregate.AggregateFunctions;
import smile.classification.*;
import smile.data.*;
import smile.data.formula.Formula;
import smile.data.vector.IntVector;
import smile.math.MathEx;
import smile.validation.metric.Accuracy;
import weka.core.*;
import weka.classifiers.trees.RandomForest;
import weka.classifiers.Evaluation;
import java.util.ArrayList;
import java.util.stream.IntStream;
import java.util.Arrays;

// Load the wine dataset
CsvReadOptions options = 
    CsvReadOptions.builder(System.getProperty("user.home") + "/wine-dataset/WineQT.csv")
        .separator(';')
        .build();

Table wine = Table.read().usingOptions(options);

System.out.println("Dataset loaded: " + wine.rowCount() + " rows, " + wine.columnCount() + " columns");
System.out.println("First 5 rows:");
System.out.println(wine.first(5));
```

## Question 1: Data Exploration (2 parts)
Complete the code below to explore the wine dataset.


```python
// Part A: TODO - Display summary statistics for the wine dataset
System.out.println("Summary Statistics:");
System.out.println(wine.summary());

// Part B: TODO - Create a histogram of wine quality distribution
Figure qualityHist = Histogram.create(
    "Wine Quality Distribution",
    wine.categoricalColumn("quality")
);
Plot.show(qualityHist);


// Part B continued: TODO - Create a scatter plot of alcohol vs quality
Figure alcoholScatter = ScatterPlot.create(
    "Alcohol vs Quality",
    wine.numberColumn("quality"),
    wine.numberColumn("alcohol")
);
Plot.show(alcoholScatter);

// Provided: Group wines by quality level
Table qualityGroups = wine.summarize(
    "alcohol", AggregateFunctions.mean,
    "pH", AggregateFunctions.mean,
    "volatile acidity", AggregateFunctions.mean
).by("quality");
System.out.println("\nCharacteristics by quality level:");
System.out.println(qualityGroups);
```

## Question 2: Machine Learning with SMILE (2 parts)
Build a Random Forest model using the SMILE library to predict wine quality.


```python
// Convert Tablesaw table to SMILE DataFrame
String[] colNames = wine.columnNames().toArray(String[]::new);
double[][] data = wine.as().doubleMatrix();
DataFrame df = DataFrame.of(data, colNames);

IntVector quality = IntVector.of("quality", df.doubleVector("quality").stream()
    .mapToInt(d -> (int) d)
    .toArray());
df = df.drop("quality").merge(quality);

// Split data into training and test sets (80/20 split)
int n = df.nrows();
int[] indices = IntStream.range(0, n).toArray();
MathEx.permutate(indices); 
int splitIndex = (int)(n * 0.8);

DataFrame trainDf = df.slice(0, splitIndex);
DataFrame testDf = df.slice(splitIndex, n);

// Part A: TODO - Train a Random Forest model using SMILE
smile.classification.RandomForest rf = // Define the formula: quality is the target
Formula formula = Formula.lhs("quality");

// Train the Random Forest model
smile.classification.RandomForest rf = smile.classification.RandomForest.fit(
    formula,
    trainDf
);


// Part B: TODO - Calculate and display model accuracy
int[] yTrue = testDf.stream().mapToInt(r -> r.getInt("quality")).toArray();
int[] yPred = // Make predictions on the test set
int[] yPred = rf.predict(testDf);

// Get true values
int[] yTrue = testDf.intVector("quality").toIntArray();

// Compute accuracy
double accuracy = Accuracy.of(yTrue, yPred);
System.out.printf("SMILE Random Forest Accuracy: %.2f%%\n", accuracy * 100);


double accuracy = // YOUR CODE HERE
System.out.printf("SMILE Random Forest Accuracy: %.2f%%\n", accuracy * 100);
```


```python
// Convert to Weka format
ArrayList<Attribute> attributes = new ArrayList<>();
for (String col : wine.columnNames()) {
    if (!col.equals("quality")) {
        attributes.add(new Attribute(col));
    }
}

IntColumn qualityCol = (IntColumn) wine.intColumn("quality");
int minQuality = (int) qualityCol.min();
int maxQuality = (int) qualityCol.max();
ArrayList<String> qualityVals = new ArrayList<>();
for (int i = minQuality; i <= maxQuality; i++) {
    qualityVals.add(String.valueOf(i));
}
attributes.add(new Attribute("quality", qualityVals));

Instances wData = new Instances("Wine", attributes, wine.rowCount());
wData.setClassIndex(wData.numAttributes() - 1);

for (int i = 0; i < wine.rowCount(); i++) {
    double[] vals = new double[wData.numAttributes()];
    for (int j = 0; j < wine.columnCount() - 1; j++) {
        vals[j] = ((NumberColumn<?,?>) wine.column(j)).getDouble(i);
    }
    vals[wData.numAttributes() - 1] = qualityVals.indexOf(String.valueOf(qualityCol.get(i)));
    wData.add(new DenseInstance(1.0, vals));
}

// Split data
int trainSize = (int) Math.round(wData.numInstances() * 0.8);
Instances train = new Instances(wData, 0, trainSize);
Instances test = new Instances(wData, trainSize, wData.numInstances() - trainSize);

// TODO - Train Weka Random Forest and calculate accuracy
RandomForest wekaRf = new RandomForest();
try {
    wekaRf.buildClassifier(train); // train model

    Evaluation eval = new Evaluation(train);
    eval.evaluateModel(wekaRf, test); // test model

    System.out.printf("Weka Random Forest Accuracy: %.2f%%\n", eval.pctCorrect());

    System.out.println("\nModel Comparison Complete!");
    System.out.println("Which model performed better? Analyze the results above.");
    
} catch (Exception e) {
    e.printStackTrace();
}

```
