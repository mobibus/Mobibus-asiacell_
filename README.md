<!  محمد جواد frn.mohmed.wmobibus>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة خطوط الفاتورة | Postpaid Calculator</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Font: Cairo & Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#eef2ff',
                            100: '#e0e7ff',
                            500: '#6366f1',
                            600: '#4f46e5',
                            700: '#4338ca',
                            900: '#312e81',
                        },
                        accent: {
                            emerald: '#10b981',
                            amber: '#f59e0b',
                            rose: '#f43f5e',
                            cyan: '#06b6d4',
                        }
                    },
                    fontFamily: {
                        sans: ['Cairo', 'Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Cairo', sans-serif;
            background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 50%, #0f172a 100%);
            min-height: 100vh;
        }
        .glass-panel {
            background: rgba(255, 255, 255, 0.04);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .glass-card {
            background: rgba(255, 255, 255, 0.07);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.12);
            transition: all 0.3s ease;
        }
        .glass-card:hover {
            transform: translateY(-3px);
            border-color: rgba(99, 102, 241, 0.4);
            box-shadow: 0 10px 30px -10px rgba(79, 70, 229, 0.3);
        }
        .custom-input {
            background: rgba(15, 23, 42, 0.6);
            border: 1px solid rgba(255, 255, 255, 0.15);
            color: #ffffff;
            transition: all 0.2s ease;
        }
        .custom-input:focus {
            outline: none;
            border-color: #6366f1;
            box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.25);
            background: rgba(15, 23, 42, 0.8);
        }
        /* Hide scrollbar for Chrome, Safari and Opera */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        /* Hide scrollbar for IE, Edge and Firefox */
        .no-scrollbar {
            -ms-overflow-style: none;  /* IE and Edge */
            scrollbar-width: none;  /* Firefox */
        }
    </style>
</head>
<body class="text-slate-100 flex flex-col justify-between p-3 md:p-6 antialiased selection:bg-brand-500 selection:text-white">

    <!-- Toast Notification -->
    <div id="toast" class="fixed top-5 left-1/2 -translate-x-1/2 z-50 transform -translate-y-20 opacity-0 transition-all duration-300 ease-out bg-emerald-600 text-white px-6 py-3 rounded-2xl shadow-2xl flex items-center space-x-3 space-x-reverse border border-emerald-400/30">
        <i class="fa-solid fa-circle-check text-xl"></i>
        <span id="toast-msg" class="font-semibold text-sm">تم نسخ التقرير بنجاح!</span>
    </div>

    <div class="max-w-6xl mx-auto w-full space-y-6">
        
        <!-- Header Section -->
        <header class="glass-panel rounded-3xl p-6 text-center relative overflow-hidden shadow-2xl">
            <div class="absolute -top-24 -right-24 w-60 h-60 bg-brand-500/20 rounded-full blur-3xl pointer-events-none"></div>
            <div class="absolute -bottom-24 -left-24 w-60 h-60 bg-accent-cyan/20 rounded-full blur-3xl pointer-events-none"></div>
            
            <div class="relative z-10 flex flex-col items-center justify-center space-y-3">
                <div class="w-16 h-16 bg-gradient-to-tr from-brand-600 to-accent-cyan rounded-2xl flex items-center justify-center shadow-lg shadow-brand-500/30 ring-4 ring-white/10 mb-1">
                    <i class="fa-solid fa-file-invoice-dollar text-3xl text-white"></i>
                </div>
                <h1 class="text-2xl sm:text-4xl font-black tracking-tight text-transparent bg-clip-text bg-gradient-to-r from-white via-slate-200 to-indigo-200">
                    حاسبة خطوط الفاتورة التناسبية
                </h1>
                <p class="text-slate-400 text-xs sm:text-sm max-w-xl leading-relaxed">
                    احسب مستحقات الفاتورة، الدقائق، وحزم الإنترنت بالتناسب الدقيق (Pro-rata) وحسب تاريخ الاستخدام بأسلوب عصري وسريع.
                </p>
            </div>
        </header>

        <!-- Main Layout: Grid of Form & Outputs -->
        <main class="grid grid-cols-1 lg:grid-cols-12 gap-6">
            
            <!-- Left Panel: Input Controls (5 Cols) -->
            <section class="lg:col-span-5 glass-panel rounded-3xl p-5 sm:p-7 space-y-5 flex flex-col justify-between shadow-xl">
                <div>
                    <div class="flex items-center space-x-3 space-x-reverse mb-5 border-b border-white/10 pb-3">
                        <i class="fa-solid fa-sliders text-brand-500 text-lg"></i>
                        <h2 class="text-lg font-bold text-white">إعدادات وباقة الخط</h2>
                    </div>

                    <form id="calcForm" onsubmit="event.preventDefault();" class="space-y-4">
                        
                        <!-- Monthly Fee Input -->
                        <div>
                            <label class="block text-xs font-semibold text-slate-300 mb-1.5">
                                <i class="fa-solid fa-money-bill-wave text-emerald-400 ml-1"></i> سعر الباقة الشهري (د.ع)
                            </label>
                            <div class="relative">
                                <input type="number" id="monthlyFee" value="25000" min="0" step="500" class="w-full custom-input rounded-xl py-2.5 px-4 pr-10 text-sm font-semibold focus:ring-0">
                                <span class="absolute left-3 top-2.5 text-xs text-slate-400 font-normal">د.ع</span>
                            </div>
                        </div>

                        <!-- Included Minutes -->
                        <div class="grid grid-cols-2 gap-3">
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1.5">
                                    <i class="fa-solid fa-phone text-amber-400 ml-1"></i> إجمالي الدقائق
                                </label>
                                <input type="number" id="totalMinutes" value="500" min="0" class="w-full custom-input rounded-xl py-2.5 px-3 text-sm font-semibold">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1.5">
                                    <i class="fa-solid fa-wifi text-cyan-400 ml-1"></i> إجمالي الإنترنت (GB)
                                </label>
                                <input type="number" id="totalGB" value="12" min="0" step="0.5" class="w-full custom-input rounded-xl py-2.5 px-3 text-sm font-semibold">
                            </div>
                        </div>

                        <!-- Billing Cycle Start Day -->
                        <div>
                            <label class="block text-xs font-semibold text-slate-300 mb-1.5">
                                <i class="fa-solid fa-calendar-day text-brand-500 ml-1"></i> يوم تجديد الفاتورة (شهرياً)
                            </label>
                            <select id="cycleStartDay" class="w-full custom-input rounded-xl py-2.5 px-3 text-sm font-semibold">
                                <!-- JS will populate options 1-31 -->
                            </select>
                        </div>

                        <!-- Computation Method Toggle -->
                        <div class="bg-slate-900/40 p-3 rounded-2xl border border-white/5 space-y-3">
                            <label class="block text-xs font-semibold text-slate-300">طريقة الحساب حسب:</label>
                            <div class="grid grid-cols-2 gap-2">
                                <button type="button" id="btnModeDays" onclick="setMode('days')" class="py-2 px-3 rounded-xl text-xs font-bold transition-all bg-brand-600 text-white shadow-md">
                                    <i class="fa-solid fa-hashtag ml-1"></i> عدد الأيام مباشرة
                                </button>
                                <button type="button" id="btnModeDate" onclick="setMode('date')" class="py-2 px-3 rounded-xl text-xs font-bold transition-all bg-slate-800 text-slate-400 hover:text-white">
                                    <i class="fa-solid fa-calendar-alt ml-1"></i> اختيار تاريخ اليوم
                                </button>
                            </div>

                            <!-- Input based on Mode -->
                            <div id="daysInputGroup" class="pt-1">
                                <label class="block text-xs font-medium text-slate-400 mb-1">الأيام المنقضية من الدورة:</label>
                                <div class="flex items-center space-x-2 space-x-reverse">
                                    <input type="range" id="daysPassedRange" min="1" max="30" value="24" class="w-full accent-brand-500 h-2 bg-slate-700 rounded-lg cursor-pointer">
                                    <input type="number" id="daysPassedInput" min="1" max="31" value="24" class="w-20 text-center custom-input rounded-xl py-1.5 text-xs font-bold">
                                </div>
                            </div>

                            <div id="dateInputGroup" class="hidden pt-1">
                                <label class="block text-xs font-medium text-slate-400 mb-1">تاريخ اليوم:</label>
                                <input type="date" id="currentDateInput" class="w-full custom-input rounded-xl py-2 px-3 text-xs font-semibold">
                            </div>
                        </div>

                        <!-- Days in Month Setting -->
                        <div>
                            <div class="flex justify-between items-center mb-1">
                                <label class="text-xs font-semibold text-slate-300">عدد أيام الشهر المالي:</label>
                                <span id="daysInMonthVal" class="text-xs text-brand-500 font-bold">30 يوم</span>
                            </div>
                            <div class="grid grid-cols-4 gap-2">
                                <button type="button" onclick="setMonthDays(28)" class="month-day-btn py-1.5 rounded-xl text-xs font-bold bg-slate-800 text-slate-300 border border-white/5 hover:bg-brand-600/30">28</button>
                                <button type="button" onclick="setMonthDays(29)" class="month-day-btn py-1.5 rounded-xl text-xs font-bold bg-slate-800 text-slate-300 border border-white/5 hover:bg-brand-600/30">29</button>
                                <button type="button" onclick="setMonthDays(30)" class="month-day-btn active py-1.5 rounded-xl text-xs font-bold bg-brand-600 text-white shadow">30</button>
                                <button type="button" onclick="setMonthDays(31)" class="month-day-btn py-1.5 rounded-xl text-xs font-bold bg-slate-800 text-slate-300 border border-white/5 hover:bg-brand-600/30">31</button>
                            </div>
                        </div>

                    </form>
                </div>

                <!-- Action Controls -->
                <div class="pt-4 border-t border-white/10 flex gap-3">
                    <button type="button" onclick="resetForm()" class="w-1/3 py-2.5 rounded-xl text-xs font-bold text-slate-400 bg-slate-800 hover:bg-slate-700 transition">
                        <i class="fa-solid fa-rotate-left ml-1"></i> إعادة ضبط
                    </button>
                    <button type="button" onclick="copySummary()" class="w-2/3 py-2.5 rounded-xl text-xs font-bold text-white bg-gradient-to-r from-brand-600 to-brand-500 hover:from-brand-500 hover:to-brand-600 shadow-lg shadow-brand-600/30 transition">
                        <i class="fa-regular fa-copy ml-1"></i> نسخ التقرير
                    </button>
                </div>
            </section>

            <!-- Right Panel: Calculation Dashboard Cards (7 Cols) -->
            <section class="lg:col-span-7 space-y-5">
                
                <!-- Main Highlights: Bill Amount -->
                <div class="glass-card rounded-3xl p-6 relative overflow-hidden border-2 border-brand-500/30 bg-gradient-to-br from-brand-900/40 via-slate-900/60 to-slate-900">
                    <div class="absolute -left-10 -bottom-10 w-40 h-40 bg-brand-500/10 rounded-full blur-2xl"></div>
                    <div class="flex items-center justify-between mb-3">
                        <span class="text-xs font-bold uppercase tracking-wider text-brand-500 bg-brand-500/10 px-3 py-1 rounded-full border border-brand-500/20">
                            المبلغ المستحق لغاية اليوم
                        </span>
                        <i class="fa-solid fa-sack-dollar text-brand-500 text-2xl"></i>
                    </div>
                    <div class="flex items-baseline space-x-2 space-x-reverse">
                        <h3 id="resDueAmount" class="text-4xl sm:text-5xl font-black tracking-tight text-white">0</h3>
                        <span class="text-base sm:text-xl font-bold text-emerald-400">دينار عراقي</span>
                    </div>
                    <p class="text-xs text-slate-400 mt-2 flex items-center">
                        <i class="fa-solid fa-circle-info ml-1.5 text-brand-500"></i>
                        يمثل النسبة المستحقة عن استهلاك <span id="resDaysPassedLabel" class="font-bold text-white mx-1">0</span> يوم من أصل <span id="resTotalDaysLabel" class="font-bold text-white mx-1">30</span> يوم.
                    </p>
                </div>

                <!-- Grid Result Cards -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    
                    <!-- Minutes Card -->
                    <div class="glass-card rounded-2xl p-5 border-l-4 border-l-amber-400">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <p class="text-xs text-slate-400 font-semibold">الدقائق المتاحة النازلة</p>
                                <h4 class="text-2xl font-bold text-white mt-1" id="resMinutes">0 <span class="text-xs font-normal text-slate-400">دقيقة</span></h4>
                            </div>
                            <div class="w-10 h-10 rounded-xl bg-amber-400/10 text-amber-400 flex items-center justify-center text-lg">
                                <i class="fa-solid fa-phone"></i>
                            </div>
                        </div>
                        <div class="w-full bg-slate-800 rounded-full h-1.5 mt-3 overflow-hidden">
                            <div id="barMinutes" class="bg-amber-400 h-full rounded-full transition-all duration-500" style="width: 0%"></div>
                        </div>
                        <p class="text-[11px] text-slate-400 mt-2">من أصل <span id="resTotalMinutes" class="font-bold text-slate-300">500</span> دقيقة إجمالية</p>
                    </div>

                    <!-- GB Internet Card -->
                    <div class="glass-card rounded-2xl p-5 border-l-4 border-l-cyan-400">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <p class="text-xs text-slate-400 font-semibold">إنترنت النازل (غيغابايت)</p>
                                <h4 class="text-2xl font-bold text-white mt-1" id="resGB">0 <span class="text-xs font-normal text-slate-400">GB</span></h4>
                            </div>
                            <div class="w-10 h-10 rounded-xl bg-cyan-400/10 text-cyan-400 flex items-center justify-center text-lg">
                                <i class="fa-solid fa-wifi"></i>
                            </div>
                        </div>
                        <div class="w-full bg-slate-800 rounded-full h-1.5 mt-3 overflow-hidden">
                            <div id="barGB" class="bg-cyan-400 h-full rounded-full transition-all duration-500" style="width: 0%"></div>
                        </div>
                        <p class="text-[11px] text-slate-400 mt-2 font-mono" id="resMB">تساوي: 0 MB</p>
                    </div>

                    <!-- Remaining Days Card -->
                    <div class="glass-card rounded-2xl p-5 border-l-4 border-l-rose-400">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <p class="text-xs text-slate-400 font-semibold">الأيام المتبقية للتجديد</p>
                                <h4 class="text-2xl font-bold text-white mt-1" id="resRemainingDays">0 <span class="text-xs font-normal text-slate-400">يوم</span></h4>
                            </div>
                            <div class="w-10 h-10 rounded-xl bg-rose-400/10 text-rose-400 flex items-center justify-center text-lg">
                                <i class="fa-solid fa-hourglass-half"></i>
                            </div>
                        </div>
                        <p class="text-[11px] text-slate-400 mt-3">تاريخ التجديد القادم: <span id="resNextRenewalDate" class="font-bold text-rose-300">--</span></p>
                    </div>

                    <!-- Remaining Amount Card -->
                    <div class="glass-card rounded-2xl p-5 border-l-4 border-l-emerald-400">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <p class="text-xs text-slate-400 font-semibold">المتبقي لاكتمال الفاتورة</p>
                                <h4 class="text-2xl font-bold text-white mt-1" id="resRemainingAmount">0 <span class="text-xs font-normal text-slate-400">د.ع</span></h4>
                            </div>
                            <div class="w-10 h-10 rounded-xl bg-emerald-400/10 text-emerald-400 flex items-center justify-center text-lg">
                                <i class="fa-solid fa-piggy-bank"></i>
                            </div>
                        </div>
                        <p class="text-[11px] text-slate-400 mt-3">يدفع مع نهاية كامل دورة الشهر</p>
                    </div>

                </div>

                <!-- Detailed Breakdown Summary Box -->
                <div class="glass-panel rounded-2xl p-5 space-y-3">
                    <h4 class="text-xs font-bold text-slate-300 uppercase tracking-wider flex items-center">
                        <i class="fa-solid fa-list-check ml-2 text-brand-500"></i> تفاصيل الحساب التناسبي (Pro-rata)
                    </h4>
                    <div class="divide-y divide-white/5 text-xs text-slate-300">
                        <div class="py-2 flex justify-between">
                            <span>التكلفة اليومية الثابتة:</span>
                            <span class="font-bold text-white" id="resDailyRate">0 د.ع / يوم</span>
                        </div>
                        <div class="py-2 flex justify-between">
                            <span>نسبة الاستهلاك المنقضية:</span>
                            <span class="font-bold text-brand-500" id="resPercentage">0%</span>
                        </div>
                        <div class="py-2 flex justify-between">
                            <span>الدقائق المتبقية لنزولها:</span>
                            <span class="font-bold text-amber-400" id="resRemainingMinutes">0 دقيقة</span>
                        </div>
                        <div class="py-2 flex justify-between">
                            <span>الإنترنت المتبقي لنزوله:</span>
                            <span class="font-bold text-cyan-400" id="resRemainingGB">0 GB</span>
                        </div>
                    </div>
                </div>

            </section>
        </main>

        <!-- Footer -->
        <footer class="text-center text-xs text-slate-500 py-4 border-t border-white/5">
            تطبيق آلة حاسبة لخطوط الفاتورة أسياسيل / موبي باص /  التناسبية &copy; 2026
        </footer>
    </div>

    <!-- JavaScript Calculation Engine -->
    <script>
        // State Variables
        let calculationMode = 'days'; // 'days' or 'date'
        let daysInMonth = 30;

        // Initialize Options on DOM Load
        document.addEventListener('DOMContentLoaded', () => {
            populateCycleDays();
            
            // Set default date input to today
            const today = new Date();
            const yyyy = today.getFullYear();
            const mm = String(today.getMonth() + 1).padStart(2, '0');
            const dd = String(today.getDate()).padStart(2, '0');
            document.getElementById('currentDateInput').value = `${yyyy}-${mm}-${dd}`;

            // Attach event listeners for inputs
            const inputIds = ['monthlyFee', 'totalMinutes', 'totalGB', 'cycleStartDay', 'daysPassedInput', 'currentDateInput'];
            inputIds.forEach(id => {
                const el = document.getElementById(id);
                if(el) el.addEventListener('input', calculate);
            });

            // Range Slider Sync
            const range = document.getElementById('daysPassedRange');
            const numInput = document.getElementById('daysPassedInput');

            range.addEventListener('input', (e) => {
                numInput.value = e.target.value;
                calculate();
            });

            numInput.addEventListener('input', (e) => {
                range.value = e.target.value;
                calculate();
            });

            // Initial calculation
            calculate();
        });

        // Populate Start Day Dropdown (1 to 31)
        function populateCycleDays() {
            const select = document.getElementById('cycleStartDay');
            select.innerHTML = '';
            for (let i = 1; i <= 31; i++) {
                const opt = document.createElement('option');
                opt.value = i;
                opt.textContent = `يوم ${i} من الشهر`;
                if (i === 27) opt.selected = true; // Default day 27
                select.appendChild(opt);
            }
        }

        // Mode Switcher
        function setMode(mode) {
            calculationMode = mode;
            const btnDays = document.getElementById('btnModeDays');
            const btnDate = document.getElementById('btnModeDate');
            const groupDays = document.getElementById('daysInputGroup');
            const groupDate = document.getElementById('dateInputGroup');

            if (mode === 'days') {
                btnDays.className = "py-2 px-3 rounded-xl text-xs font-bold transition-all bg-brand-600 text-white shadow-md";
                btnDate.className = "py-2 px-3 rounded-xl text-xs font-bold transition-all bg-slate-800 text-slate-400 hover:text-white";
                groupDays.classList.remove('hidden');
                groupDate.classList.add('hidden');
            } else {
                btnDate.className = "py-2 px-3 rounded-xl text-xs font-bold transition-all bg-brand-600 text-white shadow-md";
                btnDays.className = "py-2 px-3 rounded-xl text-xs font-bold transition-all bg-slate-800 text-slate-400 hover:text-white";
                groupDate.classList.remove('hidden');
                groupDays.classList.add('hidden');
            }
            calculate();
        }

        // Set Month Days (28, 29, 30, 31)
        function setMonthDays(days) {
            daysInMonth = days;
            document.getElementById('daysInMonthVal').textContent = `${days} يوم`;
            document.getElementById('daysPassedRange').max = days;
            
            // Highlight active button
            const btns = document.querySelectorAll('.month-day-btn');
            btns.forEach(btn => {
                if (parseInt(btn.textContent) === days) {
                    btn.className = "month-day-btn active py-1.5 rounded-xl text-xs font-bold bg-brand-600 text-white shadow";
                } else {
                    btn.className = "month-day-btn py-1.5 rounded-xl text-xs font-bold bg-slate-800 text-slate-300 border border-white/5 hover:bg-brand-600/30";
                }
            });

            calculate();
        }

        // Main Calculation Engine
        function calculate() {
            // Get User Inputs
            const monthlyFee = parseFloat(document.getElementById('monthlyFee').value) || 0;
            const totalMinutes = parseFloat(document.getElementById('totalMinutes').value) || 0;
            const totalGB = parseFloat(document.getElementById('totalGB').value) || 0;
            const cycleStartDay = parseInt(document.getElementById('cycleStartDay').value) || 27;

            let daysPassed = 0;

            if (calculationMode === 'days') {
                daysPassed = parseInt(document.getElementById('daysPassedInput').value) || 0;
            } else {
                // Calculate days passed based on date input and cycle start day
                const dateVal = document.getElementById('currentDateInput').value;
                if (dateVal) {
                    const selectedDate = new Date(dateVal);
                    const currentDay = selectedDate.getDate();

                    if (currentDay >= cycleStartDay) {
                        daysPassed = (currentDay - cycleStartDay) + 1;
                    } else {
                        daysPassed = (daysInMonth - cycleStartDay + 1) + currentDay;
                    }
                }
            }

            // Boundary adjustments
            if (daysPassed > daysInMonth) daysPassed = daysInMonth;
            if (daysPassed < 1) daysPassed = 1;

            const remainingDays = daysInMonth - daysPassed;

            // Calculations
            const dueAmount = (monthlyFee / daysInMonth) * daysPassed;
            const remainingAmount = monthlyFee - dueAmount;
            
            const allocatedMinutes = (totalMinutes / daysInMonth) * daysPassed;
            const remainingMinutes = totalMinutes - allocatedMinutes;

            const allocatedGB = (totalGB / daysInMonth) * daysPassed;
            const remainingGB = totalGB - allocatedGB;
            const allocatedMB = allocatedGB * 1024;

            const dailyRate = monthlyFee / daysInMonth;
            const percentagePassed = (daysPassed / daysInMonth) * 100;

            // DOM Updates
            document.getElementById('resDueAmount').textContent = Math.round(dueAmount).toLocaleString('ar-IQ');
            document.getElementById('resDaysPassedLabel').textContent = daysPassed;
            document.getElementById('resTotalDaysLabel').textContent = daysInMonth;

            // Cards Update
            document.getElementById('resMinutes').innerHTML = `${Math.round(allocatedMinutes)} <span class="text-xs font-normal text-slate-400">دقيقة</span>`;
            document.getElementById('resTotalMinutes').textContent = totalMinutes;
            document.getElementById('barMinutes').style.width = `${percentagePassed}%`;

            document.getElementById('resGB').innerHTML = `${allocatedGB.toFixed(2)} <span class="text-xs font-normal text-slate-400">GB</span>`;
            document.getElementById('resMB').textContent = `تساوي تقريباً: ${Math.round(allocatedMB).toLocaleString()} MB`;
            document.getElementById('barGB').style.width = `${percentagePassed}%`;

            document.getElementById('resRemainingDays').innerHTML = `${remainingDays} <span class="text-xs font-normal text-slate-400">يوم</span>`;
            document.getElementById('resRemainingAmount').innerHTML = `${Math.round(remainingAmount).toLocaleString('ar-IQ')} <span class="text-xs font-normal text-slate-400">د.ع</span>`;

            // Breakdown Update
            document.getElementById('resDailyRate').textContent = `${Math.round(dailyRate).toLocaleString()} د.ع / يوم`;
            document.getElementById('resPercentage').textContent = `${percentagePassed.toFixed(1)}%`;
            document.getElementById('resRemainingMinutes').textContent = `${Math.round(remainingMinutes)} دقيقة`;
            document.getElementById('resRemainingGB').textContent = `${remainingGB.toFixed(2)} GB`;

            // Next Renewal Date Prediction
            const today = new Date();
            let renewalMonth = today.getMonth();
            let renewalYear = today.getFullYear();
            if (today.getDate() >= cycleStartDay) {
                renewalMonth++;
                if (renewalMonth > 11) {
                    renewalMonth = 0;
                    renewalYear++;
                }
            }
            const nextRenewal = new Date(renewalYear, renewalMonth, cycleStartDay);
            document.getElementById('resNextRenewalDate').textContent = `${nextRenewal.getFullYear()}/${nextRenewal.getMonth()+1}/${nextRenewal.getDate()}`;
        }

        // Copy Summary to Clipboard
        function copySummary() {
            const due = document.getElementById('resDueAmount').textContent;
            const days = document.getElementById('resDaysPassedLabel').textContent;
            const totalDays = document.getElementById('resTotalDaysLabel').textContent;
            const minutes = document.getElementById('resMinutes').innerText;
            const gb = document.getElementById('resGB').innerText;

            const summaryText = `📊 *تقرير فاتورة الخط التناسبي:*
--------------------------------
💰 *المبلغ المستحق حالياً:* ${due} دينار عراقي
📅 *عدد الأيام المنقضية:* ${days} من أصل ${totalDays} يوم
📞 *الدقائق النازلة:* ${minutes}
🌐 *الإنترنت النازل:* ${gb}
--------------------------------
تم الحساب بواسطة حاسبة الفاتورة التناسبية.`;

            // Fallback execCommand clipboard copy
            const textArea = document.createElement("textarea");
            textArea.value = summaryText;
            document.body.appendChild(textArea);
            textArea.select();
            document.execCommand('copy');
            document.body.removeChild(textArea);

            showToast("تم نسخ تقرير الفاتورة بنجاح!");
        }

        // Reset Form Values
        function resetForm() {
            document.getElementById('monthlyFee').value = 25000;
            document.getElementById('totalMinutes').value = 500;
            document.getElementById('totalGB').value = 12;
            document.getElementById('cycleStartDay').value = 27;
            document.getElementById('daysPassedInput').value = 24;
            document.getElementById('daysPassedRange').value = 24;
            setMonthDays(30);
            setMode('days');
            calculate();
            showToast("تمت إعادة ضبط المدخلات");
        }

        // Show Toast Function
        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').textContent = msg;
            toast.classList.remove('-translate-y-20', 'opacity-0');
            toast.classList.add('translate-y-0', 'opacity-100');

            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('-translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
