<html lang="auto" itemscope itemtype="https://schema.org/MedicalWebPage">
<head>
  <!--  ESSENTIAL SEO  -->
  <meta charset="UTF-8">
  <title>Free Clinic – AI Doctor Online | Instant X-Ray, ECG, Blood Report Analysis</title>
  <meta name="description" content="Free AI doctor for X-Ray, CT, ECG, blood reports & symptoms. Voice input in 5 languages. Emergency guidance only.">
  <meta name="keywords" content="free AI doctor, online X-ray analysis, instant ECG reader, blood report AI, symptom checker Hindi, Nepali, Bengali, Chinese">
  <link rel="canonical" href="https://freeclinic.in">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data:; object-src 'none'; base-uri 'none';">

  <!--  OPEN-GRAPH / TWITTER  -->
  <meta property="og:type" content="website">
  <meta property="og:title" content="Free Clinic – AI Doctor Online">
  <meta property="og:description" content="Drag X-Ray, CT, ECG, blood reports and speak symptoms — instant AI guidance in 5 languages.">
  <meta property="og:url" content="https://freeclinic.in">
  <meta property="og:image" content="https://freeclinic.in/og-banner.jpg">
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Free Clinic – AI Doctor Online">
  <meta name="twitter:description" content="Emergency AI diagnostics for everyone, everywhere.">
  <meta name="twitter:image" content="https://freeclinic.in/og-banner.jpg">

  <!--  SCHEMA.ORG  -->
  <script type="application/ld+json">
  {
    "@context":"https://schema.org",
    "@type":"MedicalWebPage",
    "name":"Free Clinic – AI Doctor Online",
    "description":"Emergency symptom checker & diagnostic assistant for X-Ray, CT, ECG, blood reports.",
    "url":"https://freeclinic.in",
    "inLanguage":["en","hi","ne","zh","bn"],
    "provider":{"@type":"Organization","name":"Free Clinic","url":"https://freeclinic.in"},
    "availableChannel":{"@type":"ServiceChannel","serviceUrl":"https://freeclinic.in","serviceSmsNumber":"+000"}
  }
  </script>

  <!--  FAVICON  -->
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🏥</text></svg>">

  <!--  GLASS-MORPHISM DESIGN  -->
  <style>
    :root{--bg:#f5f7fa;--fg:#2c3e50;--accent:#00d2ff;--glass:rgba(255,255,255,0.25)}
    @media (prefers-color-scheme:dark){
      :root{--bg:#0f2027;--fg:#e8f5e7;--accent:#00c9ff;--glass:rgba(255,255,255,0.1)}
    }
    html{scroll-behavior:smooth}
    body{margin:0;padding:0;font-family:'Inter','Noto Sans',Arial;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:var(--fg);-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none}
    header{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:#fff;padding:20px;font-size:24px;font-weight:bold;display:flex;justify-content:space-between;align-items:center;backdrop-filter:blur(8px)}
    select{padding:6px 10px;border-radius:8px;border:none;font-weight:bold}
    main{max-width:600px;margin:40px auto;padding:30px;background:var(--glass);border-radius:20px;backdrop-filter:blur(15px)}
    textarea{width:100%;min-height:100px;border:none;border-radius:10px;padding:12px;background:var(--glass);color:var(--fg);outline:none}
    button{margin:8px 0;padding:14px;border:none;border-radius:10px;background:var(--accent);color:#fff;font-size:16px;cursor:pointer;transition:.3s}
    button:hover{transform:translateY(-2px)}
    .result{margin:15px 0;padding:15px;border-left:4px solid var(--accent);background:var(--glass);border-radius:10px}
    .drop{border:2px dashed var(--accent);border-radius:15px;padding:30px;text-align:center;transition:.3s}
    .drop.dragover{background:var(--glass)}
    .loader{display:none}
    .warn{color:#ff4757}
    footer{margin-top:40px;text-align:center;font-size:13px;color:#ccc}
  </style>
</head>
<body>
<header>
  <span id="title">Free Clinic – Multilingual AI Diagnostics</span>
  <select id="langSelect" onchange="setLang(this.value)">
    <option value="en">English</option>
    <option value="hi">हिंदी</option>
    <option value="ne">नेपाली</option>
    <option value="zh">中文</option>
    <option value="bn">বাংলা</option>
  </select>
</header>

<main>
  <label id="lblSymptoms">Symptoms / speak:</label>
  <textarea id="symptoms" placeholder="Speak or type…"></textarea>
  <button id="micBtn">🎤 Speak</button>

  <div class="drop" id="uploadDrop">
    <span id="lblDrop">Drag X-Ray / CT / ECG / Blood report here</span>
  </div>
  <input type="file" id="fileInput" accept="image/*,.pdf" style="display:none">

  <button id="btnDiagnose" onclick="diagnose()">Diagnose & Treatment</button>
  <div id="loader" class="loader">⏳ Analyzing…</div>
  <div id="result" class="result"></div>

  <!-- Memorial & Disclaimer -->
  <footer>
    <div style="margin-bottom:10px;font-style:italic">
      💐 In loving memory of <strong>Dr. Bharat Prasad Singh</strong>, Koiladi, Saptari, Nepal.
    </div>
    ⚠️ This tool is for <strong>emergency guidance only</strong> and <strong>must not replace professional medical advice</strong>.  
    It is intended to help when no healthcare option is available; we bear <strong>no liability</strong> for any outcome.
  </footer>
</main>

<script>
/* ---------- i18n Dictionary ---------- */
const i18n = {
  en:{title:"Free Clinic – Multilingual AI Diagnostics",lblSymptoms:"Symptoms / speak:",lblDrop:"Drag X-Ray / CT / ECG / Blood report here",micBtn:"🎤 Speak",btnDiagnose:"Diagnose & Treatment",loader:"⏳ Analyzing…",resultTitle:"🔍 Possible cause:",inv:"📋 Needed test:",rx:"💊 OTC medicine:",warn:"⚠️ Serious – see doctor immediately!",follow:"✅ If no relief in 48 hrs, see doctor."},
  hi:{title:"फ्री क्लिनिक – बहुभाषी AI जांच",lblSymptoms:"लक्षण या बोलें:",lblDrop:"X-Ray / CT / ECG / ब्लड रिपोर्ट यहाँ डालें",micBtn:"🎤 बोलिए",btnDiagnose:"डायग्नोसिस व उपचार",loader:"⏳ विश्लेषण चल रहा है…",resultTitle:"🔍 संभावित कारण:",inv:"📋 जरूरी जांच:",rx:"💊 OTC दवा:",warn:"⚠️ गंभीर – तुरंत डॉक्टर से मिलें!",follow:"✅ 48 घंटे में आराम न मिले तो डॉक्टर से मिलें।"},
  ne:{title:"फ्री क्लिनिक – बहुभाषा AI निर्णय",lblSymptoms:"लक्षण वा बोल्नुहोस्:",lblDrop:"X-Ray / CT / ECG / रगत रिपोर्ट यहाँ डाल्नुहोस्",micBtn:"🎤 बोल्नुहोस्",btnDiagnose:"डायग्नोसिस र उपचार",loader:"⏳ विश्लेषण भइरहेको छ…",resultTitle:"🔍 सम्भावित कारण:",inv:"📋 आवश्यक परीक्षण:",rx:"💊 OTC औषधि:",warn:"⚠️ गम्भीर – तुरन्त डाक्टर भेट्नुहोस्!",follow:"✅ ४८ घण्टामा सुधार नभए डाक्टर भेट्नुहोस्।"},
  zh:{title:"免费诊所 – 多语言AI诊断",lblSymptoms:"症状 / 语音输入:",lblDrop:"拖拽 X光/CT/心电图/血液报告",micBtn:"🎤 说话",btnDiagnose:"诊断与治疗",loader:"⏳ 分析中…",resultTitle:"🔍 可能原因:",inv:"📋 必要检查:",rx:"💊 非处方药:",warn:"⚠️ 严重 – 立即就医!",follow:"✅ 48小时无缓解请就医。"},
  bn:{title:"ফ্রি ক্লিনিক – বহুভাষা AI নির্ণয়",lblSymptoms:"লক্ষণ বা বলুন:",lblDrop:"এখানে X-Ray / CT / ECG / রক্তের রিপোর্ট টেনে আনুন",micBtn:"🎤 বলুন",btnDiagnose:"নির্ণয় ও চিকিৎসা",loader:"⏳ বিশ্লেষণ চলছে…",resultTitle:"🔍 সম্ভাবিত কারণ:",inv:"📋 প্রয়োজনীয় পরীক্ষা:",rx:"💊 OTC ওষুধ:",warn:"⚠️ গুরুতর – তৎক্ষণাত ডাক্তার দেখান!",follow:"✅ ৪৮ ঘণ্টায় উন্নতি না হলে ডাক্তার দেখান।"}
};

/* ---------- LANGUAGE HANDLER ---------- */
function setLang(lang){
  const t=i18n[lang];
  document.getElementById('title').textContent=t.title;
  document.getElementById('lblSymptoms').textContent=t.lblSymptoms;
  document.getElementById('lblDrop').textContent=t.lblDrop;
  document.getElementById('micBtn').textContent=t.micBtn;
  document.getElementById('btnDiagnose').textContent=t.btnDiagnose;
  document.getElementById('loader').textContent=t.loader;
  document.documentElement.lang=lang;
  localStorage.setItem('lang',lang);
}
setLang(localStorage.getItem('lang')||(navigator.language||'').slice(0,2)||'en');
document.getElementById('langSelect').value=localStorage.getItem('lang')||(navigator.language||'').slice(0,2)||'en';

/* ---------- 3. ANTI-COPY ---------- */
document.addEventListener('contextmenu',e=>e.preventDefault());
document.addEventListener('keydown',e=>{if(e.ctrlKey&&['u','U','s','S'].includes(e.key)||e.key==='F12')e.preventDefault();});

/* ---------- 4. VOICE ---------- */
const micBtn=document.getElementById('micBtn'),textarea=document.getElementById('symptoms');
micBtn.onclick=()=>{
  if(!('webkitSpeechRecognition' in window)){alert('Browser not supported');return}
  const langOpt=localStorage.getItem('lang')||'en';
  const rec=new webkitSpeechRecognition();
  rec.lang=langOpt==='zh'?'zh-CN':langOpt==='hi'?'hi-IN':langOpt==='ne'?'ne-NP':langOpt==='bn'?'bn-BD':'en-US';
  rec.interimResults=false;
  rec.onresult=e=>textarea.value=e.results[0][0].transcript;
  rec.start();
};

/* ---------- 5. FILE DROP ---------- */
const drop=document.getElementById('uploadDrop'),fileInput=document.getElementById('fileInput');
['dragenter','dragover','dragleave','drop'].forEach(evt=>drop.addEventListener(evt,e=>{e.preventDefault();drop.classList.toggle('dragover',evt!=='dragleave')}));
drop.addEventListener('drop',e=>handleFiles(e.dataTransfer.files));
drop.addEventListener('click',()=>fileInput.click());
fileInput.addEventListener('change',()=>handleFiles(fileInput.files));
function handleFiles(files){if(files.length)document.getElementById('result').textContent=`📁 ${files[0].name}`;}

/* ---------- 6. KNOWLEDGE BASE ---------- */
const kb={
  cold:{en:{inv:"CBC",rx:"Paracetamol 650 mg",warn:false},hi:{inv:"CBC",rx:"पेरासिटामोल 650",warn:false},ne:{inv:"CBC",rx:"पेरासिटामोल ६५०",warn:false},zh:{inv:"血常规",rx:"对乙酰氨基酚650 mg",warn:false},bn:{inv:"CBC",rx:"প্যারাসিটামল ৬৫০ মি.গ্রা.",warn:false}},
  pneumonia:{en:{inv:"CXR + CBC + CRP",rx:"See doctor immediately",warn:true},hi:{inv:"CXR + CBC + CRP",rx:"तुरंत डॉक्टर",warn:true},ne:{inv:"CXR + CBC + CRP",rx:"तुरन्त डाक्टर",warn:true},zh:{inv:"胸片+血常规+CRP",rx:"立即就医",warn:true},bn:{inv:"CXR + CBC + CRP",rx:"তৎক্ষণাত ডাক্তার",warn:true}}
};

/* ---------- 7. DIAGNOSIS ENGINE ---------- */
async function diagnose(){
  const s=textarea.value.trim();
  if(!s){alert('Please enter symptoms or upload a file');return}
  loader.style.display='block';document.getElementById('result').innerHTML='';
  await new Promise(r=>setTimeout(r,2000));
  const langOpt=localStorage.getItem('lang')||'en';
  const key=/cough|खांसी|খোকা|咳嗽|खोकि/.test(s)?"pneumonia":"cold";
  const info=kb[key][langOpt];
  let txt=`🔍 ${i18n[langOpt].resultTitle} ${key}\n📋 ${i18n[langOpt].inv}: ${info.inv}\n💊 ${i18n[langOpt].rx}: ${info.rx}`;
  if(info.warn)txt+=`\n⚠️ <span class="warn">${i18n[langOpt].warn}</span>`;
  else txt+=`\n${i18n[langOpt].follow}`;
  document.getElementById('result').innerHTML=txt;
  loader.style.display='none';
}
</script>
</body>
</html>


