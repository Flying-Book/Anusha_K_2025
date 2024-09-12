---
layout: gallery
title: Gallery
description: Gallery
permalink: /gallery
menu: nav/sprint_1.html
comments: true
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Scrolling Gallery with Side-by-Side View</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background-color: #f3f3f3;
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
            overflow: hidden;
            position: relative;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
            cursor: pointer;
        }

        .gallery-item:hover {
            transform: scale(1.05);
        }

        .gallery-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        /* Description overlay */
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

        /* Modal (Side-by-side view) */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
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
        }

        .modal-img {
            width: 50%;
            max-height: 100%;
            object-fit: contain;
            overflow: auto; /* Enable scrolling if image is larger */
        }

        .modal-description {
            width: 50%;
            padding: 20px;
            overflow-y: auto;
            max-height: 100%;
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

        /* Scroll buttons */
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
            z-index: 10;
        }

        .scroll-btn.left {
            left: 10px;
        }

        .scroll-btn.right {
            right: 10px;
        }

        .scroll-btn:hover {
            background-color: rgba(0, 0, 0, 0.8);
        }

    </style>
</head>
<body>
    <div class="gallery-wrapper">
        <!-- Scroll buttons -->
        <button class="scroll-btn left" id="scroll-left">&lt;</button>
        <button class="scroll-btn right" id="scroll-right">&gt;</button>
        
        <!-- Scrolling gallery -->
        <div class="gallery-container" id="gallery">
            <!-- Gallery Item 1 -->
            <div class="gallery-item" data-image="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ec/Mona_Lisa%2C_by_Leonardo_da_Vinci%2C_from_C2RMF_retouched.jpg/460px-Mona_Lisa%2C_by_Leonardo_da_Vinci%2C_from_C2RMF_retouched.jpg" data-title="Mona Lisa" data-description="The Mona Lisa is a portrait painting by Leonardo da Vinci, widely considered an archetypal masterpiece of the Italian Renaissance. The painting's subject is Lisa Gherardini, wife of Francesco del Giocondo. The mysterious expression and subtle smile have intrigued viewers for centuries.">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ec/Mona_Lisa%2C_by_Leonardo_da_Vinci%2C_from_C2RMF_retouched.jpg/460px-Mona_Lisa%2C_by_Leonardo_da_Vinci%2C_from_C2RMF_retouched.jpg" alt="Mona Lisa" class="gallery-img">
                <div class="description">"Mona Lisa" - Leonardo da Vinci</div>
            </div>

            <!-- Gallery Item 2 -->
            <div class="gallery-item" data-image="" data-title="Starry Night" data-description="Starry Night is one of Dutch artist Vincent van Gogh's most famous paintings, depicting a swirling night sky over a small town. Painted in 1889, it reflects van Gogh's emotions and imagination, showcasing bold color and expressive brushwork.">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg/1513px-Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg?20121101035929" alt="Starry Night" class="gallery-img">
                <div class="description">"Starry Night" - Vincent van Gogh</div>
            </div>

            <!-- Gallery Item 3 -->
            <div class="gallery-item" data-image="https://upload.wikimedia.org/wikipedia/commons/e/ea/The_Scream.jpg" data-title="The Scream" data-description="The Scream by Edvard Munch is a symbol of existential angst and despair. Created in 1893, this iconic work captures the raw emotional intensity of a figure on a bridge, with vibrant colors and swirling shapes portraying the turmoil of the human soul.">
                <img src="https://upload.wikimedia.org/wikipedia/commons/e/ea/The_Scream.jpg" alt="The Scream" class="gallery-img">
                <div class="description">"The Scream" - Edvard Munch</div>
            </div>

            <!-- Gallery Item 4 -->
            <div class="gallery-item" data-image="https://upload.wikimedia.org/wikipedia/commons/6/6a/Les_Demoiselles_d%27Avignon.jpg" data-title="Les Demoiselles d'Avignon" data-description="Les Demoiselles d'Avignon by Pablo Picasso is a revolutionary piece that marked the beginning of Cubism. Painted in 1907, the artwork depicts five nude female figures with disjointed and angular forms, challenging traditional depictions of the human body.">
                <img src="https://upload.wikimedia.org/wikipedia/commons/6/6a/Les_Demoiselles_d%27Avignon.jpg" alt="Les Demoiselles d'Avignon" class="gallery-img">
                <div class="description">"Les Demoiselles d'Avignon" - Pablo Picasso</div>
            </div>

            <!-- Gallery Item 5 -->
            <div class="gallery-item" data-image="https://upload.wikimedia.org/wikipedia/commons/5/55/The_Persistence_of_Memory.jpg" data-title="The Persistence of Memory" data-description="The Persistence of Memory by Salvador Dalí is a surreal masterpiece, known for its melting clocks and dreamlike landscape. Painted in 1931, the work explores themes of time, reality, and memory, with its haunting and enigmatic visual elements.">
                <img src="https://upload.wikimedia.org/wikipedia/commons/5/55/The_Persistence_of_Memory.jpg" alt="The Persistence of Memory" class="gallery-img">
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
        // Get the gallery container and buttons
        const gallery = document.getElementById("gallery");
        const scrollLeftBtn = document.getElementById("scroll-left");
        const scrollRightBtn = document.getElementById("scroll-right");

        // Scroll the gallery to the right
        scrollRightBtn.addEventListener('click', () => {
            gallery.scrollBy({ left: 500, behavior: 'smooth' });
        });

        // Scroll the gallery to the left
        scrollLeftBtn.addEventListener('click', () => {
            gallery.scrollBy({ left: -500, behavior: 'smooth' });
        });

        // Modal functionality
        const modal = document.getElementById("artModal");
        const modalImg = document.getElementById("modalImg");
        const modalTitle = document.getElementById("modalTitle");
        const modalDesc = document.getElementById("modalDesc");
        const closeModal = document.getElementById("closeModal");

        // When an art piece is clicked, open the modal with the larger image and longer description
        document.querySelectorAll('.gallery-item').forEach(item => {
            item.addEventListener('click', function() {
                const image = this.getAttribute('data-image');
                const title = this.getAttribute('data-title');
                const description = this.getAttribute('data-description');

                modalImg.src = image;
                modalTitle.textContent = title;
                modalDesc.textContent = description;

                modal.style.display = 'flex'; // Show the modal
            });
        });

        // Close the modal
        closeModal.addEventListener('click', () => {
            modal.style.display = 'none';
        });

        // Close the modal if the user clicks outside of it
        window.addEventListener('click', (event) => {
            if (event.target === modal) {
                modal.style.display = 'none';
            }
        });
    </script>
</body>
</html>
