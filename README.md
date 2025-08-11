<html lang="en" itemscope itemtype="https://schema.org/MedicalWebPage">
<head>
  <meta charset="UTF-8">
  <title>Free Clinic – AI Doctor Online (Fixed)</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <style>
    :root{--bg:#f5f7fa;--fg:#2c3e50;--accent:#00d2ff}
    body{margin:0;padding:0;font-family:Inter,Arial;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:var(--fg)}
    header{background:var(--accent);color:#fff;padding:15px;font-size:22px;text-align:center}
    select{margin-left:10px;padding:4px;border-radius:4px;border:none}
    main{max-width:600px;margin:40px auto;padding:20px;background:#fff;border-radius:12px}
    textarea{width:100%;min-height:100px;border:1px solid #ccc;border-radius:6px;padding:8px}
    button{width:100%;padding:12px;margin:8px 0;border:none;border-radius:6px;background:var(--accent);color:#fff;font-size:16px;cursor:pointer}
    .result{margin:15px 0;padding:12px;border-left:4px solid var(--accent);background:#f5f5f5}
    .drop{border:2px dashed var(--accent);border-radius:8px;padding:20px;text-align:center}
    .drop.dragover{background:#f0f0f0}
    footer{text-align:center;font-size:13px;color:#555;margin-top:30px}
  </style>
</head>
<body>
<header>
  Free Clinic – AI Doctor <select id="langSelect"></select>
</header>

<main>
  <label>Symptoms / speak:</label>
  <textarea id="symptoms" placeholder="Type your symptoms…"></textarea>
  <button id="micBtn">🎤 Speak</button>

  <div class="drop" id="uploadDrop">
    Drag X-Ray / CT / ECG / Blood report here
  </div>
  <input type="file" id="fileInput" accept="image/*,.pdf" style="display:none">

  <button onclick="diagnose()">Diagnose & Treatment</button>
  <div id="loader" style="display:none">⏳ ChatGPT analysing…</div>
  <div id="result" class="result"></div>
</main>

<script>
/* ---------- Language list ---------- */
const langs = [
  {code:'en',name:'English'},
  {code:'hi',name:'हिंदी'},
  {code:'ne',name:'नेपाली'},
  {code:'zh',name:'中文'},
  {code:'bn',name:'বাংলা'},
  {code:'es',name:'Español'},
  {code:'fr',name:'Français'},
  {code:'ar',name:'العربية'}
];

const select = document.getElementById('langSelect');
langs.forEach(l=>{
  const opt = document.createElement('option');
  opt.value = l.code;
  opt.textContent = l.name;
  select.appendChild(opt);
});

/* ---------- ChatGPT powered ---------- */
const OPENAI_KEY = 'sk-YOUR-OPENAI-KEY-HERE'; // ← paste your key

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
          {role:'system',content:`You are an emergency AI doctor. Reply in ${select.value}. Give 1 likely cause, 1 essential test, 1 OTC medicine (with generic name + brand in brackets) and warn to see doctor if serious. Keep under 80 words.`},
          {role:'user',content:s}
        ],
        max_tokens:120
      })
    });
    const json = await res.json();
    document.getElementById('result').innerHTML = json.choices[0].message.content;
  }catch(e){
    document.getElementById('result').innerHTML = '⚠️ API error – please check your OpenAI key or network.';
  }
  document.getElementById('loader').style.display='none';
}

/* ---------- Voice input ---------- */
document.getElementById('micBtn').onclick = () => {
  if(!('webkitSpeechRecognition' in window)){alert('Browser not supported');return}
  const rec = new webkitSpeechRecognition();
  rec.lang = select.value==='zh'?'zh-CN':select.value==='hi'?'hi-IN':select.value==='ne'?'ne-NP':select.value==='bn'?'bn-BD':'en-US';
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
  const file=e.dataTransfer.files[0];
  if(file)alert('Image upload ready – add file-upload logic or paste key.');
});
</script>
</body>
</html>
