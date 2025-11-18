<!doctype html>
<html lang="uz">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Kasallik va Dori — Interaktiv Tibbiy Yo'riqnoma</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg1:#03040a; --bg2:#081226; --card:#071428;
  --glass: rgba(255,255,255,0.04);
  --text:#eaf4ff; --muted: rgba(234,244,255,0.7);
  --accent:#4caf50; --accent-2:#2bb673;
  --radius:14px; --shadow: 0 14px 48px rgba(2,8,20,0.7);
}
*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0;padding:36px;background:radial-gradient(800px 400px at 10% 10%, rgba(40,60,100,0.06), transparent 10%), linear-gradient(180deg,var(--bg1),var(--bg2));
  font-family:'Poppins',Arial,sans-serif;color:var(--text);-webkit-font-smoothing:antialiased;
  display:flex;align-items:flex-start;justify-content:center;
}
.wrap{width:100%;max-width:1100px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));padding:28px;border-radius:18px;box-shadow:var(--shadow);position:relative;overflow:hidden}
.header{display:flex;justify-content:space-between;align-items:center;gap:12px;margin-bottom:14px}
.title{margin:0;font-size:22px}
.subtitle{margin:0;color:var(--muted);font-size:13px}
.form{display:flex;flex-wrap:wrap;gap:12px;align-items:flex-end}
.field{background:var(--glass);padding:10px;border-radius:12px;border:1px solid rgba(255,255,255,0.03);display:flex;flex-direction:column}
.label{font-size:13px;color:var(--muted);margin-bottom:8px}
select{background:transparent;border:none;color:var(--text);padding:8px 10px;font-size:15px;outline:none;min-width:260px}
.button{background:linear-gradient(180deg,var(--accent),var(--accent-2));border:none;color:white;padding:10px 16px;border-radius:10px;cursor:pointer;font-weight:600;box-shadow:0 8px 20px rgba(43,182,115,0.12)}
.grid{display:grid;grid-template-columns:2fr 1fr;gap:16px;margin-top:18px}
.panel{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));padding:16px;border-radius:12px;border:1px solid rgba(255,255,255,0.03)}
.card{padding:12px;border-radius:10px;background:rgba(255,255,255,0.02);margin-bottom:10px}
.h3{margin:0;font-size:16px;color:#fff}
.small{font-size:13px;color:var(--muted);margin-top:8px}
.list{margin:8px 0;padding:0;list-style:disc;padding-left:18px;color:var(--muted)}
.meds{display:flex;flex-wrap:wrap;gap:8px;margin-top:10px}
.pill{background:rgba(255,255,255,0.03);padding:8px 10px;border-radius:10px;font-size:14px}
.price{font-weight:700;color:#fff;margin-top:12px}
.note{font-size:13px;color:var(--muted);margin-top:10px}
.footer{margin-top:12px;text-align:center;color:var(--muted);font-size:13px}

@media(max-width:980px){.grid{grid-template-columns:1fr}select{min-width:190px}}
</style>
</head>
<body>
<div class="wrap" role="application" aria-labelledby="main-title">
  <div class="header">
    <div>
      <h1 id="main-title" class="title">Kasallik va Dori vositalari — Interaktiv Yo'riqnoma</h1>
      <div class="subtitle">Iltimos, toifa va kasallik turini tanlang. Bu ma'lumot ta'limiy xarakterga ega. Aniqlash va davolash uchun vrachga murojaat qiling.</div>
    </div>
    <div class="subtitle">UI: qoramtir kechki fon, silliq effektlar va professional ohang.</div>
  </div>

  <form id="flowForm" class="form" onsubmit="return false;" aria-describedby="guide">
    <div class="field">
      <label class="label">Iltimos, toifa tanlang</label>
      <select id="category" aria-label="Kategoriya tanlang">
        <option value="">— Toifa tanlang —</option>
      </select>
    </div>

    <div class="field">
      <label class="label">Iltimos, kasallik turini tanlang</label>
      <select id="disease" aria-label="Kasallik tanlang" disabled>
        <option value="">— Avval toifa tanlang —</option>
      </select>
    </div>

    <div class="field">
      <label class="label">Dori vositasini tanlang</label>
      <select id="med" aria-label="Dori vositasini tanlang" disabled>
        <option value="">— Avval kasallik tanlang —</option>
      </select>
    </div>

    <div style="display:flex;align-items:flex-end">
      <button id="showBtn" class="button" type="button" disabled>Ko'rsatish</button>
    </div>
  </form>

  <div id="guide" class="small">Bosqichma-bosqich: Toifa → Kasallik turi (asosiy belgilari ko‘rsatiladi) → Dori vositasi (tanlang) → Dori narxi.</div>

  <div class="grid" role="region" aria-live="polite">
    <div class="panel" id="mainPanel">
      <div class="card">
        <h3 class="h3" id="diseaseTitle">Kasallik turi haqida ma'lumot</h3>
        <div id="symptoms" class="small">Iltimos, avval toifa va kasallik turini tanlang — asosiy belgilari shu yerda ko‘rsatiladi.</div>
      </div>

      <div class="card">
        <h3 class="h3">Tavsiya qilingan dori vositalari</h3>
        <div id="medList" class="meds"><div class="small">Kasallik tanlangandan so'ng dori vositalari shu yerda ro'yxatlanadi.</div></div>
        <div id="medNote" class="note"></div>
      </div>
    </div>

    <div class="panel" id="sidePanel">
      <div class="card">
        <h3 class="h3">Tanlangan dori vositasi narxi</h3>
        <div id="priceBox" class="small">Dori vositasini tanlang — narx shu yerda ko‘rinadi.</div>
      </div>

      <div class="card">
        <h3 class="h3">Tez yordam eslatmasi</h3>
        <div class="small">Agar simptomlar og‘ir bo‘lsa (nafas olish qiyinlashuvi, kuchli bosh aylanish, og‘riqning kuchayishi) — darhol shifoxonaga murojaat qiling.</div>
      </div>
    </div>
  </div>

  <div class="footer">Ma'lumotlar ta'limiy maqsadlarda berilgan. Aniq tashxis va davolash uchun vrach bilan bog'laning.</div>
</div>

<script>
// Polished Uzbek labels and DB with symptoms and up to 5 medicines (name + price)
// Prices are in so'm and fixed. Symptoms are 3-4 concise phrases (adabiy til).
const DB = {
  "yuqumli": {
    "gripp": {
      title:"Gripp (yelkalanish va shamollash)", 
      symptoms:["Isitma va titroq", "Qalqonchan holda bo‘lgan kuchsizlanish", "Yo‘tal va burun oqishi"],
      meds:[
        {name:"Paratsetamol", price:6000},
        {name:"Ibuprofen", price:9000},
        {name:"Oseltamivir (shifokor nazorati)", price:28000},
        {name:"Vitamin C tabletkalari", price:7000},
        {name:"Suv va rehydratatsiya vositalari (Regidron)", price:6000}
      ],
      note:"Simptomatik davolash; antiviral vositalar faqat shifokor ko‘rsatmasi bilan."
    },
    "angina": {
      title:"Angina (tomoq infektsiyasi)",
      symptoms:["Tomoqda og‘riq va yutishda qiyinchilik", "Bo‘yin bezlarining shishishi", "Isitma boʻlishi mumkin"],
      meds:[
        {name:"Amoksiklav", price:25000},
        {name:"Azitromitsin", price:22000},
        {name:"Iliq tuzli chayish", price:0},
        {name:"Og‘riqni kamaytiruvchi tabletkalar", price:8000},
        {name:"Pastki dam olish va suyuqlik ko‘p ichish", price:0}
      ],
      note:"Bakterial anginada antibiotiklarni faqat vrach belgilaydi."
    },
    "pnevmoniya": {
      title:"Pnevmoniya (o‘pka yallig‘lanishi)",
      symptoms:["Tungi yo‘tal va balg‘am hosil bo‘lishi", "Tana haroratining ko‘tarilishi", "Nafas olishda qisqarlik"],
      meds:[
        {name:"Ceftriakson (IV, shifoxona)", price:40000},
        {name:"Azitromitsin", price:22000},
        {name:"Paratsetamol (isitma uchun)", price:6000},
        {name:"Nebulizatsion terapiya", price:15000},
        {name:"Oxygen terapiyasi (zarur bo‘lsa)", price:0}
      ],
      note:"Pnevmoniya — shifoxona va vrach tashxisini talab qiladi."
    },
    "bronxit": {
      title:"Bronxit (nafas yo‘llari yallig‘lanishi)",
      symptoms:["Kuchli yo‘tal (quruq yoki nam)", "Ko‘krakda og‘riq", "Charchoq va ishtahasizlik"],
      meds:[
        {name:"Ambroksol sirop", price:7000},
        {name:"Bromgeksin", price:8000},
        {name:"Erespal (bronxorelaksant)", price:15000},
        {name:"Azitromitsin (antibiotik)", price:22000},
        {name:"Inhalyatsion bronxodilatator (salbutamol)", price:14000}
      ],
      note:"Yo‘tal turi aniqlangach, to‘liq davolash belgilanadi."
    },
    "kon'yunktivit": {
      title:"Ko‘z kon'yunktiviti (ko‘zning yallig'lanishi)",
      symptoms:["Qizillash va yirtilish", "Ko‘zdan oqindi kelishi", "Yorug'likdan noqulaylik"],
      meds:[
        {name:"Albucid tomchilari", price:8000},
        {name:"Tobramitsin tomchilari", price:14000},
        {name:"Iliq kompresslar", price:0},
        {name:"Ko‘z gigiyenasi vositalari", price:5000},
        {name:"Antiallergik tomchilar (zarur bo‘lsa)", price:12000}
      ],
      note:"Ko‘z infeksiyalari tez tarqaladi — shaxsiy buyumlarni bo‘lishmang."
    },
    "tomoq og'rig'i": {
      title:"Tomoq og'rig'i (faringit)",
      symptoms:["Tomoqda achishish yoki yonish", "Yutishda noqulaylik", "Yorqin bo‘lmagan ovoz"],
      meds:[
        {name:"Tantum Verde spreyi", price:18000},
        {name:"Strepsils lozenglari", price:6000},
        {name:"Iliq tuzli chayish", price:0},
        {name:"Og‘riqni kamaytiruvchi tabletkalar", price:8000},
        {name:"Dam olish va suyuqlik", price:0}
      ],
      note:"Agar 48 soatdan ortiq davom etsa, vrachga murojaat qiling."
    },
    "otit": {
      title:"Otit (quloq infektsiyasi)",
      symptoms:["Quloq og'rig'i", "Quyoshli yoki qorong'u shovqin sezgisi", "Isitma (bolalarda)"],
      meds:[
        {name:"Otipaks tomchilar", price:12000},
        {name:"Amoksiklav", price:25000},
        {name:"Og‘riqni kamaytiruvchi vositalar", price:8000},
        {name:"Iliq kompress", price:0},
        {name:"Pediatr nazorati", price:0}
      ],
      note:"Bolalarda otit tez-tez uchraydi — pediatr ko‘rsatmasisiz antibiotik bermang."
    },
    "zaxm": {
      title:"Zaxm (jarohat va infeksiya natijasi)",
      symptoms:["Yara joyida og'riq va qizillik", "Yara atrofida yallig'lanish", "Olovsiz chiqayotgan suyuqlik"],
      meds:[
        {name:"Tetanus immunoglobulin (zarur bo'lsa)", price:150000},
        {name:"Antibiotik kursi (vrach belgilaydi)", price:25000},
        {name:"Antiseptik yechimlar", price:8000},
        {name:"Yara tiklash uchun malham", price:12000},
        {name:"Tetiklantiruvchi dorilar (kerak bo'lsa)", price:0}
      ],
      note:"Yarani tozalash va vaksina holatini tekshirish zarur."
    },
    "koronavirus": {
      title:"COVID-19 (koronavirus infektsiyasi)",
      symptoms:["Isitma va yo‘tal", "Naqqa hidoligi o‘zgarishi (ba'zan)", "Charchoq va muskullar og‘rig‘i"],
      meds:[
        {name:"Paratsetamol", price:6000},
        {name:"Ibuprofen", price:9000},
        {name:"Vitamin C", price:7000},
        {name:"Rehydratatsiya vositalari", price:6000},
        {name:"Nebulizatsion terapiya (zarur bo'lsa)", price:15000}
      ],
      note:"Antiviral dori faqat vrach tavsiyasi bilan."
    },
    "pankreatit": {
      title:"Pankreatit (oshqozon osti bezi yallig'lanishi)",
      symptoms:["Tirishish qo‘ng‘ir og'riq", "Qorin yuqori qismida og'riq", "Ishtahasizlik va qusish"],
      meds:[
        {name:"Kreon (pankreatin)", price:35000},
        {name:"Drotaverin", price:8000},
        {name:"Omez (omeprazol)", price:12000},
        {name:"Og'riqni yengillashtiruvchi vositalar", price:10000},
        {name:"IV rehydratatsiya (zarur bo'lsa)", price:0}
      ],
      note:"Pankreatit jiddiy holat — shifokor nazorati zarur."
    }
  },
  "oshqozon": {
    "gastrit": {
      title:"Gastrit (oshqozon yallig'lanishi)",
      symptoms:["Qorin yuqori qismida achishish", "Yoqimsiz og'riq yoki to‘yinganlik hissi", "Shishish va gaz"],
      meds:[
        {name:"Omez (omeprazol)", price:12000},
        {name:"Ranitidin", price:8000},
        {name:"Almagel", price:9000},
        {name:"Dietaga rioya qilish (medikamental yordam)", price:0},
        {name:"Probiotiklar", price:9000}
      ],
      note:"Gastrolog bilan maslahatlashish tavsiya etiladi."
    },
    "oshqozon yarasi": {
      title:"Oshqozon yarasi",
      symptoms:["Qorin og'rig‘i (ochlikda kuchayadi)", "Qaynash va qayt qilish", "Qon bilan ich ketishi yoki qora najas (og'ir)"],
      meds:[
        {name:"Omez", price:12000},
        {name:"De-nol", price:18000},
        {name:"Amoksiklav", price:25000},
        {name:"Antisekretor preparatlar", price:14000},
        {name:"Parenteral reabilitatsiya (zarur bo'lsa)", price:0}
      ],
      note:"Agar qon ketishi belgisi bo‘lsa — darhol vrachga murojaat qiling."
    },
    "diabet": {
      title:"Qandli diabet (2-tur)",
      symptoms:["Tez charchash", "Tez-tez siyish", "Og‘irlik yo‘qotish yoki ko‘payishi"],
      meds:[
        {name:"Metformin", price:15000},
        {name:"Glibenklamid", price:12000},
        {name:"Insulin (vial yoki pen)", price:60000},
        {name:"Glikemiyani nazorat qilish vositalari", price:25000},
        {name:"Dietologik maslahat", price:0}
      ],
      note:"Doimiy nazorat va parhez zarur."
    },
    "diarreya": {
      title:"Ich ketishi (diarreya)",
      symptoms:["Suvli najas", "Qorin og‘rig‘i va kramp", "Suyuq yo‘qotish belgilar (bosim pasayishi)"],
      meds:[
        {name:"Smecta", price:10000},
        {name:"Regidron", price:6000},
        {name:"Loperamid", price:9000},
        {name:"Sorbeks (sorbent)", price:7000},
        {name:"Probiotiklar", price:9000}
      ],
      note:"Suyuqlik yo'qotilishini oldini olish muhim."
    },
    "sistit": {
      title:"Sistit (siydik yo‘li infektsiyasi — ayollar uchun)",
      symptoms:["Siydik qilinganida og‘riq yoki yonish", "Tez-tez siyish ehtiyojining ortishi", "Pastki qorin bezovtaligi"],
      meds:[
        {name:"Furadonin", price:14000},
        {name:"Kanefron", price:18000},
        {name:"Nitroksolin", price:12000},
        {name:"Ko‘p suyuqlik", price:0},
        {name:"Siydik yo‘li gigiyenasi vositalari", price:5000}
      ],
      note:"Pediatr yoki ginekolog maslahatini oling."
    },
    "hemorroy": {
      title:"Gemorroy (ichki yoki tashqi tomoni)",
      symptoms:["Aniq qon ketishi defekatsiya paytida", "Og‘riq va qichishish", "Tashqi shish paydo bo‘lishi mumkin"],
      meds:[
        {name:"Relief shamchasi", price:20000},
        {name:"Hepatrombin G malhami", price:22000},
        {name:"Detraleks tabletkalari", price:45000},
        {name:"Yallig‘lanishga qarshi malhamlar", price:12000},
        {name:"Tolali ovqatlar va suyuqlik", price:0}
      ],
      note:"Agar qon ketishi ko‘p bo‘lsa — vrachga murojaat qiling."
    },
    "ko'ngil aynishi": {
      title:"Ko‘ngil aynishi va qayt qilish",
      symptoms:["Nofoydalilik va og‘irlik", "Tez-tez qusish (ba'zan)", "Suyuqlik yo‘qotish belgilar"],
      meds:[
        {name:"Metoclopramide (Cerukal)", price:9000},
        {name:"Domperidon (Reglan)", price:9000},
        {name:"Sorbents", price:7000},
        {name:"IV rehydratatsiya (zarur bo‘lsa)", price:0},
        {name:"Antiemetiklardan foydalanish (vrach ko‘rsatganda)", price:0}
      ],
      note:"Agar uzoq davom etsa, vrach tomonidan tekshirish zarur."
    }
  },
  "yurak": {
    "arterial bosim": {
      title:"Arterial gipertenziya (yuqori qon bosimi)",
      symptoms:["Bosim ko‘tarilishi (ko‘pincha bosh og‘rig‘i)", "Ko‘krakda biroz bosim", "Nafas qisqarligi (og‘ir holatlarda)"],
      meds:[
        {name:"Enalapril", price:14000},
        {name:"Losartan", price:14000},
        {name:"Amlodipin", price:10000},
        {name:"Diuretiklar (Furosemid)", price:8000},
        {name:"Hayot tarzi o‘zgartirish (kam tuz)", price:0}
      ],
      note:"Qon bosimini doimiy nazorat qilish muhim."
    },
    "yurak yetishmovchiligi": {
      title:"Yurak yetishmovchiligi",
      symptoms:["Naqshli nafas olish qiyinligi", "Charchoq va o‘tkir to‘planish", "Qorin bo‘shlig‘ida shish"],
      meds:[
        {name:"Enalapril", price:14000},
        {name:"Furosemid", price:8000},
        {name:"Digoksin", price:25000},
        {name:"Beta-blokerlar", price:15000},
        {name:"Suyuqlik cheklovlari (vrach ko‘rsatganda)", price:0}
      ],
      note:"Shifokor ko‘rsatmasi bilan dori-darmonlarni boshqaring."
    },
    "insult": {
      title:"Insult (miya qon aylanishining buzilishi)",
      symptoms:["Birdaniga yuzning yiqilishi yoki qo‘l-oyoqda kuchsizlik", "Nutq buzilishi yoki ongning pasayishi", "Kuchli bosh og‘rig‘i"],
      meds:[
        {name:"Aspirin (profilaktika)", price:8000},
        {name:"Warfarin (antikoagulyant)", price:22000},
        {name:"NOAC dori (vrach buyuradi)", price:35000},
        {name:"Trombolitik terapiya (shifoxona)", price:0},
        {name:"Reabilitatsion dorilar va terapiya", price:0}
      ],
      note:"Acil vaziyat — tez tibbiy yordam kerak."
    },
    "yurak aritmiyasi": {
      title:"Yurak aritmiyasi (ritm buzilishi)",
      symptoms:["Yurak urishining tezlashishi yoki sekinlashishi", "Bosh aylanishi", "Zaiflik va nafas qisqarligi"],
      meds:[
        {name:"Metoprolol", price:15000},
        {name:"Amiodaron", price:40000},
        {name:"Antikoagulyantlar (kerak bo‘lsa)", price:22000},
        {name:"Elektrik kardioverziya (zarurat bo‘lsa)", price:0},
        {name:"Monitorlash va EKG", price:0}
      ],
      note:"Kardiolog nazorati talab qilinadi."
    },
    "qon bosimi pastligi": {
      title:"Qon bosimi pastligi (gipotoniya)",
      symptoms:["Bosim pastligi bilan bosh aylanish", "Qorong‘ulashish hissi", "Holsizlik"],
      meds:[
        {name:"Kofein tabletka", price:5000},
        {name:"Ginseng damlamasi", price:12000},
        {name:"Suyuqlikni ko‘paytirish", price:0},
        {name:"Tuz miqdorini nazoratlash", price:0},
        {name:"Shifokor maslahatlari", price:0}
      ],
      note:"Doimiy kuzatuv zarur."
    }
  },
  "asab": {
    "bosh og'rig'i": {
      title:"Bosh og'rig'i (spastik va oddiy)",
      symptoms:["Yengil yoki o‘rtacha bosim hissi", "Charchoq va stress bilan bog‘liq", "Garchi ko‘zdan ham noqulaylik bo‘lishi mumkin"],
      meds:[
        {name:"Paratsetamol", price:6000},
        {name:"Ibuprofen", price:9000},
        {name:"Aspirin", price:8000},
        {name:"Dam olish va yotoq tartibi", price:0},
        {name:"Suyuqlikni ko‘paytirish", price:0}
      ],
      note:"Agar takrorlansa yoki og‘ir bo‘lsa, nevrologga murojaat qilishingiz kerak."
    },
    "migren": {
      title:"Migren (kuchli bosh og'rig'i)",
      symptoms:["Kuchli pulsatil og‘riq", "Ko‘zga yorqin nur sezgi sezuvchanligi", "Qusish yoki ko‘ngil aynishi"],
      meds:[
        {name:"Sumatriptan", price:30000},
        {name:"Ibuprofen", price:9000},
        {name:"Paratsetamol", price:6000},
        {name:"Kofein (qisqa muddatli yordam)", price:5000},
        {name:"Sokin, qorong‘i xona", price:0}
      ],
      note:"Profilaktika va uzoq muddatli davolash uchun nevrolog bilan maslahat."
    },
    "uyqusizlik": {
      title:"Uyqusizlik (insomniya)",
      symptoms:["Uxlashga qiynalish", "Tez-tez uyg‘onish", "Kunduzgi charchoq"],
      meds:[
        {name:"Melatonin", price:8000},
        {name:"Persen", price:7000},
        {name:"Donormil (vrach nazoratida)", price:12000},
        {name:"Uyqu gigiyenasi tavsiyalari", price:0},
        {name:"Kognitiv-terapevtik mashqlar", price:0}
      ],
      note:"Davolanayotganda shifokor bilan muvofiqlashtiring."
    },
    "depressiya": {
      title:"Depressiya (ruhiy tushkunlik)",
      symptoms:["Qiziqishning yo‘qolishi", "Kundalik faoliyatga qiziqmaslik", "Tez-tez charchash yoki uyqu buzilishi"],
      meds:[
        {name:"Sertralin", price:26000},
        {name:"Amitriptilin", price:18000},
        {name:"Novo-Passit", price:7000},
        {name:"Psixoterapiya seanslari", price:0},
        {name:"Hayot tarzi o‘zgarishi", price:0}
      ],
      note:"Davolash faqat vrach nazorati ostida."
    },
    "nevroz": {
      title:"Nevroz va asabiylashuv",
      symptoms:["Qisqa muddatli vahima yoki tashvish", "Uyqu buzilishi", "Ko‘ngil holatining o‘zgarishi"],
      meds:[
        {name:"Gidazepam", price:6000},
        {name:"Valeriana damlamasi", price:3000},
        {name:"Novopassit", price:7000},
        {name:"Stressni kamaytiruvchi mashqlar", price:0},
        {name:"Psixologik maslahat", price:0}
      ],
      note:"Uzluksiz dori qabul qilishdan oldin mutaxassis bilan maslahat."
    },
    "osteoporoz": {
      title:"Osteoporoz (suyak zichligi pasayishi)",
      symptoms:["Bo‘g‘imlarda noqulaylik", "Suyak oson sinishi", "Bel va bo‘yin og‘rig‘i"], 
      meds:[
        {name:"Kalsiy + D3", price:15000},
        {name:"Alendronat", price:40000},
        {name:"Raloksifen", price:35000},
        {name:"Fizik terapiya tavsiyalari", price:0},
        {name:"Suyak zichligini baholash (DXA)", price:0}
      ],
      note:"Suyak sog'lig'ini kuzatish va davolash muhim."
    },
    "surunkali stress": {
      title:"Surunkali stress va charchoq",
      symptoms:["Doimiy bezovtalik", "Uyqu buzilishi", "Ishga qodirlik pasayishi"],
      meds:[
        {name:"Sertralin (vrach ko‘rsatmasi bilan)", price:26000},
        {name:"Novo-Passit", price:7000},
        {name:"Melatonin (uyqu uchun)", price:8000},
        {name:"Psixoterapiya", price:0},
        {name:"Hayot tarzi o‘zgarishi", price:0}
      ],
      note:"Psixolog yoki psixiatr bilan maslahat qilish tavsiya etiladi."
    }
  },
  "allergy": {
    "allergiya": {
      title:"Allergik reaksiya",
      symptoms:["Teri qichishi yoki toshma", "Burun oqishi va hapşırış", "Og‘ir holatda nafas qisqarishi"],
      meds:[
        {name:"Loratadin", price:7000},
        {name:"Suprastin", price:5000},
        {name:"Fenistil gel", price:12000},
        {name:"Nasal spreyi (steroid)", price:15000},
        {name:"Alergendan cheklanma", price:0}
      ],
      note:"Agar nafas olishda qiyinchilik bo‘lsa — tez yordam chaqiring."
    },
    "terida toshma": {
      title:"Teri toshmasi (dermatit)",
      symptoms:["Qichishish va qizarish", "Qo‘ziqish yoki bezovtalik", "Teri qurib qolishi"],
      meds:[
        {name:"Fenistil gel", price:12000},
        {name:"Loratadin sirop", price:9000},
        {name:"Tsink malhami", price:6000},
        {name:"Namlovchi krem (emollient)", price:15000},
        {name:"Dermatolog maslahat", price:0}
      ],
      note:"Teri holatini baholash uchun mutaxassisga murojaat qiling."
    },
    "ekzema": {
      title:"Ekzema (atopik dermatit)",
      symptoms:["Xronik qichishish", "Teri qalinlashishi yoki quruqligi", "Qaytalanib keluvchi toshmalar"],
      meds:[
        {name:"Hidrokortizon krem", price:12000},
        {name:"Fenistil", price:12000},
        {name:"Namlovchi kremlar", price:15000},
        {name:"Sistemik antihistaminlar", price:7000},
        {name:"Dermatologik tekshiruv", price:0}
      ],
      note:"Uzun muddatli nazorat talab qilinadi."
    },
    "quruq teri": {
      title:"Quruq teri",
      symptoms:["Quruqlik va terida toshma", "Yorilish yoki qichishish", "Katta hududlarda noqulaylik"],
      meds:[
        {name:"Bepanten krem", price:14000},
        {name:"Nivea krem", price:10000},
        {name:"Vitamin E", price:12000},
        {name:"Namlagich vositalar", price:0},
        {name:"Dermatolog tavsiyalari", price:0}
      ],
      note:"Doimiy teri parvarishi tavsiya etiladi."
    }
  }
};

// Populate category select
const categorySel = document.getElementById('category');
const diseaseSel = document.getElementById('disease');
const medSel = document.getElementById('med');
const showBtn = document.getElementById('showBtn');
const symptomsBox = document.getElementById('symptoms');
const medList = document.getElementById('medList');
const medNote = document.getElementById('medNote');
const priceBox = document.getElementById('priceBox');
const diseaseTitle = document.getElementById('diseaseTitle');

Object.keys(DB).forEach(cat => {
  const opt = document.createElement('option');
  opt.value = cat;
  opt.textContent = cat.charAt(0).toUpperCase() + cat.slice(1);
  categorySel.appendChild(opt);
});

categorySel.addEventListener('change', () => {
  const cat = categorySel.value;
  diseaseSel.innerHTML = '';
  medSel.innerHTML = '';
  medSel.disabled = true;
  showBtn.disabled = true;
  priceBox.textContent = "Dori vositasini tanlang — narx shu yerda ko‘rinadi.";
  diseaseTitle.textContent = "Kasallik turi haqida ma'lumot";
  symptomsBox.textContent = "Iltimos, kasallik turini tanlang — asosiy belgilari shu yerda ko‘rsatiladi.";
  medList.innerHTML = '<div class="small">Kasallik tanlangandan so‘ng dori vositalari shu yerda ro\'yxatlanadi.</div>';
  medNote.textContent = "";

  if(!cat){
    diseaseSel.disabled = true;
    const o = document.createElement('option'); o.textContent = '— Avval toifa tanlang —'; diseaseSel.appendChild(o);
    return;
  }
  const diseases = Object.keys(DB[cat] || {});
  if(!diseases.length){
    diseaseSel.disabled = true;
    const o = document.createElement('option'); o.textContent = 'Bu kategoriyada kasalliklar mavjud emas'; diseaseSel.appendChild(o);
    return;
  }
  diseaseSel.disabled = false;
  const first = document.createElement('option'); first.value=''; first.textContent='— Kasallik turini tanlang —'; diseaseSel.appendChild(first);
  diseases.forEach(dk => {
    const opt = document.createElement('option');
    opt.value = dk;
    opt.textContent = DB[cat][dk].title;
    diseaseSel.appendChild(opt);
  });
});

diseaseSel.addEventListener('change', () => {
  const cat = categorySel.value;
  const dis = diseaseSel.value;
  medSel.innerHTML = '';
  medSel.disabled = true;
  showBtn.disabled = true;
  priceBox.textContent = "Dori vositasini tanlang — narx shu yerda ko‘rinadi.";
  if(!dis){
    symptomsBox.textContent = "Iltimos, kasallik turini tanlang — asosiy belgilari shu yerda ko‘rsatiladi.";
    medList.innerHTML = '<div class="small">Kasallik tanlangandan so‘ng dori vositalari shu yerda ro\'yxatlanadi.</div>';
    medNote.textContent = "";
    diseaseTitle.textContent = "Kasallik turi haqida ma'lumot";
    return;
  }
  const item = DB[cat][dis];
  diseaseTitle.textContent = item.title;
  // Show symptoms in adabiy tilda
  symptomsBox.innerHTML = '<strong>Asosiy belgilari:</strong><ul class="list">' + item.symptoms.map(s=>'<li>'+escapeHtml(s)+'</li>').join('') + '</ul>';
  // Populate meds
  medSel.disabled = false;
  const first = document.createElement('option'); first.value=''; first.textContent='— Dori vositasini tanlang —'; medSel.appendChild(first);
  item.meds.forEach((m,idx)=>{
    const opt = document.createElement('option');
    opt.value = idx;
    opt.textContent = m.name + ' — ' + (typeof m.price==='number' && m.price>0 ? formatPrice(m.price) : (m.price===0 ? 'Bepul / amaliy xizmat' : 'Narx mavjud emas'));
    medSel.appendChild(opt);
  });
  // Show med cards
  medList.innerHTML = '';
  item.meds.forEach(m => {
    const span = document.createElement('div'); span.className='pill'; span.textContent = m.name + ' — ' + (m.price>0 ? formatPrice(m.price) : (m.price===0 ? 'Bepul / amaliy xizmat' : 'Narx mavjud emas'));
    medList.appendChild(span);
  });
  medNote.textContent = item.note || '';
});

medSel.addEventListener('change', () => {
  showBtn.disabled = !medSel.value;
  priceBox.textContent = "Dori vositasini tanlang — narx shu yerda ko‘rinadi.";
});

showBtn.addEventListener('click', ()=>{
  const cat = categorySel.value;
  const dis = diseaseSel.value;
  const mIdx = medSel.value;
  if(!cat || !dis || mIdx===''){ priceBox.textContent = "Iltimos, toifa, kasallik va dori vositasini tanlang."; return; }
  const med = DB[cat][dis].meds[Number(mIdx)];
  if(!med){ priceBox.textContent = "Tanlangan dori haqida ma'lumot topilmadi."; return; }
  const priceText = (typeof med.price==='number' && med.price>0) ? formatPrice(med.price) + " so'm" : (med.price===0 ? "Bepul / amaliy xizmat" : "Narx mavjud emas");
  priceBox.innerHTML = '<div class="h3" style="margin-bottom:8px">'+escapeHtml(med.name)+'</div><div class="price">'+formatPrice(med.price) + " so'm" +'</div><div class="note" style="margin-top:8px">Iltimos, dori va dozani vrach bilan muvofiqlashtiring.</div>';
});

function formatPrice(n){
  if(typeof n!=='number' || n<=0) return '0';
  return new Intl.NumberFormat('ru-RU').format(n);
}

function escapeHtml(s){ return String(s).replace(/[&<>"]/g, function(t){ return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[t]; }); }

// Initial state message
priceBox.textContent = "Dori vositasini tanlang — narx shu yerda ko‘rinadi.";

</script>
</body>
</html>
