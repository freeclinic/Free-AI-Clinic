<html lang="auto">
<head>
  <meta charset="UTF-8">
  <title>🏥 Free Clinic – Multilingual AI Diagnostics</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #f0f4f8;
      --fg: #1e293b;
      --primary: #0ea5e9;
      --card: #ffffff;
    }
    body {
      margin: 0;
      font-family: Inter, Arial;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: var(--fg);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }
    header {
      background: var(--primary);
      color: #fff;
      padding: 20px;
      text-align: center;
      font-size: 1.6rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    select {
      padding: 6px 10px;
      border-radius: 8px;
      border: 1px solid #d1d5db;
      background: #fff;
      font-weight: 600;
    }
    main {
      max-width: 750px;
      margin: 30px auto;
      padding: 20px;
    }
    .card {
      background: var(--card);
      border-radius: 16px;
      padding: 25px;
      margin-bottom: 25px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
    }
    textarea {
      width: 100%;
      min-height: 120px;
      border: 1px solid #cbd5e1;
      border-radius: 10px;
      padding: 12px;
      font-size: 1rem;
    }
    button {
      width: 100%;
      padding: 14px;
      margin: 12px 0;
      border: none;
      border-radius: 10px;
      background: var(--primary);
      color: #fff;
      font-size: 1rem;
      cursor: pointer;
      transition: 0.3s;
    }
    button:hover {
      transform: translateY(-2px);
    }
    .result {
      background: #fff;
      border-left: 5px solid var(--primary);
      padding: 16px;
      border-radius: 10px;
      white-space: pre-wrap;
    }
    footer {
      background: #111827;
      color: #fff;
      padding: 20px;
      text-align: center;
      font-size: 0.9rem;
    }
    footer a {
      color: #7dd3fc;
    }
    .loader {
      display: none;
      text-align: center;
    }
  </style>
</head>
<body>
<header>
  <h1>🏥 Free Clinic – Multilingual AI Diagnostics</h1>
  <select id="langSelect" onchange="setLang(this.value)">
    <option value="en">English</option>
    <option value="hi">हिंदी</option>
    <option value="ne">नेपाली</option>
    <option value="zh">中文</option>
    <option value="bn">বাংলা</option>
  </select>
</header>

<main>
  <!-- Symptom -->
  <div class="card">
    <label id="lblSymptoms">Symptoms / speak:</label>
    <textarea id="symptoms" placeholder="Speak or type…"></textarea>
    <button id="micBtn">🎤 Speak</button>
    <button onclick="diagnose()">Diagnose & Treatment</button>
  </div>

  <!-- Image -->
  <div class="card">
    <label id="lblDrop">Upload X-Ray / CT / ECG / Blood report</label>
    <input type="file" id="fileInput" accept="image/*,.pdf" style="display:none">
    <button onclick="document.getElementById('fileInput').click()">Upload</button>
  </div>

  <div id="loader" class="loader">⏳ Analyzing…</div>
  <div id="result" class="result"></div>
</main>

<footer>
  📞 WhatsApp: <a href="https://wa.me/9779701881529">+977 9701881529</a> | 
  📸 Instagram: <a href="https://instagram.com/itsdrsuyash">@itsdrsuyash</a><br>
  💰 eSewa: <a href="intent://pay?pa=9869051338&pn=FreeClinic&cu=NPR">9869051338</a><br>
  💐 In loving memory of <strong>Dr. Bharat Prasad Singh</strong>, Koiladi, Saptari.
</footer>

<script>
/* ---------- i18n Dictionary ---------- */
const i18n = {
  en: {
    title: "Free Clinic – Multilingual AI Diagnostics",
    lblSymptoms: "Symptoms / speak:",
    lblDrop: "Drag X-Ray / CT / ECG / Blood report here",
    micBtn: "🎤 Speak",
    btnDiagnose: "Diagnose & Treatment",
    loader: "⏳ Analyzing…",
    resultTitle: "🔍 Possible cause:",
    inv: "📋 Needed test:",
    rx: "💊 OTC medicine:",
    warn: "⚠️ Serious – see doctor immediately!",
    follow: "✅ If no relief in 48 hrs, see doctor."
  },
  hi: {
    title: "फ्री क्लिनिक – बहुभाषी AI जांच",
    lblSymptoms: "लक्षण या बोलें:",
    lblDrop: "X-Ray / CT / ECG / ब्लड रिपोर्ट यहाँ डालें",
    micBtn: "🎤 बोलिए",
    btnDiagnose: "डायग्नोसिस व उपचार",
    loader: "⏳ विश्लेषण चल रहा है…",
    resultTitle: "🔍 संभावित कारण:",
    inv: "📋 जरूरी जांच:",
    rx: "💊 OTC दवा:",
    warn: "⚠️ गंभीर – तुरंत डॉक्टर से मिलें!",
    follow: "✅ 48 घंटे में आराम न मिले तो डॉक्टर से मिलें।"
  },
  ne: {
    title: "फ्री क्लिनिक – बहुभाषी AI जाँच",
    lblSymptoms: "लक्षण वा बोल्नुहोस्:",
    lblDrop: "X-Ray / CT / ECG / रगत रिपोर्ट यहाँ डाल्नुहोस्",
    micBtn: "🎤 बोल्नुहोस्",
    btnDiagnose: "डायग्नोसिस र उपचार",
    loader: "⏳ विश्लेषण भइरहेको छ…",
    resultTitle: "🔍 सम्भावित कारण:",
    inv: "📋 आवश्यक परीक्षण:",
    rx: "💊 OTC औषधि:",
    warn: "⚠️ गम्भीर – तुरन्त डाक्टर भेट्नुहोस्!",
    follow: "✅ ४८ घण्टामा आराम नआए डाक्तर भेट्नुहोस्।"
  },
  zh: {
    title: "免费诊所 – 多语言AI诊断",
    lblSymptoms: "症状/语音输入:",
    lblDrop: "拖拽 X光/CT/心电图/血液报告",
    micBtn: "🎤 说话",
    btnDiagnose: "诊断与治疗",
    loader: "⏳ 分析中…",
    resultTitle: "🔍 可能原因:",
    inv: "📋 必要检查:",
    rx: "💊 非处方药:",
    warn: "⚠️ 严重 – 立即就医!",
    follow: "✅ 48小时无缓解请就医。"
  },
  bn: {
    title: "ফ্রি ক্লিনিক – বহুভাষা AI নির্ণয়",
    lblSymptoms: "লক্ষণ বা বলুন:",
    lblDrop: "এখানে X-Ray / CT / ECG / রক্তের রিপোর্ট টেনে আনুন",
    micBtn: "🎤 বলুন",
    btnDiagnose: "নির্ণয় ও চিকিৎসা",
    loader: "
