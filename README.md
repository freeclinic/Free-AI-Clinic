<html lang="auto" itemscope itemtype="https://schema.org/MedicalWebPage">
<head>
  <meta charset="UTF-8">
  <title>Free Clinic – AI Doctor Online | 48 Languages | ChatGPT Powered</title>
  <meta name="description" content="Emergency AI diagnostics in 48 languages powered by ChatGPT-4. Upload X-Ray, ECG, CT, blood reports or speak symptoms for instant generic+brand medicine advice.">
  <meta name="keywords" content="free AI doctor, ChatGPT medical diagnosis, 48 language symptom checker, X-Ray analysis, ECG reader, generic medicine worldwide">
  <link rel="canonical" href="https://freeclinic.in">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data:; object-src 'none'; base-uri 'none';">
  <meta property="og:type" content="website">
  <meta property="og:title" content="Free Clinic – AI Doctor Online">
  <meta property="og:description" content="Emergency AI diagnostics in 48 languages powered by ChatGPT-4. Upload X-Ray, ECG, CT, blood reports or speak symptoms for instant generic+brand medicine advice.">
  <meta property="og:url" content="https://freeclinic.in">
  <meta property="og:image" content="https://freeclinic.in/og-banner.jpg">
  <meta name="twitter:card" content="summary_large_image">
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🏥</text></svg>">
  <style>
    :root{--bg:#f5f7fa;--fg:#2c3e50;--accent:#00d2ff;--glass:rgba(255,255,255,.25)}
    @media (prefers-color-scheme:dark){:root{--bg:#0f2027;--fg:#e8f5e7;--accent:#00c9ff;--glass:rgba(255,255,255,.1)}}
    body{margin:0;padding:0;font-family:Inter,'Noto Sans',Arial;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:var(--fg);-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none}
    header{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:#fff;padding:20px;font-size:24px;font-weight:bold;display:flex;justify-content:space-between;align-items:center;backdrop-filter:blur(8px)}
    select{padding:6px 10px;border-radius:8px;border:none;font-weight:bold}
    main{max-width:700px;margin:40px auto;padding:30px;background:var(--glass);border-radius:20px;backdrop-filter:blur(15px)}
    textarea{width:100%;min-height:100px;border:none;border-radius:10px;padding:12px;background:var(--glass);color:var(--fg);outline:none}
    button{margin:8px 0;padding:14px;border:none;border-radius:10px;background:var(--accent);color:#fff;font-size:16px;cursor:pointer;transition:.3s}
    button:hover{transform:translateY(-2px)}
    .result{margin:15px 0;padding:15px;border-left:4px solid var(--accent);background:var(--glass);border-radius:10px}
    .drop{border:2px dashed var(--accent);border-radius:15px;padding:30px;text-align:center;transition:.3s}
    .drop.dragover{background:var(--glass)} .loader{display:none}
    .warn{color:#ff4757}
    footer{margin-top:40px;text-align:center;font-size:13px;color:#ccc}
  </style>
</head>
<body>
<header>
  <span id="title">Free Clinic – AI Doctor Online</span>
  <select id="langSelect" onchange="setLang(this.value)"></select>
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
  <div id="loader" class="loader">⏳ ChatGPT analysing…</div>
  <div id="result" class="result"></div>

  <!-- CONTACT & DONATIONS -->
  <div style="margin:25px 0;text-align:center;font-size:14px;background:#ffffff22;padding:15px;border-radius:12px">
    📞 <strong>Ads / WhatsApp:</strong> <a href="https://wa.me/9779701881529" style="color:#00d2ff">+977&nbsp;9701-881529</a><br>
    📸 <strong>Instagram:</strong> <a href="https://instagram.com/itsdrsuyash" style="color:#00d2ff">@itsdrsuyash</a><br>
    💰 <strong>eSewa donation:</strong> <a href="intent://pay?pa=9869051338&pn=FreeClinic&cu=NPR#Intent;scheme=upi;package=com.esewa.android;end" style="color:#00d2ff">9869051338</a>
  </div>

  <!-- Memorial & Disclaimer -->
  <footer>
    <div style="margin-bottom:10px;font-style:italic">
      💐 In loving memory of <strong>Dr. Bharat Prasad Singh</strong>, Koiladi, Saptari.
    </div>
    ⚠️ This tool is for <strong>emergency guidance only</strong> and <strong>must not replace professional medical advice</strong>.<br>
    It is intended to help when no healthcare option is available; we bear <strong>no liability</strong> for any outcome.
  </footer>
</main>

<script>
/* ---------- 48-LANGUAGE i18n Dictionary ---------- */
const i18n = {
  en:{title:"Free Clinic – AI Doctor Online",lblSymptoms:"Symptoms / speak:",lblDrop:"Drag X-Ray / CT / ECG / Blood report here",micBtn:"🎤 Speak",btnDiagnose:"Diagnose & Treatment",loader:"⏳ ChatGPT analysing…",resultTitle:"🔍 Possible cause:",inv:"📋 Needed test:",rx:"💊 OTC medicine:",warn:"⚠️ Serious – see doctor immediately!",follow:"✅ If no relief in 48 hrs, see doctor."},
  hi:{title:"फ्री क्लिनिक – AI डॉक्टर ऑनलाइन",lblSymptoms:"लक्षण या बोलें:",lblDrop:"X-Ray / CT / ECG / ब्लड रिपोर्ट यहाँ डालें",micBtn:"🎤 बोलिए",btnDiagnose:"डायग्नोसिस व उपचार",loader:"⏳ ChatGPT विश्लेषण…",resultTitle:"🔍 संभावित कारण:",inv:"📋 जरूरी जांच:",rx:"💊 OTC दवा:",warn:"⚠️ गंभीर – तुरंत डॉक्टर से मिलें!",follow:"✅ 48 घंटे में आराम न मिले तो डॉक्टर से मिलें।"},
  ne:{title:"फ्री क्लिनिक – AI डाक्टर अनलाइन",lblSymptoms:"लक्षण वा बोल्नुहोस्:",lblDrop:"X-Ray / CT / ECG / रगत रिपोर्ट यहाँ डाल्नुहोस्",micBtn:"🎤 बोल्नुहोस्",btnDiagnose:"डायग्नोसिस र उपचार",loader:"⏳ ChatGPT विश्लेषण…",resultTitle:"🔍 सम्भावित कारण:",inv:"📋 आवश्यक परीक्षण:",rx:"💊 OTC औषधि:",warn:"⚠️ गम्भीर – तुरन्त डाक्टर भेट्नुहोस्!",follow:"✅ ४८ घण्टामा सुधार नभए डाक्टर भेट्नुहोस्।"},
  zh:{title:"免费诊所 – AI医生在线",lblSymptoms:"症状 / 语音输入:",lblDrop:"拖拽 X光/CT/心电图/血液报告",micBtn:"🎤 说话",btnDiagnose:"诊断与治疗",loader:"⏳ ChatGPT 分析中…",resultTitle:"🔍 可能原因:",inv:"📋 必要检查:",rx:"💊 非处方药:",warn:"⚠️ 严重 – 立即就医!",follow:"✅ 48小时无缓解请就医。"},
  bn:{title:"ফ্রি ক্লিনিক – AI ডাক্তার অনলাইন",lblSymptoms:"লক্ষণ বা বলুন:",lblDrop:"এখানে X-Ray / CT / ECG / রক্তের রিপোর্ট টেনে আনুন",micBtn:"🎤 বলুন",btnDiagnose:"নির্ণয় ও চিকিৎসা",loader:"⏳ ChatGPT বিশ্লেষণ…",resultTitle:"🔍 সম্ভাবিত কারণ:",inv:"📋 প্রয়োজনীয় পরীক্ষা:",rx:"💊 OTC ওষুধ:",warn:"⚠️ গুরুতর – তৎক্ষণাত ডাক্তার দেখান!",follow:"✅ ৪৮ ঘন্টায় উন্নতি না হলে ডাক্তার দেখান।"},
  es:{title:"Clínica Gratis – Doctor IA en línea",lblSymptoms:"Síntomas / hablar:",lblDrop:"Arrastra radiografía / TC / ECG / informe de sangre aquí",micBtn:"🎤 Hablar",btnDiagnose:"Diagnóstico y tratamiento",loader:"⏳ ChatGPT analizando…",resultTitle:"🔍 Posible causa:",inv:"📋 Prueba necesaria:",rx:"💊 Medicamento OTC:",warn:"⚠️ Grave – ¡consulte al médico!",follow:"✅ Si no mejora en 48h, consulte."},
  fr:{title:"Clinique Gratuite – Docteur IA en ligne",lblSymptoms:"Symptômes / parler:",lblDrop:"Glissez radio / CT / ECG / bilan sanguin ici",micBtn:"🎤 Parler",btnDiagnose:"Diagnostic et traitement",loader:"⏳ ChatGPT analyse…",resultTitle:"🔍 Cause probable:",inv:"📋 Test nécessaire:",rx:"💊 Médicament OTC:",warn:"⚠️ Grave – voir médecin!",follow:"✅ Si pas de mieux en 48 h, voir médecin."},
  ar:{title:"العيادة المجانية – طبيب ذكاء اصطناعي",lblSymptoms:"الأعراض / التحدث:",lblDrop:"اسحب الأشعة / CT / ECG / تحليل الدم هنا",micBtn:"🎤 تحدث",btnDiagnose:"التشخيص والعلاج",loader:"⏳ ChatGPT يحلل…",resultTitle:"🔍 السبب المحتمل:",inv:"📋 الفحص المطلوب:",rx:"💊 دواء بدون وصفة:",warn:"⚠️ خطير – اذهب إلى الطبيب فورًا!",follow:"✅ إذا لم يتحسن خلال 48 ساعة، اذهب للطبيب."},
  ru:{title:"Бесплатная Клиника – AI Доктор онлайн",lblSymptoms:"Симптомы / говорите:",lblDrop:"Перетащите рентген / КТ / ЭКГ / анализ крови",micBtn:"🎤 Говорить",btnDiagnose:"Диагностика и лечение",loader:"⏳ ChatGPT анализирует…",resultTitle:"🔍 Возможная причина:",inv:"📋 Необходимый тест:",rx:"💊 OTC препарат:",warn:"⚠️ Серьёзно – срочно к врачу!",follow:"✅ При отсутствии улучшения через 48 ч – к врачу."},
  pt:{title:"Clínica Grátis – Médico IA online",lblSymptoms:"Sintomas / falar:",lblDrop:"Arraste raio-X / CT / ECG / exame de sangue aqui",micBtn:"🎤 Falar",btnDiagnose:"Diagnóstico e tratamento",loader:"⏳ ChatGPT analisando…",resultTitle:"🔍 Possível causa:",inv:"📋 Teste necessário:",rx:"💊 Medicamento OTC:",warn:"⚠️ Grave – veja um médico!",follow:"✅ Se não melhorar em 48 h, consulte."},
  de:{title:"Kostenlose Klinik – KI-Ärztin online",lblSymptoms:"Symptome / sprechen:",lblDrop:"Röntgen / CT / EKG / Blutbild hier ablegen",micBtn:"🎤 Sprechen",btnDiagnose:"Diagnose & Behandlung",loader:"⏳ ChatGPT analysiert…",resultTitle:"🔍 Mögliche Ursache:",inv:"📋 Benötigter Test:",rx:"💊 OTC-Medikament:",warn:"⚠️ Ernst – sofort zum Arzt!",follow:"✅ Bei keiner Besserung in 48 h, Arzt."},
  ja:{title:"無料クリニック – AI医師オンライン",lblSymptoms:"症状 / 話す:",lblDrop:"X線 / CT / ECG / 血液検査をドラッグ",micBtn:"🎤 話す",btnDiagnose:"診断と治療",loader:"⏳ ChatGPT 分析中…",resultTitle:"🔍 考えられる原因:",inv:"📋 必要な検査:",rx:"💊 OTC薬:",warn:"⚠️ 深刻 – 医師へ!",follow:"✅ 48時間改善なしで医師へ。"},
  ko:{title:"무료 클리닉 – AI 의사 온라인",lblSymptoms:"증상 / 말하기:",lblDrop:"여기에 X선 / CT / 심전도 / 혈액 검사 드래그",micBtn:"🎤 말하기",btnDiagnose:"진단 및 치료",loader:"⏳ ChatGPT 분석 중…",resultTitle:"🔍 가능한 원인:",inv:"📋 필요한 검사:",rx:"💊 OTC 약:",warn:"⚠️ 심각 – 즉시 의사!",follow:"✅ 48시간 개선 없으면 의사."},
  it:{title:"Clinica Gratuita – Dottore IA online",lblSymptoms:"Sintomi / parlare:",lblDrop:"Trascina radiografia / TC / ECG / emocromo qui",micBtn:"🎤 Parlare",btnDiagnose:"Diagnosi e trattamento",loader:"⏳ ChatGPT analizza…",resultTitle:"🔍 Possibile causa:",inv:"📋 Test necessario:",rx:"💊 Farmaco OTC:",warn:"⚠️ Grave – vedi medico!",follow:"✅ Se non migliora in 48 h, vedi medico."},
  tr:{title:"Ücretsiz Klinik – AI Doktor çevrimiçi",lblSymptoms:"Belirtiler / konuş:",lblDrop:"X-ray / BT / EKG / kan tahlili sürükle buraya",micBtn:"🎤 Konuş",btnDiagnose:"Tanı ve tedavi",loader:"⏳ ChatGPT analiz ediyor…",resultTitle:"🔍 Olası neden:",inv:"📋 Gerekli test:",rx:"💊 OTC ilaç:",warn:"⚠️ Ciddi – hemen doktor!",follow:"✅ 48 saatte düzelme yoksa doktor."},
  th:{title:"คลินิกฟรี – หมอ AI ออนไลน์",lblSymptoms:"อาการ / พูด:",lblDrop:"ลาก X-ray / CT / ECG / รายงานเลือดที่นี่",micBtn:"🎤 พูด",btnDiagnose:"วินิจฉัยและรักษา",loader:"⏳ ChatGPT วิเคราะห์…",resultTitle:"🔍 สาเหตุที่เป็นไปได้:",inv:"📋 การทดสอบที่ต้อง:",rx:"💊 ยา OTC:",warn:"⚠️ ร้ายแรง – พบแพทย์ทันที!",follow:"✅ หากไม่ดีขึ้นใน 48 ชม. พบแพทย์."},
  vi:{title:"Phòng Khám Miễn Phí – Bác Sĩ AI Trực Tuyến",lblSymptoms:"Triệu chứng / nói:",lblDrop:"Kéo X-quang / CT / ECG / báo cáo máu vào đây",micBtn:"🎤 Nói",btnDiagnose:"Chẩn đoán và điều trị",loader:"⏳ ChatGPT đang phân tích…",resultTitle:"🔍 Nguyên nhân có thể:",inv:"📋 Xét nghiệm cần thiết:",rx:"💊 Thuốc OTC:",warn:"⚠️ Nghiêm trọng – gặp bác sĩ ngay!",follow:"✅ Nếu không cải thiện trong 48 giờ, gặp bác sĩ."},
  pl:{title:"Darmowa Klinika – AI Lekarz online",lblSymptoms:"Objawy / mów:",lblDrop:"Przeciągnij rtg / CT / EKG / morfologię tutaj",micBtn:"🎤 Mów",btnDiagnose:"Diagnoza i leczenie",loader:"⏳ ChatGPT analizuje…",resultTitle:"🔍 Możliwa przyczyna:",inv:"📋 Wymagany test:",rx:"💊 Lek OTC:",warn:"⚠️ Poważne – natychmiast do lekarza!",follow:"✅ Brak poprawy w 48 h – lekarz."},
  uk:{title:"Безкоштовна Клініка – AI Лікар онлайн",lblSymptoms:"Симптоми / говоріть:",lblDrop:"Перетягніть рентген / КТ / ЕКГ / аналіз крові",micBtn:"🎤 Говорити",btnDiagnose:"Діагностика та лікування",loader:"⏳ ChatGPT аналізує…",resultTitle:"🔍 Можлива причина:",inv:"📋 Необхідний тест:",rx:"💊 Ліки OTC:",warn:"⚠️ Серйозно – негайно до лікаря!",follow:"✅ Якщо немає поліпшення за 48 год – до лікаря."},
  nl:{title:"Gratis Kliniek – AI Dokter online",lblSymptoms:"Symptomen / spreken:",lblDrop:"Sleep X-ray / CT / ECG / bloedonderzoek hier",micBtn:"🎤 Spreken",btnDiagnose:"Diagnose en behandeling",loader:"⏳ ChatGPT analyseert…",resultTitle:"🔍 Mogelijke oorzaak:",inv:"📋 Benodigde test:",rx:"💊 OTC-medicijn:",warn:"⚠️ Ernstig – meteen naar dokter!",follow:"✅ Geen verbetering in 48 uur, dokter."},
  sv:{title:"Gratis Klinik – AI Läkare online",lblSymptoms:"Symptom / tala:",lblDrop:"Dra röntgen / CT / EKG / blodprov hit",micBtn:"🎤 Tala",btnDiagnose:"Diagnos och behandling",loader:"⏳ ChatGPT analyserar…",resultTitle:"🔍 Möjlig orsak:",inv:"📋 Nödvändigt test:",rx:"💊 OTC-läkemedel:",warn:"⚠️ Allvarligt – se läkare omedelbart!",follow:"✅ Ingen förbättring inom 48 h, se läkare."},
  da:{title:"Gratis Klinik – AI Læge online",lblSymptoms:"Symptomer / tale:",lblDrop:"Træk røntgen / CT / EKG / blodprøve her",micBtn:"🎤 Tale",btnDiagnose:"Diagnose og behandling",loader:"⏳ ChatGPT analyserer…",resultTitle:"🔍 Mulig årsag:",inv:"📋 Nødvendig test:",rx:"💊 OTC-medicin:",warn:"⚠️ Alvorlig – se læge nu!",follow:"✅ Ingen bedring i 48 timer, se læge."},
  no:{title:"Gratis Klinikk – AI Lege online",lblSymptoms:"Symptomer / snakk:",lblDrop:"Dra røntgen / CT / EKG / blodprøve hit",micBtn:"🎤 Snakk",btnDiagnose:"Diagnose og behandling",loader:"⏳ ChatGPT analyserer…",resultTitle:"🔍 Mulig årsak:",inv:"📋 Nødvendig test:",rx:"💊 OTC-medisin:",warn:"⚠️ Alvorlig – se lege med en gang!",follow:"✅ Ingen bedring i 48 timer, se lege."},
  fi:{title:"Ilmainen Klinikka – AI Lääkäri verkossa",lblSymptoms:"Oireet / puhu:",lblDrop:"Vedä röntgen / CT / EKG / verikoe tänne",micBtn:"🎤 Puhu",btnDiagnose:"Diagnoosi ja hoito",loader:"⏳ ChatGPT analysoi…",resultTitle:"🔍 Mahdollinen syy:",inv:"📋 Vaadittu testi:",rx:"💊 OTC-lääke:",warn:"⚠️ Vakava – näe lääkäri heti!",follow:"✅ Ei parannusta 48 h, näe lääkäri."},
  el:{title:"Δωρεάν Κλινική – Γιατρός AI online",lblSymptoms:"Συμπτώματα / μιλήστε:",lblDrop:"Σύρετε ακτινογραφία / CT / ECG / αίμα εδώ",micBtn:"🎤 Μιλήστε",btnDiagnose:"Διάγνωση και θεραπεία",loader:"⏳ ChatGPT αναλύει…",resultTitle:"🔍 Πιθανή αιτία:",inv:"📋 Απαραίτητη εξέταση:",rx:"💊 OTC φάρμακο:",warn:"⚠️ Σοβαρό – δείτε γιατρό άμεσα!",follow:"✅ Αν δεν υπάρξει βελτίωση σε 48 ώρες, δείτε γιατρό."},
  hu:{title:"Ingyenes Klinika – AI Orvos online",lblSymptoms:"Tünetek / beszéljen:",lblDrop:"Húzza ide röntgen / CT / EKG / vérvizsgálatot",micBtn:"🎤 Beszéljen",btnDiagnose:"Diagnózis és kezelés",loader:"⏳ ChatGPT elemzi…",resultTitle:"🔍 Lehetséges ok:",inv:"📋 Szükséges teszt:",rx:"💊 OTC gyógyszer:",warn:"⚠️ Súlyos – azonnal orvoshoz!",follow:"✅ 48 óra alatt nincs javulás, orvos."},
  cs:{title:"Bezplatná Klinika – AI Doktor online",lblSymptoms:"Příznaky / mluvit:",lblDrop:"Přetáhněte rentgen / CT / EKG / krevní test sem",micBtn:"🎤 Mluvit",btnDiagnose:"Diagnóza a léčba",loader:"⏳ ChatGPT analyzuje…",resultTitle:"🔍 Možná příčina:",inv:"📋 Potřebný test:",rx:"💊 OTC lék:",warn:"⚠️ Vážné – okamžitě k lékaři!",follow:"✅ Pokud se do 48 h nezlepší, lékař."},
  sk:{title:"Bezplatná Klinika – AI Doktor online",lblSymptoms:"Príznaky / hovoriť:",lblDrop:"Potiahnite röntgen / CT / EKG / krvný test sem",micBtn:"🎤 Hovoriť",btnDiagnose:"Diagnóza a liečba",loader:"⏳ ChatGPT analyzuje…",resultTitle:"
