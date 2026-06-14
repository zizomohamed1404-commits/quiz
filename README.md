Weaa Academy/
Creator Zidane Mohamed

  <!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>كويز التحدي الشامل</title>
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

        .screen {
            display: none;
            flex-direction: column;
            gap: 15px;
            margin-top: 20px;
        }

        .screen.active {
            display: flex;
        }

        .title-text {
            font-size: 1.3rem;
            margin-bottom: 10px;
            color: #e2e8f0;
        }

        .btn {
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

        /* Category Buttons */
        .btn.islamic { background-color: #047857; }
        .btn.islamic:hover { background-color: #065f46; border-color: #10b981; }
        .btn.general { background-color: #2563eb; }
        .btn.general:hover { background-color: #1d4ed8; border-color: #60a5fa; }

        /* Level Buttons */
        .btn.easy:hover { background-color: #059669; border-color: #10b981; }
        .btn.medium:hover { background-color: #d97706; border-color: #f59e0b; }
        .btn.hard:hover { background-color: #e11d48; border-color: #fb7185; }

        .back-btn {
            background-color: transparent;
            color: #94a3b8;
            border: 1px solid #94a3b8;
            padding: 10px;
            margin-top: 10px;
            border-radius: 8px;
            cursor: pointer;
            font-family: inherit;
        }
        .back-btn:hover { background-color: #334155; color: white; }

        /* Quiz Screen */
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

        .question-counter { font-size: 1.1rem; color: #94a3b8; font-weight: bold; }
        
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
        .live-score.bump { transform: scale(1.2); color: #10b981; }

        .question-text { font-size: 1.4rem; margin-bottom: 25px; line-height: 1.5; }
        .options-container { display: flex; flex-direction: column; gap: 12px; }
        
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
        .option-btn:hover:not(:disabled) { background-color: #475569; }
        .option-btn.correct {
            background-color: #059669 !important; border-color: #059669 !important; color: white;
            transform: scale(1.02); opacity: 1 !important;
        }
        .option-btn.wrong {
            background-color: #e11d48 !important; border-color: #e11d48 !important; color: white;
            animation: shake 0.4s; opacity: 1 !important;
        }

        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
            100% { transform: translateX(0); }
        }

        .option-btn:disabled { cursor: not-allowed; opacity: 0.6; }

        .next-btn {
            background-color: #10b981; color: white; border: none; padding: 12px 30px;
            font-size: 1.1rem; border-radius: 8px; cursor: pointer; margin-top: 25px;
            display: none; font-weight: bold; font-family: inherit; width: 100%;
        }
        .next-btn:hover { background-color: #059669; }

        /* Result Screen */
        .final-score { font-size: 2.2rem; color: #10b981; margin: 15px 0; font-weight: bold; }
        .stats-box {
            background-color: #0f172a; padding: 15px; border-radius: 10px;
            margin-bottom: 20px; display: flex; justify-content: space-around;
            border: 1px solid #334155;
        }
        .stat-item { display: flex; flex-direction: column; gap: 5px; }
        .stat-value { font-size: 1.5rem; font-weight: bold; }
        .stat-label { color: #94a3b8; font-size: 0.9rem; }

        /* Leaderboard */
        .leaderboard-container {
            margin-top: 20px; background-color: #0f172a; padding: 15px;
            border-radius: 10px; border: 1px solid #334155;
        }
        .leaderboard-title {
            color: #f8fafc; font-size: 1.2rem; margin-bottom: 15px;
            border-bottom: 1px solid #334155; padding-bottom: 10px;
        }
        .leaderboard-item {
            display: flex; justify-content: space-between; align-items: center;
            padding: 12px; margin-bottom: 10px; border-radius: 8px;
            background-color: #1e293b; font-weight: bold;
        }
        .rank-1 { background-color: rgba(255, 215, 0, 0.1); border: 1px solid #ffd700; color: #ffd700; }
        .rank-2 { background-color: rgba(192, 192, 192, 0.1); border: 1px solid #c0c0c0; color: #c0c0c0; }
        .rank-3 { background-color: rgba(205, 127, 50, 0.1); border: 1px solid #cd7f32; color: #cd7f32; }

        .restart-btn {
            background-color: #3b82f6; color: white; border: none; padding: 15px 40px;
            font-size: 1.2rem; border-radius: 8px; cursor: pointer; font-weight: bold;
            font-family: inherit; margin-top: 20px; width: 100%;
        }
        .restart-btn:hover { background-color: #2563eb; }

    </style>
</head>
<body>

    <div class="main-container">
        <div class="header" id="mainHeader">🌟 كويز التحدي الشامل</div>
        
        <!-- شاشة اختيار القسم -->
        <div id="categoryScreen" class="screen active">
            <input type="text" id="playerNameInput" class="name-input" placeholder="اكتب اسمك هنا يا بطل..." autocomplete="off">
            <div class="title-text">اختر نوع التحدي:</div>
            <button class="btn islamic" onclick="selectCategory('islamic')">🌙 أسئلة دينية</button>
            <button class="btn general" onclick="selectCategory('general')">🌍 أسئلة عامة</button>
        </div>

        <!-- شاشة اختيار المستوى -->
        <div id="levelScreen" class="screen">
            <div class="title-text" id="levelTitleText">اختر مستوى الصعوبة:</div>
            <button class="btn easy" onclick="startQuiz('easy')">🟢 مستوى سهل</button>
            <button class="btn medium" onclick="startQuiz('medium')">🟠 مستوى متوسط</button>
            <button class="btn hard" onclick="startQuiz('hard')">🔴 مستوى صعب</button>
            <button class="back-btn" onclick="goBackToCategory()">العودة لاختيار القسم</button>
        </div>

        <!-- شاشة الكويز -->
        <div id="quizScreen" class="screen">
            <div class="quiz-info-bar">
                <div class="question-counter" id="questionCounter">السؤال 1 / 15</div>
                <div class="timer-display" id="timerDisplay">⏱️ 15ث</div>
                <div class="live-score" id="liveScore">النقاط: 0</div>
            </div>
            <div class="question-text" id="questionText">جاري التحميل...</div>
            <div class="options-container" id="optionsContainer"></div>
            <button class="next-btn" id="nextBtn" onclick="goToNextQuestion()">السؤال التالي</button>
        </div>

        <!-- شاشة النتيجة -->
        <div id="resultScreen" class="screen">
            <h2 id="resultTitle">انتهى الاختبار! 🎉</h2>
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
                <div class="leaderboard-title" id="leaderboardTitle">🏆 أبطال الكويز 🏆</div>
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
            confetti({ particleCount: 80, spread: 70, origin: { y: 0.6 }, colors: ['#10b981', '#f59e0b', '#3b82f6', '#ffffff'] });
        }

        // بنك الأسئلة المدمج (تستطيع إضافة حتى 200 سؤال لكل مستوى هنا)
        const questionBank = {
            islamic: {
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
                    { q: "من هو النبي الذي ابتلعه الحوت؟", options: ["يونس عليه السلام", "أيوب عليه السلام", "يحيى عليه السلام", "يعقوب عليه السلام"], answer: 0 },
                    { q: "من هو الملك الموكل بنزول الوحي؟", options: ["ميكائيل", "إسرافيل", "جبريل", "عزرائيل"], answer: 2 },
                    { q: "ما هي السورة التي تقرأ في كل ركعة من الصلاة؟", options: ["البقرة", "الفاتحة", "الإخلاص", "الكوثر"], answer: 1 },
                    { q: "كم عدد أعياد المسلمين في السنة؟", options: ["عيد واحد", "عيدان", "ثلاثة أعياد", "أربعة أعياد"], answer: 1 },
                    { q: "ما اسم أم النبي محمد صلى الله عليه وسلم؟", options: ["حليمة السعدية", "آمنة بنت وهب", "خديجة بنت خويلد", "فاطمة بنت أسد"], answer: 1 }
       { q: "ما هو الشهر الذي يلي شهر رمضان؟", options: ["شوال", "ذو القعدة", "محرم", "شعبان"], answer: 0 },
            { q: "كم ركعة في صلاة الظهر؟", options: ["ركعتان", "3 ركعات", "4 ركعات", "5 ركعات"], answer: 2 },
            { q: "ما هي السورة التي بدأت باسم فاكهتين؟", options: ["سورة النجم", "سورة التين", "سورة العصر", "سورة الفجر"], answer: 1 },
            { q: "كم كان عمر النبي صلى الله عليه وسلم حين نزل عليه الوحي؟", options: ["30 سنة", "40 سنة", "50 سنة", "35 سنة"], answer: 1 },
            { q: "من هو النبي الذي بنى سفينة عظيمة؟", options: ["موسى", "نوح", "إبراهيم", "عيسى"], answer: 1 },
            { q: "ما هي أركان الإيمان؟", options: ["5", "6", "4", "7"], answer: 1 },
            { q: "أين توفي النبي محمد صلى الله عليه وسلم؟", options: ["مكة", "الطائف", "المدينة", "تبوك"], answer: 2 },
            { q: "ما اسم والد النبي محمد صلى الله عليه وسلم؟", options: ["عبد المطلب", "عبد الله", "أبو طالب", "حمزة"], answer: 1 },
            { q: "من هو النبي الذي كان يعمل نجاراً؟", options: ["داود", "زكريا", "موسى", "عيسى"], answer: 1 },
            { q: "ما هي السورة التي تسمى (عروس القرآن)؟", options: ["يس", "الرحمن", "الملك", "الواقعة"], answer: 1 },
            { q: "كم عدد أبواب الجنة؟", options: ["7", "8", "9", "10"], answer: 1 },
            { q: "ما اسم خازن الجنة؟", options: ["مالك", "رضوان", "جبريل", "ميكائيل"], answer: 1 },
            { q: "ما اسم خازن النار؟", options: ["مالك", "رضوان", "منكر", "نكير"], answer: 0 },
            { q: "كم سنة دعا النبي صلى الله عليه وسلم في مكة؟", options: ["10 سنوات", "13 سنة", "15 سنة", "23 سنة"], answer: 1 },
            { q: "من هو أول شهيد في الإسلام؟", options: ["حمزة", "عمار بن ياسر", "الحارث بن أبي هالة", "مصعب بن عمير"], answer: 2 },
            { q: "ما اسم مكة قديماً؟", options: ["بكة", "يثرب", "طيبة", "القادسية"], answer: 0 },
            { q: "ما هي العبادة التي تُسمى (نصف الدين)؟", options: ["الصلاة", "الصوم", "الزواج", "الحج"], answer: 2 },
            { q: "من هو النبي الذي أُتي بآيات تدل على أنه يكلم الطير؟", options: ["يوسف", "سليمان", "داود", "عيسى"], answer: 1 },
            { q: "ما هي السورة التي تعدل ثلث القرآن؟", options: ["الإخلاص", "الفاتحة", "الناس", "الفلق"], answer: 0 },
            { q: "أين هاجر المسلمون في الهجرة الأولى؟", options: ["المدينة", "الحبشة", "الشام", "اليمن"], answer: 1 }         ],
                medium: [
                    { q: "ما هي السورة التي تُسمى (قلب القرآن)؟", options: ["سورة يس", "سورة الرحمن", "سورة تبارك", "سورة الكهف"], answer: 0 },
                    { q: "من هو الصحابي الجليل الملقب بـ (سيف الله المسلول)؟", options: ["حمزة بن عبد المطلب", "خالد بن الوليد", "سعد بن معاذ", "أبو عبيدة بن الجراح"], answer: 1 },
                    { q: "من هو أول مؤذن في الإسلام؟", options: ["بلال بن رباح", "عمار بن ياسر", "صهيب الرومي", "سلمان الفارسي"], answer: 0 },
                    { q: "ما هي القبلة الأولى للمسلمين قبل الكعبة؟", options: ["المسجد النبوي", "المسجد الأموي", "المسجد الأقصى", "مسجد قباء"], answer: 2 },
                    { q: "ما هي السورة الوحيدة التي لا تبدأ بـ (بسم الله الرحمن الرحيم)؟", options: ["الأنفال", "التوبة", "النحل", "الرعد"], answer: 1 },
                    { q: "كم سنة استمر نزول الوحي بالقرآن الكريم؟", options: ["10 سنوات", "20 سنة", "23 سنة", "30 سنة"], answer: 2 },
                    { q: "ما هي الغزوة التي سُميت بـ (يوم الفرقان)؟", options: ["أحد", "الخندق", "بدر", "تبوك"], answer: 2 },
                    { q: "كم عدد سور القرآن الكريم؟", options: ["110 سورة", "114 سورة", "120 سورة", "99 سورة"], answer: 1 },
                    { q: "من هي مرضعة النبي محمد صلى الله عليه وسلم؟", options: ["أم أيمن", "ثويبة", "حليمة السعدية", "آمنة بنت وهب"], answer: 2 },
                    { q: "ما اسم الغار الذي نزل فيه الوحي لأول مرة؟", options: ["غار ثور", "غار حراء", "غار الطور", "غار أحد"], answer: 1 },
                    { q: "ما هي المعجزة التي أُسري فيها بالنبي للسماء؟", options: ["شق الصدر", "الإسراء والمعراج", "انشقاق القمر", "الهجرة"], answer: 1 },
                    { q: "من هي زوجة فرعون التي ضرب الله بها مثلاً للمؤمنين؟", options: ["مريم", "آسيا", "سارة", "هاجر"], answer: 1 },
                    { q: "كم عدد أجزاء القرآن الكريم؟", options: ["20 جزء", "30 جزء", "40 جزء", "60 جزء"], answer: 1 },
                    { q: "من هو الصحابي الذي كُلف بجمع القرآن في عهد أبي بكر؟", options: ["عبدالله بن مسعود", "زيد بن ثابت", "أبي بن كعب", "معاذ بن جبل"], answer: 1 },
                    { q: "ما هي الغزوة التي تم فيها حفر الخندق؟", options: ["بدر", "أحد", "الأحزاب", "حنين"], answer: 2 },
                    { q: "ما هي السورة التي تعادل ثلث القرآن؟", options: ["الفاتحة", "الإخلاص", "الفلق", "الناس"], answer: 1 }
            { q: "ما هي السورة التي نزلت كاملة في ليلة واحدة؟", options: ["الأنعام", "الكهف", "يس", "الرحمن"], answer: 0 },
            { q: "من الصحابي الذي هزه عرش الرحمن لموته؟", options: ["سعد بن معاذ", "جعفر الطيار", "خالد بن الوليد", "أبو بكر"], answer: 0 },
            { q: "ما هو أول عمل قام به النبي عند وصوله للمدينة؟", options: ["بناء المسجد", "المؤاخاة", "كتابة الوثيقة", "تجهيز الجيش"], answer: 0 },
            { q: "من هي الصحابية التي كانت تسمى (الرميصاء)؟", options: ["أم سليم", "أم عمارة", "أسماء بنت أبي بكر", "خديجة"], answer: 0 },
            { q: "في أي سنة فُرضت الزكاة؟", options: ["السنة 1 هـ", "السنة 2 هـ", "السنة 3 هـ", "السنة 4 هـ"], answer: 1 },
            { q: "ما اسم السيف الذي أهداه النبي لعلي بن أبي طالب؟", options: ["ذو الفقار", "البتار", "حتف", "الرسوب"], answer: 0 },
            { q: "من هو الصحابي الذي جمع الناس على صلاة التراويح؟", options: ["أبو بكر", "عمر بن الخطاب", "عثمان", "علي"], answer: 1 },
            { q: "ما اسم الغار الذي كان يختلي فيه النبي قبل البعثة؟", options: ["حراء", "ثور", "الجودي", "أحد"], answer: 0 },
            { q: "كم عدد زوجات النبي صلى الله عليه وسلم اللاتي توفي عنهن؟", options: ["9", "11", "13", "7"], answer: 1 },
            { q: "ما اسم مولى النبي الذي كان يحبه كابنه؟", options: ["زيد بن حارثة", "بلال", "صهيب", "عمار"], answer: 0 },
            { q: "من الذي لقبه النبي بـ (أمين الأمة)؟", options: ["أبو عبيدة بن الجراح", "أبو بكر", "عمر", "علي"], answer: 0 },
            { q: "ما السورة التي ذكرت فيها البسملة مرتين؟", options: ["النمل", "التوبة", "هود", "يوسف"], answer: 0 },
            { q: "ما هي الغزوة التي شارك فيها النبي ولم يقاتل؟", options: ["بدر", "أحد", "الحديبية", "العشيرة"], answer: 3 },
            { q: "من الصحابي الذي لقبه النبي بـ (سيد الشهداء)؟", options: ["حمزة", "عمر", "علي", "سعد بن معاذ"], answer: 0 },
            { q: "ما اسم خالة النبي؟", options: ["آمنة", "صفية", "فاطمة بنت أسد", "أم أيمن"], answer: 2 },
            { q: "كم عدد الرسل الذين ذكروا في القرآن؟", options: ["25", "20", "30", "15"], answer: 0 },
            { q: "ما السورة التي تسمى (الفاضحة)؟", options: ["التوبة", "المنافقون", "البقرة", "النساء"], answer: 0 },
            { q: "ما أول شيء خلقه الله؟", options: ["القلم", "العرش", "الماء", "النور"], answer: 0 },
            { q: "من الصحابي الذي لقب بـ (ذو النورين)؟", options: ["عثمان", "علي", "عمر", "أبو بكر"], answer: 0 },
            { q: "من الذي لقب بـ (الفاروق)؟", options: ["عمر", "علي", "عثمان", "حمزة"], answer: 0 }    ],
                hard: [
                    { q: "ما هي أطول سورة في القرآن الكريم؟", options: ["سورة البقرة", "سورة آل عمران", "سورة النساء", "سورة الأعراف"], answer: 0 },
                    { q: "ما هي السورة التي وردت فيها (البسملة) مرتين؟", options: ["سورة النمل", "سورة القصص", "سورة النحل", "سورة هود"], answer: 0 },
                    { q: "من هو النبي الأكثر ذكراً بالاسم في القرآن الكريم؟", options: ["محمد", "إبراهيم", "عيسى", "موسى"], answer: 3 },
                    { q: "ما اسم باب الجنة المخصص للصائمين؟", options: ["باب التوبة", "باب الريان", "باب الصلاة", "باب الجهاد"], answer: 1 },
                    { q: "من هو الصحابي الذي اهتز لموته عرش الرحمن؟", options: ["سعد بن معاذ", "سعد بن أبي وقاص", "حمزة بن عبد المطلب", "جعفر بن أبي طالب"], answer: 0 },
                    { q: "من هي أول شهيدة في الإسلام؟", options: ["خديجة بنت خويلد", "فاطمة بنت الخطاب", "سمية بنت خياط", "أسماء بنت أبي بكر"], answer: 2 },
                    { q: "من الذي قام بتغسيل النبي بعد وفاته؟", options: ["أبو بكر الصديق", "عمر بن الخطاب", "علي بن أبي طالب والعباس", "عثمان بن عفان"], answer: 2 },
                    { q: "كم عدد أبواب الجنة؟", options: ["6 أبواب", "7 أبواب", "8 أبواب", "9 أبواب"], answer: 2 },
                    { q: "في أي سنة هجرية تم صلح الحديبية؟", options: ["العام الرابع", "العام الخامس", "العام السادس", "العام الثامن"], answer: 2 },
                    { q: "ما هي السورة المنجية من عذاب القبر؟", options: ["سورة الدخان", "سورة السجدة", "سورة الملك", "سورة القيامة"], answer: 2 },
                    { q: "من هو أطول الأنبياء عمراً؟", options: ["آدم عليه السلام", "نوح عليه السلام", "شعيب عليه السلام", "إدريس عليه السلام"], answer: 1 },
                    { q: "ما اسم ملك الحبشة الذي استقبل المسلمين في الهجرة الأولى؟", options: ["المقوقس", "النجاشي", "كسرى", "هرقل"], answer: 1 },
                    { q: "من هو الصحابي الملقب بـ (ترجمان القرآن)؟", options: ["عبدالله بن مسعود", "عبدالله بن عباس", "زيد بن ثابت", "أبي بن كعب"], answer: 1 },
                    { q: "ما هو الجبل الذي رست عليه سفينة نوح؟", options: ["جبل الطور", "جبل الجودي", "جبل أحد", "جبل الصفا"], answer: 1 },
                    { q: "كم عدد السور المكية في القرآن الكريم؟", options: ["86 سورة", "93 سورة", "114 سورة", "28 سورة"], answer: 0 },
                    { q: "من هم القوم الذين أُرسل إليهم النبي هود عليه السلام؟", options: ["قوم ثمود", "قوم عاد", "قوم مدين", "قوم لوط"], answer: 1 }
           { q: "ما اسم أم النبي محمد صلى الله عليه وسلم من الرضاعة؟", options: ["حليمة السعدية", "ثويبة", "أم أيمن", "سودة"], answer: 0 },
            { q: "من هو الصحابي الذي لقب بـ (صاحب سر النبي)؟", options: ["حذيفة بن اليمان", "أبو هريرة", "عبد الله بن عمر", "عائشة"], answer: 0 },
            { q: "من هو أول من جهر بالقرآن في مكة؟", options: ["عبد الله بن مسعود", "علي بن أبي طالب", "أبو بكر", "حمزة"], answer: 0 },
            { q: "في أي غزوة استشهد مصعب بن عمير؟", options: ["بدر", "أحد", "الخندق", "حنين"], answer: 1 },
            { q: "ما اسم ناقة النبي صلى الله عليه وسلم؟", options: ["القصواء", "الغبراء", "الورقاء", "العضباء"], answer: 0 },
            { q: "ما هي السورة التي خلت من حرف (الراء)؟", options: ["الإخلاص", "الكوثر", "الفاتحة", "الناس"], answer: 0 },
            { q: "من هو النبي الذي سجدت له الملائكة؟", options: ["آدم", "إبراهيم", "موسى", "محمد"], answer: 0 },
            { q: "كم استمرت دعوة النبي السرية؟", options: ["سنتين", "3 سنوات", "4 سنوات", "5 سنوات"], answer: 1 },
            { q: "من الذي لقبه النبي بـ (أسد الله)؟", options: ["حمزة", "علي", "عمر", "خالد"], answer: 0 },
            { q: "ما اسم بئر زمزم قديماً؟", options: ["برة", "حفيرة", "أغلم", "هجر"], answer: 0 },
            { q: "من هو الصحابي الذي كتب الوحي؟", options: ["زيد بن ثابت", "أبي بن كعب", "معاوية", "كل ما سبق"], answer: 3 },
            { q: "ما السورة التي تسمى (سورة التوديع)؟", options: ["النصر", "الفتح", "الكوثر", "التوبة"], answer: 0 },
            { q: "من الذي تولى غسل النبي؟", options: ["علي بن أبي طالب", "أبو بكر", "عمر", "حمزة"], answer: 0 },
            { q: "كم كان عدد جيش المسلمين في مؤتة؟", options: ["3 آلاف", "5 آلاف", "10 آلاف", "ألف"], answer: 0 },
            { q: "من أول من هاجر إلى الحبشة؟", options: ["عثمان بن عفان", "جعفر بن أبي طالب", "علي بن أبي طالب", "حمزة"], answer: 0 },
            { q: "ما السورة التي بدأت بكلمة (تَبَّت)؟", options: ["المسد", "الكهف", "الملك", "النبأ"], answer: 0 },
            { q: "من الذي أشار بحفر الخندق؟", options: ["سلمان الفارسي", "علي بن أبي طالب", "أبو بكر", "عمر"], answer: 0 },
            { q: "من هو الصحابي الذي كان يحمل راية المهاجرين في بدر؟", options: ["مصعب بن عمير", "حمزة", "علي", "عمر"], answer: 0 },
            { q: "ما اسم النبي الذي عاشت أمه بعده؟", options: ["محمد", "عيسى", "موسى", "إبراهيم"], answer: 0 },
            { q: "من الصحابي الذي لقب بـ (ترجمان القرآن)؟", options: ["عبد الله بن عباس", "علي", "أبي بن كعب", "عمر"], answer: 0 }     ]
            },
            general: {
                easy: [
                    { q: "ما هي عاصمة مصر؟", options: ["الإسكندرية", "القاهرة", "الأقصر", "أسوان"], answer: 1 },
                    { q: "ما هو أطول نهر في العالم؟", options: ["نهر الأمازون", "نهر النيل", "نهر المسيسيبي", "نهر الفرات"], answer: 1 },
                    { q: "ما هو أسرع حيوان بري في العالم؟", options: ["الأسد", "الحصان", "الفهد", "الغزال"], answer: 2 },
                    { q: "أي كوكب يسمى بالكوكب الأحمر؟", options: ["المشتري", "الزهرة", "المريخ", "زحل"], answer: 2 },
                    { q: "ما هي عاصمة المملكة العربية السعودية؟", options: ["جدة", "مكة", "الرياض", "الدمام"], answer: 2 },
                    { q: "ما هي أكبر قارة في العالم مساحة؟", options: ["أفريقيا", "آسيا", "أوروبا", "أمريكا الشمالية"], answer: 1 },
                    { q: "ما هو الغاز الذي نتنفسه لنعيش؟", options: ["ثاني أكسيد الكربون", "الهيدروجين", "الأكسجين", "النيتروجين"], answer: 2 },
                    { q: "ما هو أكبر محيط في العالم؟", options: ["المحيط الهندي", "المحيط الأطلسي", "المحيط الهادي", "المحيط المتجمد"], answer: 2 },
                    { q: "ما هو الحيوان الذي يلقب بـ (سفينة الصحراء)؟", options: ["الحصان", "الجمل", "الفيل", "النعامة"], answer: 1 },
                    { q: "كم عدد أيام الأسبوع؟", options: ["5", "6", "7", "8"], answer: 2 },
                    { q: "ما هي العملة الرسمية للولايات المتحدة؟", options: ["اليورو", "الجنيه", "الدولار", "الين"], answer: 2 },
                    { q: "ما هي عاصمة فرنسا؟", options: ["لندن", "روما", "باريس", "مدريد"], answer: 2 },
                    { q: "ما هو الشكل الهندسي للأرض؟", options: ["مسطح", "مربع", "كروي", "مثلث"], answer: 2 },
                    { q: "كم عدد ألوان قوس قزح؟", options: ["5", "6", "7", "8"], answer: 2 },
                    { q: "عضو في جسم الإنسان مسؤول عن حاسة الشم؟", options: ["الأذن", "العين", "الأنف", "اللسان"], answer: 2 },
                    { q: "ما هو لون الدم في جسم الإنسان؟", options: ["أزرق", "أحمر", "أصفر", "أخضر"], answer: 1 }
              { q: "ما هو الكوكب الذي يسمى كوكب الأرض؟", options: ["الأزرق", "الأحمر", "الأخضر", "الذهبي"], answer: 0 },
            { q: "ما هو الحيوان الذي يغير لونه؟", options: ["الحرباء", "الأسد", "الفيل", "الزرافة"], answer: 0 },
            { q: "كم عدد عيون النحلة؟", options: ["2", "5", "8", "1"], answer: 1 },
            { q: "ما هي عاصمة السعودية؟", options: ["الرياض", "جدة", "مكة", "الدمام"], answer: 0 },
            { q: "ما الذي نستخدمه لفتح القفل؟", options: ["المفتاح", "السكين", "الملعقة", "المطرقة"], answer: 0 },
            { q: "ما هو الحيوان الذي يعيش في الماء والهواء؟", options: ["التمساح", "السمك", "الطيور المائية", "كل ما سبق"], answer: 2 },
            { q: "من مخترع المصباح الكهربائي؟", options: ["توماس إديسون", "نيوتن", "أينشتاين", "جراهام"], answer: 0 },
            { q: "كم عدد أسابيع السنة؟", options: ["48", "52", "60", "40"], answer: 1 },
            { q: "ما أطول نهر في العالم؟", options: ["النيل", "الأمازون", "الفرات", "دجلة"], answer: 0 },
            { q: "ما لون دم الحشرة؟", options: ["أحمر", "شفاف", "أخضر", "أزرق"], answer: 1 },
            { q: "ما هي عاصمة مصر؟", options: ["القاهرة", "الإسكندرية", "الأقصر", "أسوان"], answer: 0 },
            { q: "كم لون في قوس قزح؟", options: ["5", "6", "7", "8"], answer: 2 },
            { q: "ما اسم صغير الأسد؟", options: ["شبل", "مهر", "عجل", "جرو"], answer: 0 },
            { q: "ما هو أضخم حيوان؟", options: ["الحوت الأزرق", "الفيل", "الزرافة", "الأسد"], answer: 0 },
            { q: "كم عدد أصابع اليد؟", options: ["4", "5", "6", "10"], answer: 1 },
            { q: "ما اسم الكوكب الذي نعيش عليه؟", options: ["الأرض", "المريخ", "المشتري", "زحل"], answer: 0 },
            { q: "أي فصل تتساقط فيه الأوراق؟", options: ["الخريف", "الربيع", "الصيف", "الشتاء"], answer: 0 },
            { q: "ما هو المعدن الذي لا يصدأ؟", options: ["الذهب", "الحديد", "النحاس", "الفضة"], answer: 0 },
            { q: "ما هو أسرع طائر؟", options: ["الصقر", "النعامة", "العصفور", "الببغاء"], answer: 0 },
            { q: "ماذا يغطي جسم السمكة؟", options: ["الريش", "الشعر", "الحراشف", "الفرو"], answer: 2 }  ],
                medium: [
                    { q: "من هو مخترع المصباح الكهربائي؟", options: ["آينشتاين", "نيوتن", "توماس إديسون", "جراهام بيل"], answer: 2 },
                    { q: "ما هي عاصمة اليابان؟", options: ["بكين", "سيول", "طوكيو", "بانكوك"], answer: 2 },
                    { q: "ما هي أصغر قارة في العالم؟", options: ["أوروبا", "أنتاركتيكا", "أستراليا", "أمريكا الجنوبية"], answer: 2 },
                    { q: "كم عدد قارات العالم؟", options: ["5", "6", "7", "8"], answer: 2 },
                    { q: "ما هي العملة الرسمية للمملكة المتحدة؟", options: ["اليورو", "الدولار", "الجنيه الإسترليني", "الفرنك"], answer: 2 },
                    { q: "من هو مكتشف قارة أمريكا؟", options: ["فاسكو دا غاما", "ماجلان", "كريستوفر كولومبوس", "ماركو بولو"], answer: 2 },
                    { q: "ما هي عاصمة إيطاليا؟", options: ["ميلانو", "البندقية", "روما", "نابولي"], answer: 2 },
                    { q: "ما هي اللغة الرسمية في البرازيل؟", options: ["الإسبانية", "البرتغالية", "الإنجليزية", "الفرنسية"], answer: 1 },
                    { q: "ما هو أعلى جبل في العالم؟", options: ["جبل كليمنجارو", "جبل إفرست", "جبل الألب", "جبل فوجي"], answer: 1 },
                    { q: "أين يقع برج إيفل؟", options: ["روما", "لندن", "نيويورك", "باريس"], answer: 3 },
                    { q: "ما هي أكبر دولة في العالم من حيث المساحة؟", options: ["كندا", "الصين", "الولايات المتحدة", "روسيا"], answer: 3 },
                    { q: "ما هو أضخم حيوان على وجه الأرض؟", options: ["الفيل الأفريقي", "القرش الأبيض", "الحوت الأزرق", "الديناصور"], answer: 2 },
                    { q: "كم عدد أسنان الإنسان البالغ؟", options: ["28", "30", "32", "34"], answer: 2 },
                    { q: "ما هي عاصمة إسبانيا؟", options: ["برشلونة", "إشبيلية", "مدريد", "فالنسيا"], answer: 2 },
                    { q: "ما هو السائل الذي يطلق عليه لقب (الذهب الأسود)؟", options: ["القهوة", "البترول", "الماء", "الزئبق"], answer: 1 },
                    { q: "ما هو البحر الذي يفصل بين قارتي أفريقيا وأوروبا؟", options: ["البحر الأحمر", "البحر الميت", "البحر المتوسط", "بحر العرب"], answer: 2 }
             { q: "ما هي أكبر قارة في العالم؟", options: ["آسيا", "أفريقيا", "أوروبا", "أمريكا"], answer: 0 },
            { q: "ما هو العنصر الذي يرمز له بـ O؟", options: ["الأكسجين", "النيتروجين", "الهيدروجين", "الكربون"], answer: 0 },
            { q: "في أي قارة تقع مصر؟", options: ["أفريقيا", "آسيا", "أوروبا", "أمريكا"], answer: 0 },
            { q: "ما اسم أكبر محيط؟", options: ["الهادي", "الهندي", "الأطلسي", "المتجمد"], answer: 0 },
            { q: "ما هي عاصمة اليابان؟", options: ["طوكيو", "بكين", "سيول", "بانكوك"], answer: 0 },
            { q: "ما هو الغاز الذي نخرجه أثناء التنفس؟", options: ["ثاني أكسيد الكربون", "الأكسجين", "النيتروجين", "الهيليوم"], answer: 0 },
            { q: "من هو مكتشف الجاذبية؟", options: ["نيوتن", "أينشتاين", "جاليليو", "أديسون"], answer: 0 },
            { q: "ما هي العملة المستخدمة في أوروبا؟", options: ["اليورو", "الدولار", "الين", "الجنيه"], answer: 0 },
            { q: "كم يبلغ عدد كواكب المجموعة الشمسية؟", options: ["8", "9", "7", "10"], answer: 0 },
            { q: "ما هو أبرد مكان في العالم؟", options: ["القطب الجنوبي", "القطب الشمالي", "سيبيريا", "كندا"], answer: 0 },
            { q: "ما هي عاصمة فرنسا؟", options: ["باريس", "روما", "برلين", "مدريد"], answer: 0 },
            { q: "ما هي أقوى عضلة في جسم الإنسان؟", options: ["القلب", "الفك", "اللسان", "الفخذ"], answer: 1 },
            { q: "ما هو الطائر الذي لا يطير؟", options: ["النعامة", "الببغاء", "الصقر", "العقاب"], answer: 0 },
            { q: "ما اسم الكوكب الأحمر؟", options: ["المريخ", "المشتري", "زحل", "عطارد"], answer: 0 },
            { q: "ما هي أبعد كوكب عن الشمس؟", options: ["نبتون", "زحل", "المشتري", "المريخ"], answer: 0 },
            { q: "من هو مخترع الهاتف؟", options: ["ألكسندر جراهام بيل", "أديسون", "نيوتن", "أينشتاين"], answer: 0 },
            { q: "كم ساعة في اليوم؟", options: ["24", "12", "48", "20"], answer: 0 },
            { q: "ما اسم أكبر دولة في العالم مساحة؟", options: ["روسيا", "الصين", "أمريكا", "كندا"], answer: 0 },
            { q: "ما هي عاصمة إيطاليا؟", options: ["روما", "ميلانو", "فلورنسا", "نابولي"], answer: 0 },
            { q: "ما هو الشيء الذي يحترق ليضيء؟", options: ["الشمعة", "الخشب", "الفحم", "النفط"], answer: 0 }   ],
                hard: [
                    { q: "ما هي عاصمة كندا؟", options: ["تورونتو", "فانكوفر", "مونتريال", "أوتاوا"], answer: 3 },
                    { q: "من هو مخترع الهاتف؟", options: ["ألكسندر جراهام بيل", "نيكولا تسلا", "ألبرت أينشتاين", "ماركوني"], answer: 0 },
                    { q: "ما هو المعدن الوحيد الذي يوجد في حالة سائلة؟", options: ["الحديد", "الذهب", "الزئبق", "الفضة"], answer: 2 },
                    { q: "أين تقع جزر المالديف؟", options: ["المحيط الأطلسي", "المحيط الهادي", "المحيط الهندي", "البحر المتوسط"], answer: 2 },
                    { q: "ما هي أصغر دولة في العالم من حيث المساحة؟", options: ["موناكو", "سان مارينو", "الفاتيكان", "ناورو"], answer: 2 },
                    { q: "ما هي العملة الرسمية لليابان؟", options: ["اليوان", "الوون", "الروبية", "الين"], answer: 3 },
                    { q: "من هو أول إنسان صعد إلى الفضاء؟", options: ["نيل أرمسترونج", "يوري جاجارين", "باز ألدرين", "جون غلين"], answer: 1 },
                    { q: "ما هي عاصمة أستراليا؟", options: ["سيدني", "ملبورن", "كانبرا", "بريزبان"], answer: 2 },
                    { q: "من هو الرسام الذي رسم لوحة الموناليزا؟", options: ["فان جوخ", "بيكاسو", "ليوناردو دافنشي", "مايكل أنجلو"], answer: 2 },
                    { q: "ما هو أخف الغازات في الطبيعة؟", options: ["الأكسجين", "الهيليوم", "الهيدروجين", "النيتروجين"], answer: 2 },
                    { q: "من هو مؤسس شركة مايكروسوفت؟", options: ["ستيف جوبز", "بيل غيتس", "مارك زوكربيرغ", "إيلون ماسك"], answer: 1 },
                    { q: "ماذا يمثل الرمز (O) في الجدول الدوري الكيميائي؟", options: ["الذهب", "الأوزميوم", "الأكسجين", "الفضة"], answer: 2 },
                    { q: "من يعتبر مخترع أول حاسوب ميكانيكي؟", options: ["آلان تورنغ", "تشارلز بابيج", "بيل غيتس", "تيم بيرنرز لي"], answer: 1 },
                    { q: "ما هو أطول نهر في أوروبا؟", options: ["نهر الراين", "نهر الدانوب", "نهر الفولغا", "نهر التايمز"], answer: 2 },
                    { q: "أين تقع جبال الأنديز؟", options: ["أمريكا الشمالية", "أمريكا الجنوبية", "أوروبا", "آسيا"], answer: 1 },
                    { q: "ما هو أكبر كوكب في المجموعة الشمسية؟", options: ["الأرض", "زحل", "المشتري", "أورانوس"], answer: 2 }
            { q: "ما هي الدولة التي تمتلك أكبر عدد من الجزر؟", options: ["السويد", "إندونيسيا", "اليابان", "الفلبين"], answer: 0 },
            { q: "ما اسم أطول سلسلة جبال في العالم؟", options: ["الأنديز", "الهيمالايا", "الألب", "روكي"], answer: 0 },
            { q: "ما هو الغاز الأخف في الكون؟", options: ["الهيدروجين", "الهيليوم", "الأكسجين", "النيتروجين"], answer: 0 },
            { q: "كم عدد فقرات الرقبة عند الإنسان؟", options: ["7", "12", "5", "33"], answer: 0 },
            { q: "من هو الرسام الذي رسم الموناليزا؟", options: ["دافنشي", "بيكاسو", "فان جوخ", "مايكل أنجلو"], answer: 0 },
            { q: "ما هي اللغة الرسمية للبرازيل؟", options: ["البرتغالية", "الإسبانية", "الإنجليزية", "الفرنسية"], answer: 0 },
            { q: "ما هو أصغر طائر في العالم؟", options: ["الطنان", "العصفور", "الكناري", "البلبل"], answer: 0 },
            { q: "ما اسم أكبر صحراء في العالم؟", options: ["الصحراء الكبرى", "أتاكاما", "الربع الخالي", "غوبي"], answer: 0 },
            { q: "ما هي الدولة التي كانت تسمى (فارس) قديماً؟", options: ["إيران", "العراق", "تركيا", "أفغانستان"], answer: 0 },
            { q: "كم عدد عظام جسم الإنسان البالغ؟", options: ["206", "200", "210", "300"], answer: 0 },
            { q: "ما هو العنصر الذي رمزه Au؟", options: ["الذهب", "الفضة", "النحاس", "الحديد"], answer: 0 },
            { q: "ما هو أكبر بحر مغلق في العالم؟", options: ["قزوين", "الميت", "الأسود", "الأحمر"], answer: 0 },
            { q: "في أي دولة يقع معبد أنكور وات؟", options: ["كمبوديا", "تايلاند", "فيتنام", "لاوس"], answer: 0 },
            { q: "ما اسم أصغر دولة في العالم؟", options: ["الفاتيكان", "موناكو", "ناورو", "سان مارينو"], answer: 0 },
            { q: "ما هو أسرع كوكب يدور حول الشمس؟", options: ["عطارد", "الأرض", "المريخ", "المشتري"], answer: 0 },
            { q: "من هو صاحب كتاب (مقدمة ابن خلدون)؟", options: ["ابن خلدون", "المقريزي", "الطبري", "ابن بطوطة"], answer: 0 },
            { q: "ما هي الدولة التي يطلق عليها (بلاد الشمس المشرقة)؟", options: ["اليابان", "الصين", "كوريا", "تايلاند"], answer: 0 },
            { q: "ما هي العاصمة التي تقع في قارتين؟", options: ["إسطنبول", "موسكو", "القاهرة", "بغداد"], answer: 0 },
            { q: "ما هو الحيوان الذي له أطول فترة حمل؟", options: ["الفيل", "الحوت", "الزرافة", "الجمل"], answer: 0 },
            { q: "كم يبلغ طول اليوم في كوكب الزهرة؟", options: ["أطول من سنته", "أقصر من سنته", "يساوي سنته", "ليس له يوم"], answer: 0 }    ]
            }
        };

        // متغيرات النظام
        let playerName = '';
        let currentCategory = '';
        let currentLevel = '';
        let activeQuestions = [];
        let currentQuestionIndex = 0;
        let score = 0;
        let correctAnswers = 0;
        let wrongAnswers = 0;
        let timer;
        let timeLeft = 15;
        const TOTAL_QUESTIONS_PER_QUIZ = 15; // عدد الأسئلة المطلوبة لكل دورة

        // دوال التنقل بين الشاشات
        function switchScreen(screenId) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(screenId).classList.add('active');
        }

        function selectCategory(category) {
            const nameInput = document.getElementById('playerNameInput').value.trim();
            if (!nameInput) {
                alert("يرجى كتابة اسمك أولاً يا بطل!");
                return;
            }
            playerName = nameInput;
            currentCategory = category;
            
            // تغيير النصوص بناءً على القسم
            const headerText = category === 'islamic' ? '🌙 كويز المعلومات الإسلامية' : '🌍 كويز المعلومات العامة';
            document.getElementById('mainHeader').innerText = headerText;
            
            switchScreen('levelScreen');
        }

        function goBackToCategory() {
            document.getElementById('mainHeader').innerText = '🌟 كويز التحدي الشامل';
            switchScreen('categoryScreen');
        }

        // خلط المصفوفة لاختيار أسئلة عشوائية
        function shuffleArray(array) {
            let currentIndex = array.length, randomIndex;
            while (currentIndex !== 0) {
                randomIndex = Math.floor(Math.random() * currentIndex);
                currentIndex--;
                [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
            }
            return array;
        }

        function startQuiz(level) {
            currentLevel = level;
            score = 0;
            correctAnswers = 0;
            wrongAnswers = 0;
            currentQuestionIndex = 0;
            
            // جلب الأسئلة من القسم والمستوى المحددين وخلطها
            let allCategoryLevelQuestions = [...questionBank[currentCategory][currentLevel]];
            allCategoryLevelQuestions = shuffleArray(allCategoryLevelQuestions);
            
            // سحب 15 سؤال عشوائي (إذا كان البنك أقل من 15، يسحب المتوفر)
            activeQuestions = allCategoryLevelQuestions.slice(0, TOTAL_QUESTIONS_PER_QUIZ);

            document.getElementById('liveScore').innerText = `النقاط: ${score}`;
            switchScreen('quizScreen');
            loadQuestion();
        }

        function loadQuestion() {
            clearInterval(timer);
            timeLeft = 15;
            document.getElementById('timerDisplay').innerText = `⏱️ ${timeLeft}ث`;
            document.getElementById('timerDisplay').style.color = '#ef4444';
            
            document.getElementById('nextBtn').style.display = 'none';
            document.getElementById('questionCounter').innerText = `السؤال ${currentQuestionIndex + 1} / ${activeQuestions.length}`;
            
            const qData = activeQuestions[currentQuestionIndex];
            document.getElementById('questionText').innerText = qData.q;
            
            const optionsContainer = document.getElementById('optionsContainer');
            optionsContainer.innerHTML = '';
            
            qData.options.forEach((opt, index) => {
                const btn = document.createElement('button');
                btn.className = 'option-btn';
                btn.innerText = opt;
                btn.onclick = () => checkAnswer(index, btn);
                optionsContainer.appendChild(btn);
            });

            startTimer();
        }

        function startTimer() {
            timer = setInterval(() => {
                timeLeft--;
                document.getElementById('timerDisplay').innerText = `⏱️ ${timeLeft}ث`;
                
                if (timeLeft <= 5) document.getElementById('timerDisplay').style.color = '#fb7185';
                
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    handleTimeOut();
                }
            }, 1000);
        }

        function handleTimeOut() {
            playWrongSound();
            wrongAnswers++;
            disableOptions();
            showCorrectAnswer();
            document.getElementById('nextBtn').style.display = 'block';
        }

        function checkAnswer(selectedIndex, btnElement) {
            clearInterval(timer);
            disableOptions();
            
            const qData = activeQuestions[currentQuestionIndex];
            const isCorrect = selectedIndex === qData.answer;

            if (isCorrect) {
                btnElement.classList.add('correct');
                playCorrectSound();
                score += getPointsForLevel();
                correctAnswers++;
                updateLiveScore();
                triggerConfetti();
            } else {
                btnElement.classList.add('wrong');
                playWrongSound();
                wrongAnswers++;
                showCorrectAnswer();
            }

            document.getElementById('nextBtn').style.display = 'block';
        }

        function getPointsForLevel() {
            if (currentLevel === 'easy') return 10;
            if (currentLevel === 'medium') return 20;
            return 30;
        }

        function updateLiveScore() {
            const scoreEl = document.getElementById('liveScore');
            scoreEl.innerText = `النقاط: ${score}`;
            scoreEl.classList.add('bump');
            setTimeout(() => scoreEl.classList.remove('bump'), 200);
        }

        function disableOptions() {
            const btns = document.querySelectorAll('.option-btn');
            btns.forEach(btn => btn.disabled = true);
        }

        function showCorrectAnswer() {
            const btns = document.querySelectorAll('.option-btn');
            const correctIndex = activeQuestions[currentQuestionIndex].answer;
            btns[correctIndex].classList.add('correct');
        }

        function goToNextQuestion() {
            currentQuestionIndex++;
            if (currentQuestionIndex < activeQuestions.length) {
                loadQuestion();
            } else {
                endQuiz();
            }
        }

        function endQuiz() {
            switchScreen('resultScreen');
            document.getElementById('finalScore').innerText = `${score} نقطة`;
            document.getElementById('correctCount').innerText = correctAnswers;
            document.getElementById('wrongCount').innerText = wrongAnswers;

            // تحديد القسم لتحديث لوحة الشرف الخاصة به
            const lbKey = `leaderboard_${currentCategory}`;
            document.getElementById('leaderboardTitle').innerText = currentCategory === 'islamic' 
                ? '🏆 أبطال الكويز الديني 🏆' 
                : '🏆 أبطال الكويز العام 🏆';

            saveAndDisplayLeaderboard(lbKey);
        }

        function saveAndDisplayLeaderboard(storageKey) {
            let leaderboard = JSON.parse(localStorage.getItem(storageKey)) || [];
            
            // إضافة النتيجة الحالية
            leaderboard.push({ name: playerName, score: score });
            
            // ترتيب وتصفية أول 3 فقط
            leaderboard.sort((a, b) => b.score - a.score);
            leaderboard = leaderboard.slice(0, 3);
            
            localStorage.setItem(storageKey, JSON.stringify(leaderboard));
            
            // عرض اللوحة
            const listContainer = document.getElementById('leaderboardList');
            listContainer.innerHTML = '';
            
            if (leaderboard.length === 0) {
                listContainer.innerHTML = '<div style="text-align:center; color:#94a3b8;">لا توجد نتائج بعد.</div>';
                return;
            }

            leaderboard.forEach((player, index) => {
                const item = document.createElement('div');
                item.className = `leaderboard-item rank-${index + 1}`;
                item.innerHTML = `
                    <span>#${index + 1} ${player.name}</span>
                    <span>${player.score} نقطة</span>
                `;
                listContainer.appendChild(item);
            });
        }

        function resetToHome() {
            document.getElementById('playerNameInput').value = '';
            document.getElementById('mainHeader').innerText = '🌟 كويز التحدي الشامل';
            switchScreen('categoryScreen');
        }
    </script>
</body>
</html>
