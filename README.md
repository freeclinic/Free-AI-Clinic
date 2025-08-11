<html lang="auto">
<head>
  <meta charset="UTF-8">
  <title>🏥 Free Clinic – Llama AI Hospital</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    :root{--bg:#f0f4f8;--fg:#1e293b;--primary:#0ea5e9}
    body{margin:0;font-family:Inter,Arial;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:var(--fg);min-height:100vh}
    header{background:var(--primary);color:#fff;padding:20px;text-align:center;font-size:1.6rem;display:flex;justify-content:space-between;align-items:center}
    select{padding:6px 10px;border-radius:8px;border:none;background:#fff;font-weight:600}
    main{max-width:750px;margin:30px auto;padding:20px}
    .card{background:#fff;border-radius:16px;padding:25px;margin-bottom:25px;box-shadow:0 10px 30px rgba(0,0,0,.1)}
    textarea{width:100%;min-height:120px;border:1px solid #cbd5e1;border-radius:10px;padding:12px;font-size:1rem}
    button{width:100%;padding:14px;margin:12px 0;border:none;border-radius:10px;background:var(--primary);color:#fff;font-size:1rem;cursor:pointer}
    .result{background:#fff;border-left:5px solid var(--primary);padding:18px;border-radius:10px;white-space:pre-wrap}
    footer{background:#111827;color:#fff;padding:20px;text-align:center;font-size:.9rem}
    footer a{color:#7dd3fc;text-decoration:none}
    .loader{display:none;text-align:center}
  </style>
</head>
<body>
<header>
  <h1>🏥 Free Clinic – Llama AI Hospital</h1>
  <select id="langSelect"></select>
</header>

<main>
  <!-- Symptom -->
  <div class="card">
    <label id="lblSymptoms">Symptoms / speak:</label>
    <textarea id="symptoms" placeholder="Speak or type…"></textarea>
    <button id="micBtn">🎤 Speak</button>
    <button onclick="diagnose()">Get Diagnosis & Medicine</button>
  </div>

  <!-- Image -->
  <div class="card">
    <label>Upload X-Ray / ECG / CT / Blood Report</label>
    <input type="file" id="fileInput" accept="image/*,.pdf">
    <button onclick="imageDiagnose()">Analyse Image</button>
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
/* ---------- 48-LANGUAGE i18n ---------- */
const langs = [
  {code:'en',name:'English'},{code:'hi',name:'हिंदी'},{code:'ne',name:'नेपाली'},
  {code:'zh',name:'中文'},{code:'bn',name:'বাংলা'},{code:'es',name:'Español'},
  {code:'fr',name:'Français'},{code:'ar',name:'العربية'},{code:'ru',name:'Русский'},
  {code:'pt',name:'Português'},{code:'de',name:'Deutsch'},{code:'ja',name:'日本語'},
  {code:'ko',name:'한국어'},{code:'it',name:'Italiano'},{code:'tr',name:'Türkçe'},
  {code:'th',name:'ไทย'},{code:'vi',name:'Tiếng Việt'},{code:'pl',name:'Polski'},
  {code:'nl',name:'Nederlands'},{code:'sv',name:'Svenska'},{code:'da',name:'Dansk'},
  {code:'no',name:'Norsk'},{code:'fi',name:'Suomi'},{code:'el',name:'Ελληνικά'},
  {code:'hu',name:'Magyar'},{code:'cs',name:'Čeština'},{code:'sk',name:'Slovenčina'},
  {code:'uk',name:'Українська'},{code:'ro',name:'Română'},{code:'bg',name:'Български'},
  {code:'hr',name:'Hrvatski'},{code:'sl',name:'Slovenšč
