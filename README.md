<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>مولّد أسئلة الاختيار من متعدد</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Arabic:wght@400;600;700&display=swap" rel="stylesheet">
<style>
:root{--bg:#f3f5f2;--card:#fff;--ink:#1c2a2e;--mute:#5d6b6f;--line:#d9dfdb;--acc:#1f6f6b;--acc-ink:#fff;--ok:#1d7a46;--okbg:#e3f3ea;--bad:#b3362d;--badbg:#f9e5e2;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#121a1b;--card:#1b2628;--ink:#e7eeee;--mute:#9fb0b2;--line:#2c3b3d;--acc:#5cc2ba;--acc-ink:#0d1a1a;--ok:#63d391;--okbg:#173a27;--bad:#f08a80;--badbg:#421f1c}}
:root[data-theme="dark"]{--bg:#121a1b;--card:#1b2628;--ink:#e7eeee;--mute:#9fb0b2;--line:#2c3b3d;--acc:#5cc2ba;--acc-ink:#0d1a1a;--ok:#63d391;--okbg:#173a27;--bad:#f08a80;--badbg:#421f1c}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font-family:"IBM Plex Sans Arabic",Tahoma,Arial,sans-serif;line-height:1.7}
main{max-width:720px;margin:0 auto;padding:28px 16px 64px}
h1{font-size:1.7rem;margin:0 0 4px}
.sub{color:var(--mute);margin:0 0 22px}
.drop{display:block;border:2px dashed var(--line);border-radius:14px;background:var(--card);padding:28px 16px;text-align:center;cursor:pointer}
.drop:hover,.drop.on,.drop:focus-within{border-color:var(--acc)}
.drop input{position:absolute;opacity:0;width:1px;height:1px}
.fname{font-weight:600;word-break:break-word}
.row{display:flex;gap:12px;align-items:center;flex-wrap:wrap;margin:16px 0}
select,button{font:inherit}
select{padding:8px 12px;border-radius:8px;border:1px solid var(--line);background:var(--card);color:var(--ink)}
.btn{background:var(--acc);color:var(--acc-ink);border:0;border-radius:10px;padding:10px 22px;font-weight:600;cursor:pointer}
.btn:disabled{opacity:.5;cursor:not-allowed}
.btn:focus-visible,.opt:focus-visible{outline:3px solid var(--acc);outline-offset:2px}
.note{padding:12px 14px;border-radius:10px;background:var(--card);border:1px solid var(--line)}
.note.err{border-color:var(--bad);color:var(--bad)}
.bar{display:flex;justify-content:space-between;align-items:center;margin:26px 0 10px;font-weight:600}
.q{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:16px;margin-bottom:14px}
.q h3{font-size:1.05rem;margin:0 0 12px}
.opt{display:block;width:100%;text-align:right;background:transparent;color:var(--ink);border:1px solid var(--line);border-radius:10px;padding:10px 12px;margin-bottom:8px;cursor:pointer}
.opt:hover:not(:disabled){border-color:var(--acc)}
.opt:disabled{cursor:default}
.opt.ok{background:var(--okbg);border-color:var(--ok)}
.opt.bad{background:var(--badbg);border-color:var(--bad)}
.exp{margin:6px 0 0;color:var(--mute);font-size:.95rem}
@media (prefers-reduced-motion:no-preference){.opt{transition:background .15s,border-color .15s}}
.ta{width:100%;font:inherit;line-height:1.7;padding:12px;border:1px solid var(--line);border-radius:12px;background:var(--card);color:var(--ink);resize:vertical}
.ta:focus-visible{outline:3px solid var(--acc);outline-offset:1px}
.meta{color:var(--mute);font-size:.85rem;margin-top:4px}
.btn.ghost{background:transparent;color:var(--ink);border:1px solid var(--line)}
.btn.ghost:hover:not(:disabled){border-color:var(--acc)}
.count{display:flex;align-items:center;gap:8px}
.step{width:44px;height:44px;border-radius:10px;border:1px solid var(--line);background:var(--card);color:var(--ink);font-size:1.3rem;cursor:pointer}
.num{width:72px;height:44px;text-align:center;font:inherit;font-size:16px;border:1px solid var(--line);border-radius:10px;background:var(--card);color:var(--ink)}
.chips{display:flex;gap:6px;flex-wrap:wrap}
.chip{min-width:40px;height:36px;border-radius:999px;border:1px solid var(--line);background:transparent;color:var(--ink);cursor:pointer}
.chip.on{background:var(--acc);color:var(--acc-ink);border-color:var(--acc)}
.step:focus-visible,.chip:focus-visible,.num:focus-visible{outline:3px solid var(--acc);outline-offset:2px}
.btn{min-height:44px}
.ta{font-size:16px}
</style>
</head>
<body>
<div id="root"></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react/18.2.0/umd/react.production.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react-dom/18.2.0/umd/react-dom.production.min.js"></script>
<script>
const h = React.createElement;
const { useState } = React;

const SAMPLE_TEXT = "التمثيل الضوئي هو العملية التي تحوّل بها النباتات الخضراء والطحالب وبعض البكتيريا الطاقة الضوئية إلى طاقة كيميائية مخزّنة في الغلوكوز. تحدث هذه العملية في البلاستيدات الخضراء التي تحتوي على صبغة الكلوروفيل، وهي التي تمتص الضوء وتمنح النبات لونه الأخضر. تستهلك النباتات ثاني أكسيد الكربون من الهواء والماء من التربة، وتُنتج الغلوكوز والأكسجين. تتكون العملية من مرحلتين: التفاعلات الضوئية التي تحدث في أغشية الثايلاكويد وتنتج ATP وNADPH، ودورة كالفن التي تحدث في الستروما وتستخدم هذه الطاقة لتثبيت ثاني أكسيد الكربون وبناء السكريات. ويُعدّ الأكسجين الناتج من تحلل جزيئات الماء أثناء التفاعلات الضوئية.";

const SAMPLE_QS = [
  { question: "أين تحدث عملية التمثيل الضوئي داخل الخلية النباتية؟", options: ["الميتوكوندريا", "البلاستيدات الخضراء", "النواة", "الفجوة العصارية"], answer: 1, explanation: "تحتوي البلاستيدات الخضراء على الكلوروفيل الذي يمتص الضوء." },
  { question: "ما المادة التي تمتص الضوء في النبات؟", options: ["الهيموغلوبين", "الكيراتين", "الكلوروفيل", "الأنسولين"], answer: 2, explanation: "الكلوروفيل صبغة خضراء تمتص الطاقة الضوئية." },
  { question: "ما النواتج الرئيسية للتمثيل الضوئي؟", options: ["الغلوكوز والأكسجين", "الماء وثاني أكسيد الكربون", "البروتين والدهون", "النيتروجين والهيدروجين"], answer: 0, explanation: "يُنتج النبات الغلوكوز ويُطلق الأكسجين." },
  { question: "أين تحدث دورة كالفن؟", options: ["في أغشية الثايلاكويد", "في الستروما", "في الجدار الخلوي", "في السيتوبلازم"], answer: 1, explanation: "تحدث دورة كالفن في الستروما وتستخدم ATP وNADPH." }
];

function errMsg(e) {
  const m = {
    not_granted: "لم تسمح لهذا التطبيق باستخدام Claude. أعد تحميل الصفحة ووافق عند ظهور الطلب، أو جرّب زر الأسئلة التجريبية.",
    rate_limited: "بلغتَ حد الاستخدام أو كثرت الطلبات. انتظر قليلاً ثم اضغط الزر مجدداً.",
    invalid_json: "لم تكتمل نتيجة التوليد. اضغط الزر مرة أخرى.",
    prompt_too_large: "النص طويل جداً. اقتصر على جزء أقصر منه.",
    session_expired: "انتهت جلستك. سجّل الدخول إلى Claude ثم أعد المحاولة.",
    sampling_disabled: "خاصية Claude غير متاحة لحسابك أو مؤسستك.",
    empty_completion: "لم يُنتج Claude أي رد. أعد المحاولة.",
    refused: "رفض Claude معالجة هذا النص.",
    upstream_error: "انقطع الاتصال بالخدمة. أعد المحاولة."
  };
  return (e && m[e.code]) || (e && e.message) || "حدث خطأ غير متوقع. أعد المحاولة.";
}

function App() {
  const [text, setText] = useState("");
  const [count, setCount] = useState("5");
  const [busy, setBusy] = useState(false);
  const [error, setError] = useState("");
  const [qs, setQs] = useState([]);
  const [demo, setDemo] = useState(false);
  const [picked, setPicked] = useState({});

  function reset(list, isDemo) { setQs(list); setDemo(isDemo); setPicked({}); }

  const clamp = v => Math.min(30, Math.max(1, v));
  async function generate() {
    if (busy) return;
    const n = clamp(parseInt(count) || 5); setCount(String(n));
    const src = text.trim().slice(0, 60000);
    setError("");
    if (src.length < 50) { setError("الصق نصاً لا يقل عن بضع جمل (50 حرفاً على الأقل)."); return; }
    setBusy(true); reset([], false);
    try {
      const sample = await claude.use("sample");
      if (!sample) throw { message: "خاصية التوليد غير متاحة في هذا العرض. افتح الصفحة من حسابك على Claude، أو جرّب الأسئلة التجريبية." };
      const prompt = `أنت معلّم خبير في إعداد الاختبارات. ولّد ${n} أسئلة اختيار من متعدد اعتماداً على النص التالي فقط، بنفس لغة النص. لكل سؤال أربعة خيارات، واحد صحيح فقط، والبقية مشتتات معقولة، مع تفسير قصير للإجابة الصحيحة.
أعد JSON فقط بهذا الشكل بلا أي نص إضافي:
{"questions":[{"question":"","options":["","","",""],"answer":0,"explanation":""}]}
حيث answer هو رقم الخيار الصحيح (يبدأ من 0).

النص:
${src}`;
      const res = await sample.json(prompt, { cache: false });
      const raw = Array.isArray(res) ? res : (res && res.questions) || [];
      const list = raw.filter(q => q && q.question && Array.isArray(q.options) && q.options.length >= 2 && Number.isInteger(q.answer) && q.answer >= 0 && q.answer < q.options.length);
      if (!list.length) throw { message: "لم يُرجِع Claude أسئلة صالحة. أعد المحاولة." };
      reset(list, false);
    } catch (e) {
      setError(errMsg(e));
    } finally {
      setBusy(false);
    }
  }

  const answered = Object.keys(picked).length;
  const score = qs.reduce((s, q, i) => s + (picked[i] === q.answer ? 1 : 0), 0);

  return h("main", null,
    h("h1", null, "مولّد أسئلة الاختيار من متعدد"),
    h("p", { className: "sub" }, "الصق نصاً من كتابك أو ملخصك، وسيُنشئ Claude أسئلة منه فوراً."),
    h("textarea", { className: "ta", rows: 9, value: text, disabled: busy, placeholder: "الصق النص هنا…", onChange: e => setText(e.target.value) }),
    h("div", { className: "meta" }, text.trim().length + " حرفاً"),
    h("div", { className: "row" },
      h("div", { className: "count" },
        h("span", null, "عدد الأسئلة:"),
        h("button", { className: "step", disabled: busy, "aria-label": "أنقص", onClick: () => setCount(String(clamp((parseInt(count) || 0) - 1))) }, "−"),
        h("input", { className: "num", type: "number", inputMode: "numeric", min: 1, max: 30, value: count, disabled: busy, "aria-label": "عدد الأسئلة", onChange: e => setCount(e.target.value) }),
        h("button", { className: "step", disabled: busy, "aria-label": "زِد", onClick: () => setCount(String(clamp((parseInt(count) || 0) + 1))) }, "+")),
      h("div", { className: "chips" }, [5, 10, 15, 20, 30].map(v =>
        h("button", { key: v, className: "chip" + (parseInt(count) === v ? " on" : ""), disabled: busy, onClick: () => setCount(String(v)) }, v))),
      h("button", { className: "btn", disabled: busy, onClick: generate }, busy ? "جارٍ التوليد، قد يستغرق دقيقة…" : "ولّد الأسئلة")
    ),
    h("div", { className: "row" },
      h("button", { className: "btn ghost", disabled: busy, onClick: () => { setText(SAMPLE_TEXT); setError(""); } }, "ضع نصاً تجريبياً"),
      h("button", { className: "btn ghost", disabled: busy, onClick: () => { setError(""); reset(SAMPLE_QS, true); } }, "اعرض أسئلة تجريبية"),
      text && h("button", { className: "btn ghost", disabled: busy, onClick: () => { setText(""); reset([], false); } }, "امسح")
    ),
    error && h("div", { className: "note err", role: "alert" }, error),
    demo && h("div", { className: "note" }, "هذه أسئلة تجريبية جاهزة ولم تُولَّد من نصك."),
    qs.length > 0 && h("div", { className: "bar" },
      h("span", null, qs.length + " أسئلة"),
      h("span", null, "النتيجة: " + score + " / " + answered)),
    qs.map((q, i) => {
      const done = picked[i] !== undefined;
      return h("section", { className: "q", key: i },
        h("h3", null, (i + 1) + ". " + q.question),
        q.options.map((o, j) => {
          let cls = "opt";
          if (done && j === q.answer) cls += " ok";
          else if (done && j === picked[i]) cls += " bad";
          return h("button", { key: j, className: cls, disabled: done, onClick: () => setPicked({ ...picked, [i]: j }) }, String(o));
        }),
        done && q.explanation && h("p", { className: "exp" }, q.explanation));
    })
  );
}
ReactDOM.createRoot(document.getElementById("root")).render(h(App));
</script>
</body>
</html>
