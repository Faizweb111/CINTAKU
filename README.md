
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Valentine's Day Love Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: pink;
        }
        .container {
            margin-top: 50px;
        }
        .heart-img {
            width: 300px;
            transition: transform 0.3s ease-in-out;
        }
        .buttons {
            margin-top: 20px;
        }
        .love-btn, .not-btn {
            padding: 15px;
            font-size: 18px;
            border: none;
            cursor: pointer;
            border-radius: 10px;
            transition: transform 0.3s ease;
        }
        .love-btn {
            background-color: red;
            color: white;
        }
        .not-btn {
            background-color: gray;
            color: white;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Kau Suka Aku ark?....💖</h1>
        <img id="heart" class="heart-img" src="download.png" alt="Heart">
        <div class="buttons">
            <button id="loveBtn" class="love-btn" onclick="acceptLove()">SUKAAA❤️</button>
            <button id="notBtn" class="not-btn" onclick="rejectLove()">TAKK 💔</button>
        </div>
    </div>
    
    <script>
        let notSize = 1;
        let loveSize = 1;

        function rejectLove() {
            notSize *= 0.8;
            loveSize *= 1.2;
            document.getElementById("notBtn").style.transform = `scale(${notSize})`;
            document.getElementById("loveBtn").style.transform = `scale(${loveSize})`;
            document.getElementById("heart").src = "download (1).jpg"; // Change to pic1 when "Not" is clicked
        }

        function acceptLove() {
            document.querySelector(".container").innerHTML = `
                <h1>TERIMA KASIH SEBAB SUKA SAYA HIHIHIHI 💕</h1>
                <img class="heart-img" src="download (2).jpg" alt="Love Image">
            `;
        }
    </script>
</body>
</html>
      
