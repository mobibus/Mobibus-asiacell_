<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>مرتّب المستمسكات الاحترافي — تخصيص محمد جواد</title>
<!-- Google Fonts: Cairo & Tajawal -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800;900&family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet">
<!-- jsPDF Library for PDF Export -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

<style>
/* ==========================================================================
   CSS Variables & Design Tokens (Dark & Light Themes)
   ========================================================================== */
:root {
  --bg-gradient-1: #0f3823;
  --bg-gradient-2: #071e13;
  --bg-gradient-3: #1b5e3a;
  --text-main: #f0fdf4;
  --text-muted: #a7f3d0;
  --brand-green: #10b981;
  --brand-green-dark: #047857;
  --brand-gold: #f59e0b;
  --brand-gold-light: #fbbf24;
  
  --glass-bg: rgba(6, 44, 27, 0.65);
  --glass-border: rgba(52, 211, 153, 0.25);
  --glass-shadow: 0 12px 40px 0 rgba(0, 0, 0, 0.37);
  --card-bg: rgba(15, 61, 39, 0.7);
  --card-border: rgba(167, 243, 208, 0.2);
  
  --blob-1: rgba(16, 185, 129, 0.28);
  --blob-2: rgba(245, 158, 11, 0.22);
  --blob-3: rgba(5, 150, 105, 0.3);

  --page-bg: #ffffff;
  --slot-empty-bg: #f0fdf4;
  --slot-empty-border: #34d399;
  --slot-empty-text: #047857;

  box-sizing: border-box;
}

[data-theme="light"] {
  --bg-gradient-1: #e8f5e9;
  --bg-gradient-2: #c8e6c9;
  --bg-gradient-3: #a5d6a7;
  --text-main: #064e3b;
  --text-muted: #047857;
  --brand-green: #059669;
  --brand-green-dark: #047857;
  --brand-gold: #d97706;
  --brand-gold-light: #f59e0b;
  
  --glass-bg: rgba(255, 255, 255, 0.75);
  --glass-border: rgba(255, 255, 255, 0.9);
  --glass-shadow: 0 12px 35px 0 rgba(4, 120, 87, 0.15);
  --card-bg: rgba(255, 255, 255, 0.85);
  --card-border: rgba(167, 243, 208, 0.5);

  --blob-1: rgba(52, 211, 153, 0.35);
  --blob-2: rgba(251, 191, 36, 0.3);
  --blob-3: rgba(16, 185, 129, 0.25);

  --page-bg: #ffffff;
  --slot-empty-bg: #f4fbf7;
  --slot-empty-border: #10b981;
  --slot-empty-text: #047857;
}

/* Base Styles & Resets */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  -webkit-tap-highlight-color: transparent;
}

html, body {
  width: 100%;
  height: 100%;
  overflow: hidden;
  font-family: 'Cairo', 'Tajawal', -apple-system, BlinkMacSystemFont, sans-serif;
  background-color: #071e13;
  color: var(--text-main);
  direction: rtl;
  user-select: none;
}

/* Animated Dynamic Background */
.bg-canvas {
  position: fixed;
  inset: 0;
  z-index: 0;
  background: radial-gradient(circle at 85% 15%, var(--bg-gradient-3), transparent 60%),
              radial-gradient(circle at 15% 85%, var(--bg-gradient-1), transparent 70%),
              linear-gradient(135deg, var(--bg-gradient-2), var(--bg-gradient-1));
  overflow: hidden;
}

.blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(70px);
  pointer-events: none;
  animation: floatAnim 18s ease-in-out infinite alternate;
}

.b1 { width: 320px; height: 320px; top: -80px; right: -80px; background: var(--blob-1); }
.b2 { width: 380px; height: 380px; bottom: -120px; left: -100px; background: var(--blob-2); animation-delay: -5s; }
.b3 { width: 250px; height: 250px; top: 40%; left: 30%; background: var(--blob-3); animation-delay: -10s; }

@keyframes floatAnim {
  0% { transform: translate(0, 0) scale(1); }
  50% { transform: translate(40px, -30px) scale(1.12); }
  100% { transform: translate(-30px, 40px) scale(0.95); }
}

/* Glassmorphism Classes */
.glass {
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  box-shadow: var(--glass-shadow);
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
}

/* View Control */
.view {
  position: fixed;
  inset: 0;
  z-index: 10;
  display: none;
  flex-direction: column;
  padding-top: env(safe-area-inset-top, 0px);
  padding-bottom: env(safe-area-inset-bottom, 0px);
}

.view.active {
  display: flex;
}

/* Typography & Interactive UI Components */
h1, h2, h3 {
  font-weight: 800;
  line-height: 1.2;
}

button, select, input {
  font-family: inherit;
  color: inherit;
  outline: none;
  border: none;
  background: none;
}

button {
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}

button:active {
  transform: scale(0.96);
}

/* ==========================================================================
   Home View Layout
   ========================================================================== */
.home-container {
  margin: auto;
  width: min(92%, 460px);
  display: flex;
  flex-direction: column;
  gap: 20px;
  text-align: center;
  position: relative;
  z-index: 2;
  padding: 20px 0;
}

/* Animated Card Stack Hero Illustration */
.hero-stack {
  position: relative;
  height: 180px;
  width: 260px;
  margin: 0 auto 10px;
}

.hero-card {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 160px;
  height: 100px;
  margin: -50px 0 0 -80px;
  border-radius: 18px;
  border: 1px solid rgba(255, 255, 255, 0.5);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
  padding: 14px;
  display: flex;
  gap: 12px;
  transform: translate(var(--x), var(--y)) rotate(var(--r));
  animation: cardEntrance 1s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards,
             cardFloat 6s ease-in-out infinite 1s;
}

.hero-card .avatar {
  width: 36px;
  height: 46px;
  border-radius: 8px;
  background: currentColor;
  opacity: 0.35;
  flex: none;
}

.hero-card .lines {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 6px;
  padding-top: 4px;
}

.hero-card .lines span {
  height: 6px;
  border-radius: 4px;
  background: currentColor;
  opacity: 0.35;
  display: block;
}

.hero-card .lines span:last-child { width: 60%; }

.hero-card.c1 {
  --x: -45px; --y: 18px; --r: -14deg;
  color: #ffffff;
  background: linear-gradient(135deg, #059669, #10b981);
}

.hero-card.c2 {
  --x: 42px; --y: -10px; --r: 12deg;
  color: #047857;
  background: linear-gradient(135deg, #ffffff, #d1fae5);
  animation-delay: 0.15s, -2s;
}

.hero-card.c3 {
  --x: 0px; --y: 8px; --r: -2deg;
  z-index: 2;
  color: #78350f;
  background: linear-gradient(135deg, #fef3c7, #f59e0b);
  animation-delay: 0.3s, -4s;
}

@keyframes cardEntrance {
  from { opacity: 0; transform: translate(0, 60px) rotate(0) scale(0.5); }
}

@keyframes cardFloat {
  0%, 100% { transform: translate(var(--x), var(--y)) rotate(var(--r)); }
  50% { transform: translate(var(--x), calc(var(--y) - 8px)) rotate(var(--r)); }
}

.app-title {
  font-size: 32px;
  font-weight: 900;
  background: linear-gradient(135deg, #34d399, #10b981 50%, #f59e0b);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  letter-spacing: -0.5px;
}

.app-subtitle {
  font-size: 15px;
  color: var(--text-muted);
  line-height: 1.6;
  margin-top: -6px;
}

.btn-card {
  width: 100%;
  border-radius: 20px;
  padding: 18px 20px;
  display: flex;
  align-items: center;
  gap: 16px;
  text-align: right;
  font-size: 17px;
  font-weight: 700;
  position: relative;
  overflow: hidden;
}

.btn-card.primary {
  background: linear-gradient(135deg, var(--brand-green-dark), var(--brand-green));
  color: #ffffff;
  border-color: rgba(52, 211, 153, 0.4);
  box-shadow: 0 10px 25px rgba(5, 150, 105, 0.4);
}

.btn-card.primary::after {
  content: "";
  position: absolute;
  top: 0; bottom: 0; width: 60px; left: -80px;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  transform: skewX(-20deg);
  animation: shine 4s ease-in-out infinite;
}

@keyframes shine {
  0%, 60% { left: -80px; }
  100% { left: 120%; }
}

.btn-card .icon-box {
  width: 48px;
  height: 48px;
  border-radius: 14px;
  display: grid;
  place-items: center;
  background: rgba(255, 255, 255, 0.2);
  font-size: 24px;
  flex: none;
}

.btn-card small {
  display: block;
  font-size: 12px;
  font-weight: 400;
  opacity: 0.85;
  margin-top: 2px;
}

/* ==========================================================================
   Editor View Layout
   ========================================================================== */
.header-bar {
  display: flex;
  align-items: center;
  gap: 10px;
  margin: 12px 14px 0;
  padding: 8px 12px;
  border-radius: 20px;
  z-index: 20;
}

.header-bar .title {
  flex: 1;
  font-weight: 800;
  font-size: 17px;
  color: var(--text-main);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.icon-btn {
  min-width: 42px;
  height: 42px;
  border-radius: 14px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.12);
  border: 1px solid var(--glass-border);
  color: var(--text-main);
  font-weight: 700;
  font-size: 14px;
  padding: 0 10px;
}

.icon-btn.accent {
  background: linear-gradient(135deg, var(--brand-gold), var(--brand-gold-light));
  color: #3e2404;
  border-color: rgba(245, 158, 11, 0.5);
  box-shadow: 0 4px 15px rgba(245, 158, 11, 0.3);
}

.icon-btn svg {
  width: 20px;
  height: 20px;
  stroke: currentColor;
  fill: none;
  stroke-width: 2.2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* Dropdown Menu Popups */
.dropdown-pop {
  position: absolute;
  top: 65px;
  min-width: 200px;
  border-radius: 18px;
  padding: 8px;
  z-index: 50;
  display: flex;
  flex-direction: column;
  gap: 4px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
  animation: popDown 0.2s ease-out;
}

.dropdown-pop[hidden] { display: none; }

.dropdown-pop button {
  padding: 10px 14px;
  text-align: right;
  border-radius: 12px;
  font-size: 14px;
  font-weight: 600;
  color: var(--text-main);
}

.dropdown-pop button:hover, .dropdown-pop button.active {
  background: var(--brand-green);
  color: #ffffff;
}

@keyframes popDown {
  from { opacity: 0; transform: translateY(-10px) scale(0.95); }
}

/* Paper Page Area Scrollable */
.scroll-area {
  flex: 1;
  overflow-y: auto;
  padding: 16px 14px 260px;
  -webkit-overflow-scrolling: touch;
  background-image: radial-gradient(rgba(52, 211, 153, 0.15) 1.2px, transparent 1.2px);
  background-size: 20px 20px;
}

.page-paper {
  position: relative;
  width: min(100%, 580px);
  margin: 0 auto 8px;
  background: var(--page-bg);
  border-radius: 4px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.35);
  overflow: hidden;
  transition: height 0.2s ease;
}

.page-label {
  width: min(100%, 580px);
  margin: 0 auto 18px;
  text-align: center;
  font-size: 13px;
  font-weight: 600;
  color: var(--text-muted);
}

/* Slots for documents inside paper */
.doc-slot {
  position: absolute;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  cursor: pointer;
  transition: outline 0.15s ease, transform 0.15s ease;
}

.doc-slot.empty {
  border: 2px dashed var(--slot-empty-border);
  background-color: var(--slot-empty-bg);
  display: grid;
  place-items: center;
  color: var(--slot-empty-text);
  font-weight: 700;
  font-size: clamp(11px, 2.8vw, 15px);
  border-radius: calc(var(--u) * 2);
  text-align: center;
  padding: 4px;
}

.doc-slot.selected {
  outline: 3px solid #10b981;
  outline-offset: 3px;
  z-index: 5;
}

.page-hint {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #6b7280;
  padding: 20px;
  text-align: center;
  font-size: 15px;
  line-height: 1.8;
  pointer-events: none;
}

/* Floating Bottom Control Dock */
.bottom-dock {
  position: fixed;
  left: 0; right: 0; bottom: 0;
  padding: 0 12px calc(12px + env(safe-area-inset-bottom, 0px));
  display: flex;
  flex-direction: column;
  gap: 10px;
  z-index: 30;
  pointer-events: none;
}

.bottom-dock > * { pointer-events: auto; }

.controls-sheet {
  border-radius: 24px;
  padding: 14px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-height: 50vh;
  overflow-y: auto;
  animation: slideUp 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.controls-sheet[hidden] { display: none; }

@keyframes slideUp {
  from { opacity: 0; transform: translateY(30px); }
}

.sheet-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-weight: 800;
  font-size: 15px;
}

.btn-row {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
}

.btn-row > * { flex: 1 1 auto; }

.chip-btn {
  padding: 10px 12px;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.12);
  border: 1px solid var(--glass-border);
  font-size: 13px;
  font-weight: 600;
  color: var(--text-main);
  white-space: nowrap;
  text-align: center;
}

.chip-btn.active {
  background: var(--brand-green);
  color: #ffffff;
  border-color: transparent;
}

.chip-btn.danger {
  color: #ef4444;
  border-color: rgba(239, 68, 68, 0.3);
}

.select-custom {
  width: 100%;
  padding: 10px 12px;
  border-radius: 12px;
  border: 1px solid var(--glass-border);
  background: var(--glass-bg);
  color: var(--text-main);
  font-size: 14px;
  font-weight: 600;
}

.select-custom option, .select-custom optgroup {
  color: #064e3b;
  background: #ffffff;
}

.range-label {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 13px;
  font-weight: 600;
}

.range-label input[type=range] {
  flex: 1;
  accent-color: var(--brand-green);
}

/* Export Bar Horizontally Scrollable */
.export-bar {
  border-radius: 20px;
  padding: 8px;
  display: flex;
  gap: 8px;
  overflow-x: auto;
  scrollbar-width: none;
}

.export-bar::-webkit-scrollbar { display: none; }

.exp-chip {
  flex: none;
  padding: 12px 16px;
  border-radius: 14px;
  font-weight: 700;
  font-size: 13px;
  background: linear-gradient(135deg, var(--brand-green), var(--brand-green-dark));
  color: #ffffff;
  white-space: nowrap;
  box-shadow: 0 4px 12px rgba(5, 150, 105, 0.3);
}

.exp-chip.outline {
  background: rgba(255, 255, 255, 0.12);
  color: var(--text-main);
  border: 1px solid var(--glass-border);
  box-shadow: none;
}

.exp-chip.gold {
  background: linear-gradient(135deg, var(--brand-gold-light), var(--brand-gold));
  color: #3e2404;
}

/* ==========================================================================
   Modals (About & Interactive Crop Modal)
   ========================================================================== */
.modal-overlay {
  position: fixed;
  inset: 0;
  z-index: 100;
  background: rgba(0, 0, 0, 0.75);
  display: grid;
  place-items: center;
  padding: 16px;
  backdrop-filter: blur(8px);
}

.modal-overlay[hidden] { display: none; }

.modal-box {
  width: min(100%, 440px);
  border-radius: 28px;
  padding: 24px;
  background: var(--bg-gradient-2);
  border: 1px solid var(--glass-border);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
