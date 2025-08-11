<html lang="auto">
<head>
  <meta charset="UTF-8">
  <title>🏥 Free Clinic – Gemini AI Hospital</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <style>
    :root{--bg:#f0f4f8;--fg:#1e293b;--primary:#0ea5e9}
    body{margin:0;font-family:Inter,Arial;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:var(--fg)}
    header{background:var(--primary);color:#fff;padding:20px;text-align:center;font-size:1.4rem}
    main{max-width:700px;margin:40px auto;padding:20px}
    .card{background:#fff;border-radius:12px;padding:20px;margin-bottom:20px}
    textarea{width:100%;min-height:110px;border:1px solid #d1d5db;border-radius:8px;padding:12px;font-size:1rem}
    button{width:100%;padding:14px;margin:8px 0;border:none;border-radius:8px;background:var(--primary);color:#fff;font-size:1rem;cursor:pointer}
    .result{background:#fff;border-left:4px solid var(--primary);padding:16px;border-radius:8px;margin-top:10px;white-space:pre-wrap}
    footer{background:#111827;color:#fff;padding:20px;text-align:center;font-size:.9rem}
    footer a{color:#7dd3fc;text-decoration:none}
    .loader{display:none;text-align:center}
  </style>
</head>
<body>
<header>🏥 Free Clinic – Gemini AI Hospital</header>

<main>
  <!-- Symptom -->
  <div class="card">
    <label>Symptoms / speak:</label>
    <textarea id="symptoms" placeholder="Type your symptoms…"></textarea>
    <button onclick="symptomDiagnose()">Get Diagnosis & Medicine</button>
  </div>

  <!-- Image -->
  <div class="card">
    <label>Upload X-Ray / ECG / CT / Blood Report</label>
    <input type="file" id="fileInput" accept="image/*,.pdf">
    <button onclick="imageDiagnose()">Analyse Image</button>
  </div>

  <div id="loader" class="loader">⏳ Gemini analysing…</div>
  <div id="result" class="result"></div>
</main>

<footer>
  📞 WhatsApp: <a href="https://wa.me/9779701881529">+977 9701881529</a> | 
  📸 Instagram: <a href="https://instagram.com/itsdrsuyash">@itsdrsuyash</a><br>
  💰 eSewa: <a href="intent://pay?pa=9869051338&pn=FreeClinic&cu=NPR#Intent;scheme=upi;package=com.esewa.android;end">9869051338</a><br>
  💐 In the loving memory of <strong> Late Dr. Bharat Prasad Singh</strong>, Koiladi, Saptari.
</footer>

<script>
/* ---------- Gemini free API ---------- */
/* 1. Symptom diagnosis */
async function symptomDiagnose() {
  const s = document.getElementById('symptoms').value.trim();
  if(!s){alert('Enter symptoms');return}
  document.getElementById('loader').style.display='block';
  document.getElementById('result').innerHTML='';
  try{
    const res = await fetch('https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview:generateContent?key=AIzaSyB6v5f8Y4t2V3d2N3d2N3d2N3d2N3d2N3d2N3',{
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body:JSON.stringify({
        contents:[
          {role:'user',parts:[
            {text:`Emergency AI doctor. Reply in 1 sentence: likely cause, 1 test, 1 OTC med (generic + brand + dose). Language: ${navigator.language}`},
            {text:s}
          ]}
        ],
        generationConfig:{maxOutputTokens:120}
      })
    });
    const json = await res.json();
    document.getElementById('result').innerHTML = json.candidates?.[0]?.content?.parts?.[0]?.text || '⚠️ Unable to analyse.';
  }catch(e){
    document.getElementById('result').innerHTML = '⚠️ Network or API error.';
  }
  document.getElementById('loader').style.display='none';
}

/* 2. Image analysis */
async function imageDiagnose() {
  const file = document.getElementById('fileInput').files[0];
  if(!file){alert('Select an image');return}
  document.getElementById('loader').style.display='block';
  document.getElementById('result').innerHTML='';
  try{
    const base64 = await new Promise((r,e)=>{const reader=new FileReader();reader.readAsDataURL(file);reader.onload=()=>r(reader.result.split(',')[1]);reader.onerror=e;});
    const res = await fetch('https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview:generateContent?key=AIzaSyB6v5f8Y4t2V3d2N3d2N3d2N3d2N3d2N3d2N3',{
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
