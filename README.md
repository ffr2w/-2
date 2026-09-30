<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مولّد أسئلة الاختيار من متعدد الذكي</title>
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
            max-height: 400px;
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

        // تقسيم النص إلى جمل واضحة
        let rawSentences = textContent.split(/[.\n]/).map(s => s.trim()).filter(s => s.length > 20);
        
        if (rawSentences.length === 0) {
            boxOutput.innerHTML = "<p style='color: #f87171;'>النص قصير جداً، يرجى وضع جمل أطول ومفيدة.</p>";
            return;
        }

        let finalHtml = "<h3>اختر الإجابة الصحيحة لكل سؤال:</h3>";
        let totalQ = Math.min(limitCount, rawSentences.length);

        // بنك خيارات وهمية إضافية للتنوع
        let generalPool = [
            "العلوم الطبيعية البحتة",
            "القرن التاسع عشر الميلادي",
            "القطاع الزراعي والصناعي",
            "نظرية العرض والطلب الكلاسيكية",
            "زيادة التكاليف الثابتة",
            "العالم الإنجليزي جون لوك",
            "الموارد البشرية المتاحة"
        ];

        for (let i = 0; i < totalQ; i++) {
            let sentence = rawSentences[i];
            let words = sentence.split(" ");
            
            if (words.length < 5) continue;

            // نختار كلمة أو كلمتين عشوائيتين من منتصف الجملة لتكون هي الجواب الصحيح
            let targetIndex = Math.floor(words.length / 2);
            let rightChoice = words[targetIndex];
            
            // تنظيف الكلمة من الرموز إن وجدت
            rightChoice = rightChoice.replace(/[.,،]/g, "");
            if (rightChoice.length < 3 && targetIndex > 0) {
                targetIndex--;
                rightChoice = words[targetIndex].replace(/[.,،]/g, "");
            }

            // إنشاء السؤال بإخفاء الجواب بـ (____)
            words[targetIndex] = "____";
            let questionText = words.join(" ");

            // تجهيز الخيارات (1 صحيح + 3 خيارات أخرى)
            let choices = [rightChoice];
            
            // أخذ خيارات خاطئة من نفس الجملة أو من البنك العام
            for (let w of words) {
                let cleanW = w.replace(/[.,،]/g, "");
                if (cleanW.length > 3 && cleanW !== "____" && !choices.includes(cleanW)) {
                    choices.push(cleanW);
                }
            }

            // إكمال الخيارات إذا كانت ناقصة من البنك العام
            while(choices.length < 4 && generalPool.length > 0) {
                let randGen = generalPool[Math.floor(Math.random() * generalPool.length)];
                if (!choices.includes(randGen)) {
                    choices.push(randGen);
                } else {
                    break;
                }
            }

            // خلط الخيارات عشوائياً
            choices.sort(() => Math.random() - 0.5);

            finalHtml += `<div class="question-box">`;
            finalHtml += `<p><strong>س${i+1}:</strong> ${questionText}</p>`;
            finalHtml += `<ul class="options-list">`;
            
            choices.forEach(ch => {
                let isRight = (ch === rightChoice);
                finalHtml += `<li onclick="verifyChoice(this, ${isRight}, '${rightChoice}')">${ch}</li>`;
            });

            finalHtml += `</ul></div>`;
        }

        boxOutput.innerHTML = finalHtml;
    }

    function verifyChoice(element, isRight, correctVal) {
        let parentList = element.parentElement;
        let allItems = parentList.querySelectorAll('li');
        
        allItems.forEach(li => {
            li.style.pointerEvents = 'none'; // تعطيل الضغط بعد الإجابة
            // تلوين الإجابة الصحيحة بالخضراء تلقائياً
            if (li.innerText.trim() === correctVal) {
                li.classList.add('correct');
            }
        });

        if (!isRight) {
            element.classList.add('wrong'); // تلوين الخيار الخطأ بالأحمر إذا اختاره المستخدم
        }
    }
</script>

</body>
</html>
