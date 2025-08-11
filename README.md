<html lang="auto" itemscope itemtype="https://schema.org/MedicalWebPage">
<head>
  <meta charset="UTF-8">
  <title>Free Clinic – AI Doctor Online (Key Inserted)</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta name="description" content="Real-time ChatGPT-powered emergency diagnostics & generic/brand medicine advice in 48 languages.">
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🏥</text></svg>">
  <style>
    :root{--bg:#f5f7fa;--fg:#2c3e50;--accent:#00d2ff;--glass:rgba(255,255,255,.25)}
    body{margin:0;padding:0;font-family:Inter,Arial;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:var(--fg)}
    header{background:var(--accent);color:#fff;padding:15px;font-size:22px;text-align:center}
    main{max-width:700px;margin:40px auto;padding:20px;background:#fff;border-radius:12px}
    textarea{width:100%;min-height:100px;border:1px solid #ccc;border-radius:6px;padding:8px}
    button{width:100%;padding:12px;margin:8px 0;border:none;border-radius:6px;background:var(--accent);color:#fff;font-size:16px;cursor:pointer}
    .result{margin:15px 0;padding:15px;border-left:4px solid var(--accent);background:#f5f5f5}
    .drop{border:2px dashed var(--accent);border-radius:8px;padding:20px;text-align:center}
    footer{text-align:center;font-size:13px;color:#555;margin-top:30px}
  </style>
</head>
<body>
<header>Free Clinic – AI Doctor (Live)</header>

<main>
  <label>Symptoms / speak:</label>
  <textarea id="symptoms" placeholder="Type or speak your symptoms…"></textarea>
  <button id="micBtn">🎤 Speak</button>

  <div class="drop" id="uploadDrop">
    Drag X-Ray / ECG / CT / Blood report here
  </div>
  <input type="file" id="fileInput" accept="image/*,.pdf" style="display:none">

  <button onclick="diagnose()">Get Diagnosis & Medicine</button>
  <div id="loader" style="display:none">⏳ ChatGPT working…</div>
  <div id="result" class="result"></div>

  <footer>
    ⚠️ Emergency guidance only – see doctor if serious.  
    💐 In memory of Dr. Bharat Prasad Singh – Koiladi, Saptari
  </footer>
</main>

<script>
/* ---------- Your OpenAI key ---------- */
const OPENAI_KEY = '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';

/* ---------- Language list ---------- */
const langs = [
  {code:'en',name:'English'}, {code:'hi',name:'हिंदी'}, {code:'ne',name:'नेपाली'},
  {code:'zh',name:'中文'}, {code:'bn',name:'বাংলা'}, {code:'es',name:'Español'},
  {code:'fr',name:'Français'}, {code:'ar',name:'العربية'}, {code:'ru',name:'Русский'},
  {code:'pt',name:'Português'}, {code:'de',name:'Deutsch'}, {code:'ja',name:'日本語'},
  {code:'ko',name:'한국어'}, {code:'it',name:'Italiano'}, {code:'tr',name:'Türkçe'},
  {code:'th',name:'ไทย'}, {code:'vi',name:'Tiếng Việt'}, {code:'pl',name:'Polski'},
  {code:'nl',name:'Nederlands'}, {code:'sv',name:'Svenska'}, {code:'da',name:'Dansk'},
  {code:'no',name:'Norsk'}, {code:'fi',name:'Suomi'}, {code:'el',name:'Ελληνικά'},
  {code:'hu',name:'Magyar'}, {code:'cs',name:'Čeština'}, {code:'sk',name:'Slovenčina'},
  {code:'uk',name:'Українська'}, {code:'ro',name:'Română'}, {code:'bg',name:'Български'},
  {code:'hr',name:'Hrvatski'}, {code:'sr',name:'Српски'}, {code:'sl',name:'Slovenščina'},
  {code:'et',name:'Eesti'}, {code:'lv',name:'Latviešu'}, {code:'lt',name:'Lietuvių'},
  {code:'mt',name:'Malti'}, {code:'sq',name:'Shqip'}, {code:'mk',name:'Македонски'},
  {code:'bs',name:'Bosanski'}, {code:'is',name:'Íslenska'}, {code:'ga',name:'Gaeilge'},
  {code:'cy',name:'Cymraeg'}, {code:'gl',name:'Galego'}, {code:'ca',name:'Català'},
  {code:'eu',name:'Euskara'}, {code:'af',name:'Afrikaans'}, {code:'sw',name:'Kiswahili'},
  {code:'zu',name:'isiZulu'}, {code:'ml',name:'മലയാളം'}, {code:'ta',name:'தமிழ்'},
  {code:'te',name:'తెలుగు'}, {code:'kn',name:'ಕನ್ನಡ'}, {code:'gu',name:'ગુજરાતી'},
  {code:'or',name:'ଓଡ଼ିଆ'}, {code:'as',name:'অসমীয়া'}, {code:'pa',name:'ਪੰਜਾਬੀ'},
  {code:'ur',name:'اردو'}
];
const select = document.createElement('select');
select.id = 'langSelect';
langs.forEach(l=>{
  const opt = document.createElement('option');
  opt.value = l.code;
  opt.textContent = l.name;
  select.appendChild(opt);
});
document.querySelector('header').appendChild(select);

/* ---------- Voice input ---------- */
document.getElementById('micBtn').onclick = () => {
  if(!('webkitSpeechRecognition' in window)){alert('Browser not supported');return}
  const lang = document.getElementById('langSelect').value;
  const rec = new webkitSpeechRecognition();
  rec.lang = lang==='zh'?'zh-CN':lang==='hi'?'hi-IN':lang==='ne'?'ne-NP':lang==='bn'?'bn-BD':'en-US';
  rec.onresult = e => document.getElementById('symptoms').value = e.results[0][0].transcript;
  rec.start();
};

/* ---------- Symptom diagnosis ---------- */
async function diagnose() {
  const s = document.getElementById('symptoms').value.trim();
  if(!s){alert('Please enter symptoms');return}
  document.getElementById('loader').style.display='block';
  document.getElementById('result').innerHTML='';
  try{
    const res = await fetch('https://api.openai.com/v1/chat/completions',{
      method:'POST',
      headers:{
        'Content-Type':'application/json',
        'Authorization':`Bearer ${OPENAI_KEY}`
      },
      body:JSON.stringify({
        model:'gpt-4o-mini',
        messages:[
          {role:'system',content:`You are an AI doctor. Reply in ${document.getElementById('langSelect').value}. Give 1 likely cause, 1 essential test, 1 OTC medicine (generic + brand in brackets with dose), warn to see doctor if serious. Keep concise.`},
          {role:'user',content:s}
        ],
        max_tokens:150
      })
    });
    const json = await res.json();
    document.getElementById('result').innerHTML = json.choices[0].message.content;
  }catch(e){
    document.getElementById('result').innerHTML = '⚠️ API error – check network or key.';
  }
  document.getElementById('loader').style.display='none';
}

/* ---------- Drag-drop image ---------- */
const drop = document.getElementById('uploadDrop');
drop.addEventListener('dragover', e=>{e.preventDefault();drop.style.background='#f0f0f0'});
drop.addEventListener('dragleave', ()=>drop.style.background='');
drop.addEventListener('drop', async e=>{
  e.preventDefault();
  const file = e.dataTransfer.files[0];
  if(!file) return;
  document.getElementById('loader').style.display='block';
  document.getElementById('result').innerHTML='';
  try{
    const base64 = await new Promise((res,rej)=>{
      const reader = new FileReader();
      reader.readAsDataURL(file);
      reader.onload = () => res(reader.result);
      reader.onerror = rej;
    });
    const res = await fetch('https://api.openai.com/v1/chat/completions',{
      method:'POST',
      headers:{
        'Content-Type':'application/json',
        'Authorization':`Bearer ${OPENAI_KEY}`
      },
      body:JSON.stringify({
        model:'gpt-4o-mini',
        messages:[
          {role:'system',content:`Medical imaging assistant. Reply in ${document.getElementById('langSelect').value}. Give 1-line impression + urgency level.`},
          {role:'user',content:[
            {type:'text',text:'Analyse this medical image.'},
            {type:'image_url',image_url:{url:base64}}
          ]}
        ],
        max_tokens:100
      })
    });
    const json = await res.json();
    document.getElementById('result').innerHTML = json.choices[0].message.content;
  }catch(e){
    document.getElementById('result').innerHTML = '⚠️ Image API error.';
  }
  document.getElementById('loader').style.display='none';
});
</script>
</body>
</html>
