---
layout: base
title: Anusha Khobare's Home Page 
description: Home Page
hide: true
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Anusha Khobare's Art Blog</title>
    <style>
        /* Removed the font-face rule for now */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Product Sans';
        }
        body {
            font-family: sans-serif;
            background-color: #1B2D2A;
            color: white;
            text-align: center;
            padding: 50px;
            font-size: 20px;
            overflow-x: hidden;
            position: relative; /* Ensure that the background animation stays behind the content */
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            margin-bottom: 100px;
        }
        canvas {
            border: 2px solid #1B2D2A;
            background: #ffcfca;
            display: block;
            margin: 50px auto;
        }
        #gameOver {
            display: none;
            font-size: 30px;
            color: red;
        }
        .gallery-wrapper {
            position: relative;
            padding: 20px;
            overflow: hidden;
        }
        .gallery-container {
            width: 100%;
            overflow-x: auto;
            white-space: nowrap;
            padding: 20px 0;
        }
        .gallery-container::-webkit-scrollbar {
            height: 10px;
        }
        .gallery-container::-webkit-scrollbar-thumb {
            background-color: #888;
            border-radius: 5px;
        }
        .gallery-container::-webkit-scrollbar-track {
            background-color: #f1f1f1;
        }
        .gallery-item {
            display: inline-block;
            width: 500px;
            height: 350px;
            margin-right: 15px;
            position: relative;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        .gallery-item:hover {
            transform: scale(1.05);
        }
        .gallery-img {
            width: 100%;
            height: 100%;
            object-fit: cover; /* Image scales to cover the entire container */
            object-position: top; /* Ensures the top part is prioritized when cropping */
        }
        .description {
            position: absolute;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.7);
            color: white;
            width: 100%;
            text-align: center;
            padding: 10px;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        .gallery-item:hover .description {
            opacity: 1;
        }
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 500px;
            background-color: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
            z-index: 9999;
        }
        .modal-content {
            display: flex;
            background-color: white;
            width: 80%;
            max-width: 900px;
            height: 80%;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            position: relative;
        }
        .modal-img {
            width: 50%;
            object-fit: contain;
        }
        .modal-description {
            width: 50%;
            padding: 20px;
            overflow-y: auto;
            color: black;
        }
        .modal-description h2 {
            margin-top: 0;
        }
        .close-btn {
            position: absolute;
            top: 20px;
            right: 30px;
            font-size: 30px;
            color: white;
            cursor: pointer;
            z-index: 10000;
        }
        .scroll-btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background-color: rgba(0, 0, 0, 0.5);
            color: white;
            border: none;
            font-size: 24px;
            padding: 10px;
            cursor: pointer;
        }
        .scroll-btn.left {
            left: 10px;
        }
        .scroll-btn.right {
            right: 10px;
        }
        .intro {
            padding: 20px;
            background-color: white;
            border-radius: 10px;
            margin-bottom: 20px;
            font-size: 24px;
            color: black;
        }
        .background-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 50%;
            height: 50%;
            z-index: -1; /* Ensure it stays behind the content */
            overflow: hidden;
            background-color: #eee; /* Fallback background color */
            animation: moveBlob 20s infinite; /* Faster animation */
        }
        @keyframes moveBlob {
            0% {
                border-radius: 10% 70% 40% 80% / 50% 20% 60% 90%;
                background: rgba(0, 0, 0, 0.5);
                transform: translate(-20%, -20%) scale(0.5) rotate(0deg);
            }
            25% {
                border-radius: 70% 10% 60% 30% / 40% 70% 20% 80%;
                background: rgba(0, 0, 0, 0.4);
                transform: translate(30%, -30%) scale(1.2) rotate(90deg);
            }
            50% {
                border-radius: 30% 10% 20% 50% / 70% 10% 80% 30%;
                background: rgba(0, 0, 0, 0.3);
                transform: translate(20%, 30%) scale(0.8) rotate(180deg);
            }
            75% {
                border-radius: 90% 5% 40% 20% / 60% 80% 30% 10%;
                background: rgba(0, 0, 0, 0.4);
                transform: translate(-40%, -20%) scale(1.5) rotate(270deg);
            }
            100% {
                border-radius: 5% 70% 80% 40% / 60% 40% 70% 50%;
                background: rgba(0, 0, 0, 0.5);
                transform: translate(-20%, -20%) scale(0.6) rotate(360deg);
            }
        }
        @media (max-width: 600px) {
            .background-animation {
                /* No specific styles for small screens yet */
            }
        }
    </style>
</head>
<body>
    <div class="background-animation"></div>
    <!-- Art Gallery Section -->
    <div class="gallery-wrapper">
        <!-- Scroll buttons -->
        <button class="scroll-btn left" id="scroll-left">&lt;</button>
        <button class="scroll-btn right" id="scroll-right">&gt;</button>
        <!-- Scrolling gallery -->
        <div class="gallery-container" id="gallery">
            <!-- Gallery Item 1 -->
            <div class="gallery-item" data-image="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ec/Mona_Lisa%2C_by_Leonardo_da_Vinci%2C_from_C2RMF_retouched.jpg/460px-Mona_Lisa%2C_by_Leonardo_da_Vinci%2C_from_C2RMF_retouched.jpg" data-title="Mona Lisa" data-description="The Mona Lisa, painted by Leonardo da Vinci in the early 16th century, is one of the most famous and recognizable paintings in the world. The portrait depicts a woman with an enigmatic expression, which has captivated audiences for centuries. The use of sfumato, a technique to blend colors and tones, adds to the mysterious quality of her smile. The painting is housed in the Louvre Museum in Paris, where it draws millions of visitors each year.">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ec/Mona_Lisa%2C_by_Leonardo_da_Vinci%2C_from_C2RMF_retouched.jpg/460px-Mona_Lisa%2C_by_Leonardo_da_Vinci%2C_from_C2RMF_retouched.jpg" alt="Mona Lisa" class="gallery-img">
                <div class="description">"Mona Lisa" - Leonardo da Vinci</div>
            </div>
            <!-- Additional Gallery Items -->
            <div class="gallery-item" data-image="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg/1513px-Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg?20121101035929" data-title="The Starry Night" data-description="The Starry Night, created by Vincent van Gogh in 1889, is a masterful depiction of the night sky swirling with energy. Painted during Van Gogh's stay at the Saint-Paul-de-Mausole asylum in Saint-Rémy-de-Provence, the work is renowned for its vibrant use of color and dynamic brushstrokes. The painting features a dramatic, almost surreal representation of the night sky over a quiet village, capturing Van Gogh's emotional state and his fascination with the cosmos. It is now housed in the Museum of Modern Art in New York City.">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg/1513px-Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg?20121101035929" alt="The Starry Night" class="gallery-img">
                <div class="description">"The Starry Night" - Vincent van Gogh</div>
            </div>
            <div class="gallery-item" data-image="https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Johannes_Vermeer_%281632-1675%29_-_The_Girl_With_The_Pearl_Earring_%281665%29.jpg/838px-Johannes_Vermeer_%281632-1675%29_-_The_Girl_With_The_Pearl_Earring_%281665%29.jpg?20140713231615" data-title="Girl with a Pearl Earring" data-description="Girl with a Pearl Earring, painted by Johannes Vermeer around 1665, is often referred to as the 'Mona Lisa of the North.' This exquisite portrait features a young woman wearing an exotic turban and a large pearl earring. The painting is celebrated for its striking use of light and shadow, and the enigmatic expression of the subject, which draws viewers into her world. The piece is housed in the Mauritshuis Museum in The Hague, Netherlands, and continues to fascinate art enthusiasts with its mysterious allure.">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Johannes_Vermeer_%281632-1675%29_-_The_Girl_With_The_Pearl_Earring_%281665%29.jpg/838px-Johannes_Vermeer_%281632-1675%29_-_The_Girl_With_The_Pearl_Earring_%281665%29.jpg?20140713231615" alt="Girl with a Pearl Earring" class="gallery-img">
                <div class="description">"Girl with a Pearl Earring" - Johannes Vermeer</div>
            </div>
            <div class="gallery-item" data-image="https://upload.wikimedia.org/wikipedia/en/d/dd/The_Persistence_of_Memory.jpg" data-title="The Persistence of Memory" data-description="The Persistence of Memory, painted by Salvador Dalí in 1931, is a hallmark of surrealist art. The painting is known for its melting clocks draped over a desolate landscape, symbolizing the fluidity and relativity of time. Dali's dreamlike imagery invites viewers to question their perceptions of reality and time. The work exemplifies Dali's unique style and his exploration of the unconscious mind. It is currently housed in the Museum of Modern Art in New York City.">
                <img src="https://upload.wikimedia.org/wikipedia/en/d/dd/The_Persistence_of_Memory.jpg" alt="The Persistence of Memory" class="gallery-img">
                <div class="description">"The Persistence of Memory" - Salvador Dalí</div>
            </div>
        </div>
    </div>
    <!-- Modal for side-by-side view -->
    <div id="artModal" class="modal">
        <span class="close-btn" id="closeModal">&times;</span>
        <div class="modal-content">
            <img id="modalImg" class="modal-img" src="" alt="Art Piece">
            <div class="modal-description">
                <h2 id="modalTitle">Title</h2>
                <p id="modalDesc">Description</p>
            </div>
        </div>
    </div>
    <script>
        // Gallery Modal Logic
        const galleryItems = document.querySelectorAll('.gallery-item');
        const modal = document.getElementById('artModal');
        const modalImg = document.getElementById('modalImg');
        const modalTitle = document.getElementById('modalTitle');
        const modalDesc = document.getElementById('modalDesc');
        const closeModal = document.getElementById('closeModal');
        
        // Open modal on gallery item click
        galleryItems.forEach(item => {
            item.addEventListener('click', () => {
                modal.style.display = 'flex';
                modalImg.src = item.getAttribute('data-image');
                modalTitle.textContent = item.getAttribute('data-title');
                modalDesc.textContent = item.getAttribute('data-description');
            });
        });
        
        // Close modal logic
        closeModal.addEventListener('click', () => {
            modal.style.display = 'none';
        });
        
        // Scroll buttons logic
        const scrollLeft = document.getElementById('scroll-left');
        const scrollRight = document.getElementById('scroll-right');
        const gallery = document.getElementById('gallery');
        
        scrollLeft.addEventListener('click', () => {
            gallery.scrollBy({ left: -300, behavior: 'smooth' });
        });
        
        scrollRight.addEventListener('click', () => {
            gallery.scrollBy({ left: 300, behavior: 'smooth' });
        });
    </script>
</body>
</html>