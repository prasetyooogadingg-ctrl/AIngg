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
    
 */
@font-face {
  font-family: 'Poppins';
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url(https://fonts.gstatic.com/s/poppins/v24/pxiEyp8kv8JHgFVrJJbecnFHGPezSQ.woff2) format('woff2');
  unicode-range: U+0900-097F, U+1CD0-1CF4, U+1CF7-1CF9, U+200C-200D, U+20A8, U+20B9, U+20F0, U+25CC, U+A830-A839, U+A8E0-A8FF, U+11B00-11B0A;
}
/* latin-ext */
@font-face {
  font-family: 'Poppins';
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url(https://fonts.gstatic.com/s/poppins/v24/pxiEyp8kv8JHgFVrJJnecnFHGPezSQ.woff2) format('woff2');
  unicode-range: U+0100-02BA, U+02BD-02C5, U+02C7-02CC, U+02CE-02D7, U+02DD-02FF, U+0304, U+0308, U+0329, U+1D00-1DBF, U+1E00-1E9F, U+1EF2-1EFF, U+2020, U+20A0-20AB, U+20AD-20C4, U+2113, U+2C60-2C7F, U+A720-A7FF;
}
/* latin */
@font-face {
  font-family: 'Poppins';
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url(https://fonts.gstatic.com/s/poppins/v24/pxiEyp8kv8JHgFVrJJfecnFHGPc.woff2) format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+0304, U+0308, U+0329, U+2000-206F, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}
/* devanagari */
@font-face {
  font-family: 'Poppins';
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url(https://fonts.gstatic.com/s/poppins/v24/pxiByp8kv8JHgFVrLCz7Z11lFd2JQEl8qw.woff2) format('woff2');
  unicode-range: U+0900-097F, U+1CD0-1CF4, U+1CF7-1CF9, U+200C-200D, U+20A8, U+20B9, U+20F0, U+25CC, U+A830-A839, U+A8E0-A8FF, U+11B00-11B0A;
}
/* latin-ext */
@font-face {
  font-family: 'Poppins';
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url(https://fonts.gstatic.com/s/poppins/v24/pxiByp8kv8JHgFVrLCz7Z1JlFd2JQEl8qw.woff2) format('woff2');
  unicode-range: U+0100-02BA, U+02BD-02C5, U+02C7-02CC, U+02CE-02D7, U+02DD-02FF, U+0304, U+0308, U+0329, U+1D00-1DBF, U+1E00-1E9F, U+1EF2-1EFF, U+2020, U+20A0-20AB, U+20AD-20C4, U+2113, U+2C60-2C7F, U+A720-A7FF;
}
/* latin */
@font-face {
  font-family: 'Poppins';
  font-style: normal;
  font-weight: 700;
  font-display: swap;
  src: url(https://fonts.gstatic.com/s/poppins/v24/pxiByp8kv8JHgFVrLCz7Z1xlFd2JQEk.woff2) format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+0304, U+0308, U+0329, U+2000-206F, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}* {
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
