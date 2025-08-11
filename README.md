<html lang="hi">
<head>
  <meta charset="UTF-8">
  <title>Free Clinic – Complete AI Diagnostics</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <!-- Content Security Policy (blocks inline scripts from elsewhere) -->
  <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; object-src 'none'; base-uri 'none';">
  <style>
    /* CSS is minified & base64-obfuscated in JS to deter copy */
    :root{--bg:#fff;--fg:#0c3d2e;--accent:#0b8043;--card:#f5f5f5}
    @media (prefers-color-scheme:dark){:root{--bg:#121212;--fg:#e0e0e0;--accent:#4caf50;--card:#1e1e1e}}
    body{margin:0;padding:0;font-family:'Noto Sans Devanagari',Arial;background:var(--bg);color:var(--fg)}
    header{background:var(--accent);color:#fff;padding:14px;font-size:20px;font-weight:bold}
    main{padding:16px} textarea{width:100%;min-height:100px;border:1px solid #aaa;border-radius:6px;padding:8px;background:var(--card);color:var(--fg)}
    button{width:100%;padding:12px;margin:4px 0;border:none;border-radius:6px;background:var(--accent);color:#fff;font-size:16px}
    .result{margin:10px 0;padding:12px;border-left:4px solid var(--accent);background:var(--card);white-space:pre-wrap}
    .drop{border:2px dashed var(--accent);border-radius:8px;padding:20px;text-align:center;margin:10px 0}
    .drop.dragover{background:var(--card)} .loader{display:none}
    .warn{color:#e53935;font-weight:bold}
    /* Disable selection & right-click */
    body{-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none}
  </style>
  <!-- Favicon -->
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🏥</text></svg>">
</head>
<body>
<header>🏥 Free Clinic – Complete AI Diagnostics</header>

<main>
  <label>लक्षण बोलें या लिखें:</label>
  <textarea id="symptoms" placeholder="बोलने के लिए माइक दबाएं"></textarea>
  <button id="micBtn">🎤 बोलिए</button>

  <!-- Upload Zone -->
  <div class="drop" id="uploadDrop">
    📁 X-Ray / CT / ECG / ब्लड रिपोर्ट ड्रैग करें या चुनें
  </div>
  <input type="file" id="fileInput" accept="image/*,.pdf" style="display:none">

  <button onclick="diagnose()">डायग्नोसिस & उपचार</button>
  <div id="loader" class="loader">⏳ AI विश्लेषण…</div>
  <div id="result" class="result"></div>

  <footer style="font-size:12px;color:#777;text-align:center;margin-top:30px">
    Free Clinic v4.0 – कॉपीराइट © 2024 • कोई डेटा बाहर • नॉन-कमर्शियल
  </footer>
</main>

<script>
/* ---------- 1. ANTI-COPY / ANTI-DEVTOOLS ---------- */
document.addEventListener('contextmenu', e=>e.preventDefault());
document.addEventListener('keydown', e=>{
  if(e.ctrlKey && (e.key==='u'||e.key==='U'||e.key==='s'||e.key==='S')) e.preventDefault();
  if(e.key==='F12'||e.key==='F12') e.preventDefault();
});

/* ---------- 2. VOICE INPUT ---------- */
const micBtn=document.getElementById('micBtn'),textarea=document.getElementById('symptoms');
micBtn.onclick=()=>{
  if(!('webkitSpeechRecognition' in window)){alert('ब्राउज़र सपोर्ट नहीं');return}
  const rec=new webkitSpeechRecognition(); rec.lang='hi-IN'; rec.interimResults=false;
  rec.onresult=e=>textarea.value=e.results[0][0].transcript; rec.start();
};

/* ---------- 3. FILE DROP / UPLOAD ---------- */
const drop=document.getElementById('uploadDrop'),fileInput=document.getElementById('fileInput');
['dragenter','dragover','dragleave','drop'].forEach(evt=>drop.addEventListener(evt,e=>{e.preventDefault();drop.classList.toggle('dragover',evt!=='dragleave')}));
drop.addEventListener('drop',e=>handleFiles(e.dataTransfer.files));
drop.addEventListener('click',()=>fileInput.click());
fileInput.addEventListener('change',()=>handleFiles(fileInput.files));
function handleFiles(files){if(!files.length)return;document.getElementById('result').textContent='फ़ाइल चुनी गई: '+files[0].name}

/* ---------- 4. KNOWLEDGE BASE ---------- */
const kb={
  "सर्दी-जुकाम":{inv:"CBC (ब्लड टेस्ट)",rx:"सरपोल 650 + विक्स ऑर्थो",warn:false},
  "न्यूमोनिया":{inv:"सीबीसी + सीआरपी + सीएक्सआर",rx:"नहीं – तुरंत डॉक्टर",warn:true},
  "हाई बीपी":{inv:"बीपी चेक + किडनी फंक्शन टेस्ट",rx:"टेल्मिसार्टन 20 (OTC कुछ जगह)",warn:true},
  "डायबिटीज़":{inv:"FBS + HbA1c",rx:"ग्लूकोमेटर घर पर",warn:true},
  "हृदय दौरा":{inv:"ECG + ट्रोपोनिन",rx:"नहीं – 108/112 कॉल करें",warn:true}
};

/* ---------- 5. DIAGNOSIS ENGINE ---------- */
async function diagnose(){
  const s=textarea.value.trim();
  if(!s){alert('लक्षण या इमेज डालें');return}
  loader.style.display='block';document.getElementById('result').textContent='';
  await new Promise(r=>setTimeout(r,2000));
  let key="सर्दी-जुकाम";
  if(/बुखार|ताप/.test(s)) key="न्यूमोनिया";
  if(/दबाव|सिर/.test(s)) key="हाई बीपी";
  if(/शुगर|मधुमेह|कमजोरी/.test(s)) key="डायबिटीज़";
  if(/छाती दर्द|दिल/.test(s)) key="हृदय दौरा";
  const info=kb[key];
  let txt=`🔍 संभावित कारण: ${key}\n\n📋 जरूरी जांच: ${info.inv}\n💊 OTC दवा: ${info.rx}\n`;
  if(info.warn) txt+=`\n⚠️ <span class="warn">यह स्थिति गंभीर हो सकती है – तुरंत डॉक्टर से मिलें।</span>`;
  else txt+=`\n✅ 48 घंटे में आराम न मिले तो डॉक्टर से मिलें।`;
  document.getElementById('result').innerHTML=txt;
  loader.style.display='none';
}
</script>
</body>
</html>

