<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <title>اختيار رقم - آسياسيل</title>
  <style>
    body {
      font-family: 'Tahoma', sans-serif;
      background: #f8f9fa;
      margin: 0;
      padding: 20px;
      direction: rtl;
    }
    header {
      text-align: center;
      background: #d60000;
      padding: 15px;
      border-radius: 8px;
      margin-bottom: 20px;
    }
    header img {
      width: 200px;
    }
    h1 {
      text-align: center;
      color: #d60000;
    }
    .options {
      display: flex;
      justify-content: center;
      gap: 15px;
      margin: 20px 0;
    }
    .option {
      background: #fff;
      border: 1px solid #ccc;
      padding: 10px 20px;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s;
    }
    .option:hover {
      background: #ffe5e5;
      border-color: #d60000;
    }
    .search-box {
      text-align: center;
      margin: 20px 0;
    }
    input {
      padding: 10px;
      width: 60%;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 16px;
    }
    button {
      padding: 10px 20px;
      margin-left: 10px;
      background: #d60000;
      color: #fff;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    .numbers {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 15px;
      margin: 20px 0;
    }
    .num-box {
      background: #fff;
      border: 1px solid #ccc;
      padding: 15px;
      text-align: center;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s;
    }
    .num-box:hover {
      background: #ffe5e5;
      border-color: #d60000;
    }
    .summary {
      background: #fff;
      border: 1px solid #ccc;
      padding: 20px;
      border-radius: 8px;
      margin-top: 20px;
    }
    .summary h2 {
      color: #d60000;
    }
  </style>
</head>
<body>
  <header>
    <img src="asiacell-logo.png" alt="Asiacell Logo">
  </header>
  <h1>اختيار رقمك المميز</h1>

  <div class="options">
    <div class="option">REGULAR LINE</div>
    <div class="option">SILVER</div>
    <div class="option">GOLD</div>
    <div class="option">GOLD+</div>
  </div>

  <div class="search-box">
    <input type="text" id="search" placeholder="أدخل 4 إلى 10 أرقام...">
    <button onclick="searchNumbers()">بحث</button>
  </div>

  <div class="numbers" id="numbers">
    <div class="num-box" onclick="selectNumber('7714736506')">7714736506</div>
    <div class="num-box" onclick="selectNumber('7714736941')">7714736941</div>
    <div class="num-box" onclick="selectNumber('7714737582')">7714737582</div>
    <div class="num-box" onclick="selectNumber('7715231635')">7715231635</div>
    <div class="num-box" onclick="selectNumber('7715231637')">7715231637</div>
    <div class="num-box" onclick="selectNumber('7715231650')">7715231650</div>
  </div>

  <div class="summary" id="summary">
    <h2>ملخص الطلب</h2>
    <p>الرقم: <span id="selectedNumber">لم يتم اختيار رقم</span></p>
    <p>السعر: 0 دينار</p>
    <p>رسوم الحجز: 0 دينار</p>
    <p>المجموع: 0 دينار</p>
  </div>

  <script>
    function selectNumber(num) {
      document.getElementById('selectedNumber').textContent = num;
    }
    function searchNumbers() {
      const filter = document.getElementById('search').value;
      const boxes = document.querySelectorAll('.num-box');
      boxes.forEach(box => {
        if (box.textContent.includes(filter)) {
          box.style.display = '';
        } else {
          box.style.display = 'none';
        }
      });
    }
  </script>
</body>
</html>
