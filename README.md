Weaa Academy/
Creator Zidane Mohamed
 <html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>كويز المعلومات الشامل</title>
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

        /* شاشات الاختيار */
        #categoryScreen, #levelScreen, #quizScreen, #resultScreen {
            display: none;
            flex-direction: column;
            gap: 15px;
            margin-top: 20px;
        }

        #categoryScreen { display: flex; } /* الشاشة الافتراضية */

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

        .title-text {
            font-size: 1.3rem;
            margin-bottom: 10px;
            color: #e2e8f0;
        }

        .btn {
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

        /* أزرار الأقسام */
        .cat-btn.islamic { background-color: #059669; }
        .cat-btn.islamic:hover { background-color: #047857; }
        .cat-btn.general { background-color: #2563eb; }
        .cat-btn.general:hover { background-color: #1d4ed8; }

        /* أزرار المستويات */
        .level-btn { background-color: #334155; }
        .level-btn.easy:hover { background-color: #059669; border-color: #10b981; }
        .level-btn.medium:hover { background-color: #d97706; border-color: #f59e0b; }
        .level-btn.hard:hover { background-color: #e11d48; border-color: #fb7185; }

        /* شاشة الكويز */
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
            font-size: 1.2rem; color: #ef4444; font-weight: bold;
            background-color: #334155; padding: 5px 15px; border-radius: 20px;
        }
        .live-score {
            font-size: 1.2rem; color: #f59e0b; font-weight: bold;
            background-color: #334155; padding: 5px 15px; border-radius: 20px;
        }

        .question-text { font-size: 1.4rem; margin-bottom: 25px; line-height: 1.5; }

        .options-container { display: flex; flex-direction: column; gap: 12px; }
        .option-btn {
            background-color: #334155; color: #f8fafc; border: 2px solid #334155;
            padding: 15px; font-size: 1.1rem; border-radius: 10px; cursor: pointer; transition: all 0.3s;
        }
        .option-btn:hover:not(:disabled) { background-color: #475569; }
        .option-btn.correct { background-color: #059669 !important; border-color: #059669 !important; color: white; }
        .option-btn.wrong { background-color: #e11d48 !important; border-color: #e11d48 !important; color: white; }
        .option-btn:disabled { cursor: not-allowed; opacity: 0.6; }

        .next-btn {
            background-color: #10b981; color: white; border: none; padding: 12px 30px;
            font-size: 1.1rem; border-radius: 8px; cursor: pointer; margin-top: 25px;
            display: none; font-weight: bold; width: 100%;
        }
        .next-btn:hover { background-color: #059669; }

        /* شاشة النتيجة */
        .final-score { font-size: 2.2rem; color: #10b981; margin: 15px 0; font-weight: bold; }
        .stats-box {
            background-color: #0f172a; padding: 15px; border-radius: 10px;
            margin-bottom: 20px; display: flex; justify-content: space-around; border: 1px solid #334155;
        }
        .stat-item { display: flex; flex-direction: column; gap: 5px; }
        .stat-value { font-size: 1.5rem; font-weight: bold; }
        .stat-label { color: #94a3b8; font-size: 0.9rem; }

        /* لوحة الشرف Leaderboard */
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
            padding: 12px; margin-bottom: 10px; border-radius: 8px; background-color: #1e293b; font-weight: bold;
        }
        .rank-1 { background-color: rgba(255, 215, 0, 0.1); border: 1px solid #ffd700; color: #ffd700; }
        .rank-2 { background-color: rgba(192, 192, 192, 0.1); border: 1px solid #c0c0c0; color: #c0c0c0; }
        .rank-3 { background-color: rgba(205, 127, 50, 0.1); border: 1px solid #cd7f32; color: #cd7f32; }

        .restart-btn {
            background-color: #3b82f6; color: white; border: none; padding: 15px 40px;
            font-size: 1.2rem; border-radius: 8px; cursor: pointer; font-weight: bold; margin-top: 20px; width: 100%;
        }
        .restart-btn:hover { background-color: #2563eb; }
    </style>
</head>
<body>

    <div class="main-container">
        <div class="header" id="mainHeader">🧠 كويز التحدي الشامل</div>
        
        <!-- شاشة اختيار القسم -->
        <div id="categoryScreen">
            <input type="text" id="playerNameInput" class="name-input" placeholder="اكتب اسمك هنا يا بطل..." autocomplete="off">
            <div class="title-text">اختر نوع التحدي:</div>
            <button class="btn cat-btn islamic" onclick="selectCategory('islamic')">🌙 أسئلة دينية</button>
            <button class="btn cat-btn general" onclick="selectCategory('general')">🌍 أسئلة عامة</button>
        </div>

        <!-- شاشة اختيار المستوى -->
        <div id="levelScreen">
            <div class="title-text" id="levelTitleText">اختر مستوى الصعوبة:</div>
            <button class="btn level-btn easy" onclick="startQuiz('easy')">🟢 مستوى سهل</button>
            <button class="btn level-btn medium" onclick="startQuiz('medium')">🟠 مستوى متوسط</button>
            <button class="btn level-btn hard" onclick="startQuiz('hard')">🔴 مستوى صعب</button>
            <button class="btn" style="background-color: #64748b; margin-top: 10px;" onclick="goBackToCategory()">🔙 رجوع</button>
        </div>

        <!-- شاشة الكويز -->
        <div id="quizScreen">
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
        <div id="resultScreen">
            <h2>انتهى الاختبار! 🎉</h2>
            <div class="final-score" id="finalScore">0 نقطة</div>
            <div class="stats-box">
                <div class="stat-item">
                    <span class="stat-value" id="correctCount" style="color: #10b981;">0</span>
                    <span class="stat-label">صحيحة</span>
                </div>
                <div class="stat-item">
                    <span class="stat-value" id="wrongCount" style="color: #ef4444;">0</span>
                    <span class="stat-label">خاطئة</span>
                </div>
            </div>
            
            <div class="leaderboard-container">
                <div class="leaderboard-title" id="leaderboardTitle">🏆 أبطال الكويز 🏆</div>
                <div id="leaderboardList"></div>
            </div>
            <button class="restart-btn" onclick="resetToHome()">العودة للقائمة الرئيسية</button>
        </div>
    </div>

    <script>
        // المتغيرات الأساسية
        let playerName = "";
        let selectedCategory = "";
        let selectedLevel = "";
        let currentQuestions = [];
        let currentQuestionIndex = 0;
        let score = 0;
        let correctAnswers = 0;
        let wrongAnswers = 0;
        let timerInterval;
        let timeLeft = 15;
        const QUESTIONS_PER_QUIZ = 15; // عدد الأسئلة المطلوبة في كل تحدي

        // ==========================================
        // بنك الأسئلة (يمكنك إضافة الـ 200 سؤال هنا)
        // ==========================================
        const questionBank = {
            islamic: {
                easy: [
                    { q: "من هو آخر الأنبياء والرسل؟", options: ["عيسى", "موسى", "محمد", "إبراهيم"], answer: 2 },
                    { q: "ما هو أول شهر في التقويم الهجري؟", options: ["رمضان", "محرم", "شوال", "رجب"], answer: 1 },
                    { q: "كم عدد الصلوات المفروضة؟", options: ["3", "4", "5", "6"], answer: 2 },
                    { q: "أين توجد الكعبة المشرفة؟", options: ["المدينة", "مكة", "القدس", "الطائف"], answer: 1 },
                    { q: "ما هي أقصر سورة في القرآن؟", options: ["الإخلاص", "الفلق", "الناس", "الكوثر"], answer: 3 },
                    // أضف باقي الـ 200 سؤال للمستوى السهل الديني هنا بنفس الصيغة
                ],
                medium: [
                    { q: "ما هي السورة التي تُسمى (قلب القرآن)؟", options: ["يس", "الرحمن", "تبارك", "الكهف"], answer: 0 },
                    { q: "من هو أول مؤذن في الإسلام؟", options: ["بلال بن رباح", "عمار بن ياسر", "صهيب الرومي", "سلمان"], answer: 0 },
                    { q: "كم سنة استمر نزول الوحي؟", options: ["10", "20", "23", "30"], answer: 2 },
                    // أضف باقي الـ 200 سؤال للمستوى المتوسط الديني هنا
                ],
                hard: [
                    { q: "ما هي السورة التي وردت فيها البسملة مرتين؟", options: ["النمل", "القصص", "النحل", "هود"], answer: 0 },
                    { q: "من هي أول شهيدة في الإسلام؟", options: ["خديجة", "فاطمة", "سمية بنت خياط", "أسماء"], answer: 2 },
                    { q: "ما اسم باب الجنة المخصص للصائمين؟", options: ["التوبة", "الريان", "الصلاة", "الجهاد"], answer: 1 },
                    // أضف باقي الـ 200 سؤال للمستوى الصعب الديني هنا
                ]
            },
            general: {
                easy: [
                    { q: "كم عدد قارات العالم؟", options: ["5", "6", "7", "8"], answer: 2 },
                    { q: "ما هو أسرع حيوان بري؟", options: ["الأسد", "الفهد", "الحصان", "النمر"], answer: 1 },
                    { q: "ما هو الكوكب الملقب بالكوكب الأحمر؟", options: ["الزهرة", "المشترى", "المريخ", "عطارد"], answer: 2 },
                    { q: "ما هي عاصمة مصر؟", options: ["الإسكندرية", "القاهرة", "الأقصر", "أسوان"], answer: 1 },
                    { q: "كم عدد أيام الأسبوع؟", options: ["5", "6", "7", "8"], answer: 2 },
                    // أضف باقي الـ 200 سؤال للمستوى السهل العام هنا
                ],
                medium: [
                    { q: "ما هي أكبر دولة في العالم من حيث المساحة؟", options: ["الصين", "أمريكا", "كندا", "روسيا"], answer: 3 },
                    { q: "من هو مخترع المصباح الكهربائي؟", options: ["نيوتن", "أينشتاين", "توماس إديسون", "جاليليو"], answer: 2 },
                    { q: "في أي قارة تقع دولة البرازيل؟", options: ["أفريقيا", "أمريكا الشمالية", "أمريكا الجنوبية", "أوروبا"], answer: 2 },
                    // أضف باقي الـ 200 سؤال للمستوى المتوسط العام هنا
                ],
                hard: [
                    { q: "ما هو العنصر الكيميائي الذي رمزه O؟", options: ["الذهب", "الأكسجين", "الفضة", "الحديد"], answer: 1 },
                    { q: "متى بدأت الحرب العالمية الثانية؟", options: ["1914", "1939", "1945", "1920"], answer: 1 },
                    { q: "من رسم لوحة الموناليزا؟", options: ["فان جوخ", "بيكاسو", "ليوناردو دا فينشي", "مايكل أنجلو"], answer: 2 },
                    // أضف باقي الـ 200 سؤال للمستوى الصعب العام هنا
                ]
            }
        };

        // التأثيرات الصوتية والاحتفال
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

        function triggerConfetti() {
            confetti({ particleCount: 100, spread: 70, origin: { y: 0.6 } });
        }

        // التحكم في الشاشات
        function selectCategory(category) {
            const nameInput = document.getElementById('playerNameInput').value.trim();
            if (!nameInput) {
                alert("رجاءً أدخل اسمك أولاً يا بطل!");
                return;
            }
            playerName = nameInput;
            selectedCategory = category;
            
            document.getElementById('categoryScreen').style.display = 'none';
            document.getElementById('levelScreen').style.display = 'flex';
            
            let catName = category === 'islamic' ? 'القسم الديني 🌙' : 'القسم العام 🌍';
            document.getElementById('levelTitleText').innerText = `اختر مستوى الصعوبة لـ (${catName}):`;
        }

        function goBackToCategory() {
            document.getElementById('levelScreen').style.display = 'none';
            document.getElementById('categoryScreen').style.display = 'flex';
        }

        function startQuiz(level) {
            selectedLevel = level;
            score = 0;
            correctAnswers = 0;
            wrongAnswers = 0;
            currentQuestionIndex = 0;
            
            // سحب الأسئلة وعمل خلط (عشوائي) واختيار 15 سؤال فقط
            let pool = questionBank[selectedCategory][selectedLevel];
            
            // خوارزمية ترتيب عشوائي للمصفوفة (Fisher-Yates Shuffle)
            let shuffledPool = [...pool].sort(() => 0.5 - Math.random());
            
            // أخذ 15 سؤال (أو أقل إذا كان البنك لا يحتوي على 15)
            currentQuestions = shuffledPool.slice(0, QUESTIONS_PER_QUIZ);

            document.getElementById('levelScreen').style.display = 'none';
            document.getElementById('quizScreen').style.display = 'block';
            
            updateLiveScore();
            loadQuestion();
        }

        function loadQuestion() {
            clearInterval(timerInterval);
            timeLeft = 15;
            document.getElementById('timerDisplay').innerText = `⏱️ ${timeLeft}ث`;
            document.getElementById('nextBtn').style.display = 'none';
            
            const qData = currentQuestions[currentQuestionIndex];
            document.getElementById('questionCounter').innerText = `السؤال ${currentQuestionIndex + 1} / ${currentQuestions.length}`;
            document.getElementById('questionText').innerText = qData.q;
            
            const optionsDiv = document.getElementById('optionsContainer');
            optionsDiv.innerHTML = '';
            
            qData.options.forEach((opt, index) => {
                const btn = document.createElement('button');
                btn.className = 'option-btn';
                btn.innerText = opt;
                btn.onclick = () => checkAnswer(index, btn);
                optionsDiv.appendChild(btn);
            });

            startTimer();
        }

        function startTimer() {
            timerInterval = setInterval(() => {
                timeLeft--;
                document.getElementById('timerDisplay').innerText = `⏱️ ${timeLeft}ث`;
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    autoFailQuestion();
                }
            }, 1000);
        }

        function autoFailQuestion() {
            const buttons = document.querySelectorAll('.option-btn');
            buttons.forEach(btn => btn.disabled = true);
            const correctIndex = currentQuestions[currentQuestionIndex].answer;
            buttons[correctIndex].classList.add('correct');
            wrongAnswers++;
            playTone(250, 'sawtooth', 0.3, 0.05); // صوت خطأ
            document.getElementById('nextBtn').style.display = 'block';
        }

        function checkAnswer(selectedIndex, btnElement) {
            clearInterval(timerInterval);
            const buttons = document.querySelectorAll('.option-btn');
            buttons.forEach(btn => btn.disabled = true);

            const correctIndex = currentQuestions[currentQuestionIndex].answer;

            if (selectedIndex === correctIndex) {
                btnElement.classList.add('correct');
                score += 10 + timeLeft; // نقاط إضافية للسرعة
                correctAnswers++;
                playTone(600, 'sine', 0.1, 0.1); // صوت صحيح
                updateLiveScore();
            } else {
                btnElement.classList.add('wrong');
                buttons[correctIndex].classList.add('correct');
                wrongAnswers++;
                playTone(250, 'sawtooth', 0.3, 0.05); // صوت خطأ
            }

            document.getElementById('nextBtn').style.display = 'block';
        }

        function updateLiveScore() {
            const scoreEl = document.getElementById('liveScore');
            scoreEl.innerText = `النقاط: ${score}`;
            scoreEl.classList.add('bump');
            setTimeout(() => scoreEl.classList.remove('bump'), 200);
        }

        function goToNextQuestion() {
            currentQuestionIndex++;
            if (currentQuestionIndex < currentQuestions.length) {
                loadQuestion();
            } else {
                endQuiz();
            }
        }

        function endQuiz() {
            document.getElementById('quizScreen').style.display = 'none';
            document.getElementById('resultScreen').style.display = 'block';
            
            document.getElementById('finalScore').innerText = `${score} نقطة`;
            document.getElementById('correctCount').innerText = correctAnswers;
            document.getElementById('wrongCount').innerText = wrongAnswers;
            
            if (correctAnswers > currentQuestions.length / 2) triggerConfetti();

            saveAndDisplayLeaderboard();
        }

        // نظام حفظ المتصدرين (لوحة شرف منفصلة لكل قسم)
        function saveAndDisplayLeaderboard() {
            // استخدام مفتاح تخزين مختلف بناءً على القسم المختار
            const storageKey = selectedCategory === 'islamic' ? 'leaderboard_islamic' : 'leaderboard_general';
            
            let leaderboard = JSON.parse(localStorage.getItem(storageKey)) || [];
            
            // إضافة النتيجة الحالية
            leaderboard.push({ name: playerName, score: score, level: selectedLevel });
            
            // ترتيب تنازلي بناءً على النقاط
            leaderboard.sort((a, b) => b.score - a.score);
            
            // الاحتفاظ بأفضل 3 فقط
            leaderboard = leaderboard.slice(0, 3);
            localStorage.setItem(storageKey, JSON.stringify(leaderboard));

            // تحديث العنوان بناءً على القسم
            let catName = selectedCategory === 'islamic' ? 'الديني' : 'العام';
            document.getElementById('leaderboardTitle').innerText = `🏆 أبطال القسم ${catName} 🏆`;

            // عرض اللوحة
            const listDiv = document.getElementById('leaderboardList');
            listDiv.innerHTML = '';
            
            leaderboard.forEach((player, index) => {
                const item = document.createElement('div');
                item.className = `leaderboard-item rank-${index + 1}`;
                
                let medal = index === 0 ? '🥇' : index === 1 ? '🥈' : '🥉';
                let lvlAr = player.level === 'easy' ? 'سهل' : player.level === 'medium' ? 'متوسط' : 'صعب';
                
                item.innerHTML = `
                    <span>${medal} ${player.name} <small>(${lvlAr})</small></span>
                    <span>${player.score} نقطة</span>
                `;
                listDiv.appendChild(item);
            });
        }

        function resetToHome() {
            document.getElementById('resultScreen').style.display = 'none';
            document.getElementById('categoryScreen').style.display = 'flex';
        }
    </script>
</body>
</html>
