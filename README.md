<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Think Before You Risk — เกมทดสอบทักษะการคิดและการตัดสินใจ</title>

  <meta name="description" content="Think Before You Risk — เกมทดสอบทักษะการคิดและการตัดสินใจ เพื่อเอาตัวรอดจากความเสี่ยงในโลกจริงและโลกออนไลน์">
  <meta property="og:title" content="Think Before You Risk — คิดก่อนเสี่ยง">
  <meta property="og:description" content="เกมทดสอบทักษะการคิดและการตัดสินใจ เพื่อเอาตัวรอดจากความเสี่ยงในโลกจริงและโลกออนไลน์">
  <meta property="og:type" content="website">

  <!-- Tailwind CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;600;700&display=swap" rel="stylesheet">

  <style>
    :root{
      --primary: #0f766e;
      --accent: #f97316;
      --bg: #f8fafc;
    }
    body { font-family: "Sarabun", system-ui, -apple-system, "Segoe UI", Roboto, Arial; background: linear-gradient(180deg,#eef2ff 0%, #f8fafc 60%); }
    .card-glass { background: linear-gradient(180deg, rgba(255,255,255,0.90), rgba(255,255,255,0.80)); backdrop-filter: blur(6px); }
    .btn-primary { background: linear-gradient(90deg,var(--primary), #0369a1); color: white; box-shadow: 0 6px 18px rgba(15,118,110,0.12); }
    /* neutral choice buttons */
    .choice-btn {
      transition: transform .18s ease, box-shadow .18s ease;
      background: white;
      border: 1px solid rgba(15,23,42,0.06);
      text-align: left;
      padding: 1rem;
      border-radius: 12px;
    }
    .choice-btn:hover { transform: translateY(-4px); box-shadow: 0 8px 20px rgba(2,6,23,0.06); }
    .progress-track { background: linear-gradient(90deg,#d1fae5 0%, #ecfeff 100%); border-radius: 999px; height: 12px; overflow: hidden; }
    .progress-fill { height: 100%; border-radius: 999px; transition: width 420ms ease; background: linear-gradient(90deg,var(--accent), #f43f5e); box-shadow: 0 6px 18px rgba(244,115,54,0.08); }
    .confetti-piece { position: absolute; width: 10px; height: 16px; opacity: 0.95; transform-origin: center; will-change: transform; animation: confetti-fall 2000ms linear forwards; }
    @keyframes confetti-fall { 0% { transform: translateY(-20vh) rotate(0deg); opacity: 1; } 100% { transform: translateY(100vh) rotate(720deg); opacity: 0.95; } }
    .fade { animation: fadeIn .28s ease-out both; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(6px) } to { opacity: 1; transform: translateY(0) } }
    .character { width: 110px; height: 110px; border-radius: 24px; background: linear-gradient(180deg,#fff 0%, #fef3c7 50%); box-shadow: 0 10px 30px rgba(2,6,23,0.06); display:flex; align-items:center; justify-content:center; }
  </style>
</head>
<body class="min-h-screen flex items-center justify-center p-6">
  <div id="app" class="w-full max-w-4xl mx-auto card-glass rounded-3xl shadow-2xl overflow-hidden border border-white/30">

    <!-- Header -->
    <header class="flex items-center gap-4 p-6 bg-gradient-to-r from-indigo-600 to-cyan-600 text-white">
      <div class="character shrink-0" aria-hidden="true">
        <svg viewBox="0 0 120 120" xmlns="http://www.w3.org/2000/svg" class="w-full h-full" role="img" aria-label="mascot">
          <defs>
            <linearGradient id="g1" x1="0" x2="1"><stop offset="0" stop-color="#fff" /><stop offset="1" stop-color="#fef08a"/></linearGradient>
            <linearGradient id="g2" x1="0" x2="1"><stop offset="0" stop-color="#60a5fa"/><stop offset="1" stop-color="#06b6d4"/></linearGradient>
          </defs>
          <rect x="6" y="6" rx="18" ry="18" width="108" height="108" fill="url(#g1)" opacity="0.95"/>
          <circle cx="42" cy="52" r="6" fill="#0f172a"/>
          <circle cx="78" cy="52" r="6" fill="#0f172a"/>
          <path d="M46 74 C56 86, 74 86, 84 74" stroke="#0f172a" stroke-width="3" fill="none" stroke-linecap="round"/>
          <rect x="22" y="30" rx="6" ry="6" width="76" height="14" fill="url(#g2)" />
          <circle cx="92" cy="37" r="6" fill="#f97316" />
        </svg>
      </div>

      <div>
        <h1 class="text-2xl font-bold">Think Before You Risk</h1>
        <p class="text-sm opacity-90">เกมทดสอบทักษะการคิดและการตัดสินใจเพื่อเอาตัวรอดจากความเสี่ยงของวัยรุ่นในโลกปัจจุบัน</p>
      </div>

      <div class="ml-auto text-right text-sm opacity-90">
        <div>เวลาเล่น: ~3 นาที</div>
        <div>คำถาม: 10 ข้อ</div>
      </div>
    </header>

    <!-- Main -->
    <main class="p-6 bg-transparent">
      <div id="page-container" class="fade"></div>
    </main>

    <footer class="p-4 text-center text-xs text-slate-600 bg-white/40">
      สร้างขึ้นเพื่อฝึกการตัดสินใจ — ข้อมูลเก็บในเครื่องเท่านั้น
    </footer>
  </div>

  <div id="confetti-root" style="position:fixed; inset:0; pointer-events:none;"></div>

<script>
/* ====== QUESTIONS (วัยรุ่น / เหตุการณ์ปัจจุบัน) ====== */
/* score: 2 = ปลอดภัย, 1 = กลาง, 0 = เสี่ยง  */
const RAW_QUESTIONS = [
  {
    id:1,
    text: "มีชาเลนจ์บน TikTok / Reels ที่ขอให้ทำท่าทางเสี่ยงแล้วแท็กเพื่อนเพื่อรับยอดวิว คุณจะทำอย่างไร?",
    choices: [
      { text: "ไม่ร่วมทำท่าที่เสี่ยง ถ่ายวิดีโอเวอร์ชันปลอดภัยหรืออธิบายเหตุผลว่าทำไมไม่ควรทำ", score:2, explain: "ปฏิเสธการทำกิจกรรมที่อันตรายและเสนอทางเลือกปลอดภัยเป็นแบบอย่างที่ดี" },
      { text: "ทำท่าแบบเดียวกันแต่ลดความเสี่ยงลงและแท็กเพื่อน", score:1, explain: "ปรับลดความเสี่ยงได้แต่ยังมีโอกาสผลักดันพฤติกรรมไม่ปลอดภัยในวงกว้าง" },
      { text: "ทำตามชาเลนจ์เต็มรูปแบบเพื่อให้ดังและมีคนกดไลก์", score:0, explain: "การทำตามชาเลนจ์เสี่ยงทำร้ายตัวเอง/ผู้อื่นและส่งเสริมพฤติกรรมไม่ปลอดภัย" }
    ]
  },
  {
    id:2,
    text: "เพื่อนแชร์ลิงก์ 'เฉลยข้อสอบ' ในกลุ่มแชทและบอกให้ดาวน์โหลดไฟล์เพื่อนำไปดู คุณจะทำอย่างไร?",
    choices: [
      { text: "ไม่ดาวน์โหลดและแจ้งครูว่ามีการเผยแพร่เอกสาร/เฉลยที่ไม่น่าเชื่อถือ", score:2, explain: "การใช้เฉลยผิดกฎหมาย/จริยธรรม ควรรายงานและหลีกเลี่ยง" },
      { text: "ดาวน์โหลดมาอ่านแค่ดูเป็นแนวทาง โดยไม่ส่งต่อ", score:1, explain: "แม้อ่านเพื่อทบทวนจะช่วยได้ แต่ไฟล์ที่ได้อาจไม่ถูกต้องหรือมีมัลแวร์" },
      { text: "ดาวน์โหลดและส่งต่อให้เพื่อนทุกคนเพื่อช่วยกันทำคะแนน", score:0, explain: "การแพร่ไฟล์เฉลยเป็นการสนับสนุนการทุจริตและผิดจริยธรรม" }
    ]
  },
  {
    id:3,
    text: "อินฟลูเอนเซอร์ชวนให้โอนเงินเพื่อเข้ากลุ่มลับที่สัญญาว่าจะสอนลงทุน/สูตรทำเงิน คุณจะทำอย่างไร?",
    choices: [
      { text: "ไม่โอน และตรวจสอบความน่าเชื่อถือของอินฟลูเอนเซอร์ผ่านแหล่งข่าวและรีวิวหลายแหล่ง", score:2, explain: "ตรวจสอบแหล่งที่มาช่วยป้องกันการถูกหลอกลวงทางการเงิน" },
      { text: "โอนไปจำนวนเล็กน้อยเพื่อลอง หากไม่จริงก็ขอเงินคืน", score:1, explain: "การทดสอบด้วยเงินเล็กน้อยยังเสี่ยงและไม่รับประกันความปลอดภัย" },
      { text: "โอนตามคำเชิญเพราะเชื่อใจอินฟลูเอนเซอร์", score:0, explain: "การโอนโดยไม่ตรวจสอบมักนำไปสู่การสูญเสียทางการเงิน" }
    ]
  },
  {
    id:4,
    text: "เพื่อนชวนให้ไปเจอคนที่รู้จักจากแอปหาคู่และขอให้ไปที่บ้านของเขาโดยบอกว่า 'คุยกันส่วนตัว' คุณจะทำอย่างไร?",
    choices: [
      { text: "นัดเจอที่สาธารณะ แจ้งคนใกล้ชิด และนัดเวลาเลิกคุยล่วงหน้า", score:2, explain: "การพบที่สาธารณะและมีคนรู้ช่วยลดความเสี่ยงด้านความปลอดภัย" },
      { text: "ไปแต่ขอให้เพื่อนมาด้วยหรือให้คนติดตามตำแหน่ง", score:1, explain: "มีเพื่อนร่วมทางช่วยลดความเสี่ยงแต่ยังต้องระวัง" },
      { text: "ไปคนเดียวที่บ้านเขาเพราะอยากได้ความเป็นส่วนตัว", score:0, explain: "ไปที่ส่วนตัวกับคนไม่รู้จักเสี่ยงต่อการถูกทำร้าย/หลอกลวง" }
    ]
  },
  {
    id:5,
    text: "คุณได้รับ DM จากบัญชีที่อ้างว่าเป็นเพื่อนเก่า ขอข้อมูลส่วนตัวและรูปเพื่อ 'อัปเดตความทรงจำ' คุณจะทำอย่างไร?",
    choices: [
      { text: "ไม่ให้ข้อมูลส่วนตัว ตรวจสอบผู้ส่งผ่านช่องทางอื่น และบล็อก/รายงานบัญชีที่ไม่ชัดเจน", score:2, explain: "ยืนยันตัวตนก่อนแชร์ข้อมูลและบล็อกบัญชีที่น่าสงสัยช่วยป้องกันการละเมิด" },
      { text: "ส่งรูปบางรูปที่ไม่ระบุตัวตนแล้วคุยต่อ", score:1, explain: "ให้ข้อมูลบางส่วนแม้ไม่ชัดเจนอาจนำไปสู่การสืบค้นเพิ่มเติม" },
      { text: "ให้ข้อมูลทั้งหมดเพราะคิดว่าเป็นเพื่อนจริง", score:0, explain: "ให้ข้อมูลกับบัญชีที่ไม่ยืนยันทำให้ข้อมูลส่วนตัวรั่วไหล" }
    ]
  },
  {
    id:6,
    text: "ครูขอให้ส่งภาพหน้าจอมือถือเพื่อยืนยันการบ้าน แต่ในภาพมีแชทและข้อมูลส่วนตัวของเพื่อนร่วมกลุ่มด้วย คุณจะทำอย่างไร?",
    choices: [
      { text: "ตัด/เบลอส่วนที่เป็นข้อมูลส่วนตัวหรือส่งเฉพาะไฟล์ที่จำเป็น", score:2, explain: "ปกป้องข้อมูลส่วนตัวของตนเองและผู้อื่นเป็นความรับผิดชอบ" },
      { text: "ส่งภาพทั้งหน้าทันทีแล้วแจ้งครูว่ามีข้อมูลส่วนตัว", score:1, explain: "การส่งทั้งหน้ามีความเสี่ยง แม้จะแจ้งหลังจากส่งก็ไม่เท่าการตัดข้อมูลออกก่อน" },
      { text: "ไม่ส่งเพราะกลัวข้อมูลรั่วไหลและยอมรับคะแนนหาย", score:0, explain: "การไม่ทำตามคำขอโดยไม่เจรจาอาจนำไปสู่ผลเสียทางการศึกษา ควรหาทางออกปลอดภัย" }
    ]
  },
  {
    id:7,
    text: "มีโพสต์ที่กล่าวหานักเรียนคนหนึ่งในกลุ่มว่าโกงการสอบ คุณจะทำอย่างไร?",
    choices: [
      { text: "ไม่แชร์ ตรวจสอบข้อเท็จจริง และแจ้งครูหรือผู้รับผิดชอบก่อนเผยแพร่", score:2, explain: "การตรวจสอบก่อนแชร์ช่วยปกป้องชื่อเสียงและลดการแพร่ข้อมูลเท็จ" },
      { text: "แชร์พร้อมคอมเมนต์ว่า 'ไม่แน่ใจ' เพื่อให้คนช่วยตรวจสอบ", score:1, explain: "การแชร์แม้มีข้อความเตือนยังเพิ่มการแพร่ข้อมูลและอาจทำร้ายผู้อื่น" },
      { text: "รีโพสต์ทันทีเพราะโกรธและอยากให้เรื่องถูกจับตามอง", score:0, explain: "การเผยแพร่ข้อมูลที่ยังไม่ยืนยันทำร้ายผู้อื่นและอาจผิดกฎหมาย" }
    ]
  },
  {
    id:8,
    text: "ขณะเรียนออนไลน์ ครูขอให้เปิดกล้องแต่คุณอยู่ในห้องที่มีข้อมูลส่วนตัวหรือคนอื่นอยู่ด้วย คุณจะทำอย่างไร?",
    choices: [
      { text: "แจ้งครูว่าไม่สะดวกเปิดกล้องตอนนี้และเสนอส่งงานหรือรูปประกอบแทน", score:2, explain: "รักษาความเป็นส่วนตัวและสื่อสารเหตุผลเป็นวิธีเหมาะสม" },
      { text: "เปิดกล้องแต่ปรับมุมให้เห็นเฉพาะหน้า/พื้นหลังเป็นกลาง", score:1, explain: "ปรับมุมช่วยได้แต่ยังอาจเปิดเผยบางข้อมูล" },
      { text: "เปิดกล้องโดยไม่คิดเพราะกลัวผลกระทบต่อคะแนน", score:0, explain: "การเปิดกล้องโดยไม่ระวังอาจเผยข้อมูลส่วนตัวของคุณหรือผู้อื่น" }
    ]
  },
  {
    id:9,
    text: "เห็นโพสต์ขายไอเท็มในเกมจากบัญชีใหม่ ราคาดีมาก แต่ต้องโอนผ่านช่องทางที่ไม่คุ้น คุณจะทำอย่างไร?",
    choices: [
      { text: "ตรวจสอบรีวิวจากหลายแหล่ง ขอหลักฐานการทำรายการจากผู้ขาย และใช้ช่องทางที่ปลอดภัยหรือระบบเอสโครว์หากเป็นไปได้", score:2, explain: "ยืนยันผู้ขายและใช้ช่องทางปลอดภัยลดความเสี่ยงการโกง" },
      { text: "ลองซื้อของชิ้นเล็กๆ เพื่อลองระบบ", score:1, explain: "การทดสอบแม้เล็กๆ ยังเสี่ยงและควรระมัดระวัง" },
      { text: "โอนทันทีเพราะกลัวพลาดโปร", score:0, explain: "โอนโดยไม่ตรวจสอบเสี่ยงถูกโกงและมีโอกาสไม่ได้รับของ" }
    ]
  },
  {
    id:10,
    text: "มีวิดีโอที่อาจเป็น deepfake กล่าวหานักเรียนคนหนึ่งในกลุ่มโรงเรียน คุณจะทำอย่างไร?",
    choices: [
      { text: "ไม่แชร์ต่อ แจ้งครูหรือผู้ดูแล และบันทึกหลักฐานเพื่อช่วยตรวจสอบว่าจริงหรือไม่", score:2, explain: "ปฏิเสธการแพร่ต่อและรายงานช่วยปกป้องผู้ถูกกล่าวหา" },
      { text: "แชร์แล้วเขียนว่า 'อาจไม่จริง' เพื่อให้คนช่วยตรวจสอบ", score:1, explain: "การแชร์แม้มีจุดประสงค์ตรวจสอบยังขยายการแพร่กระจาย" },
      { text: "แชร์ต่อทันทีเพราะคิดว่าสำคัญและอยากให้คนเห็น", score:0, explain: "การเผยแพร่ก่อนตรวจสอบทำร้ายภาพลักษณ์ผู้อื่น" }
    ]
  }
];

/* ===== utilities ===== */
const container = document.getElementById('page-container');
const confettiRoot = document.getElementById('confetti-root');

function shuffleArray(arr) {
  for (let i = arr.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [arr[i], arr[j]] = [arr[j], arr[i]];
  }
  return arr;
}

/* create working questions by shuffling question order and shuffling choices per question */
let QUESTIONS = [];
function prepareQuestions() {
  QUESTIONS = JSON.parse(JSON.stringify(RAW_QUESTIONS)); // deep copy
  shuffleArray(QUESTIONS);
  QUESTIONS.forEach(q => shuffleArray(q.choices));
}

/* ===== App state ===== */
let state = {
  name: localStorage.getItem('tbry_name') || '',
  current: 0,
  answers: []
};

function saveName(n){ state.name = n; try{ localStorage.setItem('tbry_name', n); } catch(e){} }

/* ===== render functions ===== */
function renderStart(){
  prepareQuestions();
  container.innerHTML = `
    <div class="grid md:grid-cols-2 gap-6 items-center">
      <div>
        <h2 class="text-2xl font-bold text-slate-800 mb-2">พร้อมจะทดสอบสกิลการตัดสินใจของคุณหรือยัง?</h2>
        <p class="text-slate-600 mb-4">เกมสั้น 10 คำถาม — เลือกคำตอบที่คุณคิดว่าเหมาะสมที่สุดกับสถานการณ์ของวัยรุ่นในปัจจุบัน</p>
        <div class="mb-4">
          <label class="block text-sm font-medium text-slate-700 mb-2">ชื่อผู้เล่น</label>
          <input id="player-name" value="${escapeHtml(state.name)}" placeholder="พิมพ์ชื่อหรือชื่อเล่น" class="w-full rounded-xl border border-slate-200 px-4 py-3 shadow-sm focus:outline-none focus:ring-2 focus:ring-cyan-200" />
        </div>

        <div class="flex gap-3">
          <button id="btn-start" class="btn-primary px-5 py-3 rounded-xl font-semibold hover:scale-[1.02] transition">เริ่มเล่น</button>
          <button id="btn-sample" class="px-4 py-3 rounded-xl border border-slate-200">ดูตัวอย่าง</button>
          <button id="btn-reset" class="px-4 py-3 rounded-xl border border-red-200 text-red-600">ล้างชื่อ</button>
        </div>

        <div class="mt-6 text-sm text-slate-500">
          <strong>คำแนะนำ:</strong> เลือกตัวเลือกที่คุณคิดว่าเหมาะสมที่สุด — ผลจะเป็นการประเมินเชิงคุณภาพ (ไม่แสดงคะแนนตัวเลข)
        </div>
      </div>

      <div class="text-center">
        <div class="bg-gradient-to-br from-white to-amber-50 rounded-2xl p-6 shadow-xl">
          <div class="text-left mb-3">
            <div class="text-xs text-slate-500">เครื่องมือเช็กสกิล</div>
            <div class="text-lg font-semibold text-slate-800">Think Before You Risk</div>
          </div>
          <div class="mb-4">
            <svg viewBox="0 0 320 180" class="w-full h-32 rounded-lg overflow-visible">
              <defs>
                <linearGradient id="gA" x1="0" x2="1"><stop offset="0" stop-color="#60a5fa"/><stop offset="1" stop-color="#06b6d4"/></linearGradient>
              </defs>
              <rect x="0" y="0" width="320" height="120" rx="12" fill="url(#gA)" opacity="0.12"></rect>
              <g transform="translate(12,12)"><circle cx="48" cy="48" r="24" fill="#fff"></circle></g>
            </svg>
          </div>
          <div class="text-sm text-slate-600">คำถามออกแบบสำหรับวัยรุ่น — สถานการณ์มีความใกล้เคียงกับโลกออนไลน์และการเรียนสมัยใหม่</div>
        </div>
      </div>
    </div>
  `;

  document.getElementById('btn-start').onclick = () => {
    const nm = (document.getElementById('player-name').value || 'ผู้เล่นไม่ระบุ').trim();
    saveName(nm);
    state.current = 1; state.answers = [];
    renderQuestion(1);
  };
  document.getElementById('btn-sample').onclick = renderSample;
  document.getElementById('btn-reset').onclick = ()=>{ saveName(''); state.name=''; renderStart(); }
}

function renderSample(){
  const q = QUESTIONS[0];
  container.innerHTML = `
    <div>
      <div class="flex items-center justify-between mb-4">
        <div>
          <h3 class="text-lg font-semibold">ตัวอย่างคำถาม</h3>
          <p class="text-sm text-slate-500">ลองดูตัวอย่างนี้ก่อนเริ่มเล่น</p>
        </div>
        <div class="text-sm text-slate-500">คำถาม 1 / ${QUESTIONS.length}</div>
      </div>

      <div class="bg-white rounded-xl p-5 shadow-sm border border-slate-100 mb-4">
        <p class="font-medium text-slate-800">${escapeHtml(q.text)}</p>
        <div class="mt-3 space-y-2">
          ${q.choices.map((c,i)=>`<div class="p-3 rounded-lg">${escapeHtml(c.text)}</div>`).join('')}
        </div>
      </div>

      <div class="flex gap-3">
        <button id="back" class="px-4 py-2 rounded-xl border">กลับ</button>
        <button id="begin" class="btn-primary px-4 py-2 rounded-xl">เริ่มเล่นจริง</button>
      </div>
    </div>
  `;
  document.getElementById('back').onclick = renderStart;
  document.getElementById('begin').onclick = ()=>{ state.current=1; state.answers=[]; renderQuestion(1); };
}

function renderQuestion(index){
  const q = QUESTIONS[index-1];
  if(!q) return renderResults();

  const progressPct = Math.round(((index-1)/QUESTIONS.length)*100);

  container.innerHTML = `
    <div class="space-y-4">
      <div class="flex items-center justify-between">
        <div>
          <div class="text-sm text-slate-500">ผู้เล่น: <span class="font-medium text-slate-700">${escapeHtml(state.name||'ไม่ระบุ')}</span></div>
          <h3 class="text-xl font-semibold text-slate-800 mt-1">คำถามที่ ${index} จาก ${QUESTIONS.length}</h3>
        </div>
        <div class="w-56">
          <div class="text-xs text-slate-500 mb-1">ความคืบหน้า</div>
          <div class="progress-track"><div class="progress-fill" style="width:${progressPct}%;"></div></div>
          <div class="text-xs text-slate-400 mt-1 text-right">${progressPct}%</div>
        </div>
      </div>

      <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100">
        <p class="text-base font-medium text-slate-800">${escapeHtml(q.text)}</p>
      </div>

      <div class="grid gap-3">
        ${q.choices.map((c,i)=>`
          <button data-choice="${i}" class="choice-btn" aria-label="choice-${i}">
            <div class="flex items-center justify-between">
              <div class="min-w-0">
                <div class="text-sm font-medium text-slate-800">${escapeHtml(c.text)}</div>
                <div class="text-xs text-slate-400 mt-1">ตัวเลือก ${i+1}</div>
              </div>
              <div class="text-2xl opacity-80">${i+1}</div>
            </div>
          </button>
        `).join('')}
      </div>

      <div class="flex items-center justify-between">
        <button id="btn-back" class="px-4 py-2 rounded-xl border">ย้อนกลับ</button>
        <div class="text-sm text-slate-500">คำตอบที่เลือกแล้ว: <strong class="text-slate-700">${state.answers.length}</strong></div>
      </div>
    </div>
  `;

  Array.from(container.querySelectorAll('.choice-btn')).forEach(btn=>{
    btn.onclick = ()=>{
      const cidx = Number(btn.getAttribute('data-choice'));
      const choice = q.choices[cidx];
      state.answers.push({ qid:q.id, choiceIndex:cidx, score: choice.score, explain: choice.explain, text: choice.text });
      if(state.current < QUESTIONS.length){ state.current+=1; renderQuestion(state.current); }
      else { state.current = QUESTIONS.length+1; renderResults(); }
    };
  });

  document.getElementById('btn-back').onclick = ()=>{
    if(state.current<=1){ state.current=0; renderStart(); return; }
    if(state.answers.length>0) state.answers.pop();
    state.current -= 1;
    renderQuestion(state.current);
  };
}

function renderResults(){
  const total = state.answers.reduce((s,a)=>s+a.score,0);
  const max = QUESTIONS.length * 2;
  const pct = Math.round((total/max)*100);

  let title, adv;
  if(total <= 6){
    title = "เสี่ยงสูง — ควรปรับปรุง";
    adv = ["เรียนรู้พื้นฐานความปลอดภัยออนไลน์ (OTP, ฟิชชิ่ง)", "ตั้งรหัสผ่านที่แข็งแรง & เปิด 2FA", "ไม่แชร์ข้อมูล/รูปภาพโดยไม่ได้รับอนุญาต", "หลีกเลี่ยงการโอนเงินหรือให้ข้อมูลโดยไม่ตรวจสอบ"];
  } else if(total <= 13){
    title = "พอใช้ — ควรเสริมทักษะ";
    adv = ["ฝึกสังเกตกลลวงออนไลน์และสแกม", "ทบทวนก่อนคลิกลิงก์/ดาวน์โหลด", "อ่านนโยบายความเป็นส่วนตัวก่อนให้ข้อมูล", "ปรึกษาครู/ผู้ปกครองเมื่อไม่แน่ใจ"];
  } else {
    title = "ดีมาก! — สกิลแข็งแรง";
    adv = ["ลงลึกเกี่ยวกับการจัดการความเป็นส่วนตัวบนแพลตฟอร์ม", "ช่วยสอนเพื่อนและแชร์แนวปฏิบัติที่ดี", "ตรวจสอบความปลอดภัยขั้นสูงของบัญชีและอุปกรณ์"];
  }

  container.innerHTML = `
    <div class="space-y-4">
      <div class="flex items-center justify-between">
        <div>
          <h2 class="text-2xl font-bold text-slate-800">ผลการทดสอบ</h2>
          <p class="text-sm text-slate-500">ผู้เล่น: <strong>${escapeHtml(state.name||'ไม่ระบุ')}</strong></p>
        </div>
        <div class="text-right">
          <div class="text-lg font-extrabold" style="background:linear-gradient(90deg,#f97316,#ef4444); -webkit-background-clip:text; color:transparent;">${title}</div>
          <div class="text-xs text-slate-500 mt-1">ประเมินเชิงคุณภาพ (ไม่แสดงคะแนนตัวเลข)</div>
        </div>
      </div>

      <div class="p-4 rounded-2xl bg-white border border-slate-100 shadow-sm">
        <div class="flex items-center gap-4">
          <div class="w-16 h-16 rounded-lg flex items-center justify-center bg-gradient-to-br from-amber-100 to-pink-50">
            <div class="text-3xl">🎯</div>
          </div>
          <div>
            <div class="font-semibold text-slate-800">คำแนะนำ</div>
            <div class="text-sm text-slate-600 mt-1">สิ่งที่ควรศึกษา/ปฏิบัติเพื่อเพิ่มความปลอดภัย:</div>
            <ul class="mt-2 text-sm text-slate-600 list-disc list-inside">
              ${adv.map(it=>`<li>${escapeHtml(it)}</li>`).join('')}
            </ul>
          </div>
        </div>
      </div>

      <details class="bg-white border border-slate-100 rounded-xl p-4">
        <summary class="font-medium cursor-pointer">ดูคำอธิบายสำหรับคำตอบของคุณ</summary>
        <div class="mt-3 space-y-3">
          ${QUESTIONS.map((q,idx)=>{
            const ans = state.answers.find(a=>a.qid===q.id);
            const chosen = ans ? ans : null;
            return `
              <div class="border-b border-slate-100 pb-3">
                <div class="text-sm font-medium">${idx+1}. ${escapeHtml(q.text)}</div>
                <div class="text-xs mt-1 ${chosen ? '' : 'text-red-600'}">คำตอบของคุณ: <strong>${chosen?escapeHtml(chosen.text):'ไม่ได้ตอบ'}</strong></div>
                <div class="text-xs text-slate-500 mt-1">${chosen?escapeHtml(chosen.explain):''}</div>
              </div>
            `;
          }).join('')}
        </div>
      </details>

      <div class="flex gap-3">
        <button id="btn-retry" class="btn-primary px-4 py-3 rounded-xl">เล่นอีกครั้ง</button>
        <button id="btn-share" class="px-4 py-3 rounded-xl border">คัดลอกสรุป</button>
        <button id="btn-home" class="px-4 py-3 rounded-xl border">กลับหน้าหลัก</button>
      </div>
    </div>
  `;

  if(pct >= 50) launchConfetti(24);

  document.getElementById('btn-retry').onclick = ()=>{ state.answers=[]; state.current=1; prepareQuestions(); renderQuestion(1); }
  document.getElementById('btn-home').onclick = ()=>{ state.current=0; renderStart(); }
  document.getElementById('btn-share').onclick = ()=>{
    const summary = `ThinkBeforeYouRisk | ผู้เล่น:${state.name||'ไม่ระบุ'} | ผล: ${title}`;
    copyTextToClipboard(summary);
    alert('คัดลอกข้อความสรุปแล้ว: ' + summary);
  }
}

/* ===== helpers ===== */
function escapeHtml(s){ return String(s||'').replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;'); }
function copyTextToClipboard(text){
  if(navigator.clipboard && navigator.clipboard.writeText) navigator.clipboard.writeText(text).catch(()=>fallback(text));
  else fallback(text);
  function fallback(t){ const ta=document.createElement('textarea'); ta.value=t; document.body.appendChild(ta); ta.select(); try{document.execCommand('copy')}catch(e){} ta.remove(); }
}

/* ===== confetti ===== */
function randomInt(min,max){ return Math.floor(Math.random()*(max-min+1))+min; }
function launchConfetti(count=24){
  const colors = ['#f97316','#06b6d4','#60a5fa','#f43f5e','#34d399','#f59e0b'];
  const root = confettiRoot;
  for(let i=0;i<count;i++){
    const el = document.createElement('div');
    el.className = 'confetti-piece';
    el.style.left = (Math.random()*100)+'vw';
    el.style.top = '-10vh';
    el.style.background = colors[i % colors.length];
    el.style.width = (8 + Math.random()*8)+'px';
    el.style.height = (10 + Math.random()*14)+'px';
    el.style.transform = `rotate(${randomInt(0,360)}deg)`;
    el.style.opacity = (0.7 + Math.random()*0.3);
    el.style.animationDuration = (1400 + Math.random()*1200) + 'ms';
    root.appendChild(el);
    setTimeout(()=> el.remove(), 3500);
  }
}

/* ===== start ===== */
prepareQuestions();
renderStart();
</script>
</body>
</html>
