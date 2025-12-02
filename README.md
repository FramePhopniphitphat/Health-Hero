<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>เกมทายสถานการณ์เสี่ยง – Health Hero</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; font-family: "Sarabun", system-ui, sans-serif; }
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(135deg, #fde68a, #f97316);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .app {
      background: #fffaf2;
      max-width: 700px;
      width: 95%;
      border-radius: 18px;
      padding: 20px 22px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.12);
    }
    h1 {
      margin: 0 0 6px;
      font-size: 1.4rem;
      text-align: center;
    }
    .subtitle {
      text-align: center;
      font-size: 0.9rem;
      color: #6b7280;
      margin-bottom: 16px;
    }
    .badge-row {
      display: flex;
      justify-content: center;
      gap: 6px;
      margin-bottom: 16px;
      flex-wrap: wrap;
    }
    .badge {
      padding: 4px 10px;
      border-radius: 999px;
      font-size: 0.75rem;
      color: #fff;
    }
    .badge-red { background: #ef4444; }
    .badge-orange { background: #fb923c; }
    .badge-green { background: #22c55e; }

    .status-bar {
      display: flex;
      justify-content: space-between;
      font-size: 0.85rem;
      margin-bottom: 10px;
      color: #4b5563;
    }

    .question-card {
      background: #ffffff;
      border-radius: 14px;
      padding: 16px 14px;
      border: 1px solid #f3f4f6;
      margin-bottom: 12px;
      min-height: 90px;
    }
    .question-card h2 {
      font-size: 1rem;
      margin: 0 0 8px;
      color: #111827;
    }
    .question-text {
      font-size: 0.95rem;
      color: #374151;
      line-height: 1.5;
    }

    .choices {
      display: grid;
      grid-template-columns: 1fr;
      gap: 8px;
      margin-top: 10px;
    }
    .btn {
      border: none;
      border-radius: 999px;
      padding: 10px 14px;
      font-size: 0.9rem;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      color: #fff;
      transition: transform 0.1s, box-shadow 0.1s, opacity 0.1s;
    }
    .btn:active {
      transform: translateY(1px);
      box-shadow: none;
    }
    .btn-red { background: #ef4444; box-shadow: 0 2px 5px rgba(239,68,68,0.4); }
    .btn-orange { background: #f97316; box-shadow: 0 2px 5px rgba(249,115,22,0.4); }
    .btn-green { background: #22c55e; box-shadow: 0 2px 5px rgba(34,197,94,0.4); }
    .btn-gray { background: #6b7280; box-shadow: 0 2px 5px rgba(107,114,128,0.4); }
    .btn[disabled] {
      opacity: 0.6;
      cursor: default;
    }

    .feedback {
      margin-top: 10px;
      border-radius: 12px;
      padding: 10px 12px;
      font-size: 0.9rem;
      display: none;
    }
    .feedback.correct {
      background: #ecfdf5;
      color: #166534;
      border: 1px solid #bbf7d0;
    }
    .feedback.wrong {
      background: #fef2f2;
      color: #b91c1c;
      border: 1px solid #fecaca;
    }
    .feedback strong {
      display: block;
      margin-bottom: 4px;
    }

    .next-row {
      margin-top: 10px;
      display: flex;
      justify-content: flex-end;
    }

    .summary {
      text-align: center;
      margin-top: 12px;
      padding-top: 10px;
      border-top: 1px dashed #e5e7eb;
      display: none;
      font-size: 0.9rem;
      color: #374151;
    }
    .summary h3 {
      margin: 0 0 4px;
      font-size: 1.05rem;
    }
    .summary p {
      margin: 0 0 4px;
    }

    @media (min-width: 640px) {
      .choices {
        grid-template-columns: repeat(3, 1fr);
      }
    }
  </style>
</head>
<body>
  <div class="app">
    <h1>เกมทายสถานการณ์เสี่ยง</h1>
    <div class="subtitle">
      เลือกให้ถูกว่าสถานการณ์ต่อไปนี้เป็น <b>เสี่ยงสูง / เสี่ยงปานกลาง / เสี่ยงน้อยหรือปลอดภัย</b>
    </div>

    <div class="badge-row">
      <span class="badge badge-red">🟥 เสี่ยงสูง</span>
      <span class="badge badge-orange">🟧 เสี่ยงปานกลาง</span>
      <span class="badge badge-green">🟩 เสี่ยงน้อย / ปลอดภัย</span>
    </div>

    <div class="status-bar">
      <div>ข้อที่: <span id="qNumber">1</span> / <span id="qTotal">10</span></div>
      <div>คะแนน: <span id="score">0</span></div>
    </div>

    <div class="question-card">
      <h2>สถานการณ์</h2>
      <div class="question-text" id="questionText">
        กำลังโหลดคำถาม...
      </div>

      <div class="choices">
        <button class="btn btn-red" data-choice="high">🟥 เสี่ยงสูง</button>
        <button class="btn btn-orange" data-choice="medium">🟧 เสี่ยงปานกลาง</button>
        <button class="btn btn-green" data-choice="low">🟩 เสี่ยงน้อย / ปลอดภัย</button>
      </div>

      <div class="feedback" id="feedbackBox">
        <strong id="feedbackTitle"></strong>
        <span id="feedbackText"></span>
      </div>

      <div class="next-row">
        <button class="btn btn-gray" id="nextBtn" disabled>ข้อถัดไป ▶</button>
      </div>
    </div>

    <div class="summary" id="summaryBox">
      <h3>สรุปผลการเล่น</h3>
      <p>คุณทำได้ <span id="finalScore">0</span> คะแนน จากทั้งหมด <span id="finalTotal">10</span> ข้อ</p>
      <p id="comment"></p>
      <button class="btn btn-green" id="restartBtn">เริ่มเล่นใหม่ 🔁</button>
    </div>
  </div>

  <script>
    // ข้อมูลสถานการณ์ (ไม่ระบุเนื้อหาโจ่งแจ้ง)
    const QUESTIONS = [
      {
        text: "มีคนไม่รู้จักในโซเชียลทักมาขอรูปส่วนตัวแบบลับ ๆ แลกของรางวัล",
        risk: "high",
        explain: "เป็นสถานการณ์เสี่ยงสูงต่อการถูกล่อลวง ละเมิดสิทธิ และนำไปสู่การคุกคามหรือแบล็กเมล์ได้ ควรปฏิเสธและบล็อก/รายงานบัญชีนั้นทันที."
      },
      {
        text: "เพื่อนชวนไปบ้านสองต่อสองตอนเย็น โดยไม่ได้บอกผู้ปกครองหรือผู้ใหญ่ที่ไว้ใจได้",
        risk: "medium",
        explain: "เป็นสถานการณ์เสี่ยงปานกลาง เพราะอยู่สองต่อสองในสถานที่ส่วนตัว อาจนำไปสู่สถานการณ์ไม่ปลอดภัยได้ ควรมีผู้ใหญ่รับรู้และหลีกเลี่ยงการอยู่ตามลำพัง."
      },
      {
        text: "คุยกับคนรู้จักใหม่ในออนไลน์ แต่ไม่เคยบอกชื่อจริง โรงเรียน หรือที่อยู่ของตัวเอง",
        risk: "low",
        explain: "ถือว่าเสี่ยงน้อยกว่าเมื่อเทียบกับการให้ข้อมูลส่วนตัว แต่ยังควรระมัดระวัง ไม่ส่งรูปส่วนตัว และไม่ไปพบเจอตัวจริงโดยลำพัง."
      },
      {
        text: "เพื่อนส่งคลิปอนาจารเข้ากลุ่มแชตแล้วชวนให้ส่งต่อไปห้องอื่น",
        risk: "high",
        explain: "เป็นพฤติกรรมเสี่ยงสูงและอาจผิดกฎหมายเกี่ยวกับสื่ออนาจารและการละเมิดผู้อื่น ควรหยุดส่งต่อและแจ้งผู้ใหญ่ที่รับผิดชอบ."
      },
      {
        text: "ถูกแฟนกดดันให้ทำในสิ่งที่ตนเองไม่สบายใจ โดยใช้คำขู่ว่า 'ถ้าไม่ทำ แสดงว่าไม่รักกันจริง'",
        risk: "high",
        explain: "เป็นสถานการณ์เสี่ยงสูงและเป็นการกดดันที่ไม่เคารพขอบเขต (consent) ของอีกฝ่าย ควรยืนยันสิทธิในการปฏิเสธและขอคำปรึกษาจากผู้ใหญ่ที่เชื่อถือได้."
      },
      {
        text: "ตั้งค่าความเป็นส่วนตัวในโซเชียลเป็น 'เฉพาะเพื่อน' และไม่รับแอดคนแปลกหน้า",
        risk: "low",
        explain: "เป็นพฤติกรรมที่ช่วยลดความเสี่ยงจากคนแปลกหน้าในออนไลน์ และช่วยป้องกันข้อมูลส่วนตัวได้ดีขึ้น."
      },
      {
        text: "ไปงานปาร์ตี้แล้วดื่มเครื่องดื่มแอลกอฮอล์จำนวนมากจนเริ่มควบคุมตัวเองไม่ได้",
        risk: "high",
        explain: "เป็นสถานการณ์เสี่ยงสูง เพราะการขาดสติทำให้ไม่สามารถปกป้องตนเองได้ และอาจนำไปสู่การถูกหลอกลวงหรือถูกละเมิดได้."
      },
      {
        text: "เพื่อนล้อเลียนรูปร่าง/เพศสภาพของเราในกลุ่มแชต แล้วมีการแชร์ภาพเราโดยไม่ได้ขออนุญาต",
        risk: "medium",
        explain: "เป็นความเสี่ยงด้านการถูกกลั่นแกล้งและละเมิดสิทธิ ควรบันทึกหลักฐาน ขอให้หยุดพฤติกรรม และแจ้งครูหรือผู้ปกครองช่วยเหลือ."
      },
      {
        text: "เมื่อมีคำถามเรื่องเพศที่สงสัย เลือกปรึกษาครูอนามัย/ครูแนะแนว ไม่ค้นหาจากเว็บที่ไม่น่าเชื่อถือ",
        risk: "low",
        explain: "เป็นพฤติกรรมที่เหมาะสมและปลอดภัย ช่วยให้ได้รับข้อมูลที่ถูกต้องและเหมาะสมกับวัย."
      },
      {
        text: "มีคนรู้จักขอรหัสผ่านโซเชียลมีเดียของเรา โดยอ้างว่า 'ถ้าไว้ใจกันต้องให้ดูได้'",
        risk: "high",
        explain: "เป็นสถานการณ์เสี่ยงสูง เพราะอาจนำไปสู่การเข้าถึงข้อมูลส่วนตัวหรือนำไปใช้ในทางที่ไม่เหมาะสม รหัสผ่านควรเป็นความลับส่วนบุคคล."
      },
      {
        text: "ออกไปเดินเล่นหรือวิ่งออกกำลังกายกับเพื่อนในที่สาธารณะที่มีคนพลุกพล่านและบอกผู้ปกครองแล้ว",
        risk: "low",
        explain: "เป็นกิจกรรมที่ช่วยดูแลสุขภาพและมีความปลอดภัยมากขึ้นเมื่อมีผู้อื่นอยู่ด้วยและผู้ปกครองรับทราบ."
      },
      {
        text: "ถ่ายภาพตัวเองในมุมที่ไม่เหมาะสมเก็บไว้ในโทรศัพท์ส่วนตัว โดยคิดว่าไม่มีใครเห็น",
        risk: "high",
        explain: "เป็นความเสี่ยงสูง เพราะไฟล์อาจหลุดออกไปได้จากการถูกแฮ็ก ถูกยืมมือถือ หรือสูญหาย ควรหลีกเลี่ยงการสร้างสื่อเสี่ยงตั้งแต่ต้น."
      }
    ];

    const TOTAL_QUESTIONS = 10; // จำนวนข้อที่เล่นต่อรอบ

    let currentIndex = 0;
    let score = 0;
    let questionOrder = [];

    const qNumberEl = document.getElementById("qNumber");
    const qTotalEl = document.getElementById("qTotal");
    const scoreEl = document.getElementById("score");
    const questionTextEl = document.getElementById("questionText");
    const feedbackBox = document.getElementById("feedbackBox");
    const feedbackTitle = document.getElementById("feedbackTitle");
    const feedbackText = document.getElementById("feedbackText");
    const nextBtn = document.getElementById("nextBtn");
    const summaryBox = document.getElementById("summaryBox");
    const finalScoreEl = document.getElementById("finalScore");
    const finalTotalEl = document.getElementById("finalTotal");
    const commentEl = document.getElementById("comment");
    const restartBtn = document.getElementById("restartBtn");

    const choiceButtons = document.querySelectorAll(".choices .btn");

    function shuffle(array) {
      const arr = array.slice();
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
      return arr;
    }

    function initGame() {
      score = 0;
      currentIndex = 0;
      questionOrder = shuffle(QUESTIONS).slice(0, TOTAL_QUESTIONS);
      qTotalEl.textContent = TOTAL_QUESTIONS;
      scoreEl.textContent = score;
      summaryBox.style.display = "none";
      loadQuestion();
    }

    function loadQuestion() {
      const q = questionOrder[currentIndex];
      qNumberEl.textContent = currentIndex + 1;
      questionTextEl.textContent = q.text;
      feedbackBox.style.display = "none";
      nextBtn.disabled = true;
      choiceButtons.forEach(btn => {
        btn.disabled = false;
      });
    }

    function handleChoice(choice) {
      const q = questionOrder[currentIndex];
      const correct = q.risk === choice;

      choiceButtons.forEach(btn => btn.disabled = true);
      nextBtn.disabled = false;

      if (correct) {
        score++;
        scoreEl.textContent = score;
        feedbackBox.className = "feedback correct";
        feedbackTitle.textContent = "ตอบถูก ✔";
      } else {
        feedbackBox.className = "feedback wrong";
        feedbackTitle.textContent = "ตอบยังไม่ตรง ✔ คำตอบที่เหมาะสมกว่าอยู่ด้านล่าง";
      }
      feedbackText.textContent = q.explain;
      feedbackBox.style.display = "block";
    }

    function showSummary() {
      finalScoreEl.textContent = score;
      finalTotalEl.textContent = TOTAL_QUESTIONS;
      let ratio = score / TOTAL_QUESTIONS;
      let msg = "";
      if (ratio >= 0.8) {
        msg = "เยี่ยมมาก คุณประเมินความเสี่ยงได้ดีและรู้วิธีป้องกันตนเอง";
      } else if (ratio >= 0.5) {
        msg = "ทำได้ดีพอสมควร ลองทบทวนสถานการณ์ที่ตอบผิดเพื่อพัฒนาทักษะการตัดสินใจให้ดียิ่งขึ้น";
      } else {
        msg = "ยังมีหลายสถานการณ์ที่อาจมองข้ามความเสี่ยง ลองย้อนกลับไปอ่านคำอธิบายเพื่อเสริมความรู้และป้องกันตัวเองในชีวิตจริง";
      }
      commentEl.textContent = msg;
      summaryBox.style.display = "block";
    }

    // event listeners
    choiceButtons.forEach(btn => {
      btn.addEventListener("click", () => {
        const choice = btn.getAttribute("data-choice"); // "high" | "medium" | "low"
        handleChoice(choice);
      });
    });

    nextBtn.addEventListener("click", () => {
      if (currentIndex < TOTAL_QUESTIONS - 1) {
        currentIndex++;
        loadQuestion();
      } else {
        showSummary();
      }
    });

    restartBtn.addEventListener("click", () => {
      initGame();
    });

    // เริ่มเกมครั้งแรก
    initGame();
  </script>
</body>
</html>
