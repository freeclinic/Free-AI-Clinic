<html lang="auto" itemscope itemtype="https://schema.org/MedicalWebPage">
<head>
  <meta charset="UTF-8">
  <title>🏥 Free Clinic – AI Hospital | Live Diagnosis & Medicine</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta name="description" content="AI Hospital: ChatGPT-powered emergency diagnostics in 48 languages. Upload X-Ray, ECG, CT, blood reports, speak symptoms and receive instant generic + brand medicine advice.">
  <link rel="canonical" href="https://freeclinic.in">
  <!--  Fonts & Icons  -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap">
  <style>
    :root{
      --bg:#f0f4f8;
      --fg:#1e293b;
      --primary:#0ea5e9;
      --secondary:#7dd3fc;
      --danger:#ef4444;
      --glass:rgba(255,255,255,.75);
    }
    *{margin:0;padding:0;box-sizing:border-box;font-family:Inter,Arial,sans-serif}
    body{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);min-height:100vh;display:flex;flex-direction:column;color:var(--fg)}
    header{backdrop-filter:blur(8px);background:var(--glass);padding:20px;display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid #e5e7eb}
    header h1{font-size:1.6rem;font-weight:600;color:#111827}
    select{padding:4px 8px;border-radius:6px;border:1px solid #d1d5db;background:#fff;font-weight:600}
    main{flex:1;max-width:700px;width:100%;margin:30px auto;padding:0 15px}
    .card{background:var(--glass);border-radius:16px;padding:24px;margin-bottom:20px;box-shadow:0 8px 32px rgba(0,0,0,.1)}
    label{font-weight:600;margin-bottom:.5rem;display:block}
    textarea{width:100%;min-height:110px;border:1px solid #cbd5e1;border-radius:8px;padding:12px;font-size:1rem;resize:none}
    button{width:100%;padding:14px;margin:8px 0;border:none;border-radius:8px;font-size:1rem;font-weight:600;cursor:pointer;transition:.2s}
    .btn-primary{background:var(--primary);color:#fff}
    .btn-secondary{background:var(--secondary);color:#111}
    .btn-primary:hover{filter:brightness(1.1)}
    .drop{height:120px;border:2px dashed var(--primary);border-radius:12px;display:flex;align-items:center;justify-content:center;cursor:pointer;transition:.2s}
    .drop.dragover{background:var(--secondary);border-color:var(--primary)}
    .result{background:#fff;border-left:5px solid var(--primary);padding:16px;border-radius:8px;margin-top:10px;white-space:pre-wrap}
    footer{background:#111827;color:#fff;padding:25px;text-align:center;font-size:.9rem}
    footer a{color:#7dd3fc;text-decoration:none}
    .loader{display:none;text-align:center;margin:10px 0}
    @media(max-width:600px){header h1{font-size:1.3rem}}
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
    <button class="btn-secondary" id="micBtn">🎤 Speak</button>
  </div>

  <!-- Image Upload -->
  <div class="card">
    <label id="lblDrop">Upload X-Ray, ECG, CT or Blood Report</label>
    <div class="drop" id="uploadDrop">📁 Drop file here or click to select</div>
    <input type="file" id="fileInput" accept="image/*,.pdf" style="display:none">
  </div>

  <!-- Action -->
  <button class="btn-primary" onclick="diagnose()">💡 Diagnose & Medicine Advice</button>
  <div id="loader" class="loader">⏳ ChatGPT analysing…</div>
  <div id="result" class="result"></div>
</main>

<footer>
  <!-- Contact & Donations -->
  📞 WhatsApp: <a href="https://wa.me/9779701881529">+977 9701881529</a> | 
  📸 Instagram: <a href="https://instagram.com/itsdrsuyash">@itsdrsuyash</a><br>
  💰 eSewa: <a href="intent://pay?pa=9869051338&pn=FreeClinic&cu=NPR#Intent;scheme=upi;package=com.esewa.android;end">9869051338</a><br>
  💐 In loving memory of <strong>Dr. Bharat Prasad Singh</strong>, Koiladi, Saptari
</footer>

<script>
/* ---------- 48-language list ---------- */
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
/* ---------- Voice ---------- */
document.getElementById('micBtn').onclick = () => {
  const lang = langSelect.value;
  const rec = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
  rec.lang = lang==='zh'?'zh-CN':lang==='hi'?'hi-IN':lang==='ne'?'ne-NP':lang==='bn'?'bn-BD':'en-US';
  rec.onresult = e => document.getElementById('symptoms').value = e.results[0][0].transcript;
  rec.start();
};
/* ---------- Drag-drop ---------- */
const drop = document.getElementById('uploadDrop');
const fileInput = document.getElementById('fileInput');
['dragover','dragleave','drop'].forEach(evt=>drop.addEventListener(evt,e=>{
  e.preventDefault();
  drop.classList.toggle('dragover',evt==='dragover');
}));
drop.addEventListener('drop', e=>{
  e.preventDefault();
  fileInput.files=e.dataTransfer.files;
});
drop.addEventListener('click', ()=>fileInput.click());
/* ---------- Diagnosis ---------- */
const OPENAI_KEY = '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';
async function diagnose() {
  const s = document.getElementById('symptoms').value.trim();
  const file = document.getElementById('fileInput').files[0];
  if(!s && !file){alert('Type symptoms or upload image');return}
  document.getElementById('loader').style.display='block';
  document.getElementById('result').innerHTML='';
  const lang = langSelect.value;
  let messages = [{role:'system',content:`Reply in ${lang}. Give 1 likely cause, 1 test, 1 OTC medicine (generic + brand + dose), warn visit doctor if serious.`}];
  if(s) messages.push({role:'user',content:s});
  if(file){
    const base64 = await new Promise((res,rej)=>{
      const reader=new FileReader();
      reader.readAsDataURL(file);
      reader.onload=()=>res(reader.result);
      reader.onerror=rej;
    });
    messages.push({role:'user',content:[{type:'text',text:'Analyse this medical image.'},{type:'image_url',image_url:{url:base64}}]});
  }
  try{
    const res = await fetch('https://api.openai.com/v1/chat/completions', {
      method:'POST',
      headers:{'Content-Type':'application/json','Authorization':`Bearer ${OPENAI_KEY}`},
      body:JSON.stringify({model:'gpt-4o-mini',messages,max_tokens:180})
    });
    const json = await res.json();
    document.getElementById('result').innerHTML = json.choices[0].message.content;
  }catch(e){
    document.getElementById('result').innerHTML = '⚠️ API error – please try again later.';
  }
  document.getElementById('loader').style.display='none';
}
</script>
</body>
</html>
