<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مسابقة المليون 2026 - تحدي الـ 10 ثوانٍ</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-gold: #ffd700;
            --secondary-gold: #ffaa00;
            --panel-bg: rgba(13, 22, 45, 0.9);
            --neon-blue: #00f0ff;
            --success-green: #00ff88;
            --danger-red: #ff3366;
            --crypto-purple: #8c8cff;
            --sham-cash-green: #25d366;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Cairo', sans-serif;
            user-select: none;
        }

        body {
            background: radial-gradient(circle at center, #101c3d 0%, #050811 100%);
            color: #fff;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
            padding: 15px;
        }

        .game-card {
            position: relative;
            z-index: 10;
            width: 100%;
            max-width: 850px;
            background: var(--panel-bg);
            border: 2px solid var(--primary-gold);
            border-radius: 24px;
            padding: 30px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8),
                        0 0 30px rgba(255, 215, 0, 0.2);
            backdrop-filter: blur(15px);
        }

        .header { text-align: center; margin-bottom: 25px; }

        .title {
            font-size: 2.2rem;
            font-weight: 900;
            background: linear-gradient(180deg, #ffffff 0%, var(--primary-gold) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .sub-title { color: var(--neon-blue); font-size: 1.1rem; margin-top: 5px; }

        .payment-panel {
            background: rgba(5, 10, 25, 0.9);
            border: 1.5px solid var(--secondary-gold);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 25px;
            text-align: center;
        }

        .payment-methods {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .pay-card {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 215, 0, 0.3);
            border-radius: 12px;
            padding: 15px;
            text-align: center;
        }

        .pay-card.sham { border-color: var(--sham-cash-green); }
        .pay-card.crypto { border-color: var(--crypto-purple); }

        .wallet-num {
            font-family: monospace;
            font-size: 0.85rem;
            font-weight: bold;
            padding: 8px;
            margin: 8px 0;
            background: #000;
            border-radius: 6px;
            word-break: break-all;
            direction: ltr;
        }

        .btn-whatsapp {
            background: linear-gradient(45deg, #128c7e, #25d366);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 30px;
            font-weight: 700;
            font-size: 1rem;
            cursor: pointer;
            width: 100%;
            margin-top: 15px;
            box-shadow: 0 5px 15px rgba(37, 211, 102, 0.4);
        }

        .activation-box { display: flex; gap: 10px; margin-top: 15px; flex-wrap: wrap; }

        .code-input, .name-input {
            flex: 1; min-width: 180px; padding: 12px; border-radius: 10px;
            border: 1px solid var(--primary-gold);
            background: rgba(0, 0, 0, 0.5); color: #fff; text-align: center;
            font-size: 1rem;
        }

        .btn-start {
            background: linear-gradient(180deg, var(--primary-gold) 0%, var(--secondary-gold) 100%);
            color: #000; font-weight: 900; padding: 12px 30px;
            border: none; border-radius: 10px; cursor: pointer; font-size: 1.1rem;
            width: 100%; margin-top: 10px;
        }

        .game-hud {
            display: flex; justify-content: space-between; align-items: center;
            margin-bottom: 20px; padding: 12px 20px;
            background: rgba(0, 0, 0, 0.4); border-radius: 12px;
            border: 1px solid rgba(255, 215, 0, 0.2);
        }

        .hud-label { font-size: 0.85rem; color: #aaa; }
        .hud-value { font-size: 1.3rem; font-weight: 700; color: var(--primary-gold); }

        .timer-box {
            width: 65px; height: 65px; border-radius: 50%;
            background: radial-gradient(circle, #101c3d, #000);
            border: 3px solid var(--neon-blue);
            display: flex; justify-content: center; align-items: center;
            font-size: 1.6rem; font-weight: 900; color: var(--neon-blue);
            box-shadow: 0 0 15px var(--neon-blue);
        }

        .timer-box.warning {
            border-color: var(--danger-red); color: var(--danger-red);
            box-shadow: 0 0 20px var(--danger-red);
        }

        .question-card {
            background: linear-gradient(135deg, rgba(20, 35, 70, 0.9), rgba(10, 15, 30, 0.95));
            border: 2px solid var(--primary-gold); border-radius: 18px;
            padding: 25px; margin-bottom: 25px; text-align: center;
            font-size: 1.3rem; font-weight: 700; min-height: 100px;
            display: flex; align-items: center; justify-content: center;
        }

        .options-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; }

        @media (max-width: 600px) { .options-grid { grid-template-columns: 1fr; } }

        .option-btn {
            background: linear-gradient(180deg, #112244 0%, #0a1428 100%);
            border: 1.5px solid rgba(255, 215, 0, 0.4); border-radius: 12px;
            padding: 16px; color: #fff; font-size: 1.1rem; font-weight: 600;
            cursor: pointer; text-align: right; padding-right: 20px;
        }

        .option-btn.correct {
            background: linear-gradient(180deg, #00b050 0%, #00612c 100%) !important;
            border-color: var(--success-green) !important; color: #fff !important;
        }

        .option-btn.wrong {
            background: linear-gradient(180deg, #c00000 0%, #600000 100%) !important;
            border-color: var(--danger-red) !important; color: #fff !important;
        }

        .result-screen { display: none; text-align: center; padding: 20px; }
        .result-title { font-size: 2.5rem; font-weight: 900; margin-bottom: 15px; }
        .result-title.win { color: var(--primary-gold); }
        .result-title.lose { color: var(--danger-red); }

        .sound-toggle {
            position: absolute; top: 20px; left: 20px;
            background: rgba(255, 255, 255, 0.1); border: 1px solid var(--primary-gold);
            border-radius: 50%; width: 40px; height: 40px; cursor: pointer;
            display: flex; justify-content: center; align-items: center; color: #fff;
        }

        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div class="game-card">
        <button class="sound-toggle" id="soundToggle" onclick="toggleSound()">🔊</button>

        <div class="header">
            <h1 class="title">مسابقة المليون 2026</h1>
            <p class="sub-title">🔥 تحدي الـ 10 ثوانٍ - 50 سؤالاً عشوائياً 🔥</p>
        </div>

        <!-- START SCREEN -->
        <div id="startScreen">
            <div class="payment-panel">
                <h3>💳 طرق وشروط الاشتراك (1$ فقط)</h3>
                <div class="payment-methods">
                    <div class="pay-card sham">
                        <h4 style="color: var(--sham-cash-green);">🇸🇾 Sham Cash</h4>
                        <p style="font-size: 0.85rem; color: #bbb;">رقم المحفظة:</p>
                        <div class="wallet-num" style="color: var(--sham-cash-green); font-size: 1rem;">8020541796461939</div>
                    </div>
                    <div class="pay-card crypto">
                        <h4 style="color: var(--crypto-purple);">🌐 Crypto Wallet (USDT / ETH)</h4>
                        <p style="font-size: 0.85rem; color: #bbb;">عنوان المحفظة (EVM):</p>
                        <div class="wallet-num" style="color: var(--crypto-purple);">0x91516f1011c415ff30cB2B0825d939Ba4FF03505</div>
                    </div>
                </div>
                <button class="btn-whatsapp" onclick="openWhatsApp()">
                    📲 إرسال إثبات الدفع لـ واتساب الإدارة (00963933711873)
                </button>
            </div>

            <div style="background: rgba(0,0,0,0.3); padding: 15px; border-radius: 12px;">
                <p style="text-align: center; margin-bottom: 10px; font-weight: bold; color: var(--primary-gold);">
                    أدخل بياناتك وكود التفعيل لبدء التحدي:
                </p>
                <div class="activation-box">
                    <input type="text" id="playerName" class="name-input" placeholder="اسمك الكريم">
                    <input type="text" id="accessCode" class="code-input" placeholder="كود التفعيل (مثل: DEMO10)">
                    <button class="btn-start" onclick="startGame()">ابدأ التحدي 🚀</button>
                </div>
            </div>
        </div>

        <!-- GAME SCREEN -->
        <div id="gameScreen" class="hidden">
            <div class="game-hud">
                <div class="hud-item">
                    <div class="hud-label">المتسابق</div>
                    <div class="hud-value" id="hudName">المتسابق</div>
                </div>
                <div class="hud-item">
                    <div class="timer-box" id="timerBox">10</div>
                </div>
                <div class="hud-item">
                    <div class="hud-label">السؤال</div>
                    <div class="hud-value"><span id="currentQNum">1</span> / 50</div>
                </div>
                <div class="hud-item">
                    <div class="hud-label">الرصيد</div>
                    <div class="hud-value" id="hudScore">$0</div>
                </div>
            </div>

            <div class="question-card" id="questionText">جاري تحميل السؤال...</div>
            <div class="options-grid" id="optionsContainer"></div>
        </div>

        <!-- RESULT SCREEN -->
        <div id="resultScreen" class="result-screen">
            <h2 id="resultTitle" class="result-title">تهانينا! 🎉</h2>
            <p id="resultSubtitle" style="font-size: 1.2rem; color: #ddd;"></p>
            <div style="font-size: 1.5rem; margin: 20px 0; color: var(--neon-blue);" id="finalScore">الرصيد: $0</div>
            <button class="btn-start" onclick="resetToStart()">العودة للقائمة الرئيسية 🔄</button>
        </div>
    </div>

    <script>
        // الأكواد المسموح بها للدخول
        const validCodes = ["DEMO10", "WIN2026", "VIP100", "CASH2026", "USER001", "USER002"];
        const usedCodes = [];

        class SoundEffects {
            constructor() { this.ctx = null; this.muted = false; }
            init() { if (!this.ctx) this.ctx = new (window.AudioContext || window.webkitAudioContext)(); }

            playCorrect() {
                if (this.muted) return; this.init();
                const now = this.ctx.currentTime, osc = this.ctx.createOscillator(), g = this.ctx.createGain();
                osc.type = 'triangle'; osc.frequency.setValueAtTime(523.25, now);
                osc.frequency.setValueAtTime(659.25, now + 0.1); osc.frequency.setValueAtTime(783.99, now + 0.2);
                g.gain.setValueAtTime(0.3, now); g.gain.exponentialRampToValueAtTime(0.001, now + 0.6);
                osc.connect(g); g.connect(this.ctx.destination);
                osc.start(now); osc.stop(now + 0.6);
            }

            playWrong() {
                if (this.muted) return; this.init();
                const now = this.ctx.currentTime, osc = this.ctx.createOscillator(), g = this.ctx.createGain();
                osc.type = 'sawtooth'; osc.frequency.setValueAtTime(150, now);
                osc.frequency.exponentialRampToValueAtTime(40, now + 0.6);
                g.gain.setValueAtTime(0.4, now); g.gain.exponentialRampToValueAtTime(0.001, now + 0.6);
                osc.connect(g); g.connect(this.ctx.destination);
                osc.start(now); osc.stop(now + 0.6);
            }

            playTick() {
                if (this.muted) return; this.init();
                const now = this.ctx.currentTime, osc = this.ctx.createOscillator(), g = this.ctx.createGain();
                osc.type = 'sine'; osc.frequency.setValueAtTime(800, now);
                g.gain.setValueAtTime(0.05, now); g.gain.exponentialRampToValueAtTime(0.001, now + 0.05);
                osc.connect(g); g.connect(this.ctx.destination);
                osc.start(now); osc.stop(now + 0.05);
            }
        }

        const soundFX = new SoundEffects();
        function toggleSound() {
            soundFX.muted = !soundFX.muted;
            document.getElementById('soundToggle').innerText = soundFX.muted ? '🔇' : '🔊';
        }

        const questionBank = [
            { q: "ما هي عاصمة مصر؟", options: ["الإسكندرية", "القاهرة", "الجيزة", "الأقصر"], answer: 1 },
            { q: "ما هو أطول نهر في العالم؟", options: ["الأمازون", "النيل", "الميسيسيبي", "الدانوب"], answer: 1 },
            { q: "كم عدد كواكب المجموعة الشمسية؟", options: ["7", "8", "9", "10"], answer: 1 },
            { q: "ما هو رمز عنصر الأكسجين؟", options: ["O", "H", "Fe", "Au"], answer: 0 },
            { q: "من مكتشف جاذبية الأرض؟", options: ["آينشتاين", "نيوتن", "غاليلو", "تسلا"], answer: 1 },
            { q: "تقع البرازيل في قارة؟", options: ["آسيا", "أفريقيا", "أمريكا الجنوبية", "أوروبا"], answer: 2 },
            { q: "أكبر حيوان في العالم؟", options: ["الفيل", "الحوت الأزرق", "القرش", "الزرافة"], answer: 1 },
            { q: "عاصمة الدولة الأموية؟", options: ["بغداد", "القاهرة", "دمشق", "القدس"], answer: 2 },
            { q: "عدد أضلاع المثلث؟", options: ["3", "4", "5", "6"], answer: 0 },
            { q: "عملة اليابان؟", options: ["اليوان", "الين", "الدولار", "الروبية"], answer: 1 },
            { q: "قائل 'أنا أفكّر إذاً أنا موجود'؟", options: ["سقراط", "ديكارت", "أرسطو", "أفلاطون"], answer: 1 },
            { q: "أسرع حيوان بري؟", options: ["الأسد", "الفهد", "الغزال", "الحصان"], answer: 1 },
            { q: "أطول سورة في القرآن؟", options: ["آل عمران", "البقرة", "النساء", "المائدة"], answer: 1 },
            { q: "عام اندلاع الحرب العالمية الأولى؟", options: ["1914", "1918", "1939", "1945"], answer: 0 },
            { q: "يتكون الألماس أساساً من عنصر؟", options: ["الكربون", "الحديد", "السيليكون", "النحاس"], answer: 0 },
            { q: "أكبر قارات العالم مساحة؟", options: ["أفريقيا", "أمريكا الشمالية", "آسيا", "أوروبا"], answer: 2 },
            { q: "أكثر غاز انتشاراً في الغلاف الجوي؟", options: ["الأكسجين", "النيتروجين", "ثاني أكسيد الكربون", "الهيدروجين"], answer: 1 },
            { q: "بطل كأس العالم لكرة القدم 2022؟", options: ["فرنسا", "البرازيل", "الأرجنتين", "كرواتيا"], answer: 2 },
            { q: "اللغتان الرسميتان لكندا؟", options: ["إنجليزي وإسباني", "إنجليزي وفرنسي", "فرنسي وألماني", "إنجليزي وهولندي"], answer: 1 },
            { q: "المادة الخضراء في النباتات؟", options: ["الكاروتين", "الكلوروفيل", "الهيموغلوبين", "الميلانين"], answer: 1 },
            { q: "أصغر دولة في العالم؟", options: ["موناكو", "الفاتيكان", "سان مارينو", "المالديف"], answer: 1 },
            { q: "عدد أحرف اللغة العربية؟", options: ["26", "28", "30", "24"], answer: 1 },
            { q: "مخترع المصباح الكهربائي؟", options: ["توماس إديسون", "تسلا", "غراهام بيل", "نيوتن"], answer: 0 },
            { q: "أكثر دولة سكاناً حالياً؟", options: ["الصين", "الهند", "أمريكا", "إندونيسيا"], answer: 1 },
            { q: "العضو المسؤول عن ضخ الدم؟", options: ["الدماغ", "الرئة", "القلب", "الكبد"], answer: 2 },
            { q: "أطول سلسلة جبال بالعالم؟", options: ["الهيمالايا", "الألب", "الأنديز", "الأطلس"], answer: 2 },
            { q: "أسرع وسيلة لنقل البيانات حالياً؟", options: ["الألياف الضوئية", "النحاس", "اللاسلكي", "الأقمار"], answer: 0 },
            { q: "مجموع زوايا المربع الإجمالية؟", options: ["180", "270", "360", "540"], answer: 2 },
            { q: "الكوكب الملقب بـ الكوكب الأحمر؟", options: ["الزهرة", "المريخ", "المشتري", "زحل"], answer: 1 },
            { q: "المعدن السائل الوحيد في الحرارة العادية؟", options: ["الزئبق", "الحديد", "الرصاص", "الألومنيوم"], answer: 0 },
            { q: "مؤلف ملحمة الشاهنامة؟", options: ["الفردوسي", "المتنبي", "أبو تمام", "الخيام"], answer: 0 },
            { q: "العضو المسؤول عن تصفية الدم؟", options: ["القلب", "الكليتان", "الطحال", "البنكرياس"], answer: 1 },
            { q: "الدولة المعروفة بـ بلاد الرافدين قديماً؟", options: ["مصر", "العراق", "سوريا", "اليمن"], answer: 1 },
            { q: "عدد أسنان الإنسان البالغ الطبيعية؟", options: ["28", "30", "32", "34"], answer: 2 },
            { q: "الحيوان البحر الذكي صديق الإنسان؟", options: ["القرش", "الدولفين", "الحوت", "الأخطبوط"], answer: 1 },
            { q: "ما هي لغة الإسبرانتو؟", options: ["اصطناعية", "قديمة", "أفريقية", "آسيوية"], answer: 0 },
            { q: "الكوكب صاحب أكبر عدد حلقات؟", options: ["المشتري", "زحل", "أورانوس", "نبتون"], answer: 1 },
            { q: "مؤسس شركة أبل Apple؟", options: ["بيل غيتس", "ستيف جوبز", "مارك", "ماسك"], answer: 1 },
            { q: "وحدة قياس شدة التيار الكهربائي؟", options: ["الفولت", "الأمبير", "الواط", "الأوم"], answer: 1 },
            { q: "كم عدد قارات العالم؟", options: ["5", "6", "7", "8"], answer: 2 },
            { q: "المحيط الأكبر مساحة في العالم؟", options: ["الأطلسي", "الهادي", "الهندي", "المتجمد"], answer: 1 },
            { q: "الشاعر الملقب بـ أمير الشعراء؟", options: ["أحمد شوقي", "حافظ إبراهيم", "قباني", "جبران"], answer: 0 },
            { q: "الهرمون المسؤول عن تنظيم السكر؟", options: ["الأدرينالين", "الأنسولين", "الثايروكسين", "الدوبامين"], answer: 1 },
            { q: "الدولة الشهيرة ببرج إيفل؟", options: ["إيطاليا", "فرنسا", "ألمانيا", "إسبانيا"], answer: 1 },
            { q: "أسرع طائرة نفاثة في التاريخ؟", options: ["SR-71 بلاكبيرد", "كونكورد", "F-22", "بوينغ"], answer: 0 },
            { q: "وقعت غزوة بدر الكبرى سنة؟", options: ["2 هـ", "3 هـ", "5 هـ", "8 هـ"], answer: 0 },
            { q: "أصل علم الجبر والهندسة؟", options: ["الحضارة الإسلامية", "الرومانية", "الصينية", "المايا"], answer: 0 },
            { q: "المكون الرئيسي لمادة الزجاج؟", options: ["الرمل", "الكلس", "الإسمنت", "الصلصال"], answer: 0 },
            { q: "عدد الدقائق في اليوم الواحد؟", options: ["1200", "1440", "1600", "1800"], answer: 1 },
            { q: "أندر فصيلة دم لدى البشر؟", options: ["O-", "AB-", "A+", "B-"], answer: 1 }
        ];

        let currentQuestions = [], currentIndex = 0, score = 0, timer = null, timeLeft = 10, playerName = "";

        function openWhatsApp() {
            const name = (document.getElementById('playerName').value || '').trim() || 'غير محدد';
            const msg = `مرحباً، أريد الاشتراك في مسابقة المليون 2026.\nالاسم: ${name}\nقمت بتحويل رسم المشاركة وأرفق إثبات الدفع.`;
            window.open('https://wa.me/963933711873?text=' + encodeURIComponent(msg), '_blank');
        }

        function startGame() {
            const nameInput = document.getElementById('playerName').value.trim();
            const codeInput = document.getElementById('accessCode').value.trim().toUpperCase();

            if (!nameInput) {
                alert("يرجى إدخال اسمك الكريم!");
                return;
            }

            if (!codeInput) {
                alert("يرجى إدخال كود التفعيل!");
                return;
            }

            if (usedCodes.includes(codeInput)) {
                alert("عذراً، هذا الكود مستخدم من قبل!");
                return;
            }

            if (!validCodes.includes(codeInput)) {
                alert("كود التفعيل غير صحيح! يرجى التواصل مع الإدارة عبر الواتساب للحصول على كود مفعل.");
                return;
            }

            usedCodes.push(codeInput);
            playerName = nameInput;
            document.getElementById('hudName').innerText = playerName;
            currentQuestions = [...questionBank].sort(() => Math.random() - 0.5);
            currentIndex = 0; score = 0;

            document.getElementById('startScreen').classList.add('hidden');
            document.getElementById('resultScreen').classList.add('hidden');
            document.getElementById('gameScreen').classList.remove('hidden');
            loadQuestion();
        }

        function loadQuestion() {
            if (currentIndex >= currentQuestions.length) { endGame(true); return; }

            clearInterval(timer); timeLeft = 10; updateTimerDisplay();
            const qData = currentQuestions[currentIndex];
            document.getElementById('currentQNum').innerText = currentIndex + 1;
            document.getElementById('hudScore').innerText = '$' + (score * 20000).toLocaleString();
            document.getElementById('questionText').innerText = qData.q;

            const container = document.getElementById('optionsContainer');
            container.innerHTML = '';

            qData.options.forEach((optText, i) => {
                const btn = document.createElement('button');
                btn.className = 'option-btn';
                btn.innerText = `${['أ', 'ب', 'ج', 'د'][i]}) ${optText}`;
                btn.onclick = () => selectOption(i, qData.answer, btn);
                container.appendChild(btn);
            });

            timer = setInterval(() => {
                timeLeft--;
                soundFX.playTick();
                updateTimerDisplay();

                if (timeLeft <= 0) {
                    clearInterval(timer);
                    soundFX.playWrong();
                    setTimeout(() => endGame(false, "انتهى الوقت المحدد!"), 1000);
                }
            }, 1000);
        }

        function updateTimerDisplay() {
            const timerBox = document.getElementById('timerBox');
            timerBox.innerText = timeLeft;
            if (timeLeft <= 3) timerBox.classList.add('warning');
            else timerBox.classList.remove('warning');
        }

        function selectOption(selectedIndex, correctIndex, btnElement) {
            clearInterval(timer);
            if (selectedIndex === correctIndex) {
                btnElement.classList.add('correct');
                soundFX.playCorrect();
                score++;
                setTimeout(() => { currentIndex++; loadQuestion(); }, 1200);
            } else {
                btnElement.classList.add('wrong');
                soundFX.playWrong();
                setTimeout(() => { endGame(false, "إجابة خاطئة!"); }, 1200);
            }
        }

        function endGame(isWin, reason = "") {
            clearInterval(timer);
            document.getElementById('gameScreen').classList.add('hidden');
            document.getElementById('resultScreen').classList.remove('hidden');

            const title = document.getElementById('resultTitle');
            const sub = document.getElementById('resultSubtitle');
            const final = document.getElementById('finalScore');

            if (isWin) {
                title.innerText = "🏆 ألف مبروك! فزت بالمليون!";
                title.className = "result-title win";
                sub.innerText = "أتممت جميع الأسئلة الـ 50 بنجاح!";
                final.innerText = "الرصيد المكتسب: $1,000,000";
            } else {
                title.innerText = "💔 انتهت اللعبة!";
                title.className = "result-title lose";
                sub.innerText = reason;
                final.innerText = `الرصيد النهائي: $${(score * 20000).toLocaleString()}`;
            }
        }

        function resetToStart() {
            document.getElementById('resultScreen').classList.add('hidden');
            document.getElementById('startScreen').classList.remove('hidden');
        }
    </script>
</body>
</html>
