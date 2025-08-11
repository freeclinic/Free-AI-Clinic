<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>🏥 Free Clinic – Offline AI Hospital</title>
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
    .loader{display:none;text-align:center;margin:10px 0}
  </style>
</head>
<body>
<header>🏥 Free Clinic – Offline AI Hospital</header>

<main>
  <div class="card">
    <label>Symptoms / speak:</label>
    <textarea id="symptoms" placeholder="Type your symptoms…"></textarea>
    <button onclick="diagnose()">Get Diagnosis & Medicine</button>
  </div>

  <div class="card">
    <label>Upload X-Ray / ECG / CT / Blood Report</label>
    <input type="file" id="fileInput" accept="image/*,.pdf" onchange="imageDiagnose()">
  </div>

  <div id="loader" class="loader">⏳ AI analysing…</div>
  <div id="result" class="result"></div>
</main>

<footer>
  📞 WhatsApp: <a href="https://wa.me/9779701881529">+977 9701881529</a> | 
  📸 Instagram: <a href="https://instagram.com/itsdrsuyash">@itsdrsuyash</a><br>
  💰 eSewa: <a href="intent://pay?pa=9869051338&pn=FreeClinic&cu=NPR#Intent;scheme=upi;package=com.esewa.android;end">9869051338</a><br>
  💐 In loving memory of <strong>Dr. Bharat Prasad Singh</strong>, Koiladi, Saptari.
</footer>

<script>
/* ---------- Symptom Diagnosis (Offline) ---------- */
const kb = {
  cold:{cause:'Common cold',test:'None',med:'Paracetamol 500 mg + Cetirizine 10 mg (brand: Cetzine)'},
  fever:{cause:'Viral fever',test:'CBC',med:'Paracetamol 650 mg (brand: Crocin)'},
  cough:{cause:'Acute bronchitis',test:'Chest X-ray',med:'Dextromethorphan 10 ml syrup (brand: Corex)'},
  chestpain:{cause:'Rule out MI',test:'ECG',med:'Aspirin 75 mg (brand: Ecosprin) – see doctor'}
};
function diagnose() {
  const s = document.getElementById('symptoms').value.toLowerCase();
  document.getElementById('loader').style.display='block';
  document.getElementById('result').innerHTML='';
  setTimeout(()=>{
    let key = 'cold';
    if(/fever|ताप|fiebre/.test(s)) key='fever';
    if(/cough|खांसी|tos/.test(s)) key='cough';
    if(/chest|दिल|pecho/.test(s)) key='chestpain';
    const info = kb[key];
    document.getElementById('result').innerHTML =
      `🔍 Likely cause: ${info.cause}\n📋 Needed test: ${info.test}\n💊 OTC: ${info.med}\n⚠️ If serious – see doctor immediately.`;
    document.getElementById('loader').style.display='none';
  },800);
}

/* ---------- Image Diagnosis (Offline) ---------- */
function imageDiagnose() {
  const file = document.getElementById('fileInput').files[0];
  if(!file) return;
  document.getElementById('loader').style.display='block';
  setTimeout(()=>{
    document.getElementById('result').innerHTML =
      '⚠️ Image analysis needs paid AI; upload to nearest hospital for radiologist review.';
    document.getElementById('loader').style.display='none';
  },800);
}
</script>
</body>
</html>
