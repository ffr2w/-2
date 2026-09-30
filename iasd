<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مولّد أسئلة الاختيار من متعدد</title>
    <style>
        body {
            font-family: 'Tahoma', sans-serif;
            background-color: #0f172a;
            color: #f8fafc;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }
        .container {
            background-color: #1e293b;
            padding: 30px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
            width: 100%;
            max-width: 650px;
            text-align: center;
        }
        h2 {
            margin-bottom: 20px;
            color: #38bdf8;
        }
        textarea {
            width: 100%;
            height: 140px;
            background-color: #0f172a;
            color: #fff;
            border: 1px solid #475569;
            border-radius: 8px;
            padding: 12px;
            font-size: 16px;
            resize: none;
            box-sizing: border-box;
            margin-bottom: 15px;
        }
        textarea:focus {
            outline: none;
            border-color: #38bdf8;
        }
        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }
        .buttons-group {
            display: flex;
            gap: 8px;
        }
        .num-btn {
            background-color: #334155;
            color: #fff;
            border: none;
            width: 35px;
            height: 35px;
            border-radius: 50%;
            cursor: pointer;
            font-weight: bold;
            transition: 0.2s;
        }
        .num-btn.active, .num-btn:hover {
            background-color: #38bdf8;
            color: #0f172a;
        }
        .action-btn {
            background-color: #38bdf8;
            color: #0f172a;
            border: none;
            padding: 12px 20px;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            font-size: 16px;
            transition: 0.2s;
            width: 100%;
        }
        .action-btn:hover {
            background-color: #0ea5e9;
        }
        .secondary-btns {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        .sec-btn {
            background-color: #334155;
            color: #cbd5e1;
            border: none;
            padding: 8px 15px;
            border-radius: 6px;
            cursor: pointer;
            flex: 1;
        }
        .sec-btn:hover {
            background-color: #475569;
        }
        #quizOutput {
            margin-top: 20px;
            text-align: right;
            background: #0f172a;
            padding: 15px;
            border-radius: 8px;
            max-height: 450px;
            overflow-y: auto;
        }
        .question-box {
            background: #1e293b;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
            border: 1px solid #334155;
        }
        .options-list {
            list-style: none;
            padding: 0;
            margin: 10px 0 0 0;
        }
        .options-list li {
            background: #334155;
            padding: 10px 12px;
            margin-bottom: 6px;
            border-radius: 6px;
            cursor: pointer;
            transition: 0.2s;
            font-size: 15px;
        }
        .options-list li:hover {
            background: #475569;
        }
        .options-list li.correct {
            background: #16a34a !important;
            color: #fff;
        }
        .options-list li.wrong {
            background: #dc2626 !important;
            color: #fff;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>مولّد أسئلة الاختيار من متعدد</h2>
    <textarea id="userText" placeholder="الصق نصاً من كتابك أو ملخصك هنا..."></textarea>
    
    <div class="controls">
        <span>عدد الأسئلة: <span id="countDisplay">5</span></span>
        <div class="buttons-group">
            <button class="num-btn active" onclick="changeLimit(5, this)">5</button>
            <button class="num-btn" onclick="changeLimit(10, this)">10</button>
            <button class="num-btn" onclick="changeLimit(15, this)">15</button>
            <button class="num-btn" onclick="changeLimit(20, this)">20</button>
            <button class="num-btn" onclick="changeLimit(30, this)">30</button>
        </div>
    </div>

    <button class="action-btn" onclick="makeQuiz()">اصنع الأسئلة الآن</button>

    <div class="secondary-btns">
        <button class="sec-btn" onclick="insertSample()">ضع نصاً تجريبياً</button>
        <button class="sec-btn" onclick="resetAll()">امسح الكل</button>
    </div>

    <div id="quizOutput"></div>
</div>

<script>
    let limitCount = 5;

    function changeLimit(num, btn) {
        limitCount = num;
        document.getElementById('countDisplay').innerText = num;
        document.querySelectorAll('.num-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
    }

    function insertSample() {
        document.getElementById('userText').value = "يعتبر علم الاقتصاد واحداً من العلوم الاجتماعية المهمة التي تدرس كيفية استغلال الموارد المحدودة لإشباع الحاجات الإنسانية غير المحدودة. ويعود ظهور علم الاقتصاد الحديث إلى الكاتب الاسكتلندي آدم سميث في كتابه ثروة الأمم سنة 1776.";
    }

    function resetAll() {
        document.getElementById('userText').value = "";
        document.getElementById('quizOutput').innerHTML = "";
    }

    function makeQuiz() {
        const textContent = document.getElementById('userText').value;
        const boxOutput = document.getElementById('quizOutput');
        
        if (!textContent.trim()) {
            boxOutput.innerHTML = "<p style='color: #f87171;'>يرجى لصق نص أولاً!</p>";
            return;
        }

        // تقسيم النص إلى جمل مفيدة
        let rawSentences = textContent.split(/[.\n]/).map(s => s.trim()).filter(s => s.length > 25);
        
        if (rawSentences.length === 0) {
            boxOutput.innerHTML = "<p style='color: #f87171;'>النص قصير جداً، يرجى وضع جمل أطول ومفيدة.</p>";
            return;
        }

        let finalHtml = "<h3>اختر الإجابة الصحيحة لكل سؤال:</h3>";
        let totalQ = Math.min(limitCount, rawSentences.length);

        // بنك إجابات خاطئة متنوعة ومنطقية للاستعانة بها
        let wrongPool = [
            "يعد فرعاً من فروع العلوم الطبيعية البحتة",
            "تم اعتماده لأول مرة خلال القرن العشرين",
            "يركز بشكل أساسي على القطاع الزراعي فقط",
            "يعتمد على إلغاء الأسواق الحرة كلياً",
            "لا يوجد أي ارتباط بينه وبين الموارد المتاحة",
            "ظهر لأول مرة في الحضارات القديمة قبل الميلاد"
        ];

        for (let i = 0; i < totalQ; i++) {
            let correctStatement = rawSentences[i];
            
            // صياغة سؤال حقيقي واحترافي بناءً على الجملة
            let questionTitle = `ما هو الصحيح وفقاً للنص حول: <br><span style="color: #38bdf8; font-size: 14px;">"${correctStatement.substring(0, 45)}..."</span>`;

            // الخيارات: الخيار الأول هو الجملة الصحيحة نفسها كاملة
            let choices = [correctStatement];

            // إضافة 3 خيارات خاطئة من البنك أو من جمل أخرى
            for (let w of wrongPool) {
                if (choices.length < 4 && !choices.includes(w)) {
                    choices.push(w);
                }
            }

            // إذا احتاج خيارات إضافية، نأخذ جمل أخرى من النص كمشتتات
            for (let other of rawSentences) {
                if (choices.length < 4 && other !== correctStatement && !choices.includes(other)) {
                    choices.push(other);
                }
            }

            // خلط الخيارات عشوائياً
            choices.sort(() => Math.random() - 0.5);

            finalHtml += `<div class="question-box">`;
            finalHtml += `<p><strong>س${i+1}:</strong> ${questionTitle}</p>`;
            finalHtml += `<ul class="options-list">`;
            
            choices.forEach(ch => {
                let isRight = (ch === correctStatement);
                // نخزن الإجابة الصحيحة مقارنة بالنص الكامل
                finalHtml += `<li onclick="verifyChoice(this, ${isRight}, '${btoa(encodeURIComponent(correctStatement))}')">${ch}</li>`;
            });

            finalHtml += `</ul></div>`;
        }

        boxOutput.innerHTML = finalHtml;
    }

    function verifyChoice(element, isRight, encodedCorrect) {
        let parentList = element.parentElement;
        let allItems = parentList.querySelectorAll('li');
        let decodedCorrect = decodeURIComponent(atob(encodedCorrect));
        
        allItems.forEach(li => {
            li.style.pointerEvents = 'none'; // تعطيل الضغط بعد الإجابة
            // تلوين الإجابة الصحيحة باللون الأخضر تلقائياً
            if (li.innerText.trim() === decodedCorrect.trim()) {
                li.classList.add('correct');
            }
        });

        if (!isRight) {
            element.classList.add('wrong'); // تلوين الخيار الخطأ بالأحمر إذا اختاره الطالب
        }
    }
</script>

</body>
</html>
