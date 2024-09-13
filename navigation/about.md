---
layout: page
title: About
permalink: /about/
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Anusha Khobare - About Me</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        .container {
            width: 80%;
            margin: auto;
            overflow: hidden;
        }
        header {
            background: #333;
            color: #fff;
            padding-top: 30px;
            min-height: 70px;
            border-bottom: #ddd 3px solid;
            text-align: center;
        }
        header h1 {
            margin: 0;
            font-size: 2.5em;
        }
        .accordion {
            background: #9429ff;
            color: #fff;
            cursor: pointer;
            padding: 15px;
            border: none;
            text-align: left;
            outline: none;
            font-size: 1.2em;
            width: 100%;
            border-radius: 8px;
            margin-bottom: 5px;
        }
        .accordion:hover {
            background: #5e18a3;
        }
        .panel {
            padding: 20px;
            background: #fff;
            display: none;
            overflow: hidden;
            border-radius: 8px;
            margin-bottom: 20px;
        }
        img {
            max-width: 100%;
            height: auto;
            border-radius: 8px;
            margin-bottom: 20px;
        }
        h2, h3 {
            color: #333;
        }
        .slot {
            margin: 10px 0;
            padding: 10px;
            border: 1px dashed #ccc;
            border-radius: 8px;
            text-align: center;
            color: #888;
        }
        .gallery {
            display: block;
            white-space: nowrap;
            overflow-x: auto;
            padding: 10px 0;
        }
        .gallery img {
            display: inline-block;
            margin-right: 10px;
            max-height: 150px;
            border-radius: 8px;
            cursor: pointer;
        }
        .description {
            display: none;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 8px;
            background: #fff;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <button class="accordion">About Me</button>
        <div class="panel">
            <p>My name is Anusha Khobare, and I am currently in the 11th grade. Last year, I took the AP Computer Science Principles (CSP) course, which ignited my passion for technology and programming. This year, I am thrilled to be taking AP Computer Science A (CSA) to further develop my skills in software development and algorithms.</p>
            <p>I have experience with several technologies, including JavaScript, HTML, SCSS, and SQLite databases. I am always eager to learn more and apply my knowledge to real-world projects.</p>
        </div>

        <button class="accordion">Location & Background</button>
        <div class="panel">
            <p>I was born and have lived in San Diego all my life. I attended Stone Ranch Elementary, Oak Valley Middle School, and I am currently a student at Del Norte High School.</p>
            <img src="https://www.eisenhowerlibrary.gov/sites/default/files/images/flag-designs-15.png" alt="United States Flag" data-description="lived in US all my life)">
        </div>

        <button class="accordion">Hobbies</button>
        <div class="panel">
            <div class="gallery">
                <img src="https://www.mercurynews.com/wp-content/uploads/2016/08/20151201__dancecard1.jpg?w=1024" alt="Indian Classical Dance" data-description="Indian Classical Dance (Kathak for 10 years)">
                <img src="https://images.squarespace-cdn.com/content/v1/51fa08cae4b0d906af519976/1570122007211-IQK6JRPK86S1YKTIO89S/Lithuania.jpg" alt="Reading" data-description="Reading">
                <img src="https://cdn.britannica.com/26/84526-050-45452C37/Gateway-monument-India-entrance-Mumbai-Harbour-coast.jpg" alt="Travel" data-description="Travel">
                <img src="https://www.premiumbeat.com/blog/wp-content/uploads/2020/07/Camera-Tech-Cover-photo.jpg?w=875&h=490&crop=1" alt="Art" data-description="Art/Drawing/Photography">
            </div>
            <div id="image-description" class="description"></div>
        </div>

        <button class="accordion">Personal Interests</button>
        <div class="panel">
            <p>My personal interests include:</p>
            <ul>
                <li><strong>Books:</strong> I have a deep love for reading.</li>
                <li><strong>Music:</strong> I enjoy listening to various types of music.</li>
                <li><strong>Beach:</strong> Living in San Diego, I love spending time at the beach.</li>
                <li><strong>Strawberry Ice Cream:</strong> Strawberry ice cream is my favorite treat.</li>
            </ul>
        </div>

        <button class="accordion">Past CSP Projects</button>
        <div class="panel">
            <h3>Project 1: Fitness Tracker</h3>
            <p><strong>Description:</strong> This project started as a simple fitness tracker and evolved into a comprehensive health tracking application.</p>
            <ul>
                <li><strong>Water Tracking:</strong> Developed a feature for tracking water intake using a moving bar.</li>
                <li><strong>Food Tracker:</strong> Implemented a system for tracking food intake, storing user data in local storage, and generating a health score based on USDA recommendations. Included pie charts for visualizing intake versus recommended values and integrated ML-based suggestions.</li>
                <li><strong>Expanded Features:</strong> Added additional trackers for sleep, fitness, and stress, along with a profile creation feature for personalized tracking.</li>
            </ul>
            <p><strong>Technologies Used:</strong> JavaScript, HTML, CSS, Local Storage, D3.js, SQLite, Python</p>
            <p><a href="#">Backend Repository</a> | <a href="#">Frontend Link</a></p>

            <h3>Project 2: Calorie Burned Calculator</h3>
            <p><strong>Description:</strong> Developed a calorie burned calculator using the Seaborn library, initially created in Jupyter Notebooks and later implemented as a model and API.</p>
            <ul>
                <li><strong>Data Processing:</strong> Included one-hot encoding, data cleaning, training, and predictions.</li>
                <li><strong>Backend:</strong> Featured an SQLite backend with GET and POST requests.</li>
            </ul>
            <p><strong>Technologies Used:</strong> Python, Jupyter Notebooks, Seaborn, Pandas, Scikit-learn, SQLite, Flask</p>
            <p><a href="#">Backend Repository</a> | <a href="#">Frontend Repository</a></p>

            <h3>Project 3: Third Trimester Museum Project</h3>
            <p><strong>Description:</strong> This project combined elements from two previous triangle projects, focusing on developing a system for sorting and searching through an array of exercise cards.</p>
            <ul>
                <li><strong>Exercise Cards:</strong> Implemented features for sorting and searching exercise cards based on editable attributes like likes and intensity.</li>
                <li><strong>Backend:</strong> Used SQLite for storing and retrieving exercise card data.</li>
            </ul>
            <p><strong>Technologies Used:</strong> JavaScript, HTML, CSS, SQLite</p>
            <p><a href="#">Frontend Repository</a> | <a href="#">Backend Repository</a></p>
        </div>
    </div>

    <script>
        // Get all accordion buttons
        var acc = document.getElementsByClassName("accordion");
        var i;

        // Add event listeners to each accordion button
        for (i = 0; i < acc.length; i++) {
            acc[i].addEventListener("click", function() {
                // Toggle between adding and removing the "active" class
                // to highlight the button that controls the panel
                this.classList.toggle("active");

                // Toggle the panel's visibility
                var panel = this.nextElementSibling;
                if (panel.style.display === "block") {
                    panel.style.display = "none";
                } else {
                    panel.style.display = "block";
                }
            });
        }

        // Image click event handler to show descriptions
        var images = document.querySelectorAll('.gallery img');
        var descriptionBox = document.getElementById('image-description');

        images.forEach(function(image) {
            image.addEventListener('click', function() {
                descriptionBox.textContent = this.getAttribute('data-description');
                descriptionBox.style.display = 'block';
            });
        });
    </script>
</body>
</html>


<!-- # About Me
My name is Anusha Khobare, and I am currently in 11th grade. Last year, I took the AP Computer Science Principles (CSP) course, which fueled my passion for technology and programming. This year, I am excited to be taking AP Computer Science A (CSA) to further develop my skills in software development and algorithms.

I have experience in several technologies, including JavaScript, HTML, SCSS, and SQLite databases. I'm always eager to learn more and apply my knowledge to real-world projects.
## Personal Intrests
![image](https://github.com/user-attachments/assets/a68ba24f-40e6-41d7-a61a-a90cf4ce3e90)
The freeform picture includes books because I love to read. It also includes music because I like to listen to music. I added a picture of the beach because I live in San Diego and love to go to the beach. I included a picture of strawberry ice cream for food because it is my favorite food.

# Past CSP Projects

## Project 1: Fitness Tracker

**Description:** This project started as a simple fitness tracker and eventually evolved into a comprehensive health tracking application.

- **Water Tracking:** Developed a feature for tracking water intake using a moving bar.
- **Food Tracker:** Implemented a food tracking system that stores user data in local storage and generates a health score by comparing user intake with USDA recommended values. This feature includes pie charts to help users visualize the difference between their intake and recommended values.
- **Enhanced with ML:** Integrated a `food.csv` dataset from Kaggle connected to an SQLite backend. This enhancement provided ML-based suggestions for fruit and vegetable intake based on user lifestyle.
- **Expanded Features:** The final version of the project included additional trackers for sleep, fitness, and stress, as well as a profile creation feature for personalized tracking.

**Technologies Used:** JavaScript, HTML, CSS, Local Storage, D3.js (for pie charts), SQLite, Python (for ML algorithms)  
**Backend Repository:** [GitHub Repository](#)  
**Frontend Link:** [Live Demo](#)

## Project 2: Calorie Burned Calculator

**Description:** This project is a calorie burned calculator developed using the Seaborn library. Initially developed in Jupyter Notebooks, it was later implemented in a model and API form.

- **Data Processing:** Included one-hot encoding, data cleaning (dropping blank data values in the table), training the data, and making predictions.
- **Backend:** Similar to the ML capabilities of the fitness tracker, this project also featured an SQLite backend with GET and POST requests.

**Technologies Used:** Python, Jupyter Notebooks, Seaborn, Pandas, Scikit-learn, SQLite, Flask (for API)  
**Backend Repository:** [GitHub Repository](#)  
**Frontend Repository:** [GitHub Repository](#)

## Project 3: Third Trimester Museum Project

**Description:** This project combined elements from two previous triangle projects. My contribution focused on developing a system for sorting and searching through an array of exercise cards.

- **Exercise Cards:** Implemented a feature for sorting and searching exercise cards based on editable attributes like likes and intensity.
- **Backend:** Utilized an SQLite database for storing and retrieving exercise card data.

**Technologies Used:** JavaScript, HTML, CSS, SQLite  
**Frontend Repository:** [GitHub Repository](#)  
**Backend Repository:** [GitHub Repository](#)



Creator of Student 2025 -->
