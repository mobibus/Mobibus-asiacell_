<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>باقات خط الفاتورة Elite & Red Plus</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&display=swap" rel="stylesheet">
<style>
:root {
  --red-main: #e11d48;
  --red-dark: #be123c;
  --bg-dark-1: #0f172a;
  --bg-dark-2: #1e293b;
  --text-main: #f8fafc;
  --text-muted: #94a3b8;
  --glass-bg: rgba(255, 255, 255, 0.05);
  --glass-border: rgba(255, 255, 255, 0.12);
  --card-shadow: 0 12px 32px rgba(0, 0, 0, 0.4);
  --gold: #f59e0b;
  --green: #10b981;
}

[data-theme="light"] {
  --bg-dark-1: #f8fafc;
  --bg-dark-2: #e2e8f0;
  --text-main: #0f172a;
  --text-muted: #475569;
  --glass-bg: rgba(255, 255, 255, 0.85);
  --glass-border: rgba(225, 29, 72, 0.15);
  --card-shadow: 0 10px 25px rgba(225, 29, 72, 0.08);
}

* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
body { font-family: 'Cairo', sans-serif; color: var(--text-main); background: linear-gradient(135deg, var(--bg-dark-1), var(--bg-dark-2)); min-height: 100vh; padding: 20px 12px; }
.container { max-width: 1200px; margin: 0 auto; display: flex; flex-direction: column; gap: 24px; }

header { display: flex; justify-content: space-between; align-items: center; padding: 16px 24px; border-radius: 20px; background: var(--glass-bg); border: 1px solid var(--glass-border); box-shadow: var(--card-shadow); backdrop-filter: blur(12px); }
.brand-title { font-size: 22px; font-weight: 900; color: var(--red-main); }
.theme-btn { padding: 8px 16px; border-radius: 12px; background: var(--glass-bg); border: 1px solid var(--glass-border); cursor: pointer; font-weight: 700; color: var(--text-main); }

.hero { padding: 32px 20px; border-radius: 24px; background: linear-gradient(135deg, var(--red-dark), var(--red-main)); color: #fff; text-align: center; box-shadow: var(--card-shadow); }
.hero h1 { font-size: 28px; font-weight: 900; margin-bottom: 10px; }
.hero p { opacity: 0.95; font-size: 15px; max-width: 750px; margin: 0 auto; line-height: 1.6; }

.section-title { font-size: 22px; font-weight: 800; color: var(--red-main); display: flex; align-items: center; gap: 8px; margin-top: 10px; }

/* Grid Cards */
.pkg-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(340px, 1fr)); gap: 20px; }
.pkg-card { padding: 24px; border-radius: 24px; background: var(--glass-bg); border: 1px solid var(--glass-border); box-shadow: var(--card-shadow); backdrop-filter: blur(10px); display: flex; flex-direction: column; gap: 16px; transition: transform 0.2s; }
.pkg-card:hover { transform: translateY(-4px); }
.pkg-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid var(--glass-border); padding-bottom: 12px; }
.pkg-price { font-size: 24px; font-weight: 900; color: var(--gold); }
.pkg-badge { font-size: 12px; font-weight: 800; padding: 4px 10px; border-radius: 10px; background: rgba(225, 29, 72, 0.15); color: var(--red-main); }

.pkg-details { display: flex; flex-direction: column; gap: 10px; font-size: 14px; }
.line-box { background: rgba(255, 255, 255, 0.03); border: 1px solid var(--glass-border); padding: 10px; border-radius: 12px; display: flex; flex-direction: column; gap: 4px; }
.line-title { font-weight: 800; color: var(--red-main); font-size: 13px; }
.line-desc { font-weight: 700; color: var(--text-main); font-size: 13px; }

.extra-features { background: rgba(16, 185, 129, 0.1); border: 1px solid rgba(16, 185, 129, 0.2); padding: 10px; border-radius: 12px; display: flex; flex-direction: column; gap: 4px; }
.extra-title { font-weight: 800; color: var(--green); font-size: 13px; }

.btn-order { width: 100%; padding: 12px; border-radius: 14px; background: var(--red-main); color: #fff; font-size: 15px; font-weight: 800; border: none; cursor: pointer; transition: 0.2s; margin-top: 8px; }
.btn-order:hover { background: var(--red-dark); }

/* FAQ Section */
.faq-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 16px; margin-top: 10px; }
.faq-card { padding: 20px; border-radius: 20px; background: var(--glass-bg); border: 1px solid var(--glass-border); box-shadow: var(--card-shadow); }
.faq-card h3 { font-size: 15px; font-weight: 800; color: var(--red-main); margin-bottom: 8px; }
.faq-card p, .faq-card ul { font-size: 13px; color: var(--text-muted); line-height: 1.7; }
.faq-card ul { padding-right: 16px; }

/* Modal */
.modal { position: fixed; inset: 0; background: rgba(0,0,0,0.7); backdrop-filter: blur(6px); display: grid; place-items: center; padding: 16px; z-index: 100; }
.modal[hidden] { display: none; }
.modal-box { width: min(100%, 420px); padding: 24px; border-radius: 24px; background: var(--bg-dark-1); border: 1px solid var(--glass-border); box-shadow: var(--card-shadow); display: flex; flex-direction: column; gap: 14px; }
.modal-box h3 { color: var(--red-main); }
.modal-box input { width: 100%; padding: 12px; border-radius: 12px; border: 1px solid var(--glass-border); background: var(--glass-bg); color: var(--text-main); font-weight: 600; }
.modal-actions { display: flex; gap: 10px; }
.modal-actions button { flex: 1; padding: 10px; border-radius: 12px; font-weight: 700; cursor: pointer; }
.btn-submit { background: var(--red-main); color: #fff; border: none; }
.btn-cancel { background: transparent; border: 1px solid var(--glass-border); color: var(--text-main); }
</style>
</head>
<body>

<div class="container">
  <header>
    <div class="brand-title">Elite & Red Plus — خدمات الباقات</div>
    <button class="theme-btn" id="themeToggle">🌓 المظهر</button>
  </header>

  <div class="hero">
    <h1>باقات خط الفاتورة Elite — تفاصيل كاملة</h1>
    <p>استعراض مخصص لجميع الباقات مع تفصيل سعات الخطوط المضافة، المزايا، والخط الرئيسي بدقة متناهية.</p>
  </div>

  <div class="section-title">📦 قائمة الباقات وتفاصيل الخطوط المضافة</div>

  <div class="pkg-grid">
    <!-- باقة 120 -->
    <div class="pkg-card">
      <div class="pkg-header">
        <span class="pkg-price">120,000 د.ع</span>
        <span class="pkg-badge">الباقة الكبرى</span>
      </div>
      <div class="pkg-details">
        <div class="line-box">
          <span class="line-title">تفاصيل الخطوط المضافة (5 خطوط):</span>
          <span class="line-desc">• 500 دقيقة + 60 كيكا (لكل خط)</span>
        </div>
        <div class="extra-features">
          <span class="extra-title">مزايا الخط الرئيسي:</span>
          <span>• يمتلك 7 تطبيقات مجانية</span>
          <span>• 60 دقيقة دولية + 5 كيكا إنترنت</span>
        </div>
      </div>
      <button class="btn-order" onclick="openReserve('باقة 120,000 د.ع')">طلب الاشتراك</button>
    </div>

    <!-- باقة 100 -->
    <div class="pkg-card">
      <div class="pkg-header">
        <span class="pkg-price">100,000 د.ع</span>
        <span class="pkg-badge">باقة مميزة</span>
      </div>
      <div class="pkg-details">
        <div class="line-box">
          <span
