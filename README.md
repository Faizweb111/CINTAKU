<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Website Biodata</title>
    <link rel="stylesheet" href="styles.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #cce7ff;
            background-image: linear-gradient(to right, #cce7ff, #80d0ff);
            color: #004080;
        }
        /*kotak luar*/
        .container {
            margin-top: 50px;
            padding: 20px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            display: inline-block;
            width: 80%;
        }
        /*button*/
        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 20px 26px;
            margin: 10px;
            cursor: pointer;
            border-radius: 8px;
            font-size: 16px;
            transition: transform 0.3s ease, background 0.3s ease;
        }
        button:hover {
            transform: scale(1.1);
            background-color: #0056b3;
        }
        /*kotak luar2*/
        .content {
            margin-top: 20px;
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.5s ease, transform 0.5s ease;
            display: none;
        }
        .show {
            opacity: 1;
            transform: translateY(0);
            display: block;
        }
        /*dalam bio*/
        .biodata-entry {
            border-bottom: 3px solid #007bff;
            padding: 15px;
            margin-bottom: 10px;
        }
        img {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            margin-top: 15px;
            border: 4px solid #007bff;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 style="color: #ff6600; text-shadow: 2px 2px 5px rgba(0,0,0,0.2);">BIODATA KELAS 3K</h1>
        <button onclick="showContent('home')">Home</button>
        <button onclick="showContent('biodata')">Biodata</button>
        <button onclick="showContent('register')">Biodata Register</button>
        
        <div id="home" class="content show">
            <h2>Welcome to Website Biodata 3K</h2>
            <p>Terima kasih kerana melawat laman web ini!</p>
        </div>
        
        <div id="biodata" class="content">
            <h2>Biodata</h2>
            <div id="biodata-list"></div>
        </div>
        
        <div id="register" class="content">
            <h2>Biodata Register</h2>
            <form id="registerForm">
                <input type="text" id="nama" placeholder="Nama Penuh" required><br>
                <br>
                <input type="email" id="email" placeholder="Email" required><br>
                <br>
                <input type="number" id="umur" placeholder="Umur" required><br>
                <br>
                <input type="text" id="alamat" placeholder="Alamat" required><br>
                <br>
                <input type="text" id="ic" placeholder="Nombor IC" required><br>
                <br>
                <textarea id="bio" placeholder="Bio Diri" required></textarea><br>
                <br>
                <input type="file" id="gambar" accept="image/*" required><br>
                <br>
                <button type="submit">Daftar</button>
            </form>
        </div>
    </div>
     <div class="footer">
        <p>&copy; 2025 Portal Biodata Kelas. Hak Cipta Terpelihara Faiz.</p>
    </div>

    <script>
        function showContent(id) {
            document.querySelectorAll('.content').forEach(div => {
                div.classList.remove('show');
            });
            document.getElementById(id).classList.add('show');
        }
        
        document.getElementById('registerForm').addEventListener('submit', function(event) {
            event.preventDefault();
            
            let nama = document.getElementById('nama').value;
            let email = document.getElementById('email').value;
            let umur = document.getElementById('umur').value;
            let alamat = document.getElementById('alamat').value;
            let ic = document.getElementById('ic').value;
            let bio = document.getElementById('bio').value;
            let gambar = document.getElementById('gambar').files[0];
            
            let reader = new FileReader();
            reader.onload = function(e) {
                let newEntry = `<div class='biodata-entry'>
                    <img src="${e.target.result}" alt="Gambar">
                    <p><strong>Nama:</strong> ${nama}</p>
                   
                    <p><strong>Umur:</strong> ${umur} tahun</p>
                   
                    <p><strong>Nombor IC:</strong> ${ic}</p>
                    <p><strong>Bio:</strong> ${bio}</p>
                </div>`;
                
                document.getElementById('biodata-list').innerHTML += newEntry;
                localStorage.setItem('biodataList', document.getElementById('biodata-list').innerHTML);
            };
            reader.readAsDataURL(gambar);
            
            this.reset();
        });
        
        window.onload = function() {
            if (localStorage.getItem('biodataList')) {
                document.getElementById('biodata-list').innerHTML = localStorage.getItem('biodataList');
            }
        }
    </script>
</body>
</html>

             
   
