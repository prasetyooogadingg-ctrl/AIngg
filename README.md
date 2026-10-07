<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Web AR - Filter Lucu</title>
    <link rel="stylesheet" href="style.css">
    
    <!-- Script A-Frame dan MindAR Face Tracking -->
    <script src="https://aframe.io/releases/1.3.0/aframe.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/mind-ar@1.2.2/dist/mindar-face-aframe.prod.js"></script>
</head>
<body>

    <!-- Landing Page -->
    <div id="landing-page">
        <div class="card">
            <h1>✨ Filter Wajah AR Lucu ✨</h1>
            <p>Jadilah badut sulap! Kamera akan melacak wajahmu dan memasangkan filter secara otomatis.</p>
            <button id="start-btn">Mulai Kamera AR</button>
            <p class="note">*Izinkan akses kamera saat popup muncul ya!</p>
        </div>
    </div>

    <!-- Container AR (Awalnya kosong, akan diisi oleh JavaScript) -->
    <div id="ar-container"></div>

    <script src="script.js"></script>
    
</body>
</html>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
}

body {
    background-color: #ffe6f2; /* Warna pink pastel */
    overflow: hidden; /* Mencegah scroll saat kamera aktif */
}

/* Styling Landing Page */
#landing-page {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 99%, #fecfef 100%);
    z-index: 10;
}

.card {
    background: white;
    padding: 40px;
    border-radius: 20px;
    text-align: center;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    width: 90%;
}

h1 {
    color: #ff4757;
    font-size: 24px;
    margin-bottom: 15px;
}

p {
    color: #57606f;
    margin-bottom: 25px;
    font-size: 15px;
    line-height: 1.5;
}

.note {
    font-size: 12px;
    color: #a4b0be;
    margin-top: 15px;
    margin-bottom: 0;
}

button {
    background-color: #ff4757;
    color: white;
    border: none;
    padding: 15px 30px;
    font-size: 16px;
    font-weight: bold;
    border-radius: 50px;
    cursor: pointer;
    transition: transform 0.2s, background-color 0.2s;
    box-shadow: 0 4px 15px rgba(255, 71, 87, 0.4);
}

button:hover {
    background-color: #ff6b81;
    transform: scale(1.05);
}

/* Styling AR Container */
#ar-container {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: 1;
}
document.addEventListener('DOMContentLoaded', () => {
    const startBtn = document.getElementById('start-btn');
    const landingPage = document.getElementById('landing-page');
    const arContainer = document.getElementById('ar-container');

    startBtn.addEventListener('click', () => {
        // 1. Sembunyikan Landing Page
        landingPage.style.display = 'none';

        // 2. Masukkan sistem AR ke dalam container
        // anchorIndex 1 = Ujung Hidung
        // anchorIndex 10 = Dahi (Kening)
        arContainer.innerHTML = `
            <a-scene mindar-face embedded color-space="sRGB" renderer="colorManagement: true, physicallyCorrectLights" vr-mode-ui="enabled: false" device-orientation-permission-ui="enabled: false">
                <a-camera active="false" position="0 0 0"></a-camera>

                <!-- Filter Hidung Badut Merah -->
                <a-entity mindar-face-target="anchorIndex: 1">
                    <a-sphere color="#ff0000" radius="0.08" position="0 0 0"></a-sphere>
                </a-entity>

                <!-- Filter Topi Lucu di Dahi -->
                <a-entity mindar-face-target="anchorIndex: 10">
                    <!-- Tabung Topi -->
                    <a-cylinder color="#9b59b6" height="0.4" radius="0.15" position="0 0.2 0"></a-cylinder>
                    <!-- Pinggiran Topi -->
                    <a-torus color="#f1c40f" radius="0.25" radius-tubular="0.02" position="0 0 0" rotation="90 0 0"></a-torus>
                </a-entity>
            </a-scene>
        `;
    });
    
});# 📸 Web AR Funny Face Filter
Sebuah website berbasis Augmented Reality (AR) yang ringan dan bisa dijalankan langsung di browser HP maupun Laptop tanpa perlu install aplikasi tambahan. 

Proyek ini mendeteksi wajah pengguna secara *real-time* dan menempelkan objek 3D (Hidung Badut & Topi) menggunakan MindAR dan A-Frame.

## 🚀 Fitur
- **Landing Page Interaktif:** UI yang menarik sebelum mengaktifkan kamera.
- **Privacy Safe:** Kamera hanya meminta izin dan menyala setelah user menekan tombol mulai.
- **Face Tracking Real-Time:** 3D model secara presisi mengikuti pergerakan hidung dan kepala.

## 🛠️ Teknologi yang Digunakan
- HTML5, CSS3, JavaScript
- [A-Frame](https://aframe.io/) (Untuk rendering objek 3D)
- [MindAR.js](https://hiukim.github.io/mind-ar-js-doc/) (Untuk WebAR Face Tracking)

## 🌐 Cara Menjalankan (Deployment)
Karena website ini menggunakan API Kamera (WebRTC), browser **MEWAJIBKAN** website berjalan di protokol `https://` agar kamera bisa menyala.

**Cara paling mudah menjalankan secara gratis:**
1. Upload folder ini ke repository GitHub kamu.
2. Buka **Settings** di repository tersebut.
3. Pilih menu **Pages** di sebelah kiri.
4. Pada bagian *Build and deployment -> Source*, pilih branch `main` atau `master`.
5. Klik **Save**. Tunggu sekitar 1-2 menit.
6. GitHub akan memberikan link website (contoh: `https://username.github.io/nama-repo`).
7. Buka link tersebut di HP kamu, izinkan kamera, dan nikmati filternya!
