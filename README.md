Weaa Academy/
Creator Zidane Mohamed
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>كويز المعلومات الإسلامية</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #0f172a;
            color: #f8fafc;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .main-container {
            background-color: #1e293b;
            width: 90%;
            max-width: 650px;
            border-radius: 16px;
            padding: 30px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            text-align: center;
            position: relative;
            z-index: 10;
        }

        .header {
            font-size: 1.8rem;
            color: #10b981;
            margin-bottom: 20px;
            font-weight: bold;
            border-bottom: 2px solid #334155;
            padding-bottom: 15px;
        }

        /* شاشة اختيار المستوى وإدخال الاسم */
        #levelScreen {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 20px;
        }

        .name-input {
            width: 90%;
            padding: 15px;
            font-size: 1.2rem;
            border-radius: 10px;
            border: 2px solid #334155;
            background-color: #0f172a;
            color: #f8fafc;
            text-align: center;
            margin: 0 auto 15px auto;
            font-family: inherit;
            transition: all 0.3s;
        }

        .name-input:focus {
            outline: none;
            border-color: #10b981;
            box-shadow: 0 0 10px rgba(16, 185, 129, 0.3);
        }

        .level-title {
            font-size: 1.3rem;
            margin-bottom: 10px;
            color: #e2e8f0;
        }

        .level-btn {
            background-color: #334155;
            color: white;
            border: 2px solid transparent;
            padding: 15px;
            font-size: 1.2rem;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            font-family: inherit;
            font-weight: bold;
        }

        .level-btn.easy:hover { background-color: #059669; border-color: #10b981; }
        .level-btn.medium:hover { background-color: #d97706; border-color: #f59e0b; }
        .level-btn.hard:hover { background-color: #e11d48; border-color: #fb7185; }

        /* شاشة الكويز */
        #quizScreen {
            display: none;
        }

        .quiz-info-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #0f172a;
            padding: 10px 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            border: 1px solid #334155;
            flex-wrap: wrap;
            gap: 10px;
        }

        .question-counter {
            font-size: 1.1rem;
            color: #94a3b8;
            font-weight: bold;
        }

        .timer-display {
            font-size: 1.2rem;
            color: #ef4444;
            font-weight: bold;
            background-color: #334155;
            padding: 5px 15px;
            border-radius: 20px;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .live-score {
            font-size: 1.2rem;
            color: #f59e0b;
            font-weight: bold;
            background-color: #334155;
            padding: 5px 15px;
            border-radius: 20px;
            transition: transform 0.2s;
        }
        
        .live-score.bump {
            transform: scale(1.2);
            color: #10b981;
        }

        .question-text {
            font-size: 1.4rem;
            margin-bottom: 25px;
            line-height: 1.5;
        }

        .options-container {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .option-btn {
            background-color: #334155;
            color: #f8fafc;
            border: 2px solid #334155;
            padding: 15px;
            font-size: 1.1rem;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            font-family: inherit;
        }

        .option-btn:hover:not(:disabled) {
            background-color: #475569;
        }

        .option-btn.correct {
            background-color: #059669 !important;
            border-color: #059669 !important;
            color: white;
            transform: scale(1.02);
            opacity: 1 !important;
        }

        .option-btn.wrong {
            background-color: #e11d48 !important;
            border-color: #e11d48 !important;
            color: white;
            animation: shake 0.4s;
            opacity: 1 !important;
        }

        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
            100% { transform: translateX(0); }
        }

        .option-btn:disabled {
            cursor: not-allowed;
            opacity: 0.6;
        }

        .next-btn {
            background-color: #10b981;
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 1.1rem;
            border-radius: 8px;
            cursor: pointer;
            margin-top: 25px;
            display: none;
            font-weight: bold;
            font-family: inherit;
            width: 100%;
        }

        .next-btn:hover { background-color: #059669; }

        /* شاشة النتيجة */
        #resultScreen {
            display: none;
        }

        .final-score {
            font-size: 2.2rem;
            color: #10b981;
            margin: 15px 0;
            font-weight: bold;
        }

        .stats-box {
            background-color: #0f172a;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            display: flex;
            justify-content: space-around;
            border: 1px solid #334155;
        }

        .stat-item {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }

        .stat-value {
            font-size: 1.5rem;
            font-weight: bold;
        }

        .stat-label {
            color: #94a3b8;
            font-size: 0.9rem;
        }

        /* لوحة الشرف Leaderboard */
        .leaderboard-container {
            margin-top: 20px;
            background-color: #0f172a;
            padding: 15px;
            border-radius: 10px;
            border: 1px solid #334155;
        }

        .leaderboard-title {
            color: #f8fafc;
            font-size: 1.2rem;
            margin-bottom: 15px;
            border-bottom: 1px solid #334155;
            padding-bottom: 10px;
        }

        .leaderboard-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px;
            margin-bottom: 10px;
            border-radius: 8px;
            background-color: #1e293b;
            font-weight: bold;
        }

        .rank-1 { background-color: rgba(255, 215, 0, 0.1); border: 1px solid #ffd700; color: #ffd700; }
        .rank-2 { background-color: rgba(192, 192, 192, 0.1); border: 1px solid #c0c0c0; color: #c0c0c0; }
        .rank-3 { background-color: rgba(205, 127, 50, 0.1); border: 1px solid #cd7f32; color: #cd7f32; }

        .restart-btn {
            background-color: #3b82f6;
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.2rem;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            font-family: inherit;
            margin-top: 20px;
            width: 100%;
        }

        .restart-btn:hover { background-color: #2563eb; }
    </style>
</head>
<body>

    <div class="main-container">
        <div class="header">🌙 كويز المعلومات الإسلامية</div>
        
        <div id="levelScreen">
            <input type="text" id="playerNameInput" class="name-input" placeholder="اكتب اسمك هنا يا بطل..." autocomplete="off">
            <div class="level-title">اختر مستوى الصعوبة لبدء التحدي:</div>
            <button class="level-btn easy" onclick="startQuiz('easy')">🟢 مستوى سهل</button>
            <button class="level-btn medium" onclick="startQuiz('medium')">🟠 مستوى متوسط</button>
            <button class="level-btn hard" onclick="startQuiz('hard')">🔴 مستوى صعب</button>
        </div>

        <div id="quizScreen">
            <div class="quiz-info-bar">
                <div class="question-counter" id="questionCounter">السؤال 1 / 20</div>
                <div class="timer-display" id="timerDisplay">⏱️ 15ث</div>
                <div class="live-score" id="liveScore">النقاط: 0</div>
            </div>
            
            <div class="question-text" id="questionText">جاري التحميل...</div>
            
            <div class="options-container" id="optionsContainer"></div>
            
            <button class="next-btn" id="nextBtn" onclick="goToNextQuestion()">السؤال التالي</button>
        </div>

        <div id="resultScreen">
            <h2>انتهى الاختبار! 🎉</h2>
            <div class="final-score" id="finalScore">0 نقطة</div>
            
            <div class="stats-box">
                <div class="stat-item">
                    <span class="stat-value" id="correctCount" style="color: #10b981;">0</span>
                    <span class="stat-label">إجابات صحيحة</span>
                </div>
                <div class="stat-item">
                    <span class="stat-value" id="wrongCount" style="color: #ef4444;">0</span>
                    <span class="stat-label">إجابات خاطئة</span>
                </div>
            </div>

            <div id="feedbackText" style="font-size: 1.1rem; color: #94a3b8; margin-bottom: 20px;"></div>
            
            <div class="leaderboard-container">
                <div class="leaderboard-title">🏆 أبطال الكويز 🏆</div>
                <div id="leaderboardList"></div>
            </div>

            <button class="restart-btn" onclick="resetToHome()">العودة للقائمة الرئيسية</button>
        </div>
    </div>

    <script>
        // إعدادات الصوت البرمجي
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        
        function playTone(freq, type, duration, vol = 0.1) {
            if (audioCtx.state === 'suspended') audioCtx.resume();
            const oscillator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            oscillator.type = type;
            oscillator.frequency.setValueAtTime(freq, audioCtx.currentTime);
            gainNode.gain.setValueAtTime(vol, audioCtx.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + duration);
            oscillator.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            oscillator.start();
            oscillator.stop(audioCtx.currentTime + duration);
        }

        function playCorrectSound() {
            playTone(600, 'sine', 0.1, 0.1);
            setTimeout(() => playTone(800, 'sine', 0.15, 0.1), 100);
        }

        function playWrongSound() {
            playTone(250, 'sawtooth', 0.3, 0.05);
            setTimeout(() => playTone(200, 'sawtooth', 0.4, 0.05), 150);
        }

        function triggerConfetti() {
            confetti({
                particleCount: 80,
                spread: 70,
                origin: { y: 0.6 },
                colors: ['#10b981', '#f59e0b', '#3b82f6', '#ffffff']
            });
        }

        // بنك الأسئلة بالكامل
        const questionBank = {
            easy: [
                { q: "من هو آخر الأنبياء والرسل؟", options: ["عيسى عليه السلام", "موسى عليه السلام", "محمد صلى الله عليه وسلم", "إبراهيم عليه السلام"], answer: 2 },
                { q: "ما هو أول شهر في التقويم الهجري؟", options: ["رمضان", "محرم", "شوال", "رجب"], answer: 1 },
                { q: "كم عدد الصلوات المفروضة في اليوم والليلة؟", options: ["3 صلوات", "4 صلوات", "5 صلوات", "6 صلوات"], answer: 2 },
                { q: "ما هو الكتاب السماوي الذي أُنزل على سيدنا محمد؟", options: ["القرآن الكريم", "الإنجيل", "التوراة", "الزبور"], answer: 0 },
                { q: "ما هي أقصر سورة في القرآن الكريم؟", options: ["الإخلاص", "الفلق", "الناس", "الكوثر"], answer: 3 },
                { q: "أين توجد الكعبة المشرفة؟", options: ["في المدينة المنورة", "في مكة المكرمة", "في القدس", "في الطائف"], answer: 1 },
                { q: "من هو أول الخلفاء الراشدين؟", options: ["عمر بن الخطاب", "علي بن أبي طالب", "أبو بكر الصديق", "عثمان بن عفان"], answer: 2 },
                { q: "في أي شهر يصوم المسلمون؟", options: ["رجب", "شعبان", "رمضان", "ذو الحجة"], answer: 2 },
                { q: "ما هو الركن الأول من أركان الإسلام؟", options: ["الصلاة", "الزكاة", "الشهادتان", "الصوم"], answer: 2 },
                { q: "ما هي قبلة المسلمين في الصلاة؟", options: ["المسجد الأقصى", "الكعبة المشرفة", "المسجد النبوي", "جبل عرفات"], answer: 1 },
                { q: "من هو النبي الذي بنى الكعبة مع ابنه؟", options: ["نوح عليه السلام", "إبراهيم عليه السلام", "موسى عليه السلام", "يوسف عليه السلام"], answer: 1 },
                { q: "ما هو الحيوان الذي ارتبط بقصة النبي صالح؟", options: ["الناقة", "الفيل", "الحوت", "الكلب"], answer: 0 },
                { q: "من هو النبي الذي ابتلعه الحوت؟", options: ["يونس عليه السلام", "أيوب عليه السلام", "يحيى عليه السلام", "يعقوب عليه السلام"], answer: 0 },
                { q: "من هو الملك الموكل بنزول الوحي؟", options: ["ميكائيل", "إسرافيل", "جبريل", "عزرائيل"], answer: 2 },
                { q: "ما هي السورة التي تقرأ في كل ركعة من الصلاة؟", options: ["البقرة", "الفاتحة", "الإخلاص", "الكوثر"], answer: 1 },
                { q: "كم عدد أعياد المسلمين في السنة؟", options: ["عيد واحد", "عيدان", "ثلاثة أعياد", "أربعة أعياد"], answer: 1 },
                { q: "من هو عم النبي الذي نزلت فيه سورة تذمه؟", options: ["أبو طالب", "حمزة", "العباس", "أبو لهب"], answer: 3 },
                { q: "ما اسم أم النبي محمد صلى الله عليه وسلم؟", options: ["حليمة السعدية", "آمنة بنت وهب", "خديجة بنت خويلد", "فاطمة بنت أسد"], answer: 1 },
                { q: "ما اسم والد النبي محمد صلى الله عليه وسلم؟", options: ["عبد المطلب", "عبد الله", "أبو طالب", "هاشم"], answer: 1 },
                { q: "من هي أول امرأة أسلمت؟", options: ["عائشة بنت أبي بكر", "أسماء بنت أبي بكر", "خديجة بنت خويلد", "سمية بنت خياط"], answer: 2 },
                { q: "ما هو الركن الثاني من أركان الإسلام؟", options: ["الزكاة", "الصيام", "الصلاة", "الحج"], answer: 2 },
                { q: "من هو النبي الملقب بـ (خليل الله)؟", options: ["محمد", "إبراهيم", "موسى", "عيسى"], answer: 1 },
                { q: "ما هي السورة التي تسمى بأم الكتاب؟", options: ["البقرة", "يس", "الفاتحة", "الكهف"], answer: 2 },
                { q: "كم عدد ركعات صلاة الفجر؟", options: ["ركعة واحدة", "ركعتان", "ثلاث ركعات", "أربع ركعات"], answer: 1 },
                { q: "من هو الصحابي الذي نام في فراش النبي ليلة الهجرة؟", options: ["أبو بكر الصديق", "عمر بن الخطاب", "علي بن أبي طالب", "عثمان بن عفان"], answer: 2 },
                { q: "ما هو الطائر الذي تكلم مع النبي سليمان؟", options: ["الغراب", "الحمامة", "الهدهد", "النسر"], answer: 2 },
                { q: "ما هو السيف الملقب بـ (ذو الفقار) لمن كان يتبع؟", options: ["خالد بن الوليد", "علي بن أبي طالب", "حمزة بن عبد المطلب", "عمر بن الخطاب"], answer: 1 },
                { q: "ما هي السورة التي تحمي قارئها من الدجال؟", options: ["الملك", "الكهف", "البقرة", "آل عمران"], answer: 1 },
                { q: "أين ولد النبي محمد صلى الله عليه وسلم؟", options: ["المدينة المنورة", "الطائف", "مكة المكرمة", "الشام"], answer: 2 },
                { q: "ما هو اللقب الذي أطلق على النبي محمد قبل البعثة؟", options: ["الصادق الأمين", "الفاروق", "ذو النورين", "سيف الله"], answer: 0 }
            ],
            medium: [
                { q: "ما هي السورة التي تُسمى (قلب القرآن)؟", options: ["سورة يس", "سورة الرحمن", "سورة تبارك", "سورة الكهف"], answer: 0 },
                { q: "من هو الصحابي الجليل الملقب بـ (سيف الله المسلول)؟", options: ["حمزة بن عبد المطلب", "خالد بن الوليد", "سعد بن معاذ", "أبو عبيدة بن الجراح"], answer: 1 },
                { q: "من هو أول مؤذن في الإسلام؟", options: ["بلال بن رباح", "عمار بن ياسر", "صهيب الرومي", "سلمان الفارسي"], answer: 0 },
                { q: "ما هي القبلة الأولى للمسلمين قبل الكعبة؟", options: ["المسجد النبوي", "المسجد الأموي", "المسجد الأقصى", "مسجد قباء"], answer: 2 },
                { q: "ما هي السورة الوحيدة التي لا تبدأ بـ (بسم الله الرحمن الرحيم)؟", options: ["الأنفال", "التوبة", "النحل", "الرعد"], answer: 1 },
                { q: "كم سنة استمر نزول الوحي بالقرآن الكريم؟", options: ["10 سنوات", "20 سنة", "23 سنة", "30 سنة"], answer: 2 },
                { q: "ما هي الغزوة التي سُميت بـ (يوم الفرقان)؟", options: ["أحد", "الخندق", "بدر", "تبوك"], answer: 2 },
                { q: "كم عدد سور القرآن الكريم؟", options: ["110 سورة", "114 سورة", "120 سورة", "99 سورة"], answer: 1 },
                { q: "ما هي السورة التي تُسمى (عروس القرآن)؟", options: ["الواقعة", "الرحمن", "يس", "يوسف"], answer: 1 },
                { q: "من هو الصحابي الذي تستحي منه ملائكة الرحمن؟", options: ["عثمان بن عفان", "عمر بن الخطاب", "علي بن أبي طالب", "الزبير بن العوام"], answer: 0 },
                { q: "من هي مرضعة النبي محمد صلى الله عليه وسلم؟", options: ["أم أيمن", "ثويبة", "حليمة السعدية", "آمنة بنت وهب"], answer: 2 },
                { q: "إلى أي قبيلة ينتمي النبي محمد؟", options: ["خزرج", "أوس", "قريش", "ثقيف"], answer: 2 },
                { q: "ما اسم الغار الذي نزل فيه الوحي لأول مرة؟", options: ["غار ثور", "غار حراء", "غار الطور", "غار أحد"], answer: 1 },
                { q: "ما هي المعجزة التي أُسري فيها بالنبي للسماء؟", options: ["شق الصدر", "الإسراء والمعراج", "انشقاق القمر", "الهجرة"], answer: 1 },
                { q: "في أي غزوة خالف الرماة أمر النبي؟", options: ["بدر", "أحد", "مؤتة", "الخندق"], answer: 1 },
                { q: "من هي زوجة فرعون التي ضرب الله بها مثلاً للمؤمنين؟", options: ["مريم", "آسيا", "سارة", "هاجر"], answer: 1 },
                { q: "كم عدد أجزاء القرآن الكريم؟", options: ["20 جزء", "30 جزء", "40 جزء", "60 جزء"], answer: 1 },
                { q: "من هو النبي الذي تكلم في المهد صبياً؟", options: ["يحيى عليه السلام", "موسى عليه السلام", "عيسى عليه السلام", "يوسف عليه السلام"], answer: 2 },
                { q: "من هو الصحابي الذي كُلف بجمع القرآن الكريم في عهد أبي بكر؟", options: ["عبدالله بن مسعود", "زيد بن ثابت", "أبي بن كعب", "معاذ بن جبل"], answer: 1 },
                { q: "ما هي السورة التي سميت باسم امرأة؟", options: ["سورة النساء", "سورة خديجة", "سورة مريم", "سورة فاطمة"], answer: 2 },
                { q: "ما هي الغزوة التي تم فيها حفر الخندق؟", options: ["بدر", "أحد", "الأحزاب", "حنين"], answer: 2 },
                { q: "من هو قائد الفرس في معركة القادسية؟", options: ["كسرى", "رستم", "المقوقس", "هرقل"], answer: 1 },
                { q: "ما هي السورة التي تعادل ثلث القرآن؟", options: ["الفاتحة", "الإخلاص", "الفلق", "الناس"], answer: 1 },
                { q: "من هو الصحابي الذي أشار على النبي بحفر الخندق؟", options: ["عمر بن الخطاب", "سلمان الفارسي", "علي بن أبي طالب", "أبو بكر الصديق"], answer: 1 },
                { q: "في أي سنة فرض الصيام على المسلمين؟", options: ["السنة الأولى للهجرة", "السنة الثانية للهجرة", "السنة الثالثة للهجرة", "السنة الرابعة للهجرة"], answer: 1 },
                { q: "من هو كافل السيدة مريم عليها السلام؟", options: ["زكريا", "يحيى", "عيسى", "موسى"], answer: 0 },
                { q: "ما اسم الشجرة التي تنبت في قعر جهنم؟", options: ["شجرة الزيتون", "شجرة الزقوم", "شجرة التين", "شجرة الغرقد"], answer: 1 },
                { q: "من هو النبي الذي ألقي في النار ولم تحرقه؟", options: ["موسى", "إبراهيم", "يوسف", "يونس"], answer: 1 },
                { q: "ما هي الغزوة التي كانت قبل غزوة الخندق؟", options: ["أحد", "بدر", "أحزاب", "بني المصطلق"], answer: 3 },
                { q: "من هو الصحابي الذي أشار على النبي بجمع القرآن؟", options: ["عمر بن الخطاب", "أبو بكر", "عثمان", "علي"], answer: 0 }
            ],
            hard: [
                { q: "ما هي أطول سورة في القرآن الكريم؟", options: ["سورة البقرة", "سورة آل عمران", "سورة النساء", "سورة الأعراف"], answer: 0 },
                { q: "ما هي السورة التي وردت فيها (البسملة) مرتين؟", options: ["سورة النمل", "سورة القصص", "سورة النحل", "سورة هود"], answer: 0 },
                { q: "من هو النبي الأكثر ذكراً بالاسم في القرآن الكريم؟", options: ["محمد", "إبراهيم", "عيسى", "موسى"], answer: 3 },
                { q: "ما هو الاسم الآخر لغزوة الخندق؟", options: ["غزوة الأحزاب", "غزوة تبوك", "غزوة حنين", "غزوة بني قينقاع"], answer: 0 },
                { q: "ما اسم باب الجنة المخصص للصائمين؟", options: ["باب التوبة", "باب الريان", "باب الصلاة", "باب الجهاد"], answer: 1 },
                { q: "من هو الصحابي الذي اهتز لموته عرش الرحمن؟", options: ["سعد بن معاذ", "سعد بن أبي وقاص", "حمزة بن عبد المطلب", "جعفر بن أبي طالب"], answer: 0 },
                { q: "من هي أول شهيدة في الإسلام؟", options: ["خديجة بنت خويلد", "فاطمة بنت الخطاب", "سمية بنت خياط", "أسماء بنت أبي بكر"], answer: 2 },
                { q: "في أي عام ميلادي وُلد النبي محمد تقريباً؟", options: ["570 م", "610 م", "622 م", "632 م"], answer: 0 },
                { q: "ما هي السورة التي تنتهي بذكر نبيين؟", options: ["سورة الأعلى", "سورة الفجر", "سورة الغاشية", "سورة الشمس"], answer: 0 },
                { q: "من الذي قام بتغسيل النبي بعد وفاته؟", options: ["أبو بكر الصديق", "عمر بن الخطاب", "علي بن أبي طالب والعباس", "عثمان بن عفان"], answer: 2 },
                { q: "كم كان عمر النبي عند وفاته؟", options: ["60 عاماً", "63 عاماً", "65 عاماً", "70 عاماً"], answer: 1 },
                { q: "كم عدد أبواب الجنة؟", options: ["6 أبواب", "7 أبواب", "8 أبواب", "9 أبواب"], answer: 2 },
                { q: "في أي سنة هجرية تم صلح الحديبية؟", options: ["العام الرابع", "العام الخامس", "العام السادس", "العام الثامن"], answer: 2 },
                { q: "ما هي السورة المنجية من عذاب القبر؟", options: ["سورة الدخان", "سورة السجدة", "سورة الملك", "سورة القيامة"], answer: 2 },
                { q: "من هو أطول الأنبياء عمراً؟", options: ["آدم عليه السلام", "نوح عليه السلام", "شعيب عليه السلام", "إدريس عليه السلام"], answer: 1 },
                { q: "ما اسم ملك الحبشة الذي استقبل المسلمين في الهجرة الأولى؟", options: ["المقوقس", "النجاشي", "كسرى", "هرقل"], answer: 1 },
                { q: "من هو الصحابي الملقب بـ (ترجمان القرآن)؟", options: ["عبدالله بن مسعود", "عبدالله بن عباس", "زيد بن ثابت", "أبي بن كعب"], answer: 1 },
                { q: "ما هو الحيوان الذي نام مع أصحاب الكهف؟", options: ["قط", "كلب", "ذئب", "أسد"], answer: 1 },
                { q: "ما هو اسم ناقة النبي محمد صلى الله عليه وسلم؟", options: ["القصواء", "الشهباء", "العضباء", "البراق"], answer: 0 },
                { q: "ما هو الجبل الذي رست عليه سفينة نوح؟", options: ["جبل الطور", "جبل الجودي", "جبل أحد", "جبل الصفا"], answer: 1 },
                { q: "من هو الصحابي الذي أُطلق عليه لقب (أمين هذه الأمة)؟", options: ["أبو عبيدة بن الجراح", "أبو بكر الصديق", "عمر بن الخطاب", "عبد الرحمن بن عوف"], answer: 0 },
                { q: "كم عدد السور المكية في القرآن الكريم؟", options: ["86 سورة", "93 سورة", "114 سورة", "28 سورة"], answer: 0 },
                { q: "من هم القوم الذين أُرسل إليهم النبي هود عليه السلام؟", options: ["قوم ثمود", "قوم عاد", "قوم مدين", "قوم لوط"], answer: 1 },
                { q: "في أي غزوة قطعت يد الصحابي جعفر بن أبي طالب؟", options: ["غزوة بدر", "غزوة أحد", "غزوة مؤتة", "غزوة تبوك"], answer: 2 },
                { q: "ما هي السورة التي تسمى الفاضحة؟", options: ["سورة التوبة", "سورة الأحزاب", "سورة المنافقون", "سورة النور"], answer: 0 },
                { q: "من هو النبي الذي سخر الله له الجبال تسبح معه؟", options: ["سليمان", "داود", "أيوب", "يونس"], answer: 1 },
                { q: "كم كان عدد المسلمين في غزوة بدر؟", options: ["300", "313", "1000", "3000"], answer: 1 },
                { q: "من هو أول من سل سيفاً في سبيل الله؟", options: ["الزبير بن العوام", "علي بن أبي طالب", "المقداد بن عمرو", "حمزة بن عبد المطلب"], answer: 0 },
                { q: "في أي سورة ذُكرت قصة ذي القرنين؟", options: ["سورة الكهف", "سورة يوسف", "سورة البقرة", "سورة الأنبياء"], answer: 0 },
                { q: "ما هي الغزوة التي جُرح فيها النبي وكُسرت رَباعيته؟", options: ["غزوة بدر", "غزوة أحد", "غزوة الخندق", "غزوة حنين"], answer: 1 }
            ]
        };

        // المتغيرات الأساسية للكويز
        let currentQuestions = [];
        let currentQuestionIndex = 0;
        let score = 0;
        let correctCount = 0;
        let wrongCount = 0;
        let timerInterval;
        let timeLeft = 15;
        let playerName = "";

        // بدء الكويز
        function startQuiz(level) {
            const nameInput = document.getElementById('playerNameInput').value.trim();
            playerName = nameInput !== "" ? nameInput : "بطل مجهول";
            
            // جلب الأسئلة بناءً على المستوى، ترتيبها عشوائياً، ثم اختيار 20 سؤال
            let allQuestions = [...questionBank[level]];
            allQuestions.sort(() => Math.random() - 0.5);
            currentQuestions = allQuestions.slice(0, 20);

            currentQuestionIndex = 0;
            score = 0;
            correctCount = 0;
            wrongCount = 0;

            document.getElementById('levelScreen').style.display = 'none';
            document.getElementById('resultScreen').style.display = 'none';
            document.getElementById('quizScreen').style.display = 'block';
            document.getElementById('liveScore').innerText = `النقاط: ${score}`;

            loadQuestion();
        }

        // تحميل وعرض السؤال
        function loadQuestion() {
            clearInterval(timerInterval);
            timeLeft = 15;
            document.getElementById('timerDisplay').innerText = `⏱️ ${timeLeft}ث`;
            document.getElementById('nextBtn').style.display = 'none';
            
            document.getElementById('questionCounter').innerText = `السؤال ${currentQuestionIndex + 1} / ${currentQuestions.length}`;
            
            const q = currentQuestions[currentQuestionIndex];
            document.getElementById('questionText').innerText = q.q;
            
            const optionsContainer = document.getElementById('optionsContainer');
            optionsContainer.innerHTML = '';
            
            q.options.forEach((opt, index) => {
                const btn = document.createElement('button');
                btn.className = 'option-btn';
                btn.innerText = opt;
                btn.onclick = () => checkAnswer(btn, index);
                optionsContainer.appendChild(btn);
            });

            startTimer();
        }

        // تشغيل المؤقت
        function startTimer() {
            timerInterval = setInterval(() => {
                timeLeft--;
                document.getElementById('timerDisplay').innerText = `⏱️ ${timeLeft}ث`;
                if(timeLeft <= 0) {
                    clearInterval(timerInterval);
                    handleTimeout();
                }
            }, 1000);
        }

        // عند انتهاء الوقت
        function handleTimeout() {
            playWrongSound();
            wrongCount++;
            disableOptions();
            showCorrectAnswer();
            document.getElementById('nextBtn').style.display = 'block';
        }

        // فحص الإجابة
        function checkAnswer(selectedBtn, selectedIndex) {
            clearInterval(timerInterval);
            disableOptions();
            
            const q = currentQuestions[currentQuestionIndex];
            if(selectedIndex === q.answer) {
                selectedBtn.classList.add('correct');
                playCorrectSound();
                score += 10;
                correctCount++;
                
                const scoreDisplay = document.getElementById('liveScore');
                scoreDisplay.innerText = `النقاط: ${score}`;
                scoreDisplay.classList.add('bump');
                setTimeout(() => scoreDisplay.classList.remove('bump'), 200);
            } else {
                selectedBtn.classList.add('wrong');
                playWrongSound();
                wrongCount++;
                showCorrectAnswer();
            }
            
            document.getElementById('nextBtn').style.display = 'block';
        }

        // إيقاف تفاعل الأزرار
        function disableOptions() {
            const btns = document.querySelectorAll('.option-btn');
            btns.forEach(btn => btn.disabled = true);
        }

        // إظهار الإجابة الصحيحة
        function showCorrectAnswer() {
            const q = currentQuestions[currentQuestionIndex];
            const btns = document.querySelectorAll('.option-btn');
            btns[q.answer].classList.add('correct');
        }

        // الانتقال للسؤال التالي
        function goToNextQuestion() {
            currentQuestionIndex++;
            if(currentQuestionIndex < currentQuestions.length) {
                loadQuestion();
            } else {
                showResult();
            }
        }

        // إظهار النتائج النهائية
        function showResult() {
            document.getElementById('quizScreen').style.display = 'none';
            document.getElementById('resultScreen').style.display = 'block';
            
            document.getElementById('finalScore').innerText = `${score} نقطة`;
            document.getElementById('correctCount').innerText = correctCount;
            document.getElementById('wrongCount').innerText = wrongCount;
            
            const feedbackBox = document.getElementById('feedbackText');
            if(correctCount >= 15) {
                feedbackBox.innerText = "ممتاز! معلوماتك الإسلامية رائعة جداً 🌟";
                triggerConfetti();
            } else if(correctCount >= 10) {
                feedbackBox.innerText = "جيد جداً! لكن يمكنك التحسن أكثر 💪";
            } else {
                feedbackBox.innerText = "حاول مرة أخرى لتطوير معلوماتك القيمة 📚";
            }
            
            updateLeaderboard();
        }

        // تحديث لوحة الشرف
        function updateLeaderboard() {
            let leaderboard = JSON.parse(localStorage.getItem('islamicQuizLeaderboard')) || [];
            leaderboard.push({ name: playerName, score: score });
            
            // ترتيب تنازلي حسب النقاط
            leaderboard.sort((a, b) => b.score - a.score);
            // الاحتفاظ بأفضل 5 لاعبين فقط
            leaderboard = leaderboard.slice(0, 5); 
            
            localStorage.setItem('islamicQuizLeaderboard', JSON.stringify(leaderboard));
            
            const list = document.getElementById('leaderboardList');
            list.innerHTML = '';
            leaderboard.forEach((entry, idx) => {
                const item = document.createElement('div');
                item.className = `leaderboard-item ${idx < 3 ? 'rank-' + (idx + 1) : ''}`;
                item.innerHTML = `<span>${idx + 1}. ${entry.name}</span><span>${entry.score} نقطة</span>`;
                list.appendChild(item);
            });
        }

        // العودة للشاشة الرئيسية
        function resetToHome() {
            document.getElementById('resultScreen').style.display = 'none';
            document.getElementById('levelScreen').style.display = 'flex';
            document.getElementById('playerNameInput').value = '';
        }
    </script>
</body>
</html>
