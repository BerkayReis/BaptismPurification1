<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vaftiz Simülasyonu</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #1a2a6c);
            background-size: 200% 200%;
            color: white;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            overflow-x: hidden;
            position: relative;
            background-attachment: fixed;
            transition: background 1s ease;
            animation: bgMove 30s linear infinite;
        }
        
        .container {
            max-width: 900px;
            width: 95%;
            text-align: center;
            padding: 2.5rem;
            background: rgba(0, 0, 0, 0.7);
            border-radius: 25px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.6);
            z-index: 10;
            backdrop-filter: blur(12px);
            margin: 25px 0;
            border: 2px solid rgba(79, 195, 247, 0.4);
        }
        
        h1 {
            font-size: 3.2rem;
            margin-bottom: 1.2rem;
            text-shadow: 0 0 15px rgba(255, 255, 255, 0.8);
            color: #4fc3f7;
            background: linear-gradient(to right, #00bcd4, #0288d1, #00bcd4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-size: 200% auto;
            animation: shine 3s linear infinite;
            letter-spacing: 1px;
            position: relative;
        }
        
        h1::after {
            content: "";
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            height: 4px;
            background: linear-gradient(to right, transparent, #00bcd4, transparent);
            border-radius: 2px;
        }
        
        .subtitle {
            font-size: 1.3rem;
            margin-bottom: 2.5rem;
            color: #e0f7fa;
            text-shadow: 0 2px 4px rgba(0,0,0,0.3);
            max-width: 700px;
            margin-left: auto;
            margin-right: auto;
            line-height: 1.6;
        }
        
        .baptism-area {
            position: relative;
            height: 400px;
            width: 100%;
            margin: 2.5rem 0;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><rect width="100" height="100" fill="%230d47a1"/><circle cx="50" cy="50" r="40" fill="%230097c9"/></svg>') center/cover;
            border-radius: 18px;
            overflow: hidden;
            box-shadow: inset 0 0 25px rgba(0, 0, 0, 0.9), 0 10px 30px rgba(0,0,0,0.4);
            border: 4px solid #4fc3f7;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .person-container {
            position: relative;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 5;
        }
        
        .person-photo {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            border: 5px solid #4fc3f7;
            background: #0d47a1;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            box-shadow: 0 0 30px rgba(0,0,0,0.7);
            position: relative;
            z-index: 10;
        }
        
        .person-photo img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
        }
        
        .default-avatar {
            font-size: 8rem;
            color: rgba(255, 255, 255, 0.8);
        }
        
        .water-pool {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 40px;
            background: rgba(64, 196, 255, 0.35);
            border-radius: 0 0 15px 15px;
            transition: height 2s ease;
            z-index: 2;
        }
        
        .controls {
            display: flex;
            flex-direction: column;
            gap: 2rem;
            margin-top: 2.5rem;
        }
        
        .control-group {
            display: flex;
            flex-direction: column;
            gap: 1.2rem;
            background: rgba(255, 255, 255, 0.08);
            padding: 2rem;
            border-radius: 15px;
            text-align: left;
            border: 1px solid rgba(79, 195, 247, 0.3);
        }
        
        .control-row {
            display: flex;
            flex-wrap: wrap;
            gap: 1.2rem;
            align-items: center;
            padding: 0.8rem 0;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }
        
        .control-row:last-child {
            border-bottom: none;
        }
        
        .control-row label {
            min-width: 200px;
            font-weight: bold;
            color: #4fc3f7;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .control-row label i {
            font-size: 1.3rem;
            width: 30px;
            text-align: center;
        }
        
        .baptize-btn {
            padding: 1.4rem 3rem;
            font-size: 1.6rem;
            font-weight: bold;
            background: linear-gradient(45deg, #00bcd4, #0288d1);
            color: white;
            border: none;
            border-radius: 60px;
            cursor: pointer;
            transition: all 0.4s ease;
            box-shadow: 0 7px 20px rgba(0, 0, 0, 0.4);
            position: relative;
            overflow: hidden;
            margin-top: 1.2rem;
            z-index: 20;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            margin-left: auto;
            margin-right: auto;
        }
        
        .baptize-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 25px rgba(0, 0, 0, 0.5);
            background: linear-gradient(45deg, #00e5ff, #039be5);
        }
        
        .baptize-btn:active {
            transform: translateY(2px);
        }
        
        .baptize-btn::after {
            content: "";
            position: absolute;
            top: -15px;
            left: -15px;
            right: -15px;
            bottom: -15px;
            background: radial-gradient(circle, rgba(255,255,255,0.5) 0%, rgba(255,255,255,0) 70%);
            opacity: 0;
            transition: opacity 0.4s;
        }
        
        .baptize-btn:hover::after {
            opacity: 1;
        }
        
        /* Su damlaları için stil */
        .water-drop {
            position: absolute;
            top: -50px;
            width: 8px;
            height: 15px;
            background: linear-gradient(to bottom, rgba(255,255,255,0.9), rgba(64, 196, 255, 0.7));
            border-radius: 50% 50% 60% 40%;
            z-index: 2;
            pointer-events: none;
            box-shadow: 0 0 12px rgba(64, 196, 255, 0.9);
        }
        
        .water-splash {
            position: absolute;
            width: 25px;
            height: 12px;
            background: rgba(64, 196, 255, 0.6);
            border-radius: 50%;
            z-index: 1;
            pointer-events: none;
            box-shadow: 0 0 10px rgba(64, 196, 255, 0.9);
        }
        
        .instructions {
            margin-top: 2.5rem;
            padding: 1.5rem;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 15px;
            font-size: 1rem;
            text-align: left;
            border: 1px solid rgba(79, 195, 247, 0.2);
        }
        
        .instructions h3 {
            margin-bottom: 1rem;
            color: #4fc3f7;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        @keyframes waterRise {
            to {
                height: 150px;
            }
        }
        
        .water-rising {
            animation: waterRise 3.5s forwards;
        }
        
        footer {
            margin-top: 2.5rem;
            text-align: center;
            font-size: 1rem;
            color: rgba(255, 255, 255, 0.8);
            padding: 1.2rem;
            width: 100%;
            background: rgba(0, 0, 0, 0.4);
            font-weight: 300;
        }
        
        /* Animasyon sınıfları */
        @keyframes fall {
            to {
                top: 100%;
                opacity: 0.5;
            }
        }
        
        @keyframes splash {
            0% {
                transform: scale(0.5);
                opacity: 1;
            }
            100% {
                transform: scale(2.5);
                opacity: 0;
            }
        }
        
        @keyframes bgMove {
            0% {
                background-position: 0% 0%;
            }
            50% {
                background-position: 100% 100%;
            }
            100% {
                background-position: 0% 0%;
            }
        }
        
        @keyframes shine {
            to {
                background-position: 200% center;
            }
        }
        
        .moving-bg {
            animation: bgMove 30s linear infinite;
        }
        
        .background-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-size: cover;
            background-position: center;
            z-index: -1;
            transition: transform 0.5s ease;
            opacity: 0.85;
        }
        
        .overlay-controls {
            display: flex;
            gap: 12px;
            align-items: center;
            flex-wrap: wrap;
        }
        
        .custom-btn {
            padding: 10px 18px;
            border: none;
            border-radius: 6px;
            color: white;
            cursor: pointer;
            font-size: 0.95rem;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s ease;
        }
        
        .remove-btn {
            background: #ff5252;
        }
        
        .remove-btn:hover {
            background: #ff0000;
            transform: translateY(-2px);
        }
        
        .action-btn {
            background: #4CAF50;
        }
        
        .action-btn:hover {
            background: #45a049;
            transform: translateY(-2px);
        }
        
        .effect-info {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-top: 12px;
            padding: 10px;
            background: rgba(0, 0, 0, 0.25);
            border-radius: 8px;
        }
        
        .checkbox-container {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 1.05rem;
        }
        
        .checkbox-container input {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }
        
        .preview-container {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid rgba(255,255,255,0.1);
        }
        
        .preview-box {
            width: 150px;
            height: 100px;
            border-radius: 8px;
            overflow: hidden;
            border: 2px solid rgba(79, 195, 247, 0.4);
            box-shadow: 0 3px 10px rgba(0,0,0,0.2);
            background: rgba(0,0,0,0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            color: #aaa;
            font-size: 0.8rem;
        }
        
        .preview-box img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .preview-title {
            width: 100%;
            text-align: left;
            color: #4fc3f7;
            font-weight: bold;
            font-size: 1.1rem;
            margin-bottom: 8px;
        }
        
        /* Modal için stiller */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.9);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        
        .modal-content {
            background: #222;
            padding: 30px;
            border-radius: 15px;
            max-width: 90%;
            width: 600px;
            max-height: 90vh;
            overflow: auto;
            box-shadow: 0 0 30px rgba(0,0,0,0.8);
            border: 2px solid #00bcd4;
            position: relative;
        }
        
        .close-modal {
            position: absolute;
            top: 15px;
            right: 15px;
            font-size: 28px;
            color: #fff;
            cursor: pointer;
            transition: color 0.3s;
        }
        
        .close-modal:hover {
            color: #ff5252;
        }
        
        .webcam-container {
            width: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 20px;
        }
        
        #webcamVideo {
            width: 100%;
            max-width: 500px;
            border-radius: 10px;
            background: #000;
        }
        
        .capture-btn {
            padding: 12px 30px;
            background: linear-gradient(45deg, #00bcd4, #0288d1);
            color: white;
            border: none;
            border-radius: 50px;
            font-size: 1.2rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s;
        }
        
        .capture-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 15px rgba(0, 188, 212, 0.6);
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 1.5rem;
                width: 98%;
            }
            
            h1 {
                font-size: 2.5rem;
            }
            
            .subtitle {
                font-size: 1.1rem;
            }
            
            .baptism-area {
                height: 320px;
            }
            
            .person-photo {
                width: 160px;
                height: 160px;
            }
            
            .control-group {
                padding: 1.5rem;
            }
            
            .control-row {
                flex-direction: column;
                align-items: flex-start;
                gap: 8px;
            }
            
            .baptize-btn {
                padding: 1.2rem 2rem;
                font-size: 1.3rem;
            }
        }
    </style>
</head>
<body>
    <div class="background-overlay" id="backgroundOverlay"></div>
    
    <div class="container">
        <h1><i class="fas fa-water"></i> VAFTİZ TÖRENİ SİMÜLASYONU</h1>
        <p class="subtitle">Kutsal suyla arının ve yeniden doğun. Müzik eşliğinde su damlalarının altında ruhunuzu arındırın.</p>
        
        <div class="baptism-area" id="baptismArea">
            <div class="person-container">
                <div class="person-photo" id="personPhoto">
                    <i class="fas fa-user default-avatar" id="defaultAvatar"></i>
                    <img id="uploadedPhoto" alt="Vaftiz edilen kişi">
                </div>
                <div class="water-pool" id="waterPool"></div>
            </div>
        </div>
        
        <div class="controls">
            <div class="control-group">
                <h3 style="color:#4fc3f7; margin-bottom:20px; display:flex; align-items:center; gap:10px;">
                    <i class="fas fa-sliders-h"></i> Simülasyon Kontrolleri
                </h3>
                
                <div class="control-row">
                    <label for="musicFile"><i class="fas fa-music"></i> Müzik Dosyası:</label>
                    <input type="file" id="musicFile" accept="audio/*" style="color:white;">
                </div>
                
                <div class="control-row">
                    <label for="photoFile"><i class="fas fa-user-circle"></i> Kişi Fotoğrafı:</label>
                    <div class="overlay-controls">
                        <input type="file" id="photoFile" accept="image/*" style="color:white;">
                        <button class="custom-btn remove-btn" id="removePhoto">
                            <i class="fas fa-times"></i> Fotoğrafı Kaldır
                        </button>
                        <button class="custom-btn action-btn" id="webcamBtn">
                            <i class="fas fa-camera"></i> Webcam ile Çek
                        </button>
                    </div>
                    
                    <div class="preview-container">
                        <div class="preview-title">Fotoğraf Önizleme:</div>
                        <div class="preview-box" id="photoPreview">
                            <span>Fotoğraf yüklenmedi</span>
                        </div>
                    </div>
                </div>
                
                <div class="effect-info">
                    <div class="checkbox-container">
                        <input type="checkbox" id="bgMovement" checked>
                        <label for="bgMovement">Vaftiz sırasında arkaplan hareket etsin</label>
                    </div>
                    <div class="checkbox-container">
                        <input type="checkbox" id="personEffect" checked>
                        <label for="personEffect">Kişiye su efekti uygula</label>
                    </div>
                </div>
            </div>
            
            <button class="baptize-btn" id="baptizeBtn">
                <i class="fas fa-hand-holding-water"></i> VAFTİZ ET
            </button>
        </div>
        
        <div class="instructions">
            <h3><i class="fas fa-info-circle"></i> Nasıl Kullanılır:</h3>
            <ol style="padding-left: 20px; line-height: 1.8;">
                <li>Kişi fotoğrafı yükleyin veya webcam ile çekin</li>
                <li>İstediğiniz bir müzik dosyası seçin (MP3, WAV, vb.)</li>
                <li>Efekt ayarlarınızı belirleyin</li>
                <li>"Vaftiz Et" butonuna basın</li>
                <li>Su damlaları dökülmeye başlayacak, seçtiğiniz müzik çalacaktır</li>
                <li>Arkaplan hareketi etkinleştirilmişse, arkaplan yavaşça hareket edecektir</li>
            </ol>
        </div>
    </div>
    
    <footer>
        <p>Kutsal Vaftiz Simülasyonu © 2023 | Ruhunuzu arındırın, yeniden doğun!</p>
    </footer>
    
    <!-- Webcam Modal -->
    <div class="modal" id="webcamModal">
        <div class="modal-content">
            <span class="close-modal" id="closeModal">&times;</span>
            <h2 style="color:#00bcd4; margin-bottom:20px; text-align:center;">
                <i class="fas fa-camera"></i> Webcam ile Fotoğraf Çek
            </h2>
            
            <div class="webcam-container">
                <video id="webcamVideo" autoplay playsinline></video>
                <button class="capture-btn" id="captureBtn">
                    <i class="fas fa-camera"></i> Fotoğraf Çek
                </button>
            </div>
            
            <div style="margin-top:25px; color:#aaa; font-size:0.9rem; text-align:center;">
                <p>Webcam'inizin kullanımına izin verin. Fotoğraf çekmek için "Fotoğraf Çek" butonuna basın.</p>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const baptizeBtn = document.getElementById('baptizeBtn');
            const musicFileInput = document.getElementById('musicFile');
            const photoFileInput = document.getElementById('photoFile');
            const removePhotoBtn = document.getElementById('removePhoto');
            const webcamBtn = document.getElementById('webcamBtn');
            const backgroundOverlay = document.getElementById('backgroundOverlay');
            const bgMovementCheckbox = document.getElementById('bgMovement');
            const personEffectCheckbox = document.getElementById('personEffect');
            const baptismArea = document.getElementById('baptismArea');
            const waterPool = document.getElementById('waterPool');
            const webcamModal = document.getElementById('webcamModal');
            const closeModal = document.getElementById('closeModal');
            const webcamVideo = document.getElementById('webcamVideo');
            const captureBtn = document.getElementById('captureBtn');
            const photoPreview = document.getElementById('photoPreview');
            const personPhoto = document.getElementById('personPhoto');
            const uploadedPhoto = document.getElementById('uploadedPhoto');
            const defaultAvatar = document.getElementById('defaultAvatar');
            
            let selectedMusicFile = null;
            let bgMovementEnabled = true;
            let personEffectEnabled = true;
            let stream = null;
            
            // Müzik dosyası seçme
            musicFileInput.addEventListener('change', function(e) {
                if (e.target.files && e.target.files[0]) {
                    selectedMusicFile = e.target.files[0];
                    showNotification(`"${selectedMusicFile.name}" müzik dosyası seçildi!`);
                }
            });
            
            // Fotoğraf seçme
            photoFileInput.addEventListener('change', function(e) {
                if (e.target.files && e.target.files[0]) {
                    const file = e.target.files[0];
                    const reader = new FileReader();
                    
                    reader.onload = function(e) {
                        uploadedPhoto.src = e.target.result;
                        uploadedPhoto.style.display = 'block';
                        defaultAvatar.style.display = 'none';
                        
                        // Önizleme
                        photoPreview.innerHTML = `<img src="${e.target.result}" alt="Kişi Fotoğrafı">`;
                        
                        showNotification(`"${file.name}" kişi fotoğrafı seçildi!`);
                    };
                    
                    reader.readAsDataURL(file);
                }
            });
            
            // Fotoğraf kaldırma
            removePhotoBtn.addEventListener('click', function() {
                uploadedPhoto.src = '';
                uploadedPhoto.style.display = 'none';
                defaultAvatar.style.display = 'block';
                photoPreview.innerHTML = `<span>Fotoğraf yüklenmedi</span>`;
                showNotification("Kişi fotoğrafı kaldırıldı!");
            });
            
            // Arkaplan hareketi kontrolü
            bgMovementCheckbox.addEventListener('change', function() {
                bgMovementEnabled = this.checked;
            });
            
            // Kişi efekti kontrolü
            personEffectCheckbox.addEventListener('change', function() {
                personEffectEnabled = this.checked;
            });
            
            // Webcam butonu
            webcamBtn.addEventListener('click', function() {
                webcamModal.style.display = 'flex';
                startWebcam();
            });
            
            // Modal kapatma
            closeModal.addEventListener('click', function() {
                webcamModal.style.display = 'none';
                stopWebcam();
            });
            
            // Webcam başlatma
            function startWebcam() {
                if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
                    navigator.mediaDevices.getUserMedia({ video: true })
                        .then(function(mediaStream) {
                            stream = mediaStream;
                            webcamVideo.srcObject = stream;
                        })
                        .catch(function(error) {
                            console.error("Webcam error: ", error);
                            showNotification("Webcam'e erişilemedi. Lütfen izinleri kontrol edin.", true);
                            webcamModal.style.display = 'none';
                        });
                } else {
                    showNotification("Tarayıcınız webcam özelliğini desteklemiyor.", true);
                    webcamModal.style.display = 'none';
                }
            }
            
            // Webcam durdurma
            function stopWebcam() {
                if (stream) {
                    stream.getTracks().forEach(track => track.stop());
                    webcamVideo.srcObject = null;
                    stream = null;
                }
            }
            
            // Fotoğraf çekme
            captureBtn.addEventListener('click', function() {
                const canvas = document.createElement('canvas');
                canvas.width = webcamVideo.videoWidth;
                canvas.height = webcamVideo.videoHeight;
                const ctx = canvas.getContext('2d');
                ctx.drawImage(webcamVideo, 0, 0, canvas.width, canvas.height);
                
                const dataUrl = canvas.toDataURL('image/png');
                
                // Kişi fotoğrafını ayarla
                uploadedPhoto.src = dataUrl;
                uploadedPhoto.style.display = 'block';
                defaultAvatar.style.display = 'none';
                
                // Önizleme
                photoPreview.innerHTML = `<img src="${dataUrl}" alt="Webcam Fotoğrafı">`;
                
                showNotification("Webcam fotoğrafı başarıyla yüklendi!");
                
                webcamModal.style.display = 'none';
                stopWebcam();
            });
            
            // Vaftiz butonuna tıklama
            baptizeBtn.addEventListener('click', function() {
                if (!selectedMusicFile) {
                    showNotification("Lütfen önce bir müzik dosyası seçin!", true);
                    return;
                }
                
                if (uploadedPhoto.style.display === 'none') {
                    showNotification("Lütfen bir kişi fotoğrafı yükleyin!", true);
                    return;
                }
                
                // Müziği çal
                const objectURL = URL.createObjectURL(selectedMusicFile);
                const audioPlayer = new Audio(objectURL);
                audioPlayer.play();
                
                // Su havuzu animasyonu
                waterPool.classList.add('water-rising');
                
                // Damlaları oluştur
                createWaterDrops();
                
                // Kişi animasyonu
                if (personEffectEnabled) {
                    personPhoto.style.transform = 'scale(1.05)';
                    personPhoto.style.boxShadow = '0 0 40px rgba(79, 195, 247, 0.8)';
                    setTimeout(() => {
                        personPhoto.style.transform = 'scale(1)';
                        personPhoto.style.boxShadow = '0 0 30px rgba(0,0,0,0.7)';
                    }, 500);
                }
                
                // Arkaplan hareketi
                if (bgMovementEnabled) {
                    backgroundOverlay.style.animation = 'bgMove 30s linear infinite';
                    
                    // 30 saniye sonra animasyonu durdur
                    setTimeout(() => {
                        backgroundOverlay.style.animation = 'none';
                    }, 30000);
                }
                
                // Butonu geçici olarak devre dışı bırak
                baptizeBtn.disabled = true;
                baptizeBtn.innerHTML = '<i class="fas fa-sync fa-spin"></i> VAFTİZ EDİLİYOR...';
                
                setTimeout(() => {
                    baptizeBtn.disabled = false;
                    baptizeBtn.innerHTML = '<i class="fas fa-hand-holding-water"></i> VAFTİZ ET';
                    waterPool.classList.remove('water-rising');
                    waterPool.style.height = "40px";
                    
                    // Başarı mesajı
                    showNotification("Vaftiz işlemi tamamlandı! Ruhunuz arındı.");
                }, 5000);
            });
            
            // Su damlalarını oluşturma fonksiyonu
            function createWaterDrops() {
                const dropCount = 200;
                
                for (let i = 0; i < dropCount; i++) {
                    setTimeout(() => {
                        createDrop();
                    }, i * 20);
                }
            }
            
            // Tek bir damla oluşturma
            function createDrop() {
                const drop = document.createElement('div');
                drop.className = 'water-drop';
                
                // Rastgele pozisyon
                const xPos = Math.random() * (baptismArea.offsetWidth - 20);
                drop.style.left = `${xPos}px`;
                
                // Rastgele boyut
                const size = 3 + Math.random() * 12;
                drop.style.width = `${size}px`;
                drop.style.height = `${size * 2}px`;
                
                // Rastgele düşme süresi
                const duration = 0.4 + Math.random() * 1.2;
                drop.style.animation = `fall ${duration}s linear forwards`;
                
                baptismArea.appendChild(drop);
                
                // Damla yere düştüğünde sıçrama efekti
                setTimeout(() => {
                    createSplash(xPos);
                    drop.remove();
                }, duration * 900);
            }
            
            // Su sıçrama efekti
            function createSplash(xPos) {
                const splash = document.createElement('div');
                splash.className = 'water-splash';
                splash.style.left = `${xPos}px`;
                splash.style.bottom = '40px';
                splash.style.animation = `splash 0.6s ease-out forwards`;
                
                baptismArea.appendChild(splash);
                
                setTimeout(() => {
                    splash.remove();
                }, 600);
            }
            
            // Bildirim fonksiyonu
            function showNotification(message, isError = false) {
                // Eğer önceki bildirim varsa kaldır
                const oldNotification = document.querySelector('.notification');
                if (oldNotification) oldNotification.remove();
                
                const notification = document.createElement('div');
                notification.className = `notification ${isError ? 'error' : ''}`;
                notification.textContent = message;
                notification.style.cssText = `
                    position: fixed;
                    top: 20px;
                    right: 20px;
                    padding: 15px 25px;
                    background: ${isError ? '#ff5252' : '#4CAF50'};
                    color: white;
                    border-radius: 8px;
                    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
                    z-index: 1000;
                    font-weight: bold;
                    animation: fadeIn 0.3s, fadeOut 0.3s 2.7s;
                `;
                
                document.body.appendChild(notification);
                
                // 3 saniye sonra kaldır
                setTimeout(() => {
                    if (notification.parentNode) {
                        notification.parentNode.removeChild(notification);
                    }
                }, 3000);
            }
            
            // CSS animation keyframes
            const style = document.createElement('style');
            style.textContent = `
                @keyframes fadeIn {
                    from { opacity: 0; transform: translateY(-20px); }
                    to { opacity: 1; transform: translateY(0); }
                }
                
                @keyframes fadeOut {
                    from { opacity: 1; transform: translateY(0); }
                    to { opacity: 0; transform: translateY(-20px); }
                }
            `;
            document.head.appendChild(style);
        });
    </script>
</body>
</html>
