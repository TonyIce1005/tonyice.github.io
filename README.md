# tonyice.github.io
昱諾電腦網站
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>昱諾電腦 YouKnowPC | Promising PC</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&family=Noto+Sans+TC:wght@300;700&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollToPlugin.min.js"></script>
    <style>
        :root {
            --bg-dark: #0a0a0a;
            --bg-section: #0d0d0d;
            --main-cyan: #00e5ff;
            --text-gray: #a0a0a0;
        }

        html, body {
            margin: 0; padding: 0;
            background: var(--bg-dark);
            color: white;
            font-family: 'Noto Sans TC', sans-serif;
            overflow-x: hidden;
            -webkit-overflow-scrolling: touch;
        }

        /* --- 1. 導覽列 --- */
        nav {
            position: fixed; 
            top: -96px; 
            left: 0; 
            width: 100%; 
            height: 100px; 
            display: flex; justify-content: space-between; align-items: center;
            padding: 0 5%; box-sizing: border-box;
            background: rgba(10, 10, 10, 0.98); backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--main-cyan); 
            box-shadow: 0 2px 10px rgba(0, 229, 255, 0.15); 
            z-index: 1000;
            transition: top 0.4s cubic-bezier(0.19, 1, 0.22, 1);
        }

        .nav-brand {
            display: flex;
            align-items: center;
            gap: 14px; 
            font-family: 'Orbitron'; 
            color: var(--main-cyan); 
            font-weight: bold; 
            font-size: 1.4rem;
        }

        .nav-logo { height: 80px; width: auto; object-fit: contain; }
        .nav-trigger { position: fixed; top: 0; left: 0; width: 100%; height: 45px; z-index: 1001; }
        .nav-trigger:hover + nav, nav:hover { top: 0; box-shadow: 0 5px 25px rgba(0, 229, 255, 0.25); }
        .nav-links { display: flex; align-items: center; }
        .nav-links a { color: white; text-decoration: none; cursor: pointer; font-weight: 700; font-size: 1.05rem; transition: 0.3s; margin-left: 25px; }
        .nav-links a:hover { color: var(--main-cyan); text-shadow: 0 0 10px var(--main-cyan); }

        /* --- 2. 主視覺區 --- */
        .hero {
            height: 100vh; 
            display: flex; 
            flex-direction: column; 
            justify-content: center; 
            align-items: center; 
            text-align: center;
            padding: 0 20px;
            box-sizing: border-box;
        }

        .hero-slogan {
            font-family: 'Orbitron', sans-serif;
            font-size: clamp(1.1rem, 2.5vw, 1.8rem); 
            color: var(--main-cyan);
            letter-spacing: 12px; 
            margin: 22px 0 18px 0;
            font-weight: 700;
            text-indent: 12px; 
        }

        /* --- 3. 通用區塊基礎樣式 --- */
        .main-section { padding: 120px 8% 100px; box-sizing: border-box; }
        .main-section:nth-of-type(even) { background: var(--bg-section); }
        .section-title { font-family: 'Orbitron'; font-size: 2.5rem; color: var(--main-cyan); text-align: center; margin-bottom: 60px; letter-spacing: 5px; }
        
        .section-content-center {
            max-width: 900px; margin: 0 auto; font-size: 1.15rem; line-height: 2.2; color: #e0e0e0; letter-spacing: 1.5px; text-align: justify;
        }

        /* --- 4. 商標與名稱由來（完美自適應無留白排版） --- */
        .origin-wrapper {
            display: flex; gap: 50px; max-width: 1200px; margin: 0 auto; flex-wrap: wrap;
        }
        
        .origin-name-side {
            flex: 1; min-width: 320px;
        }
        .name-card-sticky {
            background: rgba(255, 255, 255, 0.01); border: 1px solid rgba(0, 229, 255, 0.15); border-radius: 12px; padding: 45px 35px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5); position: sticky; top: 140px; transition: 0.4s;
        }
        .name-card-sticky:hover { border-color: var(--main-cyan); box-shadow: 0 15px 35px rgba(0, 229, 255, 0.15); }
        .name-card-sticky h3 { font-size: 1.5rem; color: #fff; margin-top: 0; margin-bottom: 25px; border-bottom: 2px solid var(--main-cyan); padding-bottom: 12px; letter-spacing: 2px; }
        .name-card-sticky p { font-size: 1.15rem; line-height: 2.2; color: #e0e0e0; text-align: justify; margin: 0; letter-spacing: 1px; }

        .origin-logo-side {
            flex: 1.3; min-width: 380px; display: flex; flex-direction: column; gap: 50px;
        }
        
        /* 每個歷代版本的直向發展貨櫃 */
        .timeline-version-block {
            display: flex; flex-direction: column; gap: 20px; width: 100%; align-items: flex-start;
        }
        
        .logo-timeline-card {
            background: rgba(255, 255, 255, 0.01); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 12px; padding: 30px 25px; transition: 0.4s; position: relative; width: 100%; box-sizing: border-box;
        }
        .logo-timeline-card::before {
            content: ''; position: absolute; left: -2px; top: 30px; width: 4px; height: 35px; background: rgba(255,255,255,0.1); transition: 0.4s;
        }
        
        /* 💡 修正核心：寬度改為 fit-content，高度 auto，完美貼合商標形狀，消滅任何黑底留白 */
        .independent-img-window {
            width: fit-content; max-width: 100%; display: flex; justify-content: center; align-items: center; 
            background: rgba(0,0,0,0.2); border: 1px solid rgba(0, 229, 255, 0.15); border-radius: 16px; padding: 0; 
            box-sizing: border-box; transition: all 0.5s cubic-bezier(0.165, 0.84, 0.44, 1); margin-left: 5px; overflow: hidden; 
        }

        .independent-history-img {
            display: block; max-width: 100%; height: auto; max-height: 400px; object-fit: contain; mix-blend-mode: screen; transition: transform 0.5s ease;
        }

        /* 懸停動態極速反饋 */
        .timeline-version-block:hover .logo-timeline-card {
            background: rgba(255, 255, 255, 0.02); border-color: rgba(0, 229, 255, 0.2); transform: translateY(-3px);
        }
        .timeline-version-block:hover .logo-timeline-card::before {
            background: var(--main-cyan); box-shadow: 0 0 10px var(--main-cyan);
        }
        .timeline-version-block:hover .independent-img-window {
            border-color: rgba(0, 229, 255, 0.4); box-shadow: 0 15px 35px rgba(0, 229, 255, 0.15); transform: translateY(-3px);
        }
        .timeline-version-block:hover .independent-history-img {
            transform: scale(1.02);
        }
        
        /* 目前官方版本高亮色彩階層 */
        .timeline-version-block.current .logo-timeline-card {
            border-color: rgba(0, 229, 255, 0.25); background: rgba(0, 229, 255, 0.01);
        }
        .timeline-version-block.current .logo-timeline-card::before { background: var(--main-cyan); box-shadow: 0 0 10px var(--main-cyan); height: 50px; }
        .timeline-version-block.current .independent-img-window { border-color: rgba(0, 229, 255, 0.25); background: rgba(0, 229, 255, 0.01); }
        
        .timeline-version-block.current:hover .logo-timeline-card { border-color: var(--main-cyan); box-shadow: 0 15px 35px rgba(0, 229, 255, 0.1); }
        .timeline-version-block.current:hover .independent-img-window { border-color: var(--main-cyan); box-shadow: 0 15px 45px rgba(0, 229, 255, 0.3); }

        .timeline-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; flex-wrap: wrap; gap: 10px; }
        .timeline-title { font-size: 1.25rem; color: #fff; font-weight: bold; }
        .current .timeline-title { color: var(--main-cyan); text-shadow: 0 0 10px rgba(0,229,255,0.2); }
        .timeline-date { font-family: 'Orbitron'; font-size: 0.9rem; color: var(--text-gray); letter-spacing: 1px; background: rgba(255,255,255,0.05); padding: 4px 12px; border-radius: 20px; }
        .current .timeline-date { background: rgba(0, 229, 255, 0.1); color: var(--main-cyan); }
        .timeline-body { font-size: 1.05rem; line-height: 1.9; color: #b5b5b5; text-align: justify; margin: 0; }

        /* --- 5. 品牌故事（Z字型錯落排版） --- */
        .story-container { max-width: 1100px; margin: 0 auto; display: flex; flex-direction: column; gap: 80px; }
        .story-row { display: flex; align-items: center; gap: 50px; width: 100%; flex-wrap: wrap; }
        .story-row:nth-child(even) { flex-direction: row-reverse; }
        
        .story-visual-side { flex: 1; min-width: 300px; display: flex; justify-content: center; align-items: center; }
        .visual-block {
            width: 100%; max-width: 320px; height: 180px; background: rgba(0, 229, 255, 0.03);
            border: 1px dashed rgba(0, 229, 255, 0.3); border-radius: 12px; display: flex; flex-direction: column;
            justify-content: center; align-items: center; font-family: 'Orbitron'; position: relative; transition: 0.5s;
        }
        .story-row:hover .visual-block { border-color: var(--main-cyan); background: rgba(0, 229, 255, 0.06); box-shadow: 0 0 20px rgba(0, 229, 255, 0.1); }
        .visual-num { font-size: 3.5rem; font-weight: bold; color: var(--main-cyan); opacity: 0.7; line-height: 1; }
        .visual-sub { font-size: 1rem; color: var(--text-gray); letter-spacing: 4px; margin-top: 5px; text-transform: uppercase; }

        .story-text-side { flex: 1.6; min-width: 320px; }
        .story-text-side h3 { font-size: 1.6rem; color: #fff; margin-top: 0; margin-bottom: 20px; letter-spacing: 2px; display: flex; align-items: center; gap: 10px; }
        .story-text-side h3::before { content: ''; display: inline-block; width: 6px; height: 22px; background: var(--main-cyan); box-shadow: 0 0 8px var(--main-cyan); }
        .story-text-side p { font-size: 1.1rem; line-height: 2.1; color: #d0d0d0; text-align: justify; margin: 0; letter-spacing: 1px; }

        /* --- 6. 作品集區塊 --- */
        #portfolio { padding: 120px 5% 80px; background: #0d0d0d; min-height: 100vh; }
        .portfolio-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 40px; max-width: 1400px; margin: 0 auto; }
        .portfolio-item { position: relative; background: rgba(255,255,255,0.02); border: 1px solid rgba(0,229,255,0.1); border-radius: 12px; transition: all 0.5s cubic-bezier(0.165, 0.84, 0.44, 1); overflow: hidden; display: flex; flex-direction: column; }
        .portfolio-item:hover { transform: translateY(-10px); border-color: var(--main-cyan); box-shadow: 0 15px 30px rgba(0,229,255,0.15); }
        .portfolio-img-container { width: 100%; height: 450px; overflow: hidden; background: #000; }
        .portfolio-img { width: 100%; height: 100%; object-fit: contain; transition: transform 0.8s ease; }
        .portfolio-item:hover .portfolio-img { transform: scale(1.05); }
        .portfolio-info { background: rgba(15, 15, 15, 0.95); padding: 20px; border-top: 1px solid rgba(0,229,255,0.1); }
        .portfolio-info h3 { margin: 0 0 5px; font-size: 1.15rem; color: #fff; letter-spacing: 1px; }
        .portfolio-info span { color: var(--main-cyan); font-size: 0.85rem; font-weight: 700; letter-spacing: 2px; }

        /* --- 7. 頁尾資訊 --- */
        footer { background: #080808; padding: 100px 5%; text-align: center; border-top: 1px solid #1a1a1a; }
        .footer-container { display: flex; flex-wrap: wrap; justify-content: center; align-items: center; gap: 60px; max-width: 1200px; margin: 0 auto; }
        .contact-details { text-align: left; font-size: 1.4rem; line-height: 2.8; flex: 1; min-width: 300px; }
        .contact-details span { color: var(--main-cyan); margin-right: 15px; font-weight: bold; }
        .social-group { display: flex; gap: 40px; justify-content: center; flex-wrap: wrap; }
        .social-box { display: flex; flex-direction: column; align-items: center; gap: 12px; }
        .social-label { font-family: 'Orbitron', sans-serif; font-weight: 700; font-size: 1.3rem; color: #ffffff; letter-spacing: 2px; text-decoration: none; transition: color 0.3s; }
        .social-label:hover { color: var(--main-cyan); text-shadow: 0 0 10px var(--main-cyan); }
        .social-qrcode { width: 140px; height: 140px; object-fit: contain; border: 1px solid rgba(0, 229, 255, 0.2); border-radius: 10px; background: #fff; padding: 6px; box-sizing: border-box; transition: all 0.4s ease; cursor: pointer; }
        .social-qrcode:hover { transform: scale(1.05); border-color: var(--main-cyan); box-shadow: 0 0 20px rgba(0, 229, 255, 0.4); }
    </style>
</head>
<body>

    <div class="nav-trigger"></div>
    
    <!-- 導覽列 -->
    <nav>
        <div class="nav-brand">
            <img class="nav-logo" src="https://i.postimg.cc/SQXZzp5V/5b313dad-6c78-4609-b9be-7374518d759d.png" alt="YouKnowPC Logo">
            <span>YOU KNOW PC</span>
        </div>
        <div class="nav-links">
            <a onclick="scrollToSection('#about')">關於昱諾</a>
            <a onclick="scrollToSection('#brand-origin')">商標由來</a>
            <a onclick="scrollToSection('#history')">品牌故事</a>
            <a onclick="scrollToSection('#portfolio')">作品集</a>
            <a onclick="scrollToSection('#contact')">聯絡我們</a>
        </div>
    </nav>

    <!-- 主視覺區 -->
    <section class="hero">
        <h1 style="font-family:'Orbitron'; font-size: clamp(2.5rem, 8vw, 5.5rem); color:var(--main-cyan); letter-spacing:15px; margin: 0;">YOU KNOW PC</h1>
        <div class="hero-slogan">Trust Starts Here</div>
        <p style="color:var(--text-gray); letter-spacing:8px; margin: 0; font-size:1.3rem;">Promising 昱諾電腦工作室</p>
    </section>

    <!-- 區塊一：關於昱諾 -->
    <section id="about" class="main-section">
        <h2 class="section-title">ABOUT US</h2>
        <div class="section-content-center">
            <p>我們是昱諾電腦工作室。成立於2024/01/23，由對於電腦充滿熱愛與熱情的高中生所創立的電腦工作室，提供客製化高階電競主機組裝、專業硬體檢測維修與系統調教服務。在這裡，我們將複雜的硬體規格轉化為您觸手可及的流暢體驗。無論您需要的是在FPS上大殺四方、沉浸於3A大作的極致高規格電競配備，還是預算有限、高CP值的二手整新主機，昱諾電腦都能依據您的核心需求，打造出最穩定、最契合的專屬硬體方案。</p>
        </div>
    </section>

    <!-- 區塊二：昱諾商標與名稱的由來（自適應寬度對齊版） -->
    <section id="brand-origin" class="main-section">
        <h2 class="section-title">BRAND ORIGIN</h2>
        <div class="origin-wrapper">
            
            <!-- 左側欄位：名稱故事 -->
            <div class="origin-name-side">
                <div class="name-card-sticky">
                    <h3>名稱構想核心</h3>
                    <p>名稱構想花了整整一個月！昱諾的昱是我的名字的中間字，除了希望能夠有個人特色外，昱本身這個字的含意我也很喜歡，如太陽高高在立竿上方，很光明很巔峰的感覺。而【諾】則是希望自己保持初衷，莫忘曾經遭宰羊的教訓，做到【誠信】與【承諾】。</p>
                </div>
            </div>
            
            <!-- 右側欄位：商標歷史縱向時間軸 -->
            <div class="origin-logo-side">
                
                <!-- 第一版區塊 -->
                <div class="timeline-version-block">
                    <div class="logo-timeline-card">
                        <div class="timeline-header">
                            <span class="timeline-title">第一版商標圖</span>
                            <span class="timeline-date">2024/02/10－2024/06/29</span>
                        </div>
                        <p class="timeline-body">原先想用字的變形來設計，但最先版本曾被評論像是小畫家出來的，我意識到還是請專業的朋友來設計好了。</p>
                    </div>
                    <div class="independent-img-window">
                        <img class="independent-history-img" src="https://i.postimg.cc/Pxh4x2JQ/di-yi-ban.jpg" alt="YouKnowPC 第一版商標">
                    </div>
                </div>
                
                <!-- 第二版區塊 -->
                <div class="timeline-version-block">
                    <div class="logo-timeline-card">
                        <div class="timeline-header">
                            <span class="timeline-title">第二版商標圖</span>
                            <span class="timeline-date">2024/06/29－2024/07/13</span>
                        </div>
                        <p class="timeline-body">第二版是目前版本的雛形，是請有背景的朋友幫我設計的，整體相較第一版好了許多。</p>
                    </div>
                    <div class="independent-img-window">
                        <img class="independent-history-img" src="https://i.postimg.cc/MTTShbxK/di-er-ban.jpg" alt="YouKnowPC 第二版商標">
                    </div>
                </div>
                
                <!-- 目前版本區塊：正面與背面圖獨立框上下雙輸出 -->
                <div class="timeline-version-block current">
                    <div class="logo-timeline-card">
                        <div class="timeline-header">
                            <span class="timeline-title">目前官方版本</span>
                            <span class="timeline-date">2024/07/13 至今</span>
                        </div>
                        <p class="timeline-body">經第二版後不斷討論與優化而來，產出了個像樣的商標！商標中的主機，前方是設計成Promising的P，寓意希望工作室能夠很有前途，而側邊與上方，則是透過【昱】變形成主機殼而來，期待工作室能夠如太陽高高在立竿上方，如日中天。</p>
                    </div>
                    <!-- 正面商標獨立框 -->
                    <div class="independent-img-window">
                        <img class="independent-history-img" src="https://i.postimg.cc/kGTwLKnL/zui-zhong-ban.jpg" alt="YouKnowPC 目前官方商標 正面">
                    </div>
                    <!-- 全新追加：背面商標獨立框 -->
                    <div class="independent-img-window">
                        <img class="independent-history-img" src="https://i.postimg.cc/g0GXL5yh/mu-qian-ban-bei-mian.jpg" alt="YouKnowPC 目前官方商標 背面">
                    </div>
                </div>
                
            </div>
        </div>
    </section>

    <!-- 區塊三：生平與品牌故事 -->
    <section id="history" class="main-section">
        <h2 class="section-title">BRAND STORY</h2>
        <div class="story-container">
            
            <!-- 01. 興趣萌芽與培養 -->
            <div class="story-row">
                <div class="story-visual-side">
                    <div class="visual-block">
                        <span class="visual-num">01</span>
                        <span class="visual-sub">Mating Stage</span>
                    </div>
                </div>
                <div class="story-text-side">
                    <h3>興趣萌芽與培養</h3>
                    <p>我在國中二年級時對於電腦的興趣逐漸萌芽，在較熟悉電腦組件的同學帶領下，開始拆拆裝裝自己的電腦，研究電腦的各種零件與性能影響，也愈來愈沉浸在電腦世界中，我開始收購一些二手零件更換自己的電腦，我從中獲得了做其他事情無法帶來的快樂，並開始嘗試學習組裝後販售，一路上磕磕碰碰，像是插錯線導致主機板短路起火，記憶體插拔角度不對導致斷掉，或是因包裝不夠完善使客人收到主機時零件四散等經驗，都成為了我成立工作室很好的養分。</p>
                </div>
            </div>

            <!-- 02. 爆殺I7？爆宰一波！ -->
            <div class="story-row">
                <div class="story-visual-side">
                    <div class="visual-block">
                        <span class="visual-num" style="color: #ff3b3b; text-shadow: 0 0 10px rgba(255,59,59,0.3);">02</span>
                        <span class="visual-sub">The Turning Point</span>
                    </div>
                </div>
                <div class="story-text-side">
                    <h3>爆殺I7？爆宰一波！</h3>
                    <p>國三時於某蝦上購買標榜20核心的電競主機，聽取店家的花言巧語如屌打市面上I7處理器，超多核心數玩大作不卡頓等購買，心心念念的期盼電腦到來，而當初我並不清楚這是那時所稱的洋垃圾，收到貨後才發現完全不符合我打線上遊戲的需求，卡頓不說，也常常跳出系統崩潰等問題，店家的消極與後來查價發現高於市場數成，再加上聽聞許多在地不知名工作室的漫天喊價與話術，使我下定決心不想再看到這種亂象，要成立自己的電腦工作室！</p>
                </div>
            </div>

            <!-- 03. 昱諾，啟動！ -->
            <div class="story-row">
                <div class="story-visual-side">
                    <div class="visual-block">
                        <span class="visual-num" style="color: #35ff35; text-shadow: 0 0 10px rgba(53,255,53,0.3);">03</span>
                        <span class="visual-sub">Launch Phase</span>
                    </div>
                </div>
                <div class="story-text-side">
                    <h3>昱諾，啟動！</h3>
                    <p>高中時因對讀書沒有太大興趣，在高一時就找一份連鎖早餐店打工，邊存錢邊拿薪水去購買更多電腦零件研究與拆解組裝，持續累積自己的經驗。後來到了高二下，開始努力在備戰學測，希望能上好大學，而到了學測考完的隔天，昱諾正式起步！</p>
                </div>
            </div>

        </div>
    </section>

    <!-- 作品集區塊 -->
    <section id="portfolio">
        <h2 class="section-title">PORTFOLIO</h2>
        <div class="portfolio-grid" id="portfolio-container"></div>
    </section>

    <!-- 頁尾資訊 -->
    <footer id="contact">
        <h2 style="font-family: Orbitron; font-size: 3rem; color: var(--main-cyan); margin-bottom: 50px; letter-spacing: 5px;">CONTACT US</h2>
        
        <div class="footer-container">
            <div class="contact-details">
                📍 <span>730 臺南市新營區東興路97號</span><br>
                📞 <span>0907-077-069</span><br>
                💬 <span>Line ID: 0903634521</span>
            </div>
            
            <div class="social-group">
                <div class="social-box">
                    <a href="https://www.facebook.com/profile.php?id=61554737102863" target="_blank" class="social-label">Facebook</a>
                    <a href="https://www.facebook.com/profile.php?id=61554737102863" target="_blank">
                        <img class="social-qrcode" src="https://i.postimg.cc/x8zDsNd2/FB-lian-jie.png" alt="YouKnowPC Facebook QR Code">
                    </a>
                </div>

                <div class="social-box">
                    <a href="https://www.instagram.com/youknow_pc/" target="_blank" class="social-label">Instagram</a>
                    <a href="https://www.instagram.com/youknow_pc/" target="_blank">
                        <img class="social-qrcode" src="https://i.postimg.cc/wjfzjpZ5/IG-lian-jie.png" alt="YouKnowPC Instagram QR Code">
                    </a>
                </div>
            </div>
        </div>
    </footer>

    <script>
        gsap.registerPlugin(ScrollToPlugin);

        /**
         * --- 作品集管理區 ---
         */
        const myProjects = [
            { title: "萬元內二手整新機", image: "https://i.postimg.cc/Hs58WFb9/unnamed-(4).jpg" },
            { title: "中高階360水冷全新海景房電競主機", image: "https://i.postimg.cc/xChqnPCt/unnamed-(3).jpg" },
            { title: "兩萬元高顏值二手整新機", image: "https://i.postimg.cc/fWSJ512Y/unnamed-(2).jpg" },
            { title: "平價全新RTX 5060輕主機", image: "https://i.postimg.cc/pLRrWr26/unnamed-(1).jpg" }
        ];

        function renderPortfolio() {
            const container = document.getElementById('portfolio-container');
            container.innerHTML = myProjects.map(p => `
                <div class="portfolio-item">
                    <div class="portfolio-img-container">
                        <img src="${p.image}" class="portfolio-img" onerror="this.src='https://via.placeholder.com/400x400?text=Image+Error'">
                    </div>
                    <div class="portfolio-info">
                        <h3>${p.title}</h3>
                        <span>作品集</span>
                    </div>
                </div>
            `).join('');
        }

        window.onload = () => { renderPortfolio(); };
        function scrollToSection(id) { gsap.to(window, { duration: 1.2, scrollTo: { y: id, autoKill: false }, ease: "power3.inOut" }); }
    </script>
</body>
</html>
