<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ücretsiz Site Yayınlama Rehberi</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2980, #26d0ce);
            color: #333;
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .container {
            max-width: 1200px;
            width: 100%;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
            padding: 40px;
            margin: 20px 0;
        }
        
        header {
            text-align: center;
            margin-bottom: 40px;
        }
        
        h1 {
            font-size: 3.5rem;
            margin-bottom: 15px;
            color: #1a2980;
            background: linear-gradient(to right, #1a2980, #26d0ce);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .subtitle {
            font-size: 1.4rem;
            color: #555;
            max-width: 800px;
            margin: 0 auto;
            line-height: 1.6;
        }
        
        .platforms {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            margin: 40px 0;
        }
        
        .platform-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            border: 1px solid #eee;
        }
        
        .platform-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
        }
        
        .platform-header {
            padding: 25px;
            background: linear-gradient(135deg, #1a2980, #26d0ce);
            color: white;
        }
        
        .platform-header h3 {
            font-size: 1.8rem;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .platform-body {
            padding: 25px;
        }
        
        .features {
            list-style: none;
            margin: 20px 0;
        }
        
        .features li {
            padding: 10px 0;
            border-bottom: 1px solid #eee;
            display: flex;
            align-items: flex-start;
            gap: 10px;
        }
        
        .features li:last-child {
            border-bottom: none;
        }
        
        .features li i {
            color: #26d0ce;
            margin-top: 4px;
        }
        
        .btn {
            display: inline-block;
            padding: 14px 28px;
            background: linear-gradient(135deg, #1a2980, #26d0ce);
            color: white;
            border: none;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            text-decoration: none;
            transition: all 0.3s;
            margin-top: 15px;
            box-shadow: 0 5px 15px rgba(38, 208, 206, 0.4);
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(38, 208, 206, 0.6);
        }
        
        .guide {
            background: white;
            border-radius: 15px;
            padding: 40px;
            margin: 40px 0;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
        }
        
        .guide h2 {
            font-size: 2.5rem;
            color: #1a2980;
            margin-bottom: 30px;
            text-align: center;
        }
        
        .steps {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            counter-reset: step-counter;
        }
        
        .step {
            position: relative;
            padding: 30px;
            background: #f9f9ff;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }
        
        .step::before {
            counter-increment: step-counter;
            content: counter(step-counter);
            position: absolute;
            top: -20px;
            left: -20px;
            width: 50px;
            height: 50px;
            background: linear-gradient(135deg, #1a2980, #26d0ce);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .step h3 {
            font-size: 1.5rem;
            margin-bottom: 15px;
            color: #1a2980;
            padding-left: 40px;
        }
        
        .step p {
            color: #555;
            line-height: 1.7;
        }
        
        footer {
            text-align: center;
            padding: 30px;
            color: white;
            width: 100%;
            margin-top: auto;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }
            
            h1 {
                font-size: 2.5rem;
            }
            
            .subtitle {
                font-size: 1.2rem;
            }
            
            .steps {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-cloud-upload-alt"></i> Ücretsiz Site Yayınlama</h1>
            <p class="subtitle">Alan adı almadan sitenizi dünyaya açın! Aşağıdaki platformlardan birini seçerek sitenizi ücretsiz yayınlayabilirsiniz.</p>
        </header>
        
        <div class="platforms">
            <!-- GitHub Pages -->
            <div class="platform-card">
                <div class="platform-header">
                    <h3><i class="fab fa-github"></i> GitHub Pages</h3>
                </div>
                <div class="platform-body">
                    <ul class="features">
                        <li><i class="fas fa-check-circle"></i> Tamamen ücretsiz</li>
                        <li><i class="fas fa-check-circle"></i> Sınırsız statik site barındırma</li>
                        <li><i class="fas fa-check-circle"></i> HTTPS desteği</li>
                        <li><i class="fas fa-check-circle"></i> GitHub ile entegrasyon</li>
                    </ul>
                    <a href="https://pages.github.com/" target="_blank" class="btn">Kullanmaya Başla</a>
                </div>
            </div>
            
            <!-- Netlify -->
            <div class="platform-card">
                <div class="platform-header">
                    <h3><i class="fas fa-bolt"></i> Netlify</h3>
                </div>
                <div class="platform-body">
                    <ul class="features">
                        <li><i class="fas fa-check-circle"></i> Süper hızlı dağıtım</li>
                        <li><i class="fas fa-check-circle"></i> Sürükle-bırak ile deploy</li>
                        <li><i class="fas fa-check-circle"></i> Form ve kimlik doğrulama</li>
                        <li><i class="fas fa-check-circle"></i> Global CDN ağı</li>
                    </ul>
                    <a href="https://www.netlify.com/" target="_blank" class="btn">Kullanmaya Başla</a>
                </div>
            </div>
            
            <!-- Vercel -->
            <div class="platform-card">
                <div class="platform-header">
                    <h3><i class="fas fa-rocket"></i> Vercel</h3>
                </div>
                <div class="platform-body">
                    <ul class="features">
                        <li><i class="fas fa-check-circle"></i> Anında dağıtım</li>
                        <li><i class="fas fa-check-circle"></i> Edge fonksiyonları</li>
                        <li><i class="fas fa-check-circle"></i> Mükemmel Next.js desteği</li>
                        <li><i class="fas fa-check-circle"></i> Gerçek zamanlı güncellemeler</li>
                    </ul>
                    <a href="https://vercel.com/" target="_blank" class="btn">Kullanmaya Başla</a>
                </div>
            </div>
        </div>
        
        <div class="guide">
            <h2><i class="fas fa-graduation-cap"></i> Site Yayınlama Adımları</h2>
            <div class="steps">
                <div class="step">
                    <h3>Platform Seçimi</h3>
                    <p>GitHub Pages, Netlify veya Vercel gibi bir platform seçin. Tümü ücretsiz ve kullanımı kolaydır.</p>
                </div>
                
                <div class="step">
                    <h3>Hesap Oluştur</h3>
                    <p>Seçtiğiniz platformda ücretsiz bir hesap oluşturun. GitHub ile giriş yapabilirsiniz.</p>
                </div>
                
                <div class="step">
                    <h3>Projenizi Yükleyin</h3>
                    <p>HTML, CSS ve JavaScript dosyalarınızı bir klasöre koyun ve platforma yükleyin.</p>
                </div>
                
                <div class="step">
                    <h3>Siteyi Yayınlayın</h3>
                    <p>Platformun talimatlarını izleyerek sitenizi yayınlayın. Birkaç dakika içinde yayında olacaktır!</p>
                </div>
            </div>
            
            <div style="text-align: center; margin-top: 40px;">
                <a href="#" class="btn" style="font-size: 1.3rem; padding: 16px 40px;">
                    <i class="fas fa-play"></i> Site Yayınlamaya Başla
                </a>
            </div>
        </div>
    </div>
    
    <footer>
        <p>© 2023 Ücretsiz Site Yayınlama Rehberi | Alan adı almadan sitenizi dünyaya açın</p>
    </footer>
</body>
</html>
