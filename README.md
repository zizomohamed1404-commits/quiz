
Weaa Academi
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>كويز المعلومات الإسلامية</title>
    <style>
        body {<img src="logo.png" alt="Islamic Banner" style="width: 100%; height: 250px; object-fit: cover; display: block; margin-bottom: 30px; border-bottom: 4px solid #10b981;">
        }

        .main-container {
            background-color: #1e293b;
            width: 90%;
            max-width: 650px;
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

        /* شاشة اختيار المستوى */
        #levelScreen {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 20px;
        }

        .level-title {
            font-size: 1.3rem;
            margin-bottom: 15px;
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
        }

        .question-counter {
            font-size: 1.1rem;
            color: #94a3b8;
            font-weight: bold;
        }

        .live-score {
            font-size: 1.2rem;
            color: #f59e0b;
            font-weight: bold;
            background-color: #334155;
            padding: 5px 15px;
            border-radius: 20px;
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

        .next-btn:hover { background-color: #059669; }

        /* شاشة النتيجة */
        #resultScreen {
            display: none;
        }

        .final-score {
            font-size: 2.5rem;
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
            margin-top: 15px;
        }

        .restart-btn:hover { background-color: #2563eb; }

        /* الكود الجديد اللي تم إضافته عشان اسمك */
        .credits {
            position: fixed;
            bottom: 15px;
            left: 15px;
            color: #94a3b8;
            font-size: 0.85rem;
            direction: ltr;
            background-color: rgba(30, 41, 59, 0.8);
            padding: 5px 10px;
            border-radius: 8px;
            z-index: 1000;
            border: 1px solid #334155;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

    </style>
</head>
<body>

    <div class="main-container">
        <div class="header">🌙 كويز المعلومات الإسلامية</div>
        
        <div id="levelScreen">
            <div class="level-title">اختر مستوى الصعوبة لبدء التحدي:</div>
            <button class="level-btn easy" onclick="startQuiz('easy')">🟢 مستوى سهل</button>
            <button class="level-btn medium" onclick="startQuiz('medium')">🟠 مستوى متوسط</button>
            <button class="level-btn hard" onclick="startQuiz('hard')">🔴 مستوى صعب</button>
        </div>

        <div id="quizScreen">
            <div class="quiz-info-bar">
                <div class="question-counter" id="questionCounter">السؤال 1 / 20</div>
                <div class="live-score" id="liveScore">النقاط: 0</div>
            </div>
            
            <div class="question-text" id="questionText">جاري التحميل...</div>
            
            <div class="options-container" id="optionsContainer"></div>
            
            <button class="next-btn" id="nextBtn" onclick="goToNextQuestion()">السؤال التالي</button>
        </div>

        <div id="resultScreen">
            <h2>انتهى الاختبار! 🎉</h2>
            <div class="final-score" id="finalScore">0 / 20</div>
            <div id="feedbackText" style="font-size: 1.2rem; color: #94a3b8; margin-bottom: 20px;"></div>
            <button class="restart-btn" onclick="resetToHome()">العودة للقائمة الرئيسية</button>
        </div>
    </div>

    <script>
        // بنك الأسئلة مقسم لـ 3 مستويات
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
                { q: "من هي أول امرأة أسلمت؟", options: ["عائشة بنت أبي بكر", "أسماء بنت أبي بكر", "خديجة بنت خويلد", "سمية بنت خياط"], answer: 2 }
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
                { q: "ما هي السورة التي سميت باسم امرأة؟", options: ["سورة النساء", "سورة خديجة", "سورة مريم", "سورة فاطمة"], answer: 2 }
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
                { q: "ما هو الجبل الذي رست عليه سفينة نوح؟", options: ["جبل الطور", "جبل الجودي", "جبل أحد", "جبل الصفا"], answer: 1 }
            ]
        };

        let currentQuestionsList = [];
        let currentIndex = 0;
        let userScore = 0;

        // عناصر الـ HTML اللي هنتعامل معاها
        const screenLevel = document.getElementById('levelScreen');
        const screenQuiz = document.getElementById('quizScreen');
        const screenResult = document.getElementById('resultScreen');
        
        const labelCounter = document.getElementById('questionCounter');
        const labelScore = document.getElementById('liveScore');
        const labelQuestion = document.getElementById('questionText');
        const boxOptions = document.getElementById('optionsContainer');
        const btnNext = document.getElementById('nextBtn');
        
        const labelFinalScore = document.getElementById('finalScore');
        const labelFeedback = document.getElementById('feedbackText');

        // دالة بداية الكويز وتحديد المستوى
        function startQuiz(difficulty) {
            currentQuestionsList = questionBank[difficulty];
            currentIndex = 0;
            userScore = 0;
            
            screenLevel.style.display = 'none';
            screenQuiz.style.display = 'block';
            
            displayQuestion();
            updateLiveScore();
        }

        // دالة عرض السؤال الحالي
        function displayQuestion() {
            btnNext.style.display = 'none';
            boxOptions.innerHTML = '';
            
            const qData = currentQuestionsList[currentIndex];
            labelCounter.innerText = `السؤال ${currentIndex + 1} / ${currentQuestionsList.length}`;
            labelQuestion.innerText = qData.q;

            qData.options.forEach((choiceText, i) => {
                const btnChoice = document.createElement('button');
                btnChoice.classList.add('option-btn');
                btnChoice.innerText = choiceText;
                btnChoice.onclick = () => verifyAnswer(i, btnChoice);
                boxOptions.appendChild(btnChoice);
            });
        }

        // دالة التأكد من الإجابة
        function verifyAnswer(selectedIndex, clickedBtn) {
            const qData = currentQuestionsList[currentIndex];
            const allChoiceBtns = boxOptions.children;

            // إيقاف كل الأزرار عشان ميخترش مرتين
            for(let j = 0; j < allChoiceBtns.length; j++) {
                allChoiceBtns[j].disabled = true;
                if (j === qData.answer) {
                    allChoiceBtns[j].classList.add('correct'); // تلوين الإجابة الصح بالأخضر دائماً
                }
            }

            // لو الإجابة صح زود العداد
            if (selectedIndex === qData.answer) {
                userScore++;
                updateLiveScore();
            } else {
                clickedBtn.classList.add('wrong'); // تلوين إجابته الغلط بالأحمر
            }

            btnNext.style.display = 'inline-block'; // إظهار زر السؤال التالي
        }

        // تحديث عداد النقاط اللايف
        function updateLiveScore() {
            labelScore.innerText = `النقاط: ${userScore}`;
        }

        // الانتقال للسؤال اللي بعده
        function goToNextQuestion() {
            currentIndex++;
            if (currentIndex < currentQuestionsList.length) {
                displayQuestion();
            } else {
                finishQuiz();
            }
        }

        // إنهاء الكويز وإظهار النتيجة
        function finishQuiz() {
            screenQuiz.style.display = 'none';
            screenResult.style.display = 'block';
            
            labelFinalScore.innerText = `${userScore} / ${currentQuestionsList.length}`;
            
            if(userScore >= 18) {
                labelFeedback.innerText = "عاش جداً! معلوماتك ممتازة 🌟";
            } else if(userScore >= 10) {
                labelFeedback.innerText = "أداؤك جيد، بس تقدر تجيب أحسن من كده 👍";
            } else {
                labelFeedback.innerText = "محتاج تراجع معلوماتك أكتر يا بطل، حاول تاني 💪";
            }
        }

        // العودة للشاشة الرئيسية
        function resetToHome() {
            screenResult.style.display = 'none';
            screenLevel.style.display = 'flex';
        }

    </script>
    
    <div class="credits">created and Prepared by zidane</div>

</body>
</html>
