<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <title>الأرقام المميزة - آسياسيل</title>
  <style>
    body {
      font-family: Tahoma;
      background-color: #f9f9f9;
      text-align: center;
    }
    h1 {
      color: #d60000;
      margin-bottom: 30px;
    }
    .category {
      margin: 20px auto;
      padding: 15px;
      border: 2px solid #d60000;
      border-radius: 12px;
      background-color: #fff;
      width: 60%;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      cursor: pointer;
    }
    .category h2 {
      margin: 0;
      color: #d60000;
    }
    .numbers {
      display: none; /* مخفية بشكل افتراضي */
      margin-top: 15px;
    }
    .number {
      display: inline-block;
      margin: 10px;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 8px;
      background-color: #ffeaea;
      font-size: 18px;
      font-weight: bold;
      color: #333;
      width: 180px;
      position: relative;
    }
    .number::before {
      content: "★";
      color: gold;
      font-size: 20px;
      position: absolute;
      left: 10px;
      top: 5px;
    }
  </style>
</head>
<body>
  <h1>الأرقام المميزة - آسياسيل</h1>

  <div class="category" onclick="toggleNumbers(this)">
    <h2>فئة 50,000 دينار</h2>
    <div class="numbers">
      <div class="number">0770 123 4567</div>
      <div class="number">0770 765 4321</div>
    </div>
  </div>

  <div class="category" onclick="toggleNumbers(this)">
    <h2>فئة 100,000 دينار</h2>
    <div class="numbers">
      <div class="number">0771 111 2222</div>
      <div class="number">0771 333 4444</div>
    </div>
  </div>

  <div class="category" onclick="toggleNumbers(this)">
    <h2>فئة 250,000 دينار</h2>
    <div class="numbers">
      <div class="number">0772 555 6666</div>
      <div class="number">0772 777 8888</div>
    </div>
  </div>

  <div class="category" onclick="toggleNumbers(this)">
    <h2>فئة 500,000 دينار</h2>
    <div class="numbers">
      <div class="number">0773 999 0000</div>
    </div>
  </div>

  <div class="category" onclick="toggleNumbers(this)">
    <h2>فئة 1,000,000 دينار</h2>
    <div class="numbers">
      <div class="number">0774 123 1234</div>
    </div>
  </div>

  <div class="category" onclick="toggleNumbers(this)">
    <h2>فئة 2,000,000 دينار</h2>
    <div class="numbers">
      <div class="number">0775 456 4567</div>
    </div>
  </div>

  <div class="category" onclick="toggleNumbers(this)">
    <h2>فئة 3,500,000 دينار</h2>
    <div class="numbers">
      <div class="number">0776 789 7890</div>
    </div>
  </div>

  <script>
    function toggleNumbers(category) {
      const numbers = category.querySelector(".numbers");
      numbers.style.display = (numbers.style.display === "block") ? "none" : "block";
    }
  </script>
</body>
</html>
