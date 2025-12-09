<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>Smart Facility Management</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    *{box-sizing:border-box;font-family:"Sarabun",system-ui,-apple-system,sans-serif;}

    body{
      margin:0;
      min-height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;
      padding:20px;
      background:linear-gradient(135deg,#ffef9f,#ffe66d,#63a4ff);
    }

    .card{
      width:100%;
      max-width:1024px;
      background:#ffffffee;
      border-radius:18px;
      box-shadow:0 8px 20px rgba(0,0,0,0.18);
      padding:20px 24px 24px;
    }

    h1{
      margin-top:0;
      text-align:center;
      color:#004e92;
    }

    .subtitle{
      text-align:center;
      color:#555;
      margin-bottom:20px;
    }

    /* LOGIN */
    #loginScreen{
      max-width:480px;
      margin:0 auto;
    }

    .form-group{
      margin-bottom:12px;
    }

    label{
      display:block;
      margin-bottom:4px;
      font-size:0.95rem;
      color:#333;
    }

    input[type="text"],
    input[type="password"]{
      width:100%;
      padding:10px 12px;
      border-radius:10px;
      border:1px solid #ccc;
      font-size:0.95rem;
    }

    .btn{
      border:none;
      border-radius:999px;
      padding:10px 18px;
      font-size:0.95rem;
      cursor:pointer;
      color:#fff;
      margin:4px 4px 4px 0;
      transition:transform .15s,box-shadow .15s,opacity .15s;
      display:inline-flex;
      align-items:center;
      justify-content:center;
      gap:6px;
    }

    .btn:hover{
      transform:translateY(-1px);
      box-shadow:0 4px 10px rgba(0,0,0,0.18);
      opacity:0.95;
    }

    .btn-green{background:#2ecc71;}
    .btn-blue{background:#3498db;}
    .btn-red{background:#e74c3c;}

    .login-actions{
      display:flex;
      flex-wrap:wrap;
      justify-content:space-between;
      align-items:center;
      margin-top:10px;
      gap:6px;
    }

    .link{
      background:none;
      border:none;
      padding:0;
      margin:0;
      color:#1a73e8;
      font-size:0.9rem;
      cursor:pointer;
      text-decoration:underline;
    }

    .hint{
      font-size:0.85rem;
      color:#777;
      margin-top:8px;
    }

    /* MAIN APP */
    #appScreen{display:none;}

    .top-bar{
      display:flex;
      justify-content:space-between;
      align-items:center;
      margin-bottom:10px;
      flex-wrap:wrap;
      gap:8px;
    }

    .user-info{
      font-size:0.9rem;
      color:#333;
    }

    .tabs{
      display:flex;
      flex-wrap:wrap;
      margin:10px -4px 16px;
    }

    .tab{
      padding:8px 14px;
      margin:4px;
      border-radius:999px;
      border:none;
      cursor:pointer;
      font-size:0.9rem;
      color:#fff;
      background:linear-gradient(135deg,#ff9f43,#ff6b1a);
      opacity:0.85;
      transition:opacity .15s,transform .15s,box-shadow .15s;
    }

    .tab:hover{
      opacity:1;
      transform:translateY(-1px);
      box-shadow:0 3px 8px rgba(0,0,0,0.18);
    }

    .tab.active{
      opacity:1;
      box-shadow:0 3px 8px rgba(0,0,0,0.22);
    }

    .badge{
      font-size:0.75rem;
      background:#e74c3c;
      color:#fff;
      padding:2px 6px;
      border-radius:999px;
      margin-left:4px;
    }

    .content{
      border-radius:14px;
      background:#f7fbff;
      padding:16px;
      border:1px solid #dde8f5;
      min-height:200px;
    }

    .section{display:none;}
    .section.active{display:block;}

    .grid{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
      gap:12px;
    }

    .card-small{
      background:#ffffff;
      border-radius:12px;
      border:1px solid #e3e3e3;
      padding:12px 14px;
    }

    .card-small h3{
      margin:0 0 4px;
      font-size:1rem;
      color:#004e92;
    }

    .metric{
      font-size:1.4rem;
      font-weight:600;
      margin:4px 0;
    }

    .label{
      font-size:0.8rem;
      color:#777;
    }

    textarea,
    select{
      width:100%;
      padding:8px 10px;
      border-radius:8px;
      border:1px solid #ccc;
      font-size:0.9rem;
      resize:vertical;
    }

    .row{
      display:flex;
      flex-wrap:wrap;
      gap:10px;
    }

    .row > div{flex:1 1 220px;}

    .muted{
      font-size:0.85rem;
      color:#777;
    }

    .admin-only-tag{
      font-size:0.75rem;
      color:#e74c3c;
      margin-left:4px;
    }

    @media(max-width:600px){
      .card{padding:18px 14px;}
    }
  </style>
</head>
<body>
<div class="card">
  <h1>Smart Facility Management</h1>
  <p class="subtitle">ระบบบริหารอาคารสถานที่อัจฉริยะ สำหรับโรงเรียน</p>

  <!-- LOGIN SCREEN -->
  <section id="loginScreen">
    <div class="form-group">
      <label for="username">ชื่อผู้ใช้</label>
      <input type="text" id="username" placeholder="เช่น teacher01, student01, admin">
    </div>
    <div class="form-group">
      <label for="password">รหัสผ่าน</label>
      <input type="password" id="password" placeholder="กรอกรหัสผ่าน">
    </div>

    <div class="login-actions">
      <button class="btn btn-blue" onclick="login()">เข้าสู่ระบบ</button>
      <div>
        <button class="link" onclick="alert('ฟังก์ชันลืมรหัสผ่าน (ตัวอย่าง)')">ลืมรหัสผ่าน</button>
        <span style="margin:0 4px;">|</span>
        <button class="link" onclick="alert('ฟังก์ชันสมัครสมาชิก (ตัวอย่าง)')">สมัครสมาชิก</button>
      </div>
    </div>

    <div style="margin-top:10px;">
      <button class="btn btn-green" onclick="loginAsAdmin()">เข้าสู่โหมดผู้ดูแล (Admin)</button>
    </div>

    <p class="hint">
      * ตัวอย่างสำหรับทดลองระบบ: ใช้ชื่อผู้ใช้ <strong>admin</strong> เพื่อเข้าสู่ระบบในโหมดผู้ดูแล<br>
      * ในการใช้งานจริงสามารถเชื่อมต่อกับระบบบัญชีโรงเรียน (SSO) ได้ในภายหลัง
    </p>
  </section>

  <!-- APP SCREEN -->
  <section id="appScreen">
    <div class="top-bar">
      <div class="user-info">
        ผู้ใช้: <strong><span id="displayUser"></span></strong>
        <span id="roleBadge" class="badge" style="display:none;">ADMIN</span>
      </div>
      <button class="btn btn-red" onclick="logout()">ออกจากระบบ</button>
    </div>

    <div class="tabs">
      <button class="tab active" data-section="dashboard" onclick="switchSection(event)">Dashboard ผู้บริหาร</button>
      <button class="tab" data-section="booking" onclick="switchSection(event)">จองห้อง / ยืมอุปกรณ์</button>
      <button class="tab" data-section="maintenance" onclick="switchSection(event)">แจ้งซ่อมออนไลน์</button>
      <button class="tab admin-only" data-section="energy" onclick="switchSection(event)">
        เปิด–ปิดไฟและแอร์ <span class="admin-only-tag">Admin</span>
      </button>
      <button class="tab admin-only" data-section="cctv" onclick="switchSection(event)">
        ดูกล้องวงจรปิด <span class="admin-only-tag">Admin</span>
      </button>
      <button class="tab" data-section="assets" onclick="switchSection(event)">ข้อมูลอาคารและอุปกรณ์</button>
      <button class="tab" data-section="sso" onclick="switchSection(event)">บัญชีโรงเรียน (SSO)</button>
    </div>

    <div class="content">
      <!-- DASHBOARD -->
      <div class="section active" id="section-dashboard">
        <h2>Dashboard สำหรับผู้บริหาร</h2>
        <p class="muted">ภาพรวมการใช้พื้นที่ พลังงาน และงานซ่อมในโรงเรียน (ข้อมูลตัวอย่าง)</p>
        <div class="grid">
          <div class="card-small">
            <h3>การใช้ห้องเรียนวันนี้</h3>
            <p class="metric">18 / 24</p>
            <p class="label">ห้องที่ถูกจองใช้งาน</p>
          </div>
          <div class="card-small">
            <h3>พลังงานไฟฟ้า (ประมาณการ)</h3>
            <p class="metric">76%</p>
            <p class="label">เทียบกับค่าเฉลี่ยปกติ</p>
          </div>
          <div class="card-small">
            <h3>งานแจ้งซ่อมค้างอยู่</h3>
            <p class="metric">5 รายการ</p>
            <p class="label">อยู่ระหว่างดำเนินการ</p>
          </div>
          <div class="card-small">
            <h3>สถานะระบบ SSO</h3>
            <p class="metric">เชื่อมต่อ</p>
            <p class="label">ครู–นักเรียนสามารถเข้าใช้งานได้</p>
          </div>
        </div>
      </div>

      <!-- BOOKING -->
      <div class="section" id="section-booking">
        <h2>ระบบจองห้องและยืมอุปกรณ์ออนไลน์</h2>
        <p class="muted">ตัวอย่างฟอร์มการจองสำหรับครู–นักเรียน</p>
        <div class="row">
          <div>
            <div class="form-group">
              <label>เลือกประเภทการจอง</label>
              <select>
                <option>จองห้องเรียน</option>
                <option>จองห้องประชุม</option>
                <option>ยืมอุปกรณ์โสตฯ / IT</option>
              </select>
            </div>
            <div class="form-group">
              <label>ชื่อห้อง / อุปกรณ์</label>
              <input type="text" placeholder="เช่น ห้องประชุม 1, โปรเจคเตอร์, ลำโพง">
            </div>
            <div class="form-group">
              <label>วัน–เวลาใช้งาน</label>
              <input type="text" placeholder="เช่น 12 มี.ค. 2569 09:00–11:00 น.">
            </div>
            <button class="btn btn-green">ส่งคำขอจอง</button>
          </div>
          <div>
            <h3>รายการจองล่าสุด (ตัวอย่าง)</h3>
            <ul class="muted">
              <li>ครู ก. จองห้องประชุม 2 – 10:00–12:00 น.</li>
              <li>ครู ข. ยืมโปรเจคเตอร์ – 13:00–15:00 น.</li>
              <li>ชั้น ม.5/3 ใช้ห้องเรียนวิทย์ – ทั้งคาบบ่าย</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- MAINTENANCE -->
      <div class="section" id="section-maintenance">
        <h2>ระบบแจ้งซ่อมออนไลน์</h2>
        <p class="muted">ผู้ใช้สามารถแจ้งปัญหาเกี่ยวกับอาคารและอุปกรณ์ได้จากในระบบ</p>
        <div class="row">
          <div>
            <div class="form-group">
              <label>ประเภทปัญหา</label>
              <select>
                <option>ไฟฟ้า</option>
                <option>แอร์</option>
                <option>โต๊ะ–เก้าอี้</option>
                <option>อุปกรณ์ IT</option>
                <option>อื่น ๆ</option>
              </select>
            </div>
            <div class="form-group">
              <label>สถานที่ / ห้อง</label>
              <input type="text" placeholder="เช่น อาคาร 2 ห้อง 210">
            </div>
            <div class="form-group">
              <label>รายละเอียดปัญหา</label>
              <textarea rows="4" placeholder="เช่น ไฟกะพริบ, แอร์ไม่เย็น, หน้าจอไม่ติด ฯลฯ"></textarea>
            </div>
            <button class="btn btn-blue">ส่งคำขอแจ้งซ่อม</button>
          </div>
          <div>
            <h3>งานซ่อมล่าสุด (ตัวอย่าง)</h3>
            <ul class="muted">
              <li>แอร์ห้อง 305 – อยู่ระหว่างรอช่าง</li>
              <li>หลอดไฟหน้าอาคาร – ซ่อมเสร็จแล้ว</li>
              <li>ปลั๊กไฟห้องโสตฯ – นัดซ่อมวันศุกร์</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- ENERGY (ADMIN) -->
      <div class="section" id="section-energy">
        <h2>ระบบเปิด–ปิดไฟและแอร์อัตโนมัติ (สำหรับผู้ดูแลระบบ)</h2>
        <p class="muted">ส่วนนี้เป็นตัวอย่างหน้าจอบริหารอุปกรณ์พลังงานในอาคาร</p>
        <div class="grid">
          <div class="card-small">
            <h3>อาคาร 1 – ห้องเรียน</h3>
            <p class="label">สถานะปัจจุบัน</p>
            <p class="metric">ไฟ: ON / แอร์: ON</p>
            <button class="btn btn-green">ปรับเป็นโหมดประหยัด</button>
          </div>
          <div class="card-small">
            <h3>อาคาร 2 – ห้องประชุม</h3>
            <p class="metric">ไฟ: OFF / แอร์: OFF</p>
            <button class="btn btn-blue">เปิดใช้งานล่วงหน้า</button>
          </div>
          <div class="card-small">
            <h3>ตั้งเวลาปิดอัตโนมัติ</h3>
            <p class="muted">ตัวอย่าง: ปิดทุกอาคารเวลา 18:30 น.</p>
            <button class="btn btn-red">แก้ไขการตั้งเวลา</button>
          </div>
        </div>
      </div>

      <!-- CCTV (ADMIN) -->
      <div class="section" id="section-cctv">
        <h2>ระบบดูกล้องวงจรปิดเพื่อความปลอดภัย (สำหรับผู้ดูแลระบบ)</h2>
        <p class="muted">ตัวอย่าง layout สำหรับฝังภาพจากกล้องวงจรปิด (ในระบบจริงจะเชื่อมกับ feed ของกล้อง)</p>
        <div class="grid">
          <div class="card-small">
            <h3>กล้อง 1 – ทางเข้าโรงเรียน</h3>
            <div style="background:#000;height:120px;border-radius:8px;"></div>
          </div>
          <div class="card-small">
            <h3>กล้อง 2 – โถงอาคารเรียน</h3>
            <div style="background:#000;height:120px;border-radius:8px;"></div>
          </div>
          <div class="card-small">
            <h3>กล้อง 3 – โรงอาหาร</h3>
            <div style="background:#000;height:120px;border-radius:8px;"></div>
          </div>
        </div>
      </div>

      <!-- ASSETS -->
      <div class="section" id="section-assets">
        <h2>ระบบข้อมูลอาคารและอุปกรณ์</h2>
        <p class="muted">ใช้เก็บข้อมูลอาคาร ห้อง และอุปกรณ์หลักในโรงเรียน</p>
        <div class="row">
          <div>
            <h3>เพิ่มข้อมูล</h3>
            <div class="form-group">
              <label>ประเภท</label>
              <select>
                <option>อาคาร</option>
                <option>ห้อง</option>
                <option>อุปกรณ์</option>
              </select>
            </div>
            <div class="form-group">
              <label>ชื่อ / รายละเอียด</label>
              <input type="text" placeholder="เช่น อาคารเรียน 1, ห้องวิทยาศาสตร์, โปรเจคเตอร์ ฯลฯ">
            </div>
            <button class="btn btn-green">บันทึกข้อมูล</button>
          </div>
          <div>
            <h3>ข้อมูลตัวอย่าง</h3>
            <ul class="muted">
              <li>อาคารเรียน 1 – 4 ชั้น – 24 ห้องเรียน</li>
              <li>ห้องประชุมใหญ่ – รองรับ 200 คน</li>
              <li>โปรเจคเตอร์ – 18 เครื่อง – ใช้งานอยู่ 14</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- SSO -->
      <div class="section" id="section-sso">
        <h2>การเชื่อมต่อกับบัญชีโรงเรียน (Single Sign-On: SSO)</h2>
        <p class="muted">
          แนวคิดการเชื่อม Smart Facility Management เข้ากับบัญชีโรงเรียน  
          เพื่อให้ครู–นักเรียนเข้าใช้งานได้ด้วยบัญชีเดียว (One Account)
        </p>
        <ul class="muted">
          <li>ใช้บัญชีอีเมลโรงเรียนในการเข้าสู่ระบบ</li>
          <li>กำหนดสิทธิ์การใช้งานตามบทบาท (นักเรียน, ครู, ผู้บริหาร, admin)</li>
          <li>ลดปัญหาการลืมรหัสผ่านหลายระบบ</li>
          <li>สามารถเชื่อมกับระบบอื่นของโรงเรียน เช่น งานทะเบียน, LMS, ระบบห้องสมุด</li>
        </ul>
        <button class="btn btn-blue">ดูแผนผังการเชื่อมต่อ SSO (ตัวอย่าง)</button>
      </div>
    </div>
  </section>
</div>

<script>
  let isAdmin = false;

  function login(){
    const user = document.getElementById("username").value.trim();
    const pass = document.getElementById("password").value.trim();

    if(!user || !pass){
      alert("กรุณากรอกชื่อผู้ใช้และรหัสผ่าน");
      return;
    }

    // ตัวอย่าง: ถ้าใส่ชื่อ admin จะถือเป็นผู้ดูแลระบบ
    isAdmin = (user.toLowerCase() === "admin");

    document.getElementById("displayUser").textContent = user;
    document.getElementById("loginScreen").style.display = "none";
    document.getElementById("appScreen").style.display = "block";

    const roleBadge = document.getElementById("roleBadge");
    const adminTabs = document.querySelectorAll(".admin-only");

    if(isAdmin){
      roleBadge.style.display = "inline-block";
      adminTabs.forEach(tab => tab.style.display = "inline-flex");
    }else{
      roleBadge.style.display = "none";
      adminTabs.forEach(tab => tab.style.display = "none");
    }
  }

  function loginAsAdmin(){
    document.getElementById("username").value = "admin";
    document.getElementById("password").value = "admin123";
    login();
  }

  function logout(){
    isAdmin = false;
    document.getElementById("appScreen").style.display = "none";
    document.getElementById("loginScreen").style.display = "block";
    document.getElementById("username").value = "";
    document.getElementById("password").value = "";
  }

  function switchSection(evt){
    const target = evt.currentTarget;
    const sectionName = target.getAttribute("data-section");

    document.querySelectorAll(".tab").forEach(t => t.classList.remove("active"));
    target.classList.add("active");

    document.querySelectorAll(".section").forEach(sec => sec.classList.remove("active"));
    document.getElementById("section-" + sectionName).classList.add("active");
  }
</script>
</body>
</html>
