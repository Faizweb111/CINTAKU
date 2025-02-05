<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portal Bantuan Selangor</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #fff3cd; margin: 0; padding: 0; }
        .container { max-width: 200px; margin: auto; padding: 20px; background-color: #ffcc00; border-radius: 10px; box-shadow: 0 0 10px rgba(0, 0, 0, 0.2); text-align: center; }
        .hidden { display: none; }
        .button { margin: 10px; padding: 10px 20px; background-color: #ff6600; color: white; border: none; cursor: pointer; border-radius: 5px; transition: 0.3s; font-size: 16px; }
        .button:hover { background-color: #cc5500; }
        .header { background-color: #ffcc00; padding: 10px; text-align: center; }
        .header img { width: 120px; }
        input, select { margin: 5px; padding: 10px; width: 90%; border-radius: 5px; border: 1px solid #ccc; font-size: 16px; }
        .list-container { text-align: left; background-color: white; padding: 15px; border-radius: 5px; }
        .footer { text-align: center; padding: 10px; background-color: #ffcc00; margin-top: 20px; font-size: 14px; }
    </style>
</head>
<body>
    <div class="header">
        <br><br>
        <h1>PORTAL BANTUAN SELANGOR</h1>
    </div>
    <div class="container">
        <div id="home">
            <button class="button" onclick="showPage('pendaftaran')">Pendaftaran</button>
            <button class="button" onclick="showPage('bantuan')">Jenis Bantuan</button>
            <button class="button" onclick="showPage('senarai')">Senarai Nama</button>
        </div>

        <div id="pendaftaran" class="hidden">
            <h2>Pendaftaran Bantuan</h2>
            <form id="formPendaftaran">
                <input type="text" id="nama" placeholder="Nama" required>
                <input type="number" id="umur" placeholder="Umur" required>
                <input type="number" id="ic" placeholder="No IC" required>
                <select id="daerah" required>
                    <option value="">Pilih Daerah</option>
                    <option value="Shah Alam">Shah Alam</option>
                    <option value="Petaling Jaya">Petaling Jaya</option>
                    <option value="Klang">Klang</option>
                    <option value="Gombak">Gombak</option>
                    <option value="Hulu Langat">Hulu Langat</option>
                    <option value="Hulu Selangor">Hulu Selangor</option>
                    <option value="Kuala Langat">Kuala Langat</option>
                    <option value="Kuala Selangor">Kuala Selangor</option>
                    <option value="Sabak Bernam">Sabak Bernam</option>
                    <option value="Sepang">Sepang</option>
                </select>
                <select id="jenisBantuan" required>
                    <option value="">Pilih Jenis Bantuan</option>
                    <option value="Bantuan Makanan">Bantuan Makanan</option>
                    <option value="Bantuan Kewangan">Bantuan Kewangan</option>
                    <option value="Bantuan Perubatan">Bantuan Perubatan</option>
                    <option value="Bantuan Pendidikan">Bantuan Pendidikan</option>
                    <option value="Bantuan Perumahan">Bantuan Perumahan</option>
                </select>
                <button type="button" class="button" onclick="daftarPengguna()">Daftar</button>
            </form>
            <button class="button" onclick="showPage('home')">Kembali</button>
        </div>

        <div id="bantuan" class="hidden">
            <h2>Jenis Bantuan</h2>
            <div class="list-container">
                <ul>
                    <li><button class="button" onclick="showSyarat('Bantuan Makanan')">Bantuan Makanan</button></li>
                    <li><button class="button" onclick="showSyarat('Bantuan Kewangan')">Bantuan Kewangan</button></li>
                    <li><button class="button" onclick="showSyarat('Bantuan Perubatan')">Bantuan Perubatan</button></li>
                    <li><button class="button" onclick="showSyarat('Bantuan Pendidikan')">Bantuan Pendidikan</button></li>
                    <li><button class="button" onclick="showSyarat('Bantuan Perumahan')">Bantuan Perumahan</button></li>
                </ul>
            </div>
            <p id="syarat" class="hidden"></p>
            <button class="button" onclick="showPage('home')">Kembali</button>
        </div>

        <div id="senarai" class="hidden">
            <h2>Senarai Pendaftar</h2>
            <div class="list-container" id="senaraiNama"></div>
            <button class="button" onclick="showPage('home')">Kembali</button>
        </div>
    </div>

    <div class="footer">
        <p>&copy; 2025 Portal Bantuan Selangor. Hak Cipta Terpelihara Faiz.</p>
    </div>

    <script>
        function showPage(page) {
            document.querySelectorAll('.container > div').forEach(div => div.classList.add('hidden'));
            document.getElementById(page).classList.remove('hidden');
        }

        function showSyarat(bantuan) {
            const syarat = document.getElementById('syarat');
            syarat.classList.remove('hidden');
            syarat.innerHTML = `<strong>${bantuan}</strong><br>✅ Umur 18 tahun ke atas<br>✅ Bermastautin di Selangor<br>✅ Berpendapatan minimum tertentu`;
        }

        function daftarPengguna() {
            const nama = document.getElementById('nama').value;
            const umur = document.getElementById('umur').value;
            const ic = document.getElementById('ic').value;
            const daerah = document.getElementById('daerah').value;
            const bantuan = document.getElementById('jenisBantuan').value;

            if (umur < 18) {
                alert('Pendaftaran hanya untuk mereka yang berumur 18 tahun ke atas.');
                return;
            }

            localStorage.setItem(nama, JSON.stringify({umur, daerah, bantuan}));
            updateSenarai();
            showPage('senarai');
        }

        function updateSenarai() {
            const senarai = document.getElementById('senaraiNama');
            senarai.innerHTML = '';
            Object.keys(localStorage).forEach(nama => {
                const data = JSON.parse(localStorage.getItem(nama));
                senarai.innerHTML += `<p><strong>${nama}</strong> (${data.umur} tahun) - ${data.daerah} - ${data.bantuan}</p>`;
            });
        }
        updateSenarai();
    </script>
</body>
</html>


  
