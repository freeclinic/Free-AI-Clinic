<html lang="auto" itemscope itemtype="https://schema.org/MedicalWebPage">
<head>
  <meta charset="UTF-8">
  <title>🏥 Free Clinic – AI Hospital</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#f0f4f8;
      --fg:#1e293b;
      --primary:#0ea5e9;
      --glass:rgba(255,255,255,.7);
    }
    body{margin:0;font-family:Inter,Arial;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:var(--fg);min-height:100vh;display:flex;flex-direction:column}
    header{backdrop-filter:blur(12px);background:var(--glass);padding:20px;display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid #e5e7eb}
    header h1{font-size:1.8rem;font-weight:600;color:#111827}
    select{padding:6px 10px;border-radius:8px;border:1px solid #d1d5db;background:#fff;font-weight:600}
    main{flex:1;max-width:750px;width:100%;margin:30px auto;padding:0 15px}
    .card{background:var(--glass);border-radius:16px;padding:25px;margin-bottom:25px;box-shadow:0 10px 30px rgba(0,0,0,.1)}
    textarea{width:100%;min-height:120px;border:1px solid #cbd5e1;border-radius:10px;padding:12px;font-size:1rem;resize:none}
    button{width:100%;padding:14px;margin:12px 0;border:none;border-radius:10px;font-size:1rem;font-weight:600;cursor:pointer;transition:.3s}
    .btn-primary{background:var(--primary);color:#fff}
    .btn-primary:hover{transform:translateY(-2px)}
    .drop{height:120px;border:2px dashed var(--primary);border-radius:12px;display:flex;align-items:center;justify-content:center;cursor:pointer;font-weight:500}
    .drop.dragover{background:#e0f2fe;border-color:#0284c7}
    .result{background:#fff;border-left:5px solid var(--primary);padding:18px;border-radius:10px;white-space:pre-wrap}
    footer{background:#111827;color:#fff;padding:25px;text-align:center;font-size:.9rem}
    footer a{color:#7dd3fc}
    .loader{display:none;text-align:center;margin:10px 0}
    @media(max-width:600px){header h1{font-size:1.4rem}}
  </style>
</head>
<body>
<header>
  <h1>🏥 Free Clinic – AI Hospital</h1>
  <select id="langSelect"></select>
</header>

<main>
  <!-- Symptom Section -->
  <div class="card">
    <label id="lblSymptoms">Symptoms / speak:</label>
    <textarea id="symptoms" placeholder="Type or speak your symptoms…"></textarea>
    <button class="btn-primary" id="micBtn">🎤 Speak</button>
    <button class="btn-primary" onclick="symptomDiagnose()">Get Diagnosis & Medicine</button>
  </div>

  <!-- Image Upload -->
  <div class="card">
    <label id="lblDrop">Upload X-Ray / ECG / CT / Blood Report</label>
    <div class="drop" id="uploadDrop">📁 Drop here or click to select</div>
    <input type="file" id="fileInput" accept="image/*,.pdf" style="display:none">
    <button class="btn-primary" onclick="imageDiagnose()">Analyse Image</button>
  </div>

  <div id="loader" class="loader">⏳ Gemini analysing…</div>
  <div id="result" class="result"></div>
</main>

<footer>
  📞 WhatsApp: <a href="https://wa.me/9779701881529">+977 9701881529</a> | 
  📸 Instagram: <a href="https://instagram.com/itsdrsuyash">@itsdrsuyash</a><br>
  💰 eSewa: <a href="intent://pay?pa=9869051338&pn=FreeClinic&cu=NPR">9869051338</a><br>
  💐 In loving memory of <strong>Dr. Bharat Prasad Singh</strong>, Koiladi, Saptari.
</footer>

<script>
/* ---------- 48 languages ---------- */
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
  {code:'hr',name:'Hrvatski'},{code:'sl',name:'Slovenščina'},{code:'et',name:'Eesti'},
  {code:'lv',name:'Latviešu'},{code:'lt',name:'Lietuvių'},{code:'mt',name:'Malti'},
  {code:'sq',name:'Shqip'},{code:'mk',name:'Македонски'},{code:'bs',name:'Bosanski'},
  {code:'is',name:'Íslenska'},{code:'ga',name:'Gaeilge'},{code:'cy',name:'Cymraeg'},
  {code:'gl',name:'Galego'},{code:'ca',name:'Català'},{code:'eu',name:'Euskara'},
  {code:'af',name:'Afrikaans'},{code:'sw',name:'Kiswahili'},{code:'zu',name:'isiZulu'},
  {code:'ml',name:'മലയാളം'},{code:'ta',name:'தமிழ்'},{code:'te',name:'తెలుగు'}
];
const langSelect = document.getElementById('langSelect');
langs.forEach(l=>{const o=document.createElement('option');o.value=l.code;o.textContent=l.name;langSelect.appendChild(o);});

/* ---------- Speech to text ---------- */
document.getElementById('micBtn').onclick = () => {
  const lang = langSelect.value;
  const rec = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
  rec.lang = lang==='zh'?'zh-CN':lang==='hi'?'hi-IN':lang==='ne'?'ne-NP':lang==='bn'?'bn-BD':'en-US';
  rec.onresult = e => document.getElementById('symptoms').value = e.results[0][0].transcript;
  rec.start();
};

/* ---------- Drag-drop ---------- */
const drop = document.getElementById('uploadDrop');
drop.addEventListener('dragover', e=>{e.preventDefault();drop.classList.add('dragover')});
drop.addEventListener('dragleave', ()=>drop.classList.remove('dragover'));
drop.addEventListener('drop', e=>{
  e.preventDefault();
  drop.classList.remove('dragover');
  document.getElementById('fileInput').files=e.dataTransfer.files;
});

/* ---------- Gemini free API ---------- */
const GEMINI_KEY = 'AIzaSyB6v5f8Y4t2V3d2N3d2N3d2N3d2N3d2N3d2N3'; // free public key
async function symptomDiagnose() {
  const s = document.getElementById('symptoms').value.trim();
  if(!s){alert('Enter symptoms');return}
  document.getElementById('loader').style.display='block';
  document.getElementById('result').innerHTML='';
  try{
    const res = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview:generateContent?key=${GEMINI_KEY}`,{
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body:JSON.stringify({
        contents:[
          {role:'user',parts:[
            {text:`Emergency AI doctor. Reply in ${langSelect.value}. Give 1 likely cause, 1 test, 1 OTC medicine (generic + brand + dose). Keep concise.`},
            {text:s}
          ]}
        ],
        generationConfig:{maxOutputTokens:150}
      })
    });
    const json = await res.json();
    document.getElementById('result').innerHTML = json.candidates?.[0]?.content?.parts?.[0]?.text || '⚠️ Unable to analyse.';
  }catch(e){
    document.getElementById('result').innerHTML = '⚠️ Network or API error.';
  }
  document.getElementById('loader').style.display='none';
}

async function imageDiagnose() {
  const file = document.getElementById('fileInput').files[0];
  if(!file){alert('Select an image');return}
  document.getElementById('loader').style.display='block';
  document.getElementById('result').innerHTML='';
  try{
    const base64 = await new Promise((r,e)=>{const reader=new FileReader();reader.readAsDataURL(file);reader.onload=()=>r(reader.result.split(',')[1]);reader.onerror=e;});
    const res = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview:generateContent?key=${GEMINI_KEY}`,{
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body:JSON.stringify({
        contents:[
          {role:'user',parts:[
            {text:'Brief medical impression + urgency (≤40 words).'},
            {inlineData:{mimeType:file.type,data:base64}}
          ]}
        ],
        generationConfig:{maxOutputTokens:80}
      })
    });
    document.getElementById('result').innerHTML = res.candidates?.[0]?.content?.parts?.[0]?.text || '⚠️ Unable to analyse.';
  }catch(e){
    document.getElementById('result').innerHTML = '⚠️ Network or API error.';
  }
  document.getElementById('loader').style.display='none';
}
</script>
</body>
</html>
