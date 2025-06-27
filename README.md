<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sanatsal Vaftiz Simülasyonu</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Playfair Display', serif;
        }
        
        body {
            background: linear-gradient(45deg, #1a0a2e, #0d0630, #1a0a2e);
            color: #e8e1ef;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            position: relative;
            background-attachment: fixed;
        }
        
        .container {
            max-width: 1000px;
            width: 95%;
            text-align: center;
            padding: 2rem;
            background: rgba(10, 5, 24, 0.85);
            border-radius: 20px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.7);
            z-index: 10;
            backdrop-filter: blur(8px);
            margin: 20px 0;
            border: 2px solid rgba(113, 89, 193, 0.5);
        }
        
        .header {
            margin-bottom: 2rem;
            padding: 1rem;
            border-bottom: 2px solid rgba(113, 89, 193, 0.3);
        }
        
        h1 {
            font-size: 3.8rem;
            margin-bottom: 0.5rem;
            color: #c9b6e4;
            text-shadow: 0 0 15px rgba(201, 182, 228, 0.6);
            font-weight: 700;
            letter-spacing: 2px;
            position: relative;
            background: linear-gradient(to right, #a78bfa, #8b5cf6, #7c3aed);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        h1::after {
            content: "";
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 300px;
            height: 3px;
            background: linear-gradient(to right, transparent, #8b5cf6, transparent);
            border-radius: 2px;
        }
        
        .subtitle {
            font-size: 1.4rem;
            margin-top: 1.5rem;
            color: #d8c7ff;
            max-width: 700px;
            margin-left: auto;
            margin-right: auto;
            line-height: 1.6;
            font-style: italic;
            text-shadow: 0 2px 4px rgba(0,0,0,0.5);
        }
        
        .simulation-area {
            position: relative;
            height: 500px;
            width: 100%;
            margin: 2rem 0;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .artistic-background {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('https://images.unsplash.com/photo-1600585154340-be6161a56a0c?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80') center/cover;
            filter: brightness(0.7) saturate(1.2) contrast(0.9);
            opacity: 0.9;
            z-index: 1;
        }
        
        .stained-glass {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, transparent 20%, #1a0a2e 150%),
                        linear-gradient(45deg, rgba(106, 27, 154, 0.2) 0%, rgba(49, 27, 146, 0.3) 100%);
            z-index: 2;
        }
        
        .baptism-scene {
            position: relative;
            width: 350px;
            height: 350px;
            z-index: 3;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .bathtub {
            width: 300px;
            height: 180px;
            background: url('https://images.unsplash.com/photo-1611158022181-3b2a2a5a5e5b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80') center/cover;
            border-radius: 10px 10px 50% 50%;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6), 
                        inset 0 -10px 30px rgba(0, 0, 0, 0.7);
            border: 5px solid #5d4a82;
            position: relative;
            overflow: hidden;
        }
        
        .person {
            position: absolute;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            width: 120px;
            height: 150px;
            background: url('https://images.unsplash.com/photo-1567532939604-b6b5b0e1607d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80') center/cover;
            border-radius: 50%;
            z-index: 4;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
        }
        
        .water-level {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 40px;
            background: linear-gradient(to top, rgba(64, 196, 255, 0.7), rgba(100, 181, 246, 0.9));
            border-radius: 0 0 50% 50%;
            transition: height 2s ease;
            z-index: 3;
        }
        
        .controls {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            margin-top: 2rem;
        }
        
        .baptize-btn {
            padding: 1.4rem 3rem;
            font-size: 1.8rem;
            font-weight: bold;
            background: linear-gradient(45deg, #7e57c2, #5e35b1, #4527a0);
            color: white;
            border: none;
            border-radius: 60px;
            cursor: pointer;
            transition: all 0.4s ease;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
            position: relative;
            overflow: hidden;
            margin: 0 auto;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            z-index: 20;
            font-family: 'Playfair Display', serif;
            letter-spacing: 1px;
        }
        
        .baptize-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.7);
            background: linear-gradient(45deg, #9575cd, #7e57c2, #673ab7);
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
            background: radial-gradient(circle, rgba(255,255,255,0.3) 0%, rgba(255,255,255,0) 70%);
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
            width: 10px;
            height: 20px;
            background: linear-gradient(to bottom, rgba(255,255,255,0.95), rgba(100, 181, 246, 0.8));
            border-radius: 50% 50% 60% 40%;
            z-index: 5;
            pointer-events: none;
            box-shadow: 0 0 15px rgba(64, 196, 255, 0.9);
            filter: blur(1px);
        }
        
        .water-splash {
            position: absolute;
            width: 30px;
            height: 15px;
            background: rgba(64, 196, 255, 0.7);
            border-radius: 50%;
            z-index: 4;
            pointer-events: none;
            box-shadow: 0 0 12px rgba(64, 196, 255, 0.9);
        }
        
        .artistic-details {
            position: absolute;
            top: 20px;
            left: 20px;
            right: 20px;
            bottom: 20px;
            pointer-events: none;
            z-index: 2;
        }
        
        .detail-1 {
            position: absolute;
            top: 10%;
            left: 10%;
            width: 80px;
            height: 80px;
            background: url('https://images.unsplash.com/photo-1595433707802-6b2626ef1c91?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1480&q=80') center/cover;
            border-radius: 50%;
            opacity: 0.7;
            transform: rotate(15deg);
        }
        
        .detail-2 {
            position: absolute;
            bottom: 20%;
            right: 10%;
            width: 100px;
            height: 100px;
            background: url('https://images.unsplash.com/photo-1617469767053-d3b523a0b982?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1742&q=80') center/cover;
            border-radius: 10px;
            opacity: 0.6;
            transform: rotate(-10deg);
        }
        
        .water-effect {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
        
        .sound-control {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(10, 5, 24, 0.8);
            border-radius: 50%;
            width: 50px;
            height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            z-index: 20;
            border: 2px solid #7e57c2;
            box-shadow: 0 5px 15px rgba(0,0,0,0.4);
        }
        
        .sound-control i {
            font-size: 24px;
            color: #c9b6e4;
        }
        
        .instructions {
            margin-top: 2rem;
            padding: 1.5rem;
            background: rgba(30, 15, 60, 0.5);
            border-radius: 15px;
            font-size: 1.1rem;
            text-align: center;
            border: 1px solid rgba(113, 89, 193, 0.3);
            max-width: 700px;
            margin-left: auto;
            margin-right: auto;
        }
        
        .instructions p {
            line-height: 1.8;
            margin-top: 10px;
        }
        
        footer {
            margin-top: 2rem;
            text-align: center;
            font-size: 1rem;
            color: rgba(232, 225, 239, 0.7);
            padding: 1.2rem;
            width: 100%;
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
        
        @keyframes waterRise {
            to {
                height: 140px;
            }
        }
        
        .water-rising {
            animation: waterRise 3.5s forwards;
        }
        
        @keyframes glow {
            0% {
                box-shadow: 0 0 10px rgba(201, 182, 228, 0.6);
            }
            50% {
                box-shadow: 0 0 30px rgba(201, 182, 228, 0.9);
            }
            100% {
                box-shadow: 0 0 10px rgba(201, 182, 228, 0.6);
            }
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 1rem;
                width: 98%;
            }
            
            h1 {
                font-size: 2.5rem;
            }
            
            .subtitle {
                font-size: 1.1rem;
            }
            
            .simulation-area {
                height: 400px;
            }
            
            .baptism-scene {
                width: 280px;
                height: 280px;
            }
            
            .bathtub {
                width: 250px;
                height: 150px;
            }
            
            .person {
                width: 100px;
                height: 130px;
            }
            
            .baptize-btn {
                padding: 1.2rem 2rem;
                font-size: 1.4rem;
            }
        }
    </style>
</head>
<body>
    <div class="water-effect" id="waterEffect"></div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-dove"></i> SANATSAL VAFTİZ</h1>
            <p class="subtitle">Kutsal suyla ruhunuzu arındırın ve yeniden doğun. Rönesans tarzında unutulmaz bir deneyim.</p>
        </div>
        
        <div class="simulation-area">
            <div class="artistic-background"></div>
            <div class="stained-glass"></div>
            
            <div class="artistic-details">
                <div class="detail-1"></div>
                <div class="detail-2"></div>
            </div>
            
            <div class="baptism-scene">
                <div class="bathtub">
                    <div class="water-level" id="waterLevel"></div>
                    <div class="person"></div>
                </div>
            </div>
        </div>
        
        <div class="controls">
            <button class="baptize-btn" id="baptizeBtn">
                <i class="fas fa-hand-holding-water"></i> VAFTİZİ BAŞLAT
            </button>
        </div>
        
        <div class="instructions">
            <p>Butona basarak sanatsal vaftiz deneyimini başlatın. Su damlaları dökülmeye başlayacak, küvet suyla dolacak ve ruhunuz arınacak.</p>
        </div>
    </div>
    
    <div class="sound-control" id="soundControl">
        <i class="fas fa-volume-up"></i>
    </div>
    
    <footer>
        <p>Sanatsal Vaftiz Simülasyonu © 2023 | Rönesans Ruhuyla Tasarlanmıştır</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const baptizeBtn = document.getElementById('baptizeBtn');
            const waterLevel = document.getElementById('waterLevel');
            const soundControl = document.getElementById('soundControl');
            const waterEffect = document.getElementById('waterEffect');
            
            // Ses efekti oluştur
            const audioContext = new (window.AudioContext || window.webkitAudioContext)();
            let waterSound;
            
            // Su sesi oluşturma fonksiyonu
            function createWaterSound() {
                waterSound = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                waterSound.type = 'sine';
                waterSound.frequency.value = 200;
                
                gainNode.gain.value = 0.1;
                
                waterSound.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                // Rastgele modülasyon
                setInterval(() => {
                    waterSound.frequency.setValueAtTime(
                        180 + Math.random() * 40, 
                        audioContext.currentTime
                    );
                }, 200);
            }
            
            // Ses kontrolü
            let isMuted = false;
            
            soundControl.addEventListener('click', function() {
                isMuted = !isMuted;
                
                if (isMuted) {
                    if (waterSound) waterSound.stop();
                    soundControl.innerHTML = '<i class="fas fa-volume-mute"></i>';
                } else {
                    createWaterSound();
                    waterSound.start();
                    soundControl.innerHTML = '<i class="fas fa-volume-up"></i>';
                }
            });
            
            // Vaftiz butonuna tıklama
            baptizeBtn.addEventListener('click', function() {
                // Su sesini başlat
                if (!isMuted) {
                    createWaterSound();
                    waterSound.start();
                }
                
                // Su seviyesi animasyonu
                waterLevel.classList.add('water-rising');
                
                // Damlaları oluştur
                createWaterDrops();
                
                // Butonu geçici olarak devre dışı bırak
                baptizeBtn.disabled = true;
                baptizeBtn.innerHTML = '<i class="fas fa-sync fa-spin"></i> VAFTİZ EDİLİYOR...';
                
                // Butona parıltı efekti ekle
                baptizeBtn.style.animation = 'glow 2s infinite';
                
                setTimeout(() => {
                    baptizeBtn.disabled = false;
                    baptizeBtn.innerHTML = '<i class="fas fa-hand-holding-water"></i> VAFTİZİ BAŞLAT';
                    waterLevel.classList.remove('water-rising');
                    waterLevel.style.height = "40px";
                    baptizeBtn.style.animation = 'none';
                    
                    // Başarı mesajı
                    showNotification("Vaftiz işlemi tamamlandı! Ruhunuz arındı.");
                }, 5000);
            });
            
            // Su damlalarını oluşturma fonksiyonu
            function createWaterDrops() {
                const dropCount = 150;
                
                for (let i = 0; i < dropCount; i++) {
                    setTimeout(() => {
                        createDrop();
                    }, i * 30);
                }
            }
            
            // Tek bir damla oluşturma
            function createDrop() {
                const drop = document.createElement('div');
                drop.className = 'water-drop';
                
                // Rastgele pozisyon
                const xPos = Math.random() * window.innerWidth;
                drop.style.left = `${xPos}px`;
                
                // Rastgele boyut
                const size = 5 + Math.random() * 15;
                drop.style.width = `${size}px`;
                drop.style.height = `${size * 2}px`;
                
                // Rastgele düşme süresi
                const duration = 0.5 + Math.random() * 1.5;
                drop.style.animation = `fall ${duration}s linear forwards`;
                
                waterEffect.appendChild(drop);
                
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
                splash.style.bottom = '0';
                splash.style.animation = `splash 0.6s ease-out forwards`;
                
                waterEffect.appendChild(splash);
                
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
                    background: ${isError ? '#ff5252' : '#7e57c2'};
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
