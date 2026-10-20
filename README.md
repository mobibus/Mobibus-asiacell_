<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة خطوط الفاتورة التناسبية | Postpaid Calculator</title>
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
                    حاسبة خطوط الفاتورة التناسبية (Pro-rata)
                </h1>
                <p class="text-slate-400 text-xs sm:text-sm max-w-xl leading-relaxed">
                    حساب المبلغ المستحق، الدقائق النازلة، والإنترنت بالتناسب مع أيام الاستخدام الفعلية للدورة.
                </p>
            </div>
        </header>

        <!-- Main Layout -->
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
                                <i class="fa-solid fa-money-bill-wave text-emerald-400 ml-1"></i> سعر الباقة الشهري الكلي (د.ع)
                            </label>
                            <div class="relative">
                                <input type="number" id="monthlyFee" value="25000" min="0" step="500" class="w-full custom-input rounded-xl py-2.5 px-4 pr-10 text-sm font-semibold">
                                <span class="absolute left-3 top-2.5 text-xs text-slate-400 font-normal">د.ع</span>
                            </div>
                        </div>

                        <!-- Included Minutes & GB -->
                        <div class="grid grid-cols-2 gap-3">
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1.5">
                                    <i class="fa-solid fa-phone text-amber-400 ml-1"></i> إجمالي الدقائق بالشهر
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
                                <i class="fa-solid fa-calendar-day text-brand-500 ml-1"></i> يوم تجديد / بداية الدورة (مثال: 27)
                            </label>
                            <select id="cycleStartDay" class="w-full custom-input rounded-xl py-2.5 px-3 text-sm font-semibold">
                                <!-- JS will populate 1-31 -->
                            </select>
                        </div>

                        <!-- Computation Mode Toggle -->
                        <div class="bg-slate-900/40 p-3 rounded-2xl border border-white/5 space-y-3">
                            <label class="block text-xs font-semibold text-slate-300">طريقة تحديد الأيام المنقضية:</label>
                            <div class="grid grid-cols-2 gap-2">
                                <button type="button" id="btnModeDays" onclick="setMode('days')" class="py-2 px-3 rounded-xl text-xs font-bold transition-all bg-brand-600 text-white shadow-md">
                                    <i class="fa-solid fa-hashtag ml-1"></i> عدد الأيام يدوياً
                                </button>
                                <button type="button" id="btnModeDate" onclick="setMode('date')" class="py-2 px-3 rounded-xl text-xs font-bold transition-all bg-slate-800 text-slate-400 hover:text-white">
                                    <i class="fa-solid fa-calendar-alt ml-1"></i> تاريخ اليوم الحالي
                                </button>
                            </div>

                            <!-- Manual Days Input -->
                            <div id="daysInputGroup" class="pt-1">
                                <label class="block text-xs font-medium text-slate-400 mb-1">الأيام المنقضية من الدورة:</label>
                                <div class="flex items-center space-x-2 space-x-reverse">
                                    <input type="range" id="daysPassedRange" min="1" max="30" value="24" class="w-full accent-brand-500 h-2 bg-slate-700 rounded-lg cursor-pointer">
                                    <input type="number" id="daysPassedInput" min="1" max="31" value="24" class="w-20 text-center custom-input rounded-xl py-1.5 text-xs font-bold">
                                </div>
                            </div>

                            <!-- Date Input -->
                            <div id="dateInputGroup" class="hidden pt-1">
                                <label class="block text-xs font-medium text-slate-400 mb-1">تاريخ اليوم:</label>
                                <input type="date" id="currentDateInput" class="w-full custom-input rounded-xl py-2 px-3 text-xs font-semibold">
                            </div>
                        </div>

                        <!-- Month Days Setting -->
                        <div>
                            <div class="flex justify-between items-center mb-1">
                               
