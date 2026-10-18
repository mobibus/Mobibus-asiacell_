<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>تجديد باقات خط الفاتورة - Elite</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&display=swap" rel="stylesheet">
<style>
:root {
  --red: #e11d48;
  --red-dark: #be123c;
  --bg1: #0f172a;
  --bg2: #1e293b;
  --ink: #f8fafc;
  --mut: #94a3b8;
  --glass: rgba(255, 255, 255, 0.05);
  --bd: rgba(255, 255, 255, 0.1);
  --sh: 0 10px 30px rgba(0,0,0,0.5);
  --gold: #f59e0b;
}

[data-theme="light"] {
  --bg1: #f8fafc;
  --bg2: #f1f5f9;
  --ink: #0f172a;
  --mut: #475569;
  --glass: rgba(255, 255, 255, 0.85);
  --bd: rgba(0, 0, 0, 0.08);
  --sh: 0 10px 25px rgba(0,0,0,0.08);
}

* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
body { font-family: 'Cairo', sans-serif; color: var(--ink); background: linear-gradient(135deg, var(--bg1), var(--bg2)); min-height: 100vh; padding: 20px 12px; }
.container { max-width: 1200px; margin: 0 auto; display: flex; flex-direction: column; gap: 24px; }

header { display: flex; justify-content: space-between; align-items: center; padding: 16px 24px; border-radius: 20px; background: var(--glass); border: 1px solid var(--bd); box-shadow: var(--sh); backdrop-filter: blur(12px); }
.brand { display: flex; align-items: center; gap: 10px; }
.brand-title { font-size: 22px; font-weight: 900; color: var(--red); }
.theme-btn { padding: 8px 16px; border-radius: 12px; background: var(--glass); border: 1px solid var(--bd); cursor: pointer; font-weight: 700; color: var(--ink); }

.hero { padding: 32px 20px; border-radius: 24px; background: linear-gradient(135deg, var(--red-dark), var(--red)); color: #fff; text-align: center; box-shadow: var(--sh); }
.hero h1 { font-size: 30px; font-weight: 900; margin-bottom: 8px; }
.hero p { opacity: 0.95; font-size: 16px; max-width: 700px; margin: 0 auto; line-height: 1.6; }

/* Table Container */
.table-card { padding: 20px; border-radius: 24px; background: var(--glass); border: 1px solid var(--bd); box-shadow: var(--sh); backdrop-filter: blur(10px); overflow-x: auto; }
.table-title { font-size: 20px; font-weight: 800; margin-bottom: 16px; color: var(--red); display: flex; align-items: center; gap: 8px; }

table { width: 100%; border-collapse: collapse; min-width: 850px; text-align: center; }
th, td { padding: 12px 10px; border: 1px solid var(--bd); font-size: 14px; }
th { background: rgba(225, 29, 72, 0.15); color: var(--ink); font-weight: 800; font-size: 15px; }
tr:hover { background: rgba(255, 255, 255, 0.03); }
.price-head { background: var(--red) !important; color: #fff !important; font-size: 17px !important; font-weight: 900 !important; }
.badge { display: inline-block; padding: 4px 8px; border-radius:
