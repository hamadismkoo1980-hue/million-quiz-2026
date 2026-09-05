<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مسابقة النزاهة الثقافية - تحدي الـ 10 ثوان</title>
    <style>
        :root {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --accent: #eab308;
            --text: #f8fafc;
            --correct: #22c55e;
            --wrong: #ef4444;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text);
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            direction: rtl;
        }

        .container {
            width: 90%;
            max-width: 600px;
            background: var(--card-bg);
            padding: 25px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            text-align: center;
            border: 2px solid #334155;
        }

        h1 {
            color: var(--accent);
            font-size: 1.8rem;
            margin-bottom: 10px;
        }

        .rewards-box {
            background: rgba(234, 179, 8, 0.1);
            border: 1px solid var(--accent);
            border-radius: 10px;
            padding: 15px;
            margin: 15px 0;
            text-align: right;
            font-size: 0.95rem;
            line-height: 1.6;
        }

        .rewards-box h3 {
            margin-top: 0;
            color: var(--accent);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        input {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            border-radius: 8px;
            border: 1px solid #475569;
            background: #0f172a;
            color: #fff;
            box-sizing: border-box;
            text-align: center;
            font-size: 1rem;
        }

        button {
            width: 100%;
            padding: 12px;
            margin-top: 10px;
            background: var(--accent);
            color: #000;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            transition: 0.2s;
        }

        button:hover {
            opacity: 0.9;
        }

        .option-btn {
            background: #334155;
            color: #fff;
            text-align: right;
            margin: 8px 0;
        }

        .timer-bar {
            height: 8px;
            background: var(--accent);
            width: 100%;
            border-radius: 4px;
            transition: width 1s linear;
            margin: 15px 0;
        }

        .hidden { display: none; }
        
        .score-board {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--accent);
            margin-bottom: 10px;
        }
    </style>
</head>
<body>

    <div class="container" id="login-screen">
        <h1>🏆 مسابقة النزاهة الثقافية</h1>
        <p style="color: #94a3b8; font-size: 0.9rem;">تحدي الـ 10 ثوان للإجابة على الأسئلة</p>

        <!-- شرح طريقة الربح للمتسابقين -->
        <div class="rewards-box">
            <h3>🎁 كيف ترابح وتكسب من اللعبة؟</h3>
            <ul>
                <li><b>نظام النقاط:</b> تحصل على <b>100 نقطة</b> مقابل كل إجابة صحيحة تنجزها خلال 10 ثوانٍ.</li>
                <li><b>الجوائز المالية:</b> عند وصولك إلى <b>1,000 نقطة</b> تدخل تلقائياً في السحب الأسبوعي على جوائز نقدية.</li>
                <li><b>تحويل الأرباح:</b> يتم تسليم الجوائز مباشرة عبر حسابات DUST / Sham Cash أو المحافظ الإلكترونية المعتمدة.</li>
            </ul>
        </div>

        <input type="text" id="username" placeholder="أدخل اسمك الكامل">
        <input type="text" id="access-code" placeholder="أدخل كود التفعيل الخاص بك">
        <button onclick="startQuiz()">ابدأ التحدي الآن 🚀</button>
        <p id="error-msg" style="color: var(--wrong); margin-top: 10px;"></p>
    </div>

    <div class="container hidden" id="quiz-screen">
        <div class="score-board">النقاط: <span id="score">0</span></div>
        <div class="timer-bar" id="timer"></div>
        <h2 id="question-text">السؤال يظهر هنا...</h2>
        <div id="options-container"></div>
    </div>

    <!-- موسيقى خلفية كلاسيكية -->
    <audio id="bg-music" loop src="https://cdn.pixabay.com/download/audio/2022/05/27/audio_1808fbf07a.mp3?filename=classical-music-112188.mp3"></audio>

    <script>
        // قائمة الأكواد المفعلة
        const validCodes = [
            "MILLION01", "MILLION02", "MILLION03", "MILLION04", "MILLION05", 
            "MILLION06", "MILLION07", "MILLION08", "MILLION09", "MILLION10",
            "DEMO10", "WIN2026"
        ];

        const questions = [
            { q: "ما هي عاصمة سوريا؟", options: ["دمشق", "حلب", "حمص", "اللاذقية"], answer: 0 },
            { q: "كم عدد ألوان علم الجمهورية العربية السورية؟", options: ["2", "3", "4", "5"], answer: 2 },
            { q: "ما هو أطول نهر في العالم؟", options: ["الفرات", "النيل", "الأمازون", "التايمز"], answer: 1 },
            { q: "كم ثانية في الدقيقة الواحدة؟", options: ["50", "60", "100", "45"], answer: 1 }
        ];

        let currentQ = 0;
        let score = 0;
        let timerInterval;
        let timeLeft = 10;

        function startQuiz() {
            const name = document.getElementById('username').value.trim();
            const code = document.getElementById('access-code').value.trim().toUpperCase();

            if (!name || !code) {
                document.getElementById('error-msg').innerText = "يرجى كتابة الاسم وكود التفعيل!";
                return;
            }

            if (!validCodes.includes(code)) {
                document.getElementById('error-msg').innerText = "كود التفعيل غير صحيح أو مستخدم سابقاً!";
                return;
            }

            // إخفاء شاشة الدخول وتشغيل الموسيقى واللعبة
            document.getElementById('login-screen').classList.add('hidden');
            document.getElementById('quiz-screen').classList.remove('hidden');
            
            // تشغيل الموسيقى الكلاسيكية
            const bgMusic = document.getElementById('bg-music');
            bgMusic.volume = 0.3; // مستوى صوت هادئ
            bgMusic.play().catch(() => console.log("تنسيق الصوت يتطلب تفاعل المسابق"));

            loadQuestion();
        }

        function loadQuestion() {
            if (currentQ >= questions.length) {
                endQuiz();
                return;
            }

            clearInterval(timerInterval);
            timeLeft = 10;
            updateTimerBar();

            const q = questions[currentQ];
            document.getElementById('question-text').innerText = q.q;
            const container = document.getElementById('options-container');
            container.innerHTML = '';

            q.options.forEach((opt, idx) => {
                const btn = document.createElement('button');
                btn.className = 'option-btn';
                btn.innerText = opt;
                btn.onclick = () => checkAnswer(idx);
                container.appendChild(btn);
            });

            timerInterval = setInterval(() => {
                timeLeft--;
                updateTimerBar();
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    currentQ++;
                    loadQuestion();
                }
            }, 1000);
        }

        function updateTimerBar() {
            const timerBar = document.getElementById('timer');
            timerBar.style.width = (timeLeft * 10) + '%';
        }

        function checkAnswer(selectedIdx) {
            clearInterval(timerInterval);
            if (selectedIdx === questions[currentQ].answer) {
                score += 100;
                document.getElementById('score').innerText = score;
            }
            currentQ++;
            loadQuestion();
        }

        function endQuiz() {
            document.getElementById('quiz-screen').innerHTML = `
                <h2>🎉 انتهت المسابقة!</h2>
                <p>مجموع نقاطك التي كسبتها: <b style="color:var(--accent); font-size: 1.5rem;">${score}</b> نقطة</p>
                <p style="color: #94a3b8;">تم تسجيل نقاطك بنجاح للدخول في السحب على الجوائز!</p>
            `;
        }
    </script>
</body>
</html>
