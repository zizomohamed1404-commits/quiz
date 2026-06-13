# quiz
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اختبر معلوماتك الإسلامية</title>
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

        .quiz-container {
            background-color: #1e293b;
            width: 90%;
            max-width: 600px;
            border-radius: 16px;
            padding: 30px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            text-align: center;
        }

        .header {
            font-size: 1.8rem;
            color: #10b981;
            margin-bottom: 20px;
            font-weight: bold;
            border-bottom: 2px solid #334155;
            padding-bottom: 15px;
        }

        .question-number {
            font-size: 1rem;
            color: #94a3b8;
            margin-bottom: 10px;
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

        .option-btn:hover {
            background-color: #475569;
            border-color: #10b981;
        }

        .option-btn.correct {
            background-color: #059669;
            border-color: #059669;
            color: white;
        }

        .option-btn.wrong {
            background-color: #e11d48;
            border-color: #e11d48;
            color: white;
        }

        .option-btn:disabled {
            cursor: not-allowed;
            opacity: 0.8;
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
        }

        .next-btn:hover {
            background-color: #059669;
        }

        .result-container {
            display: none;
        }

        .score-text {
            font-size: 2rem;
            color: #10b981;
            margin: 20px 0;
            font-weight: bold;
        }

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
        }

        .restart-btn:hover {
            background-color: #2563eb;
        }
    </style>
</head>
<body>

    <div class="quiz-container">
        <div class="header">🌙 كويز المعلومات الإسلامية</div>
        
        <div id="quizSection">
            <div class="question-number" id="questionNumber">السؤال 1 من 20</div>
            <div class="question-text" id="questionText">جاري تحميل السؤال...</div>
            <div class="options-container" id="optionsContainer">
                </div>
            <button class="next-btn" id="nextBtn" onclick="nextQuestion()">السؤال التالي</button>
        </div>

        <div class="result-container" id="resultSection">
            <h2>انتهى الاختبار! 🎉</h2>
            <div class="score-text" id="scoreText">نتيجتك: 0 / 20</div>
            <button class="restart-btn" onclick="restartQuiz()">إعادة الاختبار</button>
        </div>
    </div>

    <script>
        const questions = [
            { q: "من هو آخر الأنبياء والرسل؟", options: ["عيسى عليه السلام", "موسى عليه السلام", "محمد صلى الله عليه وسلم", "إبراهيم عليه السلام"], answer: 2 },
            { q: "كم عدد سور القرآن الكريم؟", options: ["110 سورة", "114 سورة", "120 سورة", "99 سورة"], answer: 1 },
            { q: "ما هي أطول سورة في القرآن الكريم؟", options: ["سورة البقرة", "سورة آل عمران", "سورة النساء", "سورة الأعراف"], answer: 0 },
            { q: "في أي شهر نزل القرآن الكريم؟", options: ["رجب", "شعبان", "رمضان", "محرم"], answer: 2 },
            { q: "من هو الصحابي الملقب بـ (أول الخلفاء الراشدين)؟", options: ["عمر بن الخطاب", "علي بن أبي طالب", "عثمان بن عفان", "أبو بكر الصديق"], answer: 3 },
            { q: "ما هي أقصر سورة في القرآن الكريم؟", options: ["سورة الإخلاص", "سورة الكوثر", "سورة العصر", "سورة الناس"], answer: 1 },
            { q: "كم عدد أركان الإسلام؟", options: ["4", "5", "6", "7"], answer: 1 },
            { q: "ما هو الكتاب السماوي الذي أُنزل على سيدنا عيسى عليه السلام؟", options: ["التوراة", "الزبور", "القرآن", "الإنجيل"], answer: 3 },
            { q: "ما هي السورة التي تُسمى (قلب القرآن)؟", options: ["سورة يس", "سورة الرحمن", "سورة تبارك", "سورة الكهف"], answer: 0 },
            { q: "من هو الصحابي الجليل الملقب بـ (سيف الله المسلول)؟", options: ["حمزة بن عبد المطلب", "خالد بن الوليد", "سعد بن معاذ", "أبو عبيدة بن الجراح"], answer: 1 },
            { q: "كم عدد أركان الإيمان؟", options: ["5", "6", "7", "8"], answer: 1 },
            { q: "ما هي الغزوة التي سُميت بـ (يوم الفرقان)؟", options: ["غزوة أحد", "غزوة الخندق", "غزوة بدر", "غزوة تبوك"], answer: 2 },
            { q: "من هو أول مؤذن في الإسلام؟", options: ["بلال بن رباح", "عمار بن ياسر", "صهيب الرومي", "سلمان الفارسي"], answer: 0 },
            { q: "ما هي القبلة الأولى للمسلمين قبل الكعبة؟", options: ["المسجد النبوي", "المسجد الأموي", "المسجد الأقصى", "مسجد قباء"], answer: 2 },
            { q: "ما هي السورة الوحيدة التي لا تبدأ بـ (بسم الله الرحمن الرحيم)؟", options: ["سورة الأنفال", "سورة التوبة", "سورة النحل", "سورة الرعد"], answer: 1 },
            { q: "من هي أولى زوجات النبي محمد صلى الله عليه وسلم؟", options: ["عائشة بنت أبي بكر", "حفصة بنت عمر", "خديجة بنت خويلد", "زينب بنت جحش"], answer: 2 },
            { q: "كم سنة استمر نزول الوحي بالقرآن الكريم؟", options: ["10 سنوات", "20 سنة", "23 سنة", "30 سنة"], answer: 2 },
            { q: "ما هو الجبل الذي رست عليه سفينة نبي الله نوح؟", options: ["جبل الطور", "جبل أحد", "جبل الجودي", "جبل عرفات"], answer: 2 },
            { q: "ما هي الصلاة التي ليس فيها ركوع ولا سجود؟", options: ["صلاة العيد", "صلاة الاستسقاء", "صلاة الجنازة", "صلاة الضحى"], answer: 2 },
            { q: "من هو الصحابي الذي تستحي منه ملائكة الرحمن؟", options: ["عثمان بن عفان", "عمر بن الخطاب", "علي بن أبي طالب", "الزبير بن العوام"], answer: 0 }
        ];

        let currentQuestionIndex = 0;
        let score = 0;

        const questionNumberEl = document.getElementById('questionNumber');
        const questionTextEl = document.getElementById('questionText');
        const optionsContainer = document.getElementById('optionsContainer');
        const nextBtn = document.getElementById('nextBtn');
        const quizSection = document.getElementById('quizSection');
        const resultSection = document.getElementById('resultSection');
        const scoreText = document.getElementById('scoreText');

        function loadQuestion() {
            nextBtn.style.display = 'none';
            optionsContainer.innerHTML = '';
            
            const currentQ = questions[currentQuestionIndex];
            questionNumberEl.innerText = `السؤال ${currentQuestionIndex + 1} من ${questions.length}`;
            questionTextEl.innerText = currentQ.q;

            currentQ.options.forEach((option, index) => {
                const btn = document.createElement('button');
                btn.classList.add('option-btn');
                btn.innerText = option;
                btn.onclick = () => checkAnswer(index, btn);
                optionsContainer.appendChild(btn);
            });
        }

        function checkAnswer(selectedIndex, selectedBtn) {
            const currentQ = questions[currentQuestionIndex];
            const allBtns = optionsContainer.children;

            // تعطيل كل الأزرار بعد الاختيار
            for(let i = 0; i < allBtns.length; i++) {
                allBtns[i].disabled = true;
                if (i === currentQ.answer) {
                    allBtns[i].classList.add('correct');
                }
            }

            if (selectedIndex === currentQ.answer) {
                score++;
            } else {
                selectedBtn.classList.add('wrong');
            }

            nextBtn.style.display = 'inline-block';
        }

        function nextQuestion() {
            currentQuestionIndex++;
            if (currentQuestionIndex < questions.length) {
                loadQuestion();
            } else {
                showResult();
            }
        }

        function showResult() {
            quizSection.style.display = 'none';
            resultSection.style.display = 'block';
            
            let message = "";
            if(score >= 18) message = "ما شاء الله! ممتاز جداً 🌟";
            else if(score >= 10) message = "جيد جداً! معلوماتك حلوة 👍";
            else message = "محتاج تراجع معلوماتك شوية، بالتوفيق المرة الجاية 💪";

            scoreText.innerHTML = `نتيجتك: ${score} / ${questions.length} <br> <span style="font-size:1.2rem; color:#94a3b8; display:block; margin-top:15px;">${message}</span>`;
        }

        function restartQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            quizSection.style.display = 'block';
            resultSection.style.display = 'none';
            loadQuestion();
        }

        // تشغيل الكويز أول ما الصفحة تفتح
        loadQuestion();
    </script>
</body>
</html>
