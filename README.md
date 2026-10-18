<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>حجز الأرقام المميزة</title>
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
  --glass: rgba(255, 255, 255, 0.07);
  --bd: rgba(255, 255, 255, 0.15);
  --sh: 0 10px 30px rgba(0,0,0,0.4);
}
[data-t=light] {
  --bg1: #f0fdf4;
  --bg2: #dcfce7;
  --ink: #064e3b;
  --mut: #047857;
  --glass: rgba(255, 255, 255, 0.8);
  --bd: rgba(16, 185, 129, 0.2);
  --sh: 0 10px 30px rgba(16, 185, 129, 0.15);
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
body{font-family:'Cairo',sans-serif;color:var(--ink);background:linear-gradient(135deg,var(--bg1),var(--bg2));min-height:100vh;padding:20px}
.container{max-width:1100px;margin:0 auto;display:flex;flex-direction:column;gap:20px}
header{display:flex;justify-content:space-between;align-items:center;padding:15px 24px;border-radius:20px;background:var(--glass);border:1px solid var(--bd);box-shadow:var(--sh);backdrop-filter:blur(12px)}
h1{font-size:24px;font-weight:900;background:linear-gradient(90deg,var(--g),var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.theme-btn{padding:8px 16px;border-radius:12px;background:var(--glass);border:1px solid var(--bd);cursor:pointer;font-weight:700;color:var(--ink)}
.hero-card{padding:30px;border-radius:24px;background:linear-gradient(135deg,var(--g2),var(--g));color:#fff;text-align:center;box-shadow:var(--sh)}
.hero-card h2{font-size:28px;margin-bottom:8px}
.hero-card p{opacity:0.9;font-size:15px}
.filters{display:flex;gap:12px;flex-wrap:wrap}
.filters input,.filters select{flex:1;min-width:200px;padding:12px 16px;border-radius:14px;border:1px solid var(--bd);background:var(--glass);color:var(--ink);font-size:15px;font-weight:600}
.filters input::placeholder{color:var(--mut)}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:16px}
.number-card{padding:20px;border-radius:20px;background:var(--glass);border:1px solid var(--bd);box-shadow:var(--sh);backdrop-filter:blur(10px);display:flex;flex-direction:column;gap:12px;transition:transform 0.2s}
.number-card:hover{transform:translateY(-4px)}
.num-badge{font-size:24px;font-weight:900;letter-spacing:1px;color:var(--gold);direction:ltr;text-align:right}
.num-info{display:flex;justify-content:space-between;font-size:13px;color:var(--mut);font-weight:600}
.price{font-size:18px;font-weight:800;color:var(--ink)}
.reserve-btn{padding:10px;border-radius:12px;background:linear-gradient(135deg,var(--g),var(--g2));color:#fff;font-weight:700;border:none;cursor:pointer;transition:opacity 0.2s}
.reserve-btn:active{transform:scale(0.97)}
/* Modal */
.modal{position:fixed;inset:0;background:rgba(0,0,0,0.6);backdrop-filter:blur(6px);display:grid;place-items:center;padding:16px;z-index:100}
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
    <h1>نظام حجز الأرقام المميزة</h1>
    <button class="theme-btn" id="themeToggle">🌓 المظهر</button>
  </header>

  <div class="hero-card">
    <h2>اختر رقمك المميز بكل سهولة</h2>
    <p>تصفح الأرقام المتاحة، اختر الرقم المناسب، واحتجزه خلال ثوانٍ معدودة قبل نفاذه.</p>
  </div>

  <div class="filters">
    <input type="text" id="searchInput" placeholder="ابحث برقم معين (مثلاً: 770 أو 780)...">
    <select id="catSelect">
      <option value="all">جميع الفئات</option>
      <option value="gold">أرقام ذهبية</option>
      <option value="silver">أرقام فضية</option>
      <option value="normal">أرقام مميزة عادية</option>
    </select>
  </div>

  <div class="grid" id="numbersGrid"></div>
</div>

<!-- Modal الحجز -->
<div class="modal" id="reserveModal" hidden>
  <div class="modal-box">
    <h3>تأكيد حجز الرقم</h3>
    <p id="selectedNumText" style="font-weight: 700; font-size: 18px; direction: ltr; text-align: right;"></p>
    <input type="text" id="clientName" placeholder="الاسم الكامل">
    <input type="tel" id="clientPhone" placeholder="رقم الهاتف للتواصل">
    <div class="modal-actions">
      <button class="btn-submit" id="confirmReserve">تأكيد الحجز</button>
      <button class="btn-cancel" id="closeModal">إلغاء</button>
    </div>
  </div>
</div>

<div class="toast" id="toast" hidden></div>

<script>
const $ = id => document.getElementById(id);

// بيانات تجريبية للأرقام المميزة
const numbersData = [
  { id: 1, number: '0780 999 1122', cat: 'gold', price: '150,000 د.ع', status: 'available' },
  { id: 2, number: '0771 555 4433', cat: 'silver', price: '75,000 د.ع', status: 'available' },
  { id: 3, number: '0750 333 8899', cat: 'gold', price: '200,000 د.ع', status: 'available' },
  { id: 4, number: '0790 123 4567', cat: 'normal', price: '45,000 د.ع', status: 'available' },
  { id: 5, number: '0782 777 0011', cat: 'silver', price: '90,000 د.ع', status: 'available' },
  { id: 6, number: '0770 888 2233', cat: 'gold', price: '180,000 د.ع', status: 'available' }
];

let currentSelectedNum = null;

function renderNumbers() {
  const keyword = $('searchInput').value.trim();
  const cat = $('catSelect').value;
  const grid = $('numbersGrid');
  grid.innerHTML = '';

  const filtered = numbersData.filter(item => {
    const matchKey = item.number.includes(keyword);
    const matchCat = (cat === 'all' || item.cat === cat);
    return matchKey && matchCat;
  });

  if (filtered.length === 0) {
    grid.innerHTML = '<p style="grid-column: 1/-1; text-align: center; color: var(--mut);">لا توجد أرقام مطابقة للبحث</p>';
    return;
  }

  filtered.forEach(item => {
    const card = document.createElement('div');
    card.className = 'number-card';
    card.innerHTML = `
      <div class="num-badge">${item.number}</div>
      <div class="num-info">
        <span>الفئة: ${item.cat === 'gold' ? 'ذهبية 🌟' : item.cat === 'silver' ? 'فضية 🥈' : 'مميزة'}</span>
        <span class="price">${item.price}</span>
      </div>
      <button class="reserve-btn" onclick="openModal(${item.id})">حجز الرقم</button>
    `;
    grid.appendChild(card);
  });
}

function showToast(msg) {
  const t = $('toast');
  t.textContent = msg;
  t.hidden = false;
  setTimeout(() => t.hidden = true, 3000);
}

window.openModal = function(id) {
  currentSelectedNum = numbersData.find(n => n.id === id);
  $('selectedNumText').textContent = 'الرقم المختار: ' + currentSelectedNum.number;
  $('clientName').value = '';
  $('clientPhone').value = '';$('reserveModal').hidden = false;
};

$('closeModal').onclick = () =>$('reserveModal').hidden = true;

$('confirmReserve').onclick = () => {
  const name = $('clientName').value.trim();
  const phone = $('clientPhone').value.trim();
  if (!name || !phone) {
    alert('يرجى إدخال الاسم ورقم الهاتف بشكل صحيح');
    return;
  }
  $('reserveModal').hidden = true;
  showToast('تم إرسال طلب حجز الرقم بنجاح! سنتواصل معك قريباً.');
};

$('searchInput').oninput = renderNumbers;
$('catSelect').onchange = renderNumbers;

// تبديل المظهر
$('themeToggle').onclick = () => {
  const root = document.documentElement;
  root.dataset.t = root.dataset.t === 'light' ? 'dark' : 'light';
};

renderNumbers();
</script>
</body>
</html>
