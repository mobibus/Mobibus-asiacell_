‏<!DOCTYPE html>
‏<html lang="ar" dir="rtl">
‏<head>
‏<meta charset="utf-8">
‏<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
‏<title>مرتّب المستمسكات الاحترافي</title>
‏<!-- Google Fonts: Cairo & Tajawal -->
‏<link rel="preconnect" href="https://fonts.googleapis.com">
‏<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
‏<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800;900&family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet">
‏<!-- jsPDF Library for PDF Export -->
‏<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

‏<style>
/* ==========================================================================
‏   CSS Variables & Design Tokens (Dark & Light Themes)
   ========================================================================== */
‏:root {
‏  --bg-gradient-1: #0f3823;
‏  --bg-gradient-2: #071e13;
‏  --bg-gradient-3: #1b5e3a;
‏  --text-main: #f0fdf4;
‏  --text-muted: #a7f3d0;
‏  --brand-green: #10b981;
‏  --brand-green-dark: #047857;
‏  --brand-gold: #f59e0b;
‏  --brand-gold-light: #fbbf24;
  
‏  --glass-bg: rgba(6, 44, 27, 0.65);
‏  --glass-border: rgba(52, 211, 153, 0.25);
‏  --glass-shadow: 0 12px 40px 0 rgba(0, 0, 0, 0.37);
‏  --card-bg: rgba(15, 61, 39, 0.7);
‏  --card-border: rgba(167, 243, 208, 0.2);
  
‏  --blob-1: rgba(16, 185, 129, 0.28);
‏  --blob-2: rgba(245, 158, 11, 0.22);
‏  --blob-3: rgba(5, 150, 105, 0.3);

‏  --page-bg: #ffffff;
‏  --slot-empty-bg: #f0fdf4;
‏  --slot-empty-border: #34d399;
‏  --slot-empty-text: #047857;

‏  box-sizing: border-box;
}

‏[data-theme="light"] {
‏  --bg-gradient-1: #e8f5e9;
‏  --bg-gradient-2: #c8e6c9;
‏  --bg-gradient-3: #a5d6a7;
‏  --text-main: #064e3b;
‏  --text-muted: #047857;
‏  --brand-green: #059669;
‏  --brand-green-dark: #047857;
‏  --brand-gold: #d97706;
‏  --brand-gold-light: #f59e0b;
  
‏  --glass-bg: rgba(255, 255, 255, 0.75);
‏  --glass-border: rgba(255, 255, 255, 0.9);
‏  --glass-shadow: 0 12px 35px 0 rgba(4, 120, 87, 0.15);
‏  --card-bg: rgba(255, 255, 255, 0.85);
‏  --card-border: rgba(167, 243, 208, 0.5);

‏  --blob-1: rgba(52, 211, 153, 0.35);
‏  --blob-2: rgba(251, 191, 36, 0.3);
‏  --blob-3: rgba(16, 185, 129, 0.25);

‏  --page-bg: #ffffff;
‏  --slot-empty-bg: #f4fbf7;
‏  --slot-empty-border: #10b981;
‏  --slot-empty-text: #047857;
}

‏/* Base Styles & Resets */
‏*, *::before, *::after {
‏  box-sizing: border-box;
‏  margin: 0;
‏  padding: 0;
‏  -webkit-tap-highlight-color: transparent;
}

‏html, body {
‏  width: 100%;
‏  height: 100%;
‏  overflow: hidden;
‏  font-family: 'Cairo', 'Tajawal', -apple-system, BlinkMacSystemFont, sans-serif;
‏  background-color: #071e13;
‏  color: var(--text-main);
‏  direction: rtl;
‏  user-select: none;
}

‏/* Animated Dynamic Background */
‏.bg-canvas {
‏  position: fixed;
‏  inset: 0;
‏  z-index: 0;
‏  background: radial-gradient(circle at 85% 15%, var(--bg-gradient-3), transparent 60%),
‏              radial-gradient(circle at 15% 85%, var(--bg-gradient-1), transparent 70%),
‏              linear-gradient(135deg, var(--bg-gradient-2), var(--bg-gradient-1));
‏  overflow: hidden;
}

‏.blob {
‏  position: absolute;
‏  border-radius: 50%;
‏  filter: blur(70px);
‏  pointer-events: none;
‏  animation: floatAnim 18s ease-in-out infinite alternate;
}

‏.b1 { width: 320px; height: 320px; top: -80px; right: -80px; background: var(--blob-1); }
‏.b2 { width: 380px; height: 380px; bottom: -120px; left: -100px; background: var(--blob-2); animation-delay: -5s; }
‏.b3 { width: 250px; height: 250px; top: 40%; left: 30%; background: var(--blob-3); animation-delay: -10s; }

‏@keyframes floatAnim {
‏  0% { transform: translate(0, 0) scale(1); }
‏  50% { transform: translate(40px, -30px) scale(1.12); }
‏  100% { transform: translate(-30px, 40px) scale(0.95); }
}

‏/* Glassmorphism Classes */
‏.glass {
‏  background: var(--glass-bg);
‏  border: 1px solid var(--glass-border);
‏  box-shadow: var(--glass-shadow);
‏  backdrop-filter: blur(16px) saturate(180%);
‏  -webkit-backdrop-filter: blur(16px) saturate(180%);
}

‏/* View Control */
‏.view {
‏  position: fixed;
‏  inset: 0;
‏  z-index: 10;
‏  display: none;
‏  flex-direction: column;
‏  padding-top: env(safe-area-inset-top, 0px);
‏  padding-bottom: env(safe-area-inset-bottom, 0px);
}

‏.view.active {
‏  display: flex;
}

‏/* Typography & Interactive UI Components */
‏h1, h2, h3 {
‏  font-weight: 800;
‏  line-height: 1.2;
}

‏button, select, input {
‏  font-family: inherit;
‏  color: inherit;
‏  outline: none;
‏  border: none;
‏  background: none;
}

‏button {
‏  cursor: pointer;
‏  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}

‏button:active {
‏  transform: scale(0.96);
}

/* ==========================================================================
‏   Home View Layout
   ========================================================================== */
‏.home-container {
‏  margin: auto;
‏  width: min(92%, 460px);
‏  display: flex;
‏  flex-direction: column;
‏  gap: 20px;
‏  text-align: center;
‏  position: relative;
‏  z-index: 2;
‏  padding: 20px 0;
}

‏/* Animated Card Stack Hero Illustration */
‏.hero-stack {
‏  position: relative;
‏  height: 180px;
‏  width: 260px;
‏  margin: 0 auto 10px;
}

‏.hero-card {
‏  position: absolute;
‏  left: 50%;
‏  top: 50%;
‏  width: 160px;
‏  height: 100px;
‏  margin: -50px 0 0 -80px;
‏  border-radius: 18px;
‏  border: 1px solid rgba(255, 255, 255, 0.5);
‏  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
‏  padding: 14px;
‏  display: flex;
‏  gap: 12px;
‏  transform: translate(var(--x), var(--y)) rotate(var(--r));
‏  animation: cardEntrance 1s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards,
‏             cardFloat 6s ease-in-out infinite 1s;
}

‏.hero-card .avatar {
‏  width: 36px;
‏  height: 46px;
‏  border-radius: 8px;
‏  background: currentColor;
‏  opacity: 0.35;
‏  flex: none;
}

‏.hero-card .lines {
‏  flex: 1;
‏  display: flex;
‏  flex-direction: column;
‏  gap: 6px;
‏  padding-top: 4px;
}

‏.hero-card .lines span {
‏  height: 6px;
‏  border-radius: 4px;
‏  background: currentColor;
‏  opacity: 0.35;
‏  display: block;
}

‏.hero-card .lines span:last-child { width: 60%; }

‏.hero-card.c1 {
‏  --x: -45px; --y: 18px; --r: -14deg;
‏  color: #ffffff;
‏  background: linear-gradient(135deg, #059669, #10b981);
}

‏.hero-card.c2 {
‏  --x: 42px; --y: -10px; --r: 12deg;
‏  color: #047857;
‏  background: linear-gradient(135deg, #ffffff, #d1fae5);
‏  animation-delay: 0.15s, -2s;
}

‏.hero-card.c3 {
‏  --x: 0px; --y: 8px; --r: -2deg;
‏  z-index: 2;
‏  color: #78350f;
‏  background: linear-gradient(135deg, #fef3c7, #f59e0b);
‏  animation-delay: 0.3s, -4s;
}

‏@keyframes cardEntrance {
‏  from { opacity: 0; transform: translate(0, 60px) rotate(0) scale(0.5); }
}

‏@keyframes cardFloat {
‏  0%, 100% { transform: translate(var(--x), var(--y)) rotate(var(--r)); }
‏  50% { transform: translate(var(--x), calc(var(--y) - 8px)) rotate(var(--r)); }
}

‏.app-title {
‏  font-size: 32px;
‏  font-weight: 900;
‏  background: linear-gradient(135deg, #34d399, #10b981 50%, #f59e0b);
‏  -webkit-background-clip: text;
‏  background-clip: text;
‏  color: transparent;
‏  letter-spacing: -0.5px;
}

‏.app-subtitle {
‏  font-size: 15px;
‏  color: var(--text-muted);
‏  line-height: 1.6;
‏  margin-top: -6px;
}

‏.btn-card {
‏  width: 100%;
‏  border-radius: 20px;
‏  padding: 18px 20px;
‏  display: flex;
‏  align-items: center;
‏  gap: 16px;
‏  text-align: right;
‏  font-size: 17px;
‏  font-weight: 700;
‏  position: relative;
‏  overflow: hidden;
}

‏.btn-card.primary {
‏  background: linear-gradient(135deg, var(--brand-green-dark), var(--brand-green));
‏  color: #ffffff;
‏  border-color: rgba(52, 211, 153, 0.4);
‏  box-shadow: 0 10px 25px rgba(5, 150, 105, 0.4);
}

‏.btn-card.primary::after {
‏  content: "";
‏  position: absolute;
‏  top: 0; bottom: 0; width: 60px; left: -80px;
‏  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
‏  transform: skewX(-20deg);
‏  animation: shine 4s ease-in-out infinite;
}

‏@keyframes shine {
‏  0%, 60% { left: -80px; }
‏  100% { left: 120%; }
}

‏.btn-card .icon-box {
‏  width: 48px;
‏  height: 48px;
‏  border-radius: 14px;
‏  display: grid;
‏  place-items: center;
‏  background: rgba(255, 255, 255, 0.2);
‏  font-size: 24px;
‏  flex: none;
}

‏.btn-card small {
‏  display: block;
‏  font-size: 12px;
‏  font-weight: 400;
‏  opacity: 0.85;
‏  margin-top: 2px;
}

/* ==========================================================================
‏   Editor View Layout
   ========================================================================== */
‏.header-bar {
‏  display: flex;
‏  align-items: center;
‏  gap: 10px;
‏  margin: 12px 14px 0;
‏  padding: 8px 12px;
‏  border-radius: 20px;
‏  z-index: 20;
}

‏.header-bar .title {
‏  flex: 1;
‏  font-weight: 800;
‏  font-size: 17px;
‏  color: var(--text-main);
‏  white-space: nowrap;
‏  overflow: hidden;
‏  text-overflow: ellipsis;
}

‏.icon-btn {
‏  min-width: 42px;
‏  height: 42px;
‏  border-radius: 14px;
‏  display: inline-flex;
‏  align-items: center;
‏  justify-content: center;
‏  background: rgba(255, 255, 255, 0.12);
‏  border: 1px solid var(--glass-border);
‏  color: var(--text-main);
‏  font-weight: 700;
‏  font-size: 14px;
‏  padding: 0 10px;
}

‏.icon-btn.accent {
‏  background: linear-gradient(135deg, var(--brand-gold), var(--brand-gold-light));
‏  color: #3e2404;
‏  border-color: rgba(245, 158, 11, 0.5);
‏  box-shadow: 0 4px 15px rgba(245, 158, 11, 0.3);
}

‏.icon-btn svg {
‏  width: 20px;
‏  height: 20px;
‏  stroke: currentColor;
‏  fill: none;
‏  stroke-width: 2.2;
‏  stroke-linecap: round;
‏  stroke-linejoin: round;
}

‏/* Dropdown Menu Popups */
‏.dropdown-pop {
‏  position: absolute;
‏  top: 65px;
‏  min-width: 200px;
‏  border-radius: 18px;
‏  padding: 8px;
‏  z-index: 50;
‏  display: flex;
‏  flex-direction: column;
‏  gap: 4px;
‏  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
‏  animation: popDown 0.2s ease-out;
}

‏.dropdown-pop[hidden] { display: none; }

‏.dropdown-pop button {
‏  padding: 10px 14px;
‏  text-align: right;
‏  border-radius: 12px;
‏  font-size: 14px;
‏  font-weight: 600;
‏  color: var(--text-main);
}

‏.dropdown-pop button:hover, .dropdown-pop button.active {
‏  background: var(--brand-green);
‏  color: #ffffff;
}

‏@keyframes popDown {
‏  from { opacity: 0; transform: translateY(-10px) scale(0.95); }
}

‏/* Paper Page Area Scrollable */
‏.scroll-area {
‏  flex: 1;
‏  overflow-y: auto;
‏  padding: 16px 14px 260px;
‏  -webkit-overflow-scrolling: touch;
‏  background-image: radial-gradient(rgba(52, 211, 153, 0.15) 1.2px, transparent 1.2px);
‏  background-size: 20px 20px;
}

‏.page-paper {
‏  position: relative;
‏  width: min(100%, 580px);
‏  margin: 0 auto 8px;
‏  background: var(--page-bg);
‏  border-radius: 4px;
‏  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.35);
‏  overflow: hidden;
‏  transition: height 0.2s ease;
}

‏.page-label {
‏  width: min(100%, 580px);
‏  margin: 0 auto 18px;
‏  text-align: center;
‏  font-size: 13px;
‏  font-weight: 600;
‏  color: var(--text-muted);
}

‏/* Slots for documents inside paper */
‏.doc-slot {
‏  position: absolute;
‏  background-size: cover;
‏  background-position: center;
‏  background-repeat: no-repeat;
‏  cursor: pointer;
‏  transition: outline 0.15s ease, transform 0.15s ease;
}

‏.doc-slot.empty {
‏  border: 2px dashed var(--slot-empty-border);
‏  background-color: var(--slot-empty-bg);
‏  display: grid;
‏  place-items: center;
‏  color: var(--slot-empty-text);
‏  font-weight: 700;
‏  font-size: clamp(11px, 2.8vw, 15px);
‏  border-radius: calc(var(--u) * 2);
‏  text-align: center;
‏  padding: 4px;
}

‏.doc-slot.selected {
‏  outline: 3px solid #10b981;
‏  outline-offset: 3px;
‏  z-index: 5;
}

‏.page-hint {
‏  position: absolute;
‏  inset: 0;
‏  display: flex;
‏  flex-direction: column;
‏  align-items: center;
‏  justify-content: center;
‏  color: #6b7280;
‏  padding: 20px;
‏  text-align: center;
‏  font-size: 15px;
‏  line-height: 1.8;
‏  pointer-events: none;
}

‏/* Floating Bottom Control Dock */
‏.bottom-dock {
‏  position: fixed;
‏  left: 0; right: 0; bottom: 0;
‏  padding: 0 12px calc(12px + env(safe-area-inset-bottom, 0px));
‏  display: flex;
‏  flex-direction: column;
‏  gap: 10px;
‏  z-index: 30;
‏  pointer-events: none;
}

‏.bottom-dock > * { pointer-events: auto; }

‏.controls-sheet {
‏  border-radius: 24px;
‏  padding: 14px;
‏  display: flex;
‏  flex-direction: column;
‏  gap: 10px;
‏  max-height: 50vh;
‏  overflow-y: auto;
‏  animation: slideUp 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

‏.controls-sheet[hidden] { display: none; }

‏@keyframes slideUp {
‏  from { opacity: 0; transform: translateY(30px); }
}

‏.sheet-header {
‏  display: flex;
‏  align-items: center;
‏  justify-content: space-between;
‏  font-weight: 800;
‏  font-size: 15px;
}

‏.btn-row {
‏  display: flex;
‏  gap: 8px;
‏  flex-wrap: wrap;
}

‏.btn-row > * { flex: 1 1 auto; }

‏.chip-btn {
‏  padding: 10px 12px;
‏  border-radius: 12px;
‏  background: rgba(255, 255, 255, 0.12);
‏  border: 1px solid var(--glass-border);
‏  font-size: 13px;
‏  font-weight: 600;
‏  color: var(--text-main);
‏  white-space: nowrap;
‏  text-align: center;
}

‏.chip-btn.active {
‏  background: var(--brand-green);
‏  color: #ffffff;
‏  border-color: transparent;
}

‏.chip-btn.danger {
‏  color: #ef4444;
‏  border-color: rgba(239, 68, 68, 0.3);
}

‏.select-custom {
‏  width: 100%;
‏  padding: 10px 12px;
‏  border-radius: 12px;
‏  border: 1px solid var(--glass-border);
‏  background: var(--glass-bg);
‏  color: var(--text-main);
‏  font-size: 14px;
‏  font-weight: 600;
}

‏.select-custom option, .select-custom optgroup {
‏  color: #064e3b;
‏  background: #ffffff;
}

‏.range-label {
‏  display: flex;
‏  align-items: center;
‏  gap: 10px;
‏  font-size: 13px;
‏  font-weight: 600;
}

‏.range-label input[type=range] {
‏  flex: 1;
‏  accent-color: var(--brand-green);
}

‏/* Export Bar Horizontally Scrollable */
‏.export-bar {
‏  border-radius: 20px;
‏  padding: 8px;
‏  display: flex;
‏  gap: 8px;
‏  overflow-x: auto;
‏  scrollbar-width: none;
}

‏.export-bar::-webkit-scrollbar { display: none; }

‏.exp-chip {
‏  flex: none;
‏  padding: 12px 16px;
‏  border-radius: 14px;
‏  font-weight: 700;
‏  font-size: 13px;
‏  background: linear-gradient(135deg, var(--brand-green), var(--brand-green-dark));
‏  color: #ffffff;
‏  white-space: nowrap;
‏  box-shadow: 0 4px 12px rgba(5, 150, 105, 0.3);
}

‏.exp-chip.outline {
‏  background: rgba(255, 255, 255, 0.12);
‏  color: var(--text-main);
‏  border: 1px solid var(--glass-border);
‏  box-shadow: none;
}

‏.exp-chip.gold {
‏  background: linear-gradient(135deg, var(--brand-gold-light), var(--brand-gold));
‏  color: #3e2404;
}

/* ==========================================================================
‏   Modals (About & Interactive Crop Modal)
   ========================================================================== */
‏.modal-overlay {
‏  position: fixed;
‏  inset: 0;
‏  z-index: 100;
‏  background: rgba(0, 0, 0, 0.75);
‏  display: grid;
‏  place-items: center;
‏  padding: 16px;
‏  backdrop-filter: blur(8px);
}

‏.modal-overlay[hidden] { display: none; }

‏.modal-box {
‏  width: min(100%, 440px);
‏  border-radius: 28px;
‏  padding: 24px;
‏  background: var(--bg-gradient-2);
‏  border: 1px solid var(--glass-border);
‏  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
‏  line-height: 1.8;
‏  color: var(--text-main);
}

‏.modal-box h2 {
‏  color: var(--brand-green);
‏  margin-bottom: 12px;
}

‏.modal-box a {
‏  color: var(--brand-gold-light);
‏  font-weight: 700;
‏  word-break: break-all;
}

‏/* Crop Container */
‏.crop-wrapper {
‏  width: min(100%, 540px);
‏  display: flex;
‏  flex-direction: column;
‏  gap: 16px;
‏  align-items: center;
}

‏.crop-box {
‏  position: relative;
‏  direction: ltr;
‏  display: inline-block;
‏  touch-action: none;
‏  user-select: none;
‏  max-width: 100%;
}

‏.crop-box img {
‏  display: block;
‏  max-width: 100%;
‏  max-height: 60vh;
‏  border-radius: 8px;
‏  pointer-events: none;
}

‏#cropRect {
‏  position: absolute;
‏  border: 2px solid #34d399;
‏  box-shadow: 0 0 0 9999px rgba(0, 0, 0, 0.65);
‏  touch-action: none;
‏  cursor: move;
}

‏#cropRect handle {
‏  position: absolute;
‏  width: 28px;
‏  height: 28px;
‏  background: #34d399;
‏  border-radius: 50%;
‏  border: 3px solid #ffffff;
‏  box-shadow: 0 2px 8px rgba(0,0,0,0.4);
}

‏#cropRect handle[data-pos="tl"] { left: -14px; top: -14px; }
‏#cropRect handle[data-pos="tr"] { right: -14px; top: -14px; }
‏#cropRect handle[data-pos="bl"] { left: -14px; bottom: -14px; }
‏#cropRect handle[data-pos="br"] { right: -14px; bottom: -14px; }

‏/* Toast Notification */
‏.toast-msg {
‏  position: fixed;
‏  left: 50%;
‏  top: calc(env(safe-area-inset-top, 0px) + 20px);
‏  transform: translateX(-50%);
‏  z-index: 200;
‏  background: #064e3b;
‏  color: #ffffff;
‏  padding: 12px 22px;
‏  border-radius: 20px;
‏  font-size: 14px;
‏  font-weight: 700;
‏  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
‏  border: 1px solid var(--brand-green);
‏  text-align: center;
‏  max-width: 88%;
}

‏.toast-msg[hidden] { display: none; }
‏</style>
‏</head>

‏<body>

‏<!-- Background Layer -->
‏<div class="bg-canvas">
‏  <div class="blob b1"></div>
‏  <div class="blob b2"></div>
‏  <div class="blob b3"></div>
‏</div>

<!-- ==========================================================================
‏     View 1: Home View
     ========================================================================== -->
‏<section id="homeView" class="view active">
‏  <main class="home-container">
‏    <!-- Dynamic Hero Visual -->
‏    <div class="hero-stack" aria-hidden="true">
‏      <div class="hero-card c1"><i class="avatar"></i><div class="lines"><span></span><span></span><span></span></div></div>
‏      <div class="hero-card c2"><i class="avatar"></i><div class="lines"><span></span><span></span><span></span></div></div>
‏      <div class="hero-card c3"><i class="avatar"></i><div class="lines"><span></span><span></span><span></span></div></div>
‏    </div>

‏    <h1 class="app-title">مرتّب المستمسكات</h1>
‏    <p class="app-subtitle">صوّر هويتك ومستمسكاتك ورتّبها على ورقة طباعة أوتوماتيكياً بدقة عالية جاهزة للسحب</p>

‏    <button class="btn-card primary glass" id="btnStartNew">
‏      <span class="icon-box">＋</span>
‏      <span>إنشاء ورقة مستندات جديدة<small>ورقة بيضاء بجميع قياسات الطباعة (A4, A3, ...)</small></span>
‏    </button>

‏    <button class="btn-card glass" id="btnOpenAbout">
‏      <span class="icon-box" style="background: rgba(16, 185, 129, 0.2); color: var(--brand-green);">ℹ</span>
‏      <span>عن التطبيق والتواصل<small>معلومات المطور وأدوات التطبيق</small></span>
‏    </button>
‏  </main>
‏</section>

<!-- ==========================================================================
‏     View 2: Editor View
     ========================================================================== -->
‏<section id="editorView" class="view">
‏  <!-- Top Header Navigation Bar -->
‏  <header class="header-bar glass">
‏    <button class="icon-btn" id="btnBackHome" aria-label="رجوع">
‏      <svg viewBox="0 0 24 24"><path d="M9 6l6 6-6 6"/></svg>
‏    </button>

‏    <span class="title">ورقة المستمسكات</span>

‏    <button class="icon-btn" id="btnPaperSize" aria-label="حجم الورقة">A4</button>

‏    <button class="icon-btn" id="btnToggleTheme" aria-label="تغيير المظهر">
‏      <svg viewBox="0 0 24 24"><path d="M20 14.5A8 8 0 019.5 4 8 8 0 1020 14.5z"/></svg>
‏    </button>

‏    <button class="icon-btn accent" id="btnAddDoc" aria-label="إضافة مستند">
‏      <svg viewBox="0 0 24 24"><path d="M12 5v14M5 12h14"/></svg>
‏    </button>

‏    <!-- Dropdown Popups -->
‏    <div class="dropdown-pop glass" id="popPaperSize" hidden style="right: 60px;"></div>
    
‏    <div class="dropdown-pop glass" id="popAddDoc" hidden style="left: 14px;">
‏      <button id="btnAddTwoSides">مستند بوجهين (وجه وظهر)</button>
‏      <button id="btnAddOneSide">مستند بوجه واحد فقط</button>
‏    </div>
‏  </header>

‏  <!-- Interactive Document Pages Render Container -->
‏  <div class="scroll-area" id="pagesContainer"></div>

‏  <!-- Bottom Interactive Dock & Sheet Controls -->
‏  <div class="bottom-dock">
‏    <!-- Active Document Sheet Controls -->
‏    <div class="controls-sheet glass" id="docControlsSheet" hidden>
‏      <div class="sheet-header">
‏        <span id="sheetDocTitle">المستند المحدد</span>
‏        <button class="chip-btn" id="btnCloseSheet">إغلاق ✕</button>
‏      </div>

‏      <!-- Select Preset Preset Dimensions -->
‏      <select id="selectDocPreset" class="select-custom" aria-label="نوع المستند والقياس"></select>

‏      <!-- Side Selection Toggle -->
‏      <div class="btn-row" id="rowSidesToggle">
‏        <button class="chip-btn" id="btnSelectSide0">الوجه الأول</button>
‏        <button class="chip-btn" id="btnSelectSide1">الظهر</button>
‏      </div>

‏      <!-- Image Processing Buttons -->
‏      <div class="btn-row">
‏        <button class="chip-btn" id="btnCropImage">✂ قص وتعديل</button>
‏        <button class="chip-btn" id="btnAutoDetectEdge">⌖ كشف الحواف تلقائياً</button>
‏        <button class="chip-btn" id="btnReplaceImage">🔄 استبدال الصورة</button>
‏      </div>

‏      <!-- Options Controls -->
‏      <div class="btn-row">
‏        <button class="chip-btn" id="btnRotateDimensions">⟳ تدوير الاتجاه</button>
‏        <button class="chip-btn" id="btnSwapSides">⇄ تبديل الوجه والظهر</button>
‏        <button class="chip-btn" id="btnToggleMode">الترتيب: جنب إلى جنب</button>
‏        <button class="chip-btn danger" id="btnDeleteDoc">🗑 حذف</button>
‏      </div>

‏      <!-- Sliders for Radius and Shadow -->
‏      <label class="range-label">
        انحناء الحواف:
‏        <input type="range" id="rangeRadius" min="0" max="10" step="0.5" value="3">
‏      </label>

‏      <label class="range-label">
        إضافة ظلال:
‏        <select id="selectShadow" class="select-custom" style="width: auto; flex: 1;">
‏          <option value="gray">رمادي خفيف</option>
‏          <option value="black">أسود واضح</option>
‏          <option value="none">بدون ظلال</option>
‏        </select>
‏      </label>
‏    </div>

‏    <!-- Export Options Bar -->
‏    <div class="export-bar glass" id="exportBar">
‏      <button class="exp-chip gold" data-export="pdf1200">PDF فائقة 1200 DPI</button>
‏      <button class="exp-chip" data-export="pdf600">PDF عالية 600 DPI</button>
‏      <button class="exp-chip" data-export="pdf300">PDF طباعة 300 DPI</button>
‏      <button class="exp-chip outline" data-export="pngH">صورة PNG دقة عالية</button>
‏      <button class="exp-chip outline" data-export="pngN">صورة PNG حجم عادي</button>
‏      <button class="exp-chip outline" data-export="jpg">صورة JPG</button>
‏    </div>
‏  </div>
‏</section>

<!-- ==========================================================================
‏     Modals: About Modal & Image Crop Modal
     ========================================================================== -->
‏<!-- About Modal -->
‏<div class="modal-overlay" id="modalAbout" hidden>
‏  <div class="modal-box">
‏    <h2>عن التطبيق</h2>
‏    <p>تم تطوير وتصميم هذا التطبيق المتقدم لمساعدة المستخدمين والمكتبات في العراق والوطن العربي لتنظيم وتنسيق طباعة الهويات والمستمسكات الرسمية بدقة متناهية وبأعلى جودة.</p>
‏    <br>
‏    <p>المطور: <b>ياسر جابر</b></p>
‏    <p>للبريد الإلكتروني:<br><a href="mailto:yassirgabeerh@gmail.com">yassirgabeerh@gmail.com</a></p>
‏    <p>الانستغرام:<br><a href="https://instagram.com/4assir" target="_blank" rel="noopener">@4assir</a></p>
‏    <br>
‏    <button class="exp-chip" style="width: 100%;" id="btnCloseAbout">إغلاق</button>
‏  </div>
‏</div>

‏<!-- Image Crop Modal -->
‏<div class="modal-overlay" id="modalCrop" hidden>
‏  <div class="crop-wrapper">
‏    <div class="crop-box">
‏      <img id="cropTargetImage" alt="الصورة المراد قصها">
‏      <div id="cropRect">
‏        <handle data-pos="tl"></handle>
‏        <handle data-pos="tr"></handle>
‏        <handle data-pos="bl"></handle>
‏        <handle data-pos="br"></handle>
‏      </div>
‏    </div>
‏    <div class="btn-row" style="width: 100%;">
‏      <button class="exp-chip" id="btnApplyCrop" style="flex: 1;">تطبيق القص</button>
‏      <button class="exp-chip outline" id="btnCancelCrop" style="flex: 1; background: #ffffff; color: #064e3b;">إلغاء</button>
‏    </div>
‏  </div>
‏</div>

‏<!-- Hidden File Input & Toast Component -->
‏<input type="file" id="fileInput" accept="image/*" hidden>
‏<div class="toast-msg" id="toastMessage" hidden></div>

<!-- ==========================================================================
‏     JavaScript Logic Implementation
     ========================================================================== -->
‏<script>
‏/* Helper Utilities */
‏const $ = id => document.getElementById(id);
‏const clamp = (val, min, max) => Math.max(min, Math.min(max, val));
‏const tick = () => new Promise(resolve => setTimeout(resolve, 30));

‏/* Document Presets Data [Name, Width mm, Height mm, Category] */
‏const DOCUMENT_PRESETS = [
  // الهويات
  ['البطاقة الوطنية الموحدة', 85, 55, 'الهويات'],
  ['هوية الأحوال المدنية', 85, 105, 'الهويات'],
  ['شهادة الجنسية العراقية', 165, 200, 'الهويات'],
  ['بطاقة الناخب', 85, 55, 'الهويات'],
  // وثائق رسمية
  ['بطاقة السكن', 90, 60, 'وثائق رسمية'],
  ['البطاقة التموينية', 90, 60, 'وثائق رسمية'],
  ['جواز السفر العراقي', 88, 125, 'وثائق رسمية'],
  // وثائق A4
  ['شهادة الولادة', 210, 297, 'وثائق A4'],
  ['عقد الزواج', 210, 297, 'وثائق A4'],
  ['شهادة الوفاة', 210, 297, 'وثائق A4']
];

‏/* Page Paper Sizes (mm) */
‏const PAPER_SIZES = {
‏  A3: [297, 420],
‏  A4: [210, 297],
‏  A5: [148, 210],
‏  A6: [105, 148],
‏  Letter: [215.9, 279.4]
};

‏/* Shadow Style Definitions */
‏const SHADOW_STYLES = {
‏  none: 'none',
‏  gray: '0 calc(var(--u) * 0.5) calc(var(--u) * 1.6) rgba(0, 0, 0, 0.28)',
‏  black: '0 calc(var(--u) * 0.5) calc(var(--u) * 1.6) rgba(0, 0, 0, 0.65)'
};

‏const PRINT_PADDING_MM = 2.5;

‏/* Application State */
‏const state = {
‏  pagePaper: 'A4',
‏  entries: [],
‏  selectedId: null,
‏  activeSide: 0 // 0 for front, 1 for back
};

‏let uniqueIdCounter = 0;
‏const getSelectedEntry = () => state.entries.find(e => e.id === state.selectedId);

‏/* Toast Notification Logic */
‏let toastTimeout;
‏function showToast(msg, duration = 2800) {
‏  const toast = $('toastMessage');
‏  toast.textContent = msg;
‏  toast.hidden = false;
‏  clearTimeout(toastTimeout);
‏  if (duration > 0) {
‏    toastTimeout = setTimeout(() => { toast.hidden = true; }, duration);
  }
}

‏/* Theme Handler */
‏const rootEl = document.documentElement;
‏if (window.matchMedia && window.matchMedia('(prefers-color-scheme: light)').matches) {
‏  rootEl.dataset.theme = 'light';
}
‏$('btnToggleTheme').onclick = () => {
‏  rootEl.dataset.theme = rootEl.dataset.theme === 'light' ? 'dark' : 'light';
};

‏/* View Navigation */
‏$('btnStartNew').onclick = () => {
‏  $('homeView').classList.remove('active');
‏  $('editorView').classList.add('active');
‏  renderAllPages();
};

‏$('btnBackHome').onclick = () => {
‏  $('editorView').classList.remove('active');
‏  $('homeView').classList.add('active');
};

‏$('btnOpenAbout').onclick = () => { $('modalAbout').hidden = false; };
‏$('btnCloseAbout').onclick = () => { $('modalAbout').hidden = true; };
‏$('modalAbout').onclick = e => { if (e.target.id === 'modalAbout') $('modalAbout').hidden = true; };

‏/* Header Dropdown Menus */
‏function toggleDropdown(targetId) {
‏  ['popPaperSize', 'popAddDoc'].forEach(id => {
‏    $(id).hidden = id !== targetId || !$(id).hidden;
  });
}

‏$('btnPaperSize').onclick = e => { e.stopPropagation(); toggleDropdown('popPaperSize'); };
‏$('btnAddDoc').onclick = e => { e.stopPropagation(); toggleDropdown('popAddDoc'); };
‏document.addEventListener('click', () => toggleDropdown(''));

‏/* Populate Paper Sizes Popover */
‏$('popPaperSize').innerHTML = Object.keys(PAPER_SIZES).map(key => 
‏  `<button data-paper="${key}" class="${key === state.pagePaper ? 'active' : ''}">${key}</button>`
‏).join('');

‏$('popPaperSize').onclick = e => {
‏  const paper = e.target.dataset.paper;
‏  if (!paper) return;
‏  state.pagePaper = paper;
‏  $('btnPaperSize').textContent = paper.length > 4 ? 'Ltr' : paper;
‏  [...$('popPaperSize').children].forEach(btn => {
‏    btn.classList.toggle('active', btn.dataset.paper === paper);
  });
‏  renderAllPages();
};

‏/* Image Processing Helpers */
‏const fileInput = $('fileInput');
‏let pendingUpload = null;

‏const createImageElement = src => new Promise((resolve, reject) => {
‏  const img = new Image();
‏  img.onload = () => resolve(img);
‏  img.onerror = reject;
‏  img.src = src;
});

‏const shrinkImageCanvas = (img, maxDim) => {
‏  const scale = Math.min(1, maxDim / Math.max(img.naturalWidth, img.naturalHeight));
‏  const canvas = document.createElement('canvas');
‏  canvas.width = Math.round(img.naturalWidth * scale);
‏  canvas.height = Math.round(img.naturalHeight * scale);
‏  canvas.getContext('2d').drawImage(img, 0, 0, canvas.width, canvas.height);
‏  return canvas;
};

‏const canvasToBlob = (canvas, quality) => new Promise(res => canvas.toBlob(res, 'image/jpeg', quality));

‏async function processAndLoadImage(src) {
‏  let img = await createImageElement(src);
‏  if (Math.max(img.naturalWidth, img.naturalHeight) > 3600) {
‏    const canvas = shrinkImageCanvas(img, 3600);
‏    const blob = await canvasToBlob(canvas, 0.95);
‏    canvas.width = canvas.height = 0;
‏    img = await createImageElement(URL.createObjectURL(blob));
  }
‏  const thumbCanvas = shrinkImageCanvas(img, 950);
‏  const thumbBlob = await canvasToBlob(thumbCanvas, 0.85);
‏  thumbCanvas.width = thumbCanvas.height = 0;
‏  return { src: URL.createObjectURL(thumbBlob), imgElement: img };
}

‏function promptImagePicker(entry, sideIndex) {
‏  pendingUpload = { entry, sideIndex };
‏  fileInput.value = '';
‏  fileInput.click();
}

‏fileInput.onchange = async () => {
‏  const file = fileInput.files[0];
‏  if (!file || !pendingUpload) return;
‏  const { entry, sideIndex } = pendingUpload;
  
‏  showToast('جارٍ معالجة وتحسين الصورة...', 0);
‏  try {
‏    entry.images[sideIndex] = await processAndLoadImage(URL.createObjectURL(file));
‏    $('toastMessage').hidden = true;
‏  } catch (err) {
‏    showToast('تعذّر قراءة ملف الصورة');
‏    return;
  }
  
‏  renderAllPages();
‏  // Auto prompt back side if 2-sided doc and back is missing
‏  if (entry.isTwoSides && sideIndex === 0 && !entry.images[1]) {
‏    setTimeout(() => promptImagePicker(entry, 1), 350);
  }
};

‏function createNewDocumentEntry(isTwoSides) {
‏  const newEntry = {
‏    id: ++uniqueIdCounter,
‏    isTwoSides,
‏    presetIndex: 0,
‏    isRotated: false,
‏    layoutMode: 'side', // 'side' or 'stack'
‏    borderRadius: 3,
‏    shadowStyle: 'gray',
‏    images: [null, null]
  };
‏  state.entries.push(newEntry);
‏  state.selectedId = newEntry.id;
‏  state.activeSide = 0;
‏  renderAllPages();
‏  promptImagePicker(newEntry, 0);
}

‏$('btnAddTwoSides').onclick = () => createNewDocumentEntry(true);
‏$('btnAddOneSide').onclick = () => createNewDocumentEntry(false);

‏/* Dimension Calculations & Page Layout Algorithm */
‏function getEntryDimensions(entry) {
‏  const [, w, h] = DOCUMENT_PRESETS[entry.presetIndex];
‏  return entry.isRotated ? [h, w] : [w, h];
}

‏function computePagesLayout() {
‏  const [paperW, paperH] = PAPER_SIZES[state.pagePaper];
‏  const margin = 8;
‏  const gap = 5;
‏  const pages = [[]];
‏  let currentY = margin;

‏  for (const entry of state.entries) {
‏    const [w, h] = getEntryDimensions(entry);
‏    const count = entry.isTwoSides ? 2 : 1;
‏    let boundingW, boundingH;

‏    if (entry.layoutMode === 'stack') {
‏      boundingW = w;
‏      boundingH = h * count + gap * (count - 1);
‏    } else {
‏      boundingW = w * count + gap * (count - 1);
‏      boundingH = h;
    }

‏    // Scale down if larger than page limits
‏    const scale = Math.min(1, (paperW - 2 * margin) / boundingW, (paperH - 2 * margin) / boundingH);
‏    boundingW *= scale;
‏    boundingH *= scale;
‏    const cellW = w * scale;
‏    const cellH = h * scale;
‏    const cellGap = gap * scale;

‏    if (currentY + boundingH > paperH - margin && currentY > margin) {
‏      pages.push([]);
‏      currentY = margin;
    }

‏    const currentPage = pages[pages.length - 1];
‏    const startX = (paperW - boundingW) / 2;

‏    for (let i = 0; i < count; i++) {
‏      const posX = entry.layoutMode === 'stack' ? startX : startX + (count - 1 - i) * (cellW + cellGap);
‏      const posY = entry.layoutMode === 'stack' ? currentY + i * (cellH + cellGap) : currentY;
‏      currentPage.push({
‏        entry,
‏        sideIndex: i,
‏        x: posX,
‏        y: posY,
‏        w: cellW,
‏        h: cellH
      });
    }

‏    currentY += boundingH + gap;
  }

‏  return pages;
}

‏/* Render Engine */
‏function renderAllPages() {
‏  const [paperW, paperH] = PAPER_SIZES[state.pagePaper];
‏  const container = $('pagesContainer');
‏  container.innerHTML = '';

‏  const pages = computePagesLayout();

‏  pages.forEach((pageItems, pageIdx) => {
‏    const paperDiv = document.createElement('div');
‏    paperDiv.className = 'page-paper';
‏    paperDiv.style.aspectRatio = `${paperW} / ${paperH}`;

‏    pageItems.forEach(item => {
‏      const entry = item.entry;
‏      const imgData = entry.images[item.sideIndex];
‏      const slot = document.createElement('div');
      
‏      const isSelected = state.selectedId === entry.id;
‏      slot.className = 'doc-slot' + (imgData ? '' : ' empty') + (isSelected ? ' selected' : '');
      
‏      slot.style.left = `${(item.x / paperW) * 100}%`;
‏      slot.style.top = `${(item.y / paperH) * 100}%`;
‏      slot.style.width = `${(item.w / paperW) * 100}%`;
‏      slot.style.height = `${(item.h / paperH) * 100}%`;

‏      if (imgData) {
‏        slot.style.backgroundImage = `url(${imgData.src})`;
‏        slot.style.borderRadius = `calc(var(--u) * ${entry.borderRadius})`;
‏        slot.style.boxShadow = SHADOW_STYLES[entry.shadowStyle];
‏      } else {
‏        const sideName = entry.isTwoSides ? (item.sideIndex ? 'الظهر' : 'الوجه الأول') : 'صورة المستند';
‏        slot.textContent = `＋ إضافة ${sideName}`;
      }

‏      slot.onclick = ev => {
‏        ev.stopPropagation();
‏        state.selectedId = entry.id;
‏        state.activeSide = item.sideIndex;
‏        if (!imgData) promptImagePicker(entry, item.sideIndex);
‏        renderAllPages();
      };

‏      paperDiv.appendChild(slot);
    });

‏    if (!state.entries.length) {
‏      const hint = document.createElement('div');
‏      hint.className = 'page-hint';
‏      hint.innerHTML = 'ورقة خالية جاهزة<br>اضغط على ＋ بالأعلى لإضافة هويّة أو مستمسك';
‏      paperDiv.appendChild(hint);
    }

‏    container.appendChild(paperDiv);

‏    // Dynamic unit factor calculation for CSS sizing
‏    paperDiv.style.setProperty('--u', `${paperDiv.clientWidth / paperW}px`);

‏    const label = document.createElement('div');
‏    label.className = 'page-label';
‏    label.textContent = `الصفحة ${pageIdx + 1} — قياس (${state.pagePaper})`;
‏    container.appendChild(label);
  });

‏  updateControlsSheet();
‏  requestAnimationFrame(() => {
‏    const dockHeight = document.querySelector('.bottom-dock').offsetHeight;
‏    $('pagesContainer').style.paddingBottom = `${dockHeight + 20}px`;
  });
}

‏// Window Resize debounce
‏let resizeTimer;
‏window.addEventListener('resize', () => {
‏  clearTimeout(resizeTimer);
‏  resizeTimer = setTimeout(() => {
‏    if ($('editorView').classList.contains('active')) renderAllPages();
  }, 150);
});

‏/* Populate Preset Options */
‏$('selectDocPreset').innerHTML = ['الهويات', 'وثائق رسمية', 'وثائق A4'].map(group =>
‏  `<optgroup label="${group}">
‏    ${DOCUMENT_PRESETS.map((doc, idx) => doc[3] === group ? `<option value="${idx}">${doc[0]} — (${doc[1]}×${doc[2]} مم)</option>` : '').join('')}
‏  </optgroup>`
‏).join('');

‏/* Update Controls Sheet UI */
‏function updateControlsSheet() {
‏  const entry = getSelectedEntry();
‏  const sheet = $('docControlsSheet');

‏  if (!entry) {
‏    sheet.hidden = true;
‏    return;
  }

‏  sheet.hidden = false;
‏  $('sheetDocTitle').textContent = DOCUMENT_PRESETS[entry.presetIndex][0];
‏  $('selectDocPreset').value = entry.presetIndex;

‏  $('rowSidesToggle').style.display = entry.isTwoSides ? 'flex' : 'none';
‏  $('btnSelectSide0').classList.toggle('active', state.activeSide === 0);
‏  $('btnSelectSide1').classList.toggle('active', state.activeSide === 1);

‏  $('btnSwapSides').style.display = entry.isTwoSides ? '' : 'none';
‏  $('btnToggleMode').style.display = entry.isTwoSides ? '' : 'none';
‏  $('btnToggleMode').textContent = 'الترتيب: ' + (entry.layoutMode === 'side' ? 'جنب إلى جنب' : 'الوجه فوق الظهر');

‏  $('rangeRadius').value = entry.borderRadius;
‏  $('selectShadow').value = entry.shadowStyle;
}

‏/* Sheet Events Binding */
‏$('btnCloseSheet').onclick = () => { state.selectedId = null; renderAllPages(); };
‏$('pagesContainer').onclick = () => { if (state.selectedId) { state.selectedId = null; renderAllPages(); } };

‏$('selectDocPreset').onchange = e => { getSelectedEntry().presetIndex = +e.target.value; renderAllPages(); };
‏$('btnSelectSide0').onclick = () => { state.activeSide = 0; updateControlsSheet(); };
‏$('btnSelectSide1').onclick = () => { state.activeSide = 1; updateControlsSheet(); };

‏$('btnRotateDimensions').onclick = () => { const e = getSelectedEntry(); e.isRotated = !e.isRotated; renderAllPages(); };
‏$('btnSwapSides').onclick = () => { const e = getSelectedEntry(); e.images.reverse(); renderAllPages(); };
‏$('btnToggleMode').onclick = () => { const e = getSelectedEntry(); e.layoutMode = e.layoutMode === 'side' ? 'stack' : 'side'; renderAllPages(); };
‏$('btnDeleteDoc').onclick = () => {
‏  state.entries = state.entries.filter(e => e.id !== state.selectedId);
‏  state.selectedId = null;
‏  renderAllPages();
‏  showToast('تم حذف المستند');
};

‏let frameReq = 0;
‏$('rangeRadius').oninput = e => {
‏  getSelectedEntry().borderRadius = +e.target.value;
‏  if (!frameReq) {
‏    frameReq = requestAnimationFrame(() => { frameReq = 0; renderAllPages(); });
  }
};

‏$('selectShadow').onchange = e => { getSelectedEntry().shadowStyle = e.target.value; renderAllPages(); };
‏$('btnReplaceImage').onclick = () => promptImagePicker(getSelectedEntry(), state.activeSide);

/* ==========================================================================
‏   Crop & Canvas Auto Edge Detection Logic
   ========================================================================== */
‏let cropState = null;

‏/* Algorithm to detect document edges from canvas image data */
‏function detectDocumentEdges(img) {
‏  const maxDim = 320;
‏  const scale = Math.min(1, maxDim / Math.max(img.naturalWidth, img.naturalHeight));
‏  const w = Math.max(8, Math.round(img.naturalWidth * scale));
‏  const h = Math.max(8, Math.round(img.naturalHeight * scale));

‏  const canvas = document.createElement('canvas');
‏  canvas.width = w; canvas.height = h;
‏  const ctx = canvas.getContext('2d', { willReadFrequently: true });
‏  ctx.drawImage(img, 0, 0, w, h);

‏  const imgData = ctx.getImageData(0, 0, w, h).data;
‏  let r = 0, g = 0, b = 0, count = 0;

‏  const sample = (x, y) => {
‏    const i = (y * w + x) * 4;
‏    r += imgData[i]; g += imgData[i + 1]; b += imgData[i + 2]; count++;
  };

‏  // Sample border pixels for background color estimation
‏  for (let x = 0; x < w; x++) { sample(x, 0); sample(x, h - 1); }
‏  for (let y = 0; y < h; y++) { sample(0, y); sample(w - 1, y); }

‏  r /= count; g /= count; b /= count;

‏  const rowDiffs = new Uint16Array(h);
‏  const colDiffs = new Uint16Array(w);

‏  for (let y = 0; y < h; y++) {
‏    for (let x = 0; x < w; x++) {
‏      const idx = (y * w + x) * 4;
‏      if (Math.abs(imgData[idx] - r) + Math.abs(imgData[idx + 1] - g) + Math.abs(imgData[idx + 2] - b) > 85) {
‏        rowDiffs[y]++;
‏        colDiffs[x]++;
      }
    }
  }

‏  const findBounds = (arr, length) => {
‏    let start = 0, end = arr.length - 1;
‏    while (start < end && arr[start] < length * 0.04) start++;
‏    while (end > start && arr[end] < length * 0.04) end--;
‏    return [start, end + 1];
  };

‏  const [y0, y1] = findBounds(rowDiffs, w);
‏  const [x0, x1] = findBounds(colDiffs, h);

‏  if (x1 - x0 < w * 0.2 || y1 - y0 < h * 0.2) {
‏    return { x: 0.05, y: 0.05, w: 0.9, h: 0.9 };
  }

‏  const padding = 0.015;
‏  const cropX = Math.max(0, x0 / w - padding);
‏  const cropY = Math.max(0, y0 / h - padding);
‏  const cropW = Math.min(1, x1 / w + padding) - cropX;
‏  const cropH = Math.min(1, y1 / h + padding) - cropY;

‏  return { x: cropX, y: cropY, w: cropW, h: cropH };
}

‏function updateCropBoxDOM() {
‏  const rect = cropState.rect;
‏  const style = $('cropRect').style;
‏  style.left = `${rect.x * 100}%`;
‏  style.top = `${rect.y * 100}%`;
‏  style.width = `${rect.w * 100}%`;
‏  style.height = `${rect.h * 100}%`;
}

‏function openCropModal(isAuto) {
‏  const entry = getSelectedEntry();
‏  const side = entry.isTwoSides ? state.activeSide : 0;
‏  const imgData = entry.images[side];

‏  if (!imgData) {
‏    showToast('الرجاء اختيار صورة أولاً');
‏    return;
  }

‏  cropState = {
‏    entry,
‏    side,
‏    imgData,
‏    rect: { x: 0.05, y: 0.05, w: 0.9, h: 0.9 }
  };

‏  const targetImg = $('cropTargetImage');
‏  const onImageLoad = () => {
‏    if (isAuto) {
‏      cropState.rect = detectDocumentEdges(targetImg);
‏      if (cropState.rect.w > 0.96 && cropState.rect.h > 0.96) {
‏        showToast('لم يتم كشف حواف واضحة، يمكنك الضبط يدوياً');
      }
    }
‏    updateCropBoxDOM();
  };

‏  targetImg.onload = onImageLoad;
‏  targetImg.src = imgData.src;
‏  $('modalCrop').hidden = false;
‏  if (targetImg.complete && targetImg.naturalWidth) onImageLoad();
}

‏$('btnCropImage').onclick = () => openCropModal(false);
‏$('btnAutoDetectEdge').onclick = () => openCropModal(true);
‏$('btnCancelCrop').onclick = () => { $('modalCrop').hidden = true; };

‏/* Crop Drag Interactions */
‏let dragSession = null;
‏const cropRectEl = $('cropRect');

‏cropRectEl.addEventListener('pointerdown', ev => {
‏  ev.preventDefault();
‏  dragSession = {
‏    pos: ev.target.dataset.pos || 'move',
‏    startX: ev.clientX,
‏    startY: ev.clientY,
‏    initialRect: { ...cropState.rect }
  };
‏  cropRectEl.setPointerCapture(ev.pointerId);
});

‏cropRectEl.addEventListener('pointermove', ev => {
‏  if (!dragSession) return;
‏  const imgBounds = $('cropTargetImage').getBoundingClientRect();
‏  const deltaX = (ev.clientX - dragSession.startX) / imgBounds.width;
‏  const deltaY = (ev.clientY - dragSession.startY) / imgBounds.height;

‏  let { x, y, w, h } = dragSession.initialRect;
‏  const pos = dragSession.pos;

‏  if (pos === 'move') {
‏    x = clamp(x + deltaX, 0, 1 - w);
‏    y = clamp(y + deltaY, 0, 1 - h);
‏  } else {
‏    let right = x + w;
‏    let bottom = y + h;

‏    if (pos.includes('l')) x = clamp(x + deltaX, 0, right - 0.08);
‏    if (pos.includes('r')) right = clamp(right + deltaX, x + 0.08, 1);
‏    if (pos.includes('t')) y = clamp(y + deltaY, 0, bottom - 0.08);
‏    if (pos.includes('b')) bottom = clamp(bottom + deltaY, y + 0.08, 1);

‏    w = right - x;
‏    h = bottom - y;
  }

‏  cropState.rect = { x, y, w, h };
‏  updateCropBoxDOM();
});

‏cropRectEl.addEventListener('pointerup', () => { dragSession = null; });
‏cropRectEl.addEventListener('pointercancel', () => { dragSession = null; });

‏$('btnApplyCrop').onclick = async () => {
‏  const { imgData, rect, entry, side } = cropState;
‏  const imgEl = imgData.imgElement;
‏  const nw = imgEl.naturalWidth;
‏  const nh = imgEl.naturalHeight;

‏  const canvas = document.createElement('canvas');
‏  canvas.width = Math.round(rect.w * nw);
‏  canvas.height = Math.round(rect.h * nh);

‏  const ctx = canvas.getContext('2d');
‏  ctx.drawImage(
‏    imgEl,
‏    rect.x * nw, rect.y * nh, rect.w * nw, rect.h * nh,
‏    0, 0, canvas.width, canvas.height
  );

‏  const blob = await canvasToBlob(canvas, 0.96);
‏  entry.images[side] = await processAndLoadImage(URL.createObjectURL(blob));
‏  $('modalCrop').hidden = true;
‏  renderAllPages();
};

/* ==========================================================================
‏   High Quality Export Engine (PDF, PNG, JPG)
   ========================================================================== */
‏function drawRoundedRectPath(ctx, x, y, w, h, r) {
‏  r = Math.min(r, w / 2, h / 2);
‏  ctx.beginPath();
‏  ctx.moveTo(x + r, y);
‏  ctx.arcTo(x + w, y, x + w, y + h, r);
‏  ctx.arcTo(x + w, y + h, x, y + h, r);
‏  ctx.arcTo(x, y + h, x, y, r);
‏  ctx.arcTo(x, y, x + w, y, r);
‏  ctx.closePath();
}

‏function renderItemToCanvas(item, pixelsPerMM) {
‏  const entry = item.entry;
‏  const imgEl = entry.images[item.sideIndex].imgElement;
‏  const canvas = document.createElement('canvas');

‏  canvas.width = Math.round((item.w + 2 * PRINT_PADDING_MM) * pixelsPerMM);
‏  canvas.height = Math.round((item.h + 2 * PRINT_PADDING_MM) * pixelsPerMM);

‏  const ctx = canvas.getContext('2d');
‏  ctx.fillStyle = '#ffffff';
‏  ctx.fillRect(0, 0, canvas.width, canvas.height);

‏  const x = PRINT_PADDING_MM * pixelsPerMM;
‏  const y = PRINT_PADDING_MM * pixelsPerMM;
‏  const w = item.w * pixelsPerMM;
‏  const h = item.h * pixelsPerMM;
‏  const r = entry.borderRadius * pixelsPerMM;

‏  // Render shadow
‏  if (entry.shadowStyle !== 'none') {
‏    ctx.save();
‏    ctx.shadowColor = entry.shadowStyle === 'black' ? 'rgba(0,0,0,0.65)' : 'rgba(0,0,0,0.3)';
‏    ctx.shadowBlur = 1.6 * pixelsPerMM;
‏    ctx.shadowOffsetY = 0.5 * pixelsPerMM;
‏    ctx.fillStyle = '#ffffff';
‏    drawRoundedRectPath(ctx, x, y, w, h, r);
‏    ctx.fill();
‏    ctx.restore();
  }

‏  // Draw clipped document image
‏  ctx.save();
‏  drawRoundedRectPath(ctx, x, y, w, h, r);
‏  ctx.clip();

‏  const nw = imgEl.naturalWidth;
‏  const nh = imgEl.naturalHeight;
‏  const scale = Math.max(w / nw, h / nh);
‏  const srcW = w / scale;
‏  const srcH = h / scale;

‏  ctx.drawImage(imgEl, (nw - srcW) / 2, (nh - srcH) / 2, srcW, srcH, x, y, w, h);
‏  ctx.restore();

‏  return canvas;
}

‏async function triggerFileDownload(filename, blob) {
‏  const link = document.createElement('a');
‏  link.href = URL.createObjectURL(blob);
‏  link.download = filename;
‏  document.body.appendChild(link);
‏  link.click();
‏  link.remove();
}

‏const EXPORT_CONFIGS = {
‏  pdf1200: ['pdf', 1200],
‏  pdf600: ['pdf', 600],
‏  pdf300: ['pdf', 300],
‏  pngH: ['png', 300],
‏  pngN: ['png', 150],
‏  jpg: ['jpg', 300]
};

‏let isExportBusy = false;

‏async function runExportProcess(configKey) {
‏  if (isExportBusy) return;

‏  const hasImage = state.entries.some(e => e.images[0] || e.images[1]);
‏  if (!hasImage) {
‏    showToast('يرجى إضافة صورة مستند واحدة على الأقل قبل التصدير');
‏    return;
  }

‏  const [format, targetDPI] = EXPORT_CONFIGS[configKey];
‏  isExportBusy = true;
‏  showToast('جارٍ تجهيز وبناء الملف بدقة عالية...', 0);
‏  await tick();

‏  try {
‏    const pagesLayout = computePagesLayout();
‏    const [paperW, paperH] = PAPER_SIZES[state.pagePaper];

‏    if (format === 'pdf') {
‏      const pdf = new window.jspdf.jsPDF({
‏        unit: 'mm',
‏        format: [paperW, paperH],
‏        orientation: 'p',
‏        compress: true
      });

‏      for (let pIndex = 0; pIndex < pagesLayout.length; pIndex++) {
‏        if (pIndex > 0) pdf.addPage([paperW, paperH]);

‏        for (const item of pagesLayout[pIndex]) {
‏          if (!item.entry.images[item.sideIndex]) continue;

‏          const pxFactor = Math.min(
‏            targetDPI / 25.4,
‏            Math.sqrt(36e6 / ((item.w + 2 * PRINT_PADDING_MM) * (item.h + 2 * PRINT_PADDING_MM)))
          );

‏          const docCanvas = renderItemToCanvas(item, pxFactor);
‏          pdf.addImage(
‏            docCanvas.toDataURL('image/jpeg', 0.95),
‏            'JPEG',
‏            item.x - PRINT_PADDING_MM,
‏            item.y - PRINT_PADDING_MM,
‏            item.w + 2 * PRINT_PADDING_MM,
‏            item.h + 2 * PRINT_PADDING_MM,
‏            undefined,
‏            'FAST'
          );
‏          docCanvas.width = docCanvas.height = 0;
‏          await tick();
        }
      }

‏      await triggerFileDownload('مرتب_المستمسكات.pdf', pdf.output('blob'));
‏    } else {
‏      // Export PNG / JPG
‏      const pxFactor = Math.min(targetDPI / 25.4, Math.sqrt(50e6 / (paperW * paperH)));

‏      for (let pIndex = 0; pIndex < pagesLayout.length; pIndex++) {
‏        const pageCanvas = document.createElement('canvas');
‏        pageCanvas.width = Math.round(paperW * pxFactor);
‏        pageCanvas.height = Math.round(paperH * pxFactor);

‏        const ctx = pageCanvas.getContext('2d');
‏        ctx.fillStyle = '#ffffff';
‏        ctx.fillRect(0, 0, pageCanvas.width, pageCanvas.height);

‏        for (const item of pagesLayout[pIndex]) {
‏          if (!item.entry.images[item.sideIndex]) continue;
‏          const itemCanvas = renderItemToCanvas(item, pxFactor);
‏          ctx.drawImage(
‏            itemCanvas,
‏            Math.round((item.x - PRINT_PADDING_MM) * pxFactor),
‏            Math.round((item.y - PRINT_PADDING_MM) * pxFactor)
          );
‏          itemCanvas.width = itemCanvas.height = 0;
        }

‏        const isJpg = format === 'jpg';
‏        const blob = await canvasToBlob(pageCanvas, isJpg ? 'image/jpeg' : 'image/png', 0.94);
‏        await triggerFileDownload(`مرتب_المستمسكات_${pIndex + 1}.${isJpg ? 'jpg' : 'png'}`, blob);
‏        pageCanvas.width = pageCanvas.height = 0;
      }
    }

‏    showToast('تم حفظ الملف بنجاح 🎉');
‏  } catch (err) {
‏    console.error(err);
‏    showToast('تعذّر التصدير، يُرجى تجربة دقة أقل');
  }

‏  isExportBusy = false;
}

‏$('exportBar').onclick = e => {
‏  const configKey = e.target.dataset.export;
‏  if (configKey) runExportProcess(configKey);
};

‏// Initial Start Call
‏renderAllPages();
‏</script>
‏</body>
</html>
