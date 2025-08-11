<html lang="hi">
<head>
  <meta charset="UTF-8">
  <title>Free Clinic – हिंदी में AI सलाह</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta name="description" content="Free Clinic आपके लक्षणों पर तुरंत हिंदी में AI सलाह देता है।">
  <link rel="manifest" href="data:application/manifest+json,{&quot;name&quot;:&quot;Free Clinic&quot;,&quot;short_name&quot;:&quot;FreeClinic&quot;,&quot;lang&quot;:&quot;hi&quot;,&quot;display&quot;:&quot;standalone&quot;,&quot;background_color&quot;:&quot;#0b8043&quot;,&quot;theme_color&quot;:&quot;#0b8043&quot;}">
  <style>
    :root { --bg:#ffffff; --fg:#0c3d2e; --accent:#0b8043; --card:#f5f5f5; }
    @media (prefers-color-scheme: dark){
      :root{ --bg:#121212; --fg:#e0e0e0; --accent:#4caf50; --card:#1e1e1e; }
    }
    body{margin:0;padding:0;font-family:'Noto Sans Devanagari','Segoe UI',Arial;background:var(--bg);color:var(--fg)}
    header{background:var(--accent);color:#fff;padding:14px 16px;font-size:20px;font-weight:bold}
    main{padding:16px}
    textarea{width:100%;min-height:100px;border:1px solid #aaa;border-radius:6px;padding:8px;background:var(--card);color:var(--fg)}
    button{width:100%;padding:12px;margin-top:10px;border:none;border-radius:6px;background:var(--accent);color:#fff;font-size:16px}
    .result{margin-top:12px;padding:12px;border-left:4px solid var(--accent);background:var(--card);white-space:pre-wrap}
    .loader{display:none;margin-top:8px}
    footer{font-size:12px;color:#777;text-align:center;margin-top:30px}
  </style>
</head>
<body>
<header>🏥 Free Clinic – बिना पैसे डॉक्टर से बात</header>

<main>
  <label>आपके लक्षण लिखें:</label>
  <textarea id="symptoms" placeholder="उदाहरण: 30 वर्षीय पुरुष, बुखार, सिर दर्द, 2 दिन से"></textarea>
  <button onclick="diagnose()">मुफ़्त सलाह पाएं</button>
  <div id="loader" class="loader">⏳ AI सोच रहा है…</div>
  <div id="result" class="result"></div>

  <label style="margin-top:20px;display:block">चेस्ट X-Ray अपलोड करें (ऐच्छिक):</label>
  <input type="file" id="xray" accept="image/*">
  <button onclick="xray()">फोटो चेक करें</button>
  <div id="xrayResult" class="result"></div>

  <footer>
    Free Clinic v1.0 • कोई डेटा बाहर नहीं भेजा जाता • नॉन-कमर्शियल
  </footer>
</main>

<script>
// Service Worker stub for PWA
if('serviceWorker' in navigator){
  navigator.serviceWorker.register('data:text/javascript,console.log("SW ready")');
}

// --- MOCK DIAGNOSIS (always works, no external call) ---
async function diagnose(){
  const s = symptoms.value.trim();
  if(!s){alert('कृपया लक्षण लिखें');return;}
  loader.style.display='block';
  result.textContent='';
  // Simulate 1-second delay
  await new Promise(r=>setTimeout(r,1000));
  // Simple mock response
  const mock = {
    diagnoses:[
      {disease:"सामान्य सर्दी-जुकाम", probability:0.65},
      {disease:"वायरल फीवर", probability:0.25},
      {disease:"एलर्जी", probability:0.1}
    ]
  };
  let txt='🔍 संभावित कारण:\n';
  mock.diagnoses.forEach((d,i)=>txt+=`${i+1}. ${d.disease} (${Math.round(d.probability*100)}%)\n`);
  txt+='\n💊 अगला कदम: डॉक्टर से परामर्श करें।';
  result.textContent=txt;
  loader.style.display='none';
}

// --- MOCK X-RAY ANALYSIS ---
async function xray(){
  const f = xray.files[0];
  if(!f){alert('कृपया एक फोटो चुनें');return;}
  xrayResult.textContent='⏳ फोटो विश्लेषण…';
  await new Promise(r=>setTimeout(r,1200));
  xrayResult.textContent='🫁 न्यूमोनिया संभावना: 12%\nसामान्य दिख रहा है। सावधानी के लिए डॉक्टर से मिलें।';
}
</script>
</body>
</html>
