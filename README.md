<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>خدمات أسياحيل — محمد جواد</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&display=swap" rel="stylesheet">
<style>
:root {
  --bg1: #061a12;
  --bg2: #0b2e20;
  --ink: #e8f5ee;
  --mut: #9cc7b2;
  --g: #10b981;
  --g2: #059669;
  --gold: #f59e0b;
  --red: #e11d48;
  --glass: rgba(255, 255, 255, 0.07);
  --bd: rgba(255, 255, 255, 0.15);
  --sh: 0 10px 30px rgba(0,0,0,0.4);
}
[data-t=light] {
  --bg1: #f0fdf4;
  --bg2: #dcfce7;
  --ink: #064e3b;
  --mut: #047857;
  --glass: rgba(255, 255, 255, 0.85);
  --bd: rgba(16, 185, 129, 0.2);
  --sh: 0 10px 30px rgba(16, 185, 129, 0.15);
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
body{font-family:'Cairo',sans-serif;color:var(--ink);background:linear-gradient(135deg,var(--bg1),var(--bg2));min-height:100vh;padding:16px}
.container{max-width:1150px;margin:0 auto;display:flex;flex-direction:column;gap:20px}

/* Header & Nav Tabs */
header{display:flex;justify-content:space-between;align-items:center;padding:15px 24px;border-radius:20px;background:var(--glass);border:1px solid var(--bd);box-shadow:var(--sh);backdrop-filter:blur(12px)}
.logo{font-size:22px;font-weight:900;background:linear-gradient(90deg,var(--g),var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.nav-tabs{display:flex;gap:8px}
.tab-btn{padding:8px 16px;border-radius:12px;background:var(--glass);border:1px solid var(--bd);cursor:pointer;font-weight:700;color:var(--ink);transition:0.2s}
.tab-btn.active{background:var(--g);color:#fff;border-color:transparent}
.theme-btn{padding:8px 14px;border-radius:12px;background:var(--glass);border:1px solid var(--bd);cursor:pointer;font-weight:700;color:var(--ink)}

.section-view{display:none;flex-direction:column;gap:20px}
.section-view.active{display:flex}

/* Hero */
.hero{padding:28px;border-radius:24px;background:linear-gradient(135deg,var(--g2),var(--g));color:#fff;text-align:center;box-shadow:var(--sh)}
.hero.red-bg{background:linear-gradient(135deg,#be123c,var(--red))}
.hero h2{font-size:26px;margin-bottom:6px}
.hero p{opacity:0.95;font-size:15px}

/* Filters */
.filters{display:flex;gap:12px;flex-wrap:wrap}
.filters input,.filters select{flex:1;min-width:200px;padding:12px 16px;border-radius:14px;border:1px solid var(--bd);background:var(--glass);color:var(--ink);font-size:15px;font-weight:600}
.filters input::placeholder{color:var(--mut)}

/* Grid Cards */
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:16px}
.number-card{padding:20px;border-radius:20px;background:var(--glass);border:1px solid var(--bd);box-shadow:var(--sh);backdrop-filter:blur(10px);display:flex;flex-direction:column;gap:12px;transition:transform 0.2s}
.number-card:hover{transform:translateY(-4px)}
.num-badge{font-size:22px;font-weight:900;letter-spacing:1px;color:var(--gold);direction:ltr;text-align:right}
.category-tag{font-size:13px;font-weight:700;color:var(--mut)}
.price-box{display:flex;flex-direction:column;gap:2px}
.old-price{font-size:13px;text-decoration:line-through;color:var(--mut)}
.new-price{font-size:18px;font-weight:800;color:var(--ink)}

/* Table */
.table-card{padding:16px;border-radius:20px;background:var(--glass);border:1px solid var(--bd);box-shadow:var(--sh);overflow-x:auto}
table{width:100%;border-collapse:collapse;min-width:850px;text-align:center}
th,td{padding:10px 8px;border:1px solid var(--bd);font-size:13px}
th{background:rgba(16,185,129,0.15);color:var(--ink);font-weight:800}
.price-head{background:var(--g)!important;color:#fff!important;font-size:15px!important}

/* Buttons */
.reserve-btn{padding:10px;border-radius:12px;background:linear-gradient(135deg,var(--g),var(--g2));color:#fff;font-weight:700;border:none;cursor:pointer;transition:0.2s}
.reserve-btn:active{transform:scale(0.97)}

/* Modal */
.modal{position:fixed;inset:0;background:rgba(0,0,0,0.65);backdrop-filter:blur(6px);display:grid;place-items:center;padding:16px;z-index:100}
.modal[hidden]{display:none}
.modal-box{width:min(100%,400px);padding:24px;border-radius:24px;background:var(--bg1);border:1px solid var(--bd);box-shadow:var(--sh);display:flex;flex-direction:column;gap:14px}
.modal-box h3{color:var(--g)}
.modal-box input{width:100%;padding:12px;border-radius:12px;border:1px solid var(--bd);background:var(--glass);color:var(--ink);font-weight:600}
.modal-actions{display:flex;gap:10px}
.modal-actions button{flex:1;padding:10px;border-radius:12px;font-weight:700;cursor:pointer}
.btn-submit{background:var(--g);color:#fff;border:none}
.btn-cancel{background:transparent;border:1px solid var(--bd);color:var(--ink)}

.toast{position:fixed;top:20px;left:50%;transform:translateX(-50%);background:#064e3b;color:#fff;padding:10px 20px;border-radius:14px;font-weight:700;box-shadow:var(--sh);z-index:200}
.toast[hidden]{display:none}
</style>
</head>
<body>

<div class="container">
  <header>
    <div class="logo">موبايلي VIP</div>
    <div class="nav-tabs">
      <button class="tab-btn active" onclick="switchTab('vip')">الأرقام المميزة</button>
      <button class="tab-btn" onclick="switchTab('elite')">باقات Elite</button>
    </div>
    <button class="theme-btn" id="themeToggle">🌓 المظهر</button>
  </header>

  <!-- القسم الأول: الأرقام المميزة والخصومات -->
  <div id="vipSection" class="section-view active">
    <div class="hero">
      <h2>حجز الأرقام المميزة والعروض الحصرية</h2>
      <p>اختر رقمك المميز واستفد من الخصومات الخاصة، واحجزه فوراً عبر الواتساب.</p>
    </div>

    <div class="filters">
      <input type="text" id="searchInput" placeholder="ابحث برقم معين...">
      <select id="catSelect">
        <option value="all">جميع الفئات والعروض</option>
        <option value="gold50">ذهبي (فئة 50)</option>
        <option value="gold100">ذهبي (فئة 100)</option>
        <option value="platinum">بلاتنيوم</option>
        <option value="platinum_plus">بلاتنيوم +</option>
        <option value="yaqout">ياقوت</option>
        <option value="yaqout_plus">ياقوت +</option>
        <option value="yaqout_pp">ياقوت ++</option>
      </select>
    </div>

    <div class="grid" id="numbersGrid"></div>
  </div>

  <!-- القسم الثاني: باقات Elite والفاتورة -->
  <div id="eliteSection" class="section-view">
    <div class="hero red-bg">
      <h2>باقات تجديد خط الفاتورة Elite</h2>
      <p>تعرف على تفاصيل الباقات الجديدة، زيادة الإنترنت، الدقائق، التجوال، ومزايا التواصل المجاني.</p>
    </div>

    <div class="table-card">
      <table>
        <thead>
          <tr>
            <th>الباقة الشهرية</th>
            <th class="price-head">25,000 د.ع</th>
            <th class="price-head">40,000 د.ع</th>
            <th class="price-head">60,000 د.ع</th>
            <th class="price-head">80,000 د.ع</th>
            <th class="price-head">100,000 د.ع</th>
            <th class="price-head">120,000 د.ع</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><strong>دقائق الشبكات</strong></td>
            <td>500 دقيقة</td>
            <td>1,000 دقيقة</td>
            <td>1,200 دقيقة</td>
            <td>1,600 دقيقة</td>
            <td>2,000 دقيقة</td>
            <td>2,500 دقيقة</td>
          </tr>
          <tr>
            <td><strong>الإنترنت</strong></td>
            <td>12 GB</td>
            <td>40 GB</td>
            <td>80 GB</td>
            <td>120 GB</td>
            <td>250 GB</td>
            <td>300 GB</td>
          </tr>
          <tr>
            <td><strong>التجوال الدولي</strong></td>
            <td>—</td>
            <td>—</td>
            <td>1 GB</td>
            <td>2 GB</td>
            <td>4 GB</td>
            <td>5 GB</td>
          </tr>
          <tr>
            <td><strong>منصة 1001</strong></td>
            <td colspan="6">مجاناً لجميع الباقات 🎬</td>
          </tr>
          <tr>
            <td><strong>طلب الباقة</strong></td>
            <td><button class="reserve-btn" onclick="openEliteModal('25,000 د.ع')">طلب</button></td>
            <td><button class="reserve-btn" onclick="openEliteModal('40,000 د.ع')">طلب</button></td>
            <td><button class="reserve-btn" onclick="openEliteModal('60,000 د.ع')">طلب</button></td>
            <td><button class="reserve-btn" onclick="openEliteModal('80,000 د.ع')">طلب</button></td>
            <td><button class="reserve-btn" onclick="openEliteModal('100,000 د.ع')">طلب</button></td>
            <td><button class="reserve-btn" onclick="openEliteModal('120,000 د.ع')">طلب</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>

<!-- نافذة الحجز التفاعلية (Modal) -->
<div class="modal" id="reserveModal" hidden>
  <div class="modal-box">
    <h3 id="modalTitle">تأكيد الحجز</h3>
    <p id="modalSubText" style="font-weight: 700; color: var(--gold);"></p>
    <input type="text" id="clientName" placeholder="الاسم الكامل">
    <input type="tel" id="clientPhone" placeholder="رقم الهاتف للتواصل">
    <div class="modal-actions">
      <button class="btn-submit" id="confirmReserve">إرسال الطلب عبر الواتساب</button>
      <button class="btn-cancel" id="closeModal">إلغاء</button>
    </div>
  </div>
</div>

<div class="toast" id="toast" hidden></div>

<script
