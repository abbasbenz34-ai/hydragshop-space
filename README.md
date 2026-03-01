<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hydra Dragon Ghost Shop | المجمع الرقمي</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #8b5cf6; /* أرجواني التنين */
            --secondary: #0ea5e9; /* أزرق الشبح */
            --dark: #0f172a;
            --glass: rgba(255, 255, 255, 0.1);
            --bg: #020617;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Cairo', sans-serif; }
        
        body { background-color: var(--bg); color: white; overflow-x: hidden; }

        /* --- الهيدر (شريط البحث المتقدم) --- */
        header {
            padding: 20px;
            background: rgba(15, 23, 42, 0.8);
            backdrop-filter: blur(15px);
            position: sticky;
            top: 0;
            z-index: 1000;
            border-bottom: 1px solid var(--glass);
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .logo-area { display: flex; align-items: center; gap: 10px; }
        .logo-area img { width: 45px; height: 45px; border-radius: 10px; }
        .logo-text { font-size: 1.5rem; font-weight: bold; background: linear-gradient(to left, var(--primary), var(--secondary)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }

        .search-wrapper { position: relative; width: 100%; }
        .main-search {
            width: 100%;
            padding: 15px 50px 15px 20px;
            border-radius: 12px;
            border: none;
            background: var(--glass);
            color: white;
            font-size: 1.1rem;
            outline: none;
            border: 1px solid transparent;
            transition: 0.3s;
        }
        .main-search:focus { border-color: var(--primary); box-shadow: 0 0 15px rgba(139, 92, 246, 0.3); }

        /* --- أقسام العرض (نظام Google Play) --- */
        .section-container { padding: 20px; max-width: 1200px; margin: 0 auto; }
        .row-title { font-size: 1.3rem; margin: 20px 0 10px; display: flex; align-items: center; gap: 10px; }
        
        .horizontal-scroll {
            display: flex;
            gap: 20px;
            overflow-x: auto;
            padding-bottom: 20px;
            scroll-behavior: smooth;
        }
        .horizontal-scroll::-webkit-scrollbar { height: 5px; }
        .horizontal-scroll::-webkit-scrollbar-thumb { background: var(--primary); border-radius: 10px; }

        .card {
            min-width: 160px;
            max-width: 160px;
            background: var(--glass);
            border-radius: 15px;
            padding: 12px;
            transition: 0.3s;
            cursor: pointer;
            text-decoration: none;
            color: white;
        }
        .card:hover { transform: translateY(-5px); background: rgba(255,255,255,0.2); }
        .card img { width: 100%; aspect-ratio: 1; border-radius: 12px; object-fit: cover; margin-bottom: 10px; }
        .card h4 { font-size: 0.9rem; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .card p { font-size: 0.75rem; color: #94a3b8; }

        /* --- شات بوت Hydra AI --- */
        #ai-orb {
            position: fixed;
            bottom: 30px;
            left: 30px;
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: 0 0 20px var(--primary);
            z-index: 1001;
            font-size: 25px;
        }

        #chat-window {
            position: fixed;
            bottom: 100px;
            left: 30px;
            width: 350px;
            height: 450px;
            background: #1e293b;
            border-radius: 20px;
            display: none;
            flex-direction: column;
            border: 1px solid var(--glass);
            z-index: 1000;
        }

        .chat-messages { flex: 1; padding: 15px; overflow-y: auto; display: flex; flex-direction: column; gap: 10px; }
        .msg { padding: 8px 12px; border-radius: 10px; max-width: 80%; font-size: 0.9rem; }
        .msg.bot { background: var(--glass); align-self: flex-start; }
        .msg.user { background: var(--primary); align-self: flex-end; }

        .chat-input { padding: 15px; display: flex; gap: 10px; border-top: 1px solid var(--glass); }
        .chat-input input { flex: 1; background: none; border: none; color: white; outline: none; }

        /* --- تسجيل الدخول (الربط) --- */
        .login-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9);
            display: none; justify-content: center; align-items: center; z-index: 2000;
        }
        .login-card { background: #1e293b; padding: 40px; border-radius: 25px; text-align: center; width: 90%; max-width: 400px; }
        .social-btn {
            width: 100%; padding: 12px; margin: 10px 0; border-radius: 10px; border: none;
            cursor: pointer; font-weight: bold; display: flex; align-items: center; justify-content: center; gap: 10px;
        }
    </style>
</head>
<body>

    <header>
        <div class="nav-container">
            <div class="logo-area">
                <img src="https://via.placeholder.com/100/8b5cf6/ffffff?text=H" alt="Hydra Logo">
                <span class="logo-text">HYDRA DRAGON</span>
                <button onclick="toggleLogin()" style="margin-right: auto; background: var(--glass); color: white; border: none; padding: 5px 15px; border-radius: 20px; cursor: pointer;">تسجيل دخول</button>
            </div>
            <div class="search-wrapper">
                <input type="text" class="main-search" id="mainSearch" placeholder="ابحث عن كتب، تطبيقات، فيديوهات تيك توك..." onkeypress="handleSearch(event)">
                <span style="position: absolute; left: 15px; top: 15px; color: var(--primary);">🔍</span>
            </div>
        </div>
    </header>

    <main class="section-container">
        
        <h3 class="row-title">📚 كتب وروايات مقترحة</h3>
        <div class="horizontal-scroll" id="books-row">
            </div>

        <h3 class="row-title">🎮 تطبيقات وألعاب (Google Play)</h3>
        <div class="horizontal-scroll" id="apps-row">
            <div class="card">
                <img src="https://cdn-icons-png.flaticon.com/512/2991/2991148.png" alt="Play">
                <h4>متجر بلاي</h4>
                <p>تطبيقات أندرويد</p>
            </div>
            </div>

        <h3 class="row-title">🔥 ترندات الفيديو (YouTube & TikTok)</h3>
        <div class="horizontal-scroll" id="video-row">
            </div>

    </main>

    <div id="ai-orb" onclick="toggleChat()">🐉</div>
    <div id="chat-window" id="chatWindow">
        <div style="padding: 15px; background: var(--primary); border-radius: 20px 20px 0 0; font-weight: bold;">Hydra AI Assistant</div>
        <div class="chat-messages" id="chatMessages">
            <div class="msg bot">مرحباً بك! أنا هيدرا، محركك الذكي. ابحث عن أي شيء وسأجده لك في كل المنصات.</div>
        </div>
        <div class="chat-input">
            <input type="text" id="aiInput" placeholder="اسأل هيدرا..." onkeypress="handleChat(event)">
            <button onclick="sendChatMessage()" style="background: none; border: none; color: var(--primary); cursor: pointer;">➤</button>
        </div>
    </div>

    <div class="login-overlay" id="loginOverlay">
        <div class="login-card">
            <h2>اربط حساباتك 🔗</h2>
            <p style="margin-bottom: 20px; color: #94a3b8;">لتحسين تجربة البحث في تيك توك ويوتيوب</p>
            <button class="social-btn" style="background: white; color: black;">
                <img src="https://cdn-icons-png.flaticon.com/512/2991/2991148.png" width="20"> Google
            </button>
            <button class="social-btn" style="background: black; color: white;">
                <img src="https://cdn-icons-png.flaticon.com/512/3046/3046124.png" width="20"> TikTok
            </button>
            <button onclick="toggleLogin()" style="background: none; border: none; color: #94a3b8; margin-top: 15px; cursor: pointer;">إغلاق</button>
        </div>
    </div>

    <script>
        // 1. إدارة الواجهة
        function toggleChat() {
            const win = document.getElementById('chat-window');
            win.style.display = win.style.display === 'flex' ? 'none' : 'flex';
        }

        function toggleLogin() {
            const overlay = document.getElementById('loginOverlay');
            overlay.style.display = overlay.style.display === 'flex' ? 'none' : 'flex';
        }

        // 2. محرك البحث الذكي (الرادار)
        async function handleSearch(e) {
            if (e.key === 'Enter') {
                const query = e.target.value;
                if (!query) return;
                
                // تنظيف النتائج الحالية لبدء بحث جديد
                document.getElementById('books-row').innerHTML = '<p>جاري البحث في المكتبة العالمية...</p>';
                document.getElementById('video-row').innerHTML = '<p>جاري سحب الترندات...</p>';

                // جلب الكتب من Google Books API
                fetchBooks(query);
                // جلب روابط المنصات الأخرى
                fetchExternalPlatforms(query);
            }
        }

        async function fetchBooks(query) {
            try {
                const res = await fetch(`https://www.googleapis.com/books/v1/volumes?q=${query}&maxResults=8`);
                const data = await res.json();
                const container = document.getElementById('books-row');
                container.innerHTML = '';

                data.items.forEach(item => {
                    const info = item.volumeInfo;
                    const img = info.imageLinks ? info.imageLinks.thumbnail : 'https://via.placeholder.com/150';
                    container.innerHTML += `
                        <a href="${info.previewLink}" target="_blank" class="card">
                            <img src="${img}" alt="book">
                            <h4>${info.title}</h4>
                            <p>${info.authors ? info.authors[0] : 'مؤلف غير معروف'}</p>
                        </a>
                    `;
                });
            } catch (err) { console.error("Books Error", err); }
        }

        function fetchExternalPlatforms(query) {
            const videoRow = document.getElementById('video-row');
            videoRow.innerHTML = '';

            const platforms = [
                { name: 'YouTube', icon: 'https://cdn-icons-png.flaticon.com/512/1384/1384060.png', url: `https://www.youtube.com/results?search_query=${query}` },
                { name: 'TikTok', icon: 'https://cdn-icons-png.flaticon.com/512/3046/3046124.png', url: `https://www.tiktok.com/search?q=${query}` },
                { name: 'Play Store', icon: 'https://cdn-icons-png.flaticon.com/512/2991/2991148.png', url: `https://play.google.com/store/search?q=${query}&c=apps` }
            ];

            platforms.forEach(p => {
                videoRow.innerHTML += `
                    <a href="${p.url}" target="_blank" class="card">
                        <img src="${p.icon}" alt="${p.name}">
                        <h4>نتائج ${p.name}</h4>
                        <p>اضغط للفتح المباشر</p>
                    </a>
                `;
            });
        }

        // 3. منطق الشات بوت (Hydra AI)
        function handleChat(e) { if (e.key === 'Enter') sendChatMessage(); }

        function sendChatMessage() {
            const input = document.getElementById('aiInput');
            const box = document.getElementById('chatMessages');
            if (!input.value) return;

            // رسالة المستخدم
            box.innerHTML += `<div class="msg user">${input.value}</div>`;
            
            // رد الذكاء الاصطناعي (محاكاة)
            setTimeout(() => {
                box.innerHTML += `<div class="msg bot">لقد قمت بتحديث الرادار للبحث عن "${input.value}". يمكنك رؤية النتائج في المتجر الآن.</div>`;
                box.scrollTop = box.scrollHeight;
                document.getElementById('mainSearch').value = input.value;
                handleSearch({key: 'Enter', target: {value: input.value}});
            }, 1000);

            input.value = '';
            box.scrollTop = box.scrollHeight;
        }
    </script>
</body>
</html>
