```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>لوحة تحكم قياس الحدقة السريري | Optoacademy - Rasha Hassan</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Chart.js for analytics -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Google Fonts (Cairo for professional Arabic typography) -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;900&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        cairo: ['Cairo', 'sans-serif'],
                    },
                    colors: {
                        medical: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            500: '#10b981',
                            600: '#059669',
                            700: '#047857',
                            800: '#065f46',
                            900: '#064e3b',
                        },
                        clinical: {
                            dark: '#0f172a',
                            card: '#1e293b',
                            accent: '#3b82f6',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Cairo', sans-serif;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0f172a;
        }
        ::-webkit-scrollbar-thumb {
            background: #334155;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569;
        }
    </style>
</head>
<body class="bg-clinical-dark text-slate-100 min-h-screen flex flex-col font-cairo selection:bg-emerald-500 selection:text-white">

    <!-- Top Header & Branding -->
    <header class="bg-slate-900/90 backdrop-blur border-b border-slate-800 sticky top-0 z-50 shadow-lg">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 flex flex-col md:flex-row justify-between items-center gap-4">
            
            <!-- Logo and Title -->
            <div class="flex items-center space-x-4 space-x-reverse">
                <div class="w-12 h-12 rounded-full bg-gradient-to-tr from-emerald-600 to-teal-400 flex items-center justify-center shadow-md ring-2 ring-emerald-400/50">
                    <i class="fa-solid fa-eye text-white text-xl"></i>
                </div>
                <div>
                    <div class="flex items-center gap-2">
                        <span class="text-xs font-bold uppercase tracking-wider px-2 py-0.5 bg-emerald-500/20 text-emerald-400 rounded-full border border-emerald-500/30">Optoacademy</span>
                        <span class="text-xs text-slate-400">المرجع السريري 2026</span>
                    </div>
                    <h1 class="text-lg md:text-xl font-black text-white tracking-wide">لوحة قياس الحدقة والتشخيص العصبي</h1>
                    <p class="text-xs text-emerald-300 font-semibold">إعداد أخصائية البصريات: رشا حسن (Optometrist Rasha Hassan)</p>
                </div>
            </div>

            <!-- Social Media Active Links -->
            <div class="flex items-center gap-2 sm:gap-3 flex-wrap">
                <a href="https://www.facebook.com/share/1FFgnuEC9p/" target="_blank" title="Facebook" class="w-9 h-9 rounded-full bg-slate-800 hover:bg-blue-600 text-slate-300 hover:text-white flex items-center justify-center transition shadow border border-slate-700">
                    <i class="fa-brands fa-facebook-f text-sm"></i>
                </a>
                <a href="https://www.instagram.com/rashamakhlouf2026?stkn=a2doMnBpZjZlcHkz" target="_blank" title="Instagram" class="w-9 h-9 rounded-full bg-slate-800 hover:bg-pink-600 text-slate-300 hover:text-white flex items-center justify-center transition shadow border border-slate-700">
                    <i class="fa-brands fa-instagram text-sm"></i>
                </a>
                <a href="https://tinyurl.com/RashaHassanLinkedIn" target="_blank" title="LinkedIn" class="w-9 h-9 rounded-full bg-slate-800 hover:bg-blue-700 text-slate-300 hover:text-white flex items-center justify-center transition shadow border border-slate-700">
                    <i class="fa-brands fa-linkedin-in text-sm"></i>
                </a>
                <a href="mailto:optoacadmy@gmail.com" title="Email" class="w-9 h-9 rounded-full bg-slate-800 hover:bg-emerald-600 text-slate-300 hover:text-white flex items-center justify-center transition shadow border border-slate-700">
                    <i class="fa-solid fa-envelope text-sm"></i>
                </a>
                <button onclick="openNotification('مرحباً بكم في منصة Optoacademy لأخصائيي البصريات - إعداد أخصائية البصريات رشا حسن', 'info')" class="px-3 py-1.5 bg-emerald-600 hover:bg-emerald-700 text-white rounded-lg text-xs font-bold transition shadow flex items-center gap-1.5">
                    <i class="fa-solid fa-bell"></i> تنبيهات سريعة
                </button>
            </div>
        </div>
    </header>

    <!-- Navigation Tabs -->
    <nav class="bg-slate-900/60 border-b border-slate-800 sticky top-[69px] z-40 backdrop-blur">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex space-x-1 space-x-reverse overflow-x-auto py-2 no-scrollbar">
                <button onclick="switchTab('dashboard')" id="btn-dashboard" class="tab-btn px-4 py-2 rounded-lg text-sm font-bold bg-emerald-600 text-white shadow transition flex items-center gap-2 whitespace-nowrap">
                    <i class="fa-solid fa-chart-pie"></i> لوحة المؤشرات والملخص
                </button>
                <button onclick="switchTab('calculators')" id="btn-calculators" class="tab-btn px-4 py-2 rounded-lg text-sm font-semibold text-slate-300 hover:bg-slate-800 hover:text-white transition flex items-center gap-2 whitespace-nowrap">
                    <i class="fa-solid fa-calculator"></i> الحاسبات السريرية (qPLR & Optic)
                </button>
                <button onclick="switchTab('pathways')" id="btn-pathways" class="tab-btn px-4 py-2 rounded-lg text-sm font-semibold text-slate-300 hover:bg-slate-800 hover:text-white transition flex items-center gap-2 whitespace-nowrap">
                    <i class="fa-solid fa-brain"></i> التشخيص العصبي والأمراض (RAPD & Matrix)
                </button>
                <button onclick="switchTab('comparison')" id="btn-comparison" class="tab-btn px-4 py-2 rounded-lg text-sm font-semibold text-slate-300 hover:bg-slate-800 hover:text-white transition flex items-center gap-2 whitespace-nowrap">
                    <i class="fa-solid fa-microchip"></i> مقارنة الأجهزة الآلية واليدوية
                </button>
            </div>
        </div>
    </nav>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-grow w-full space-y-6">

        <!-- ================= TAB 1: DASHBOARD & OVERVIEW ================= -->
        <div id="tab-dashboard" class="space-y-6 tab-content">
            <!-- Welcome Banner -->
            <div class="bg-gradient-to-r from-slate-900 via-emerald-950/40 to-slate-900 border border-emerald-500/30 rounded-2xl p-6 shadow-xl relative overflow-hidden">
                <div class="absolute -left-10 -bottom-10 w-48 h-48 bg-emerald-500/10 rounded-full blur-3xl pointer-events-none"></div>
                <div class="relative z-10 grid grid-cols-1 md:grid-cols-3 gap-6 items-center">
                    <div class="md:col-span-2 space-y-3">
                        <span class="px-3 py-1 bg-emerald-500/20 text-emerald-400 text-xs font-bold rounded-full border border-emerald-500/30">أكاديمية البصريات - Optoacademy</span>
                        <h2 class="text-2xl sm:text-3xl font-black text-white">النظام الرقمي الشامل لتشخيص الحدقة والفيزيولوجيا البصرية</h2>
                        <p class="text-slate-300 text-sm leading-relaxed">
                            مرجع متكامل ومحدث لعام 2026 يقدمه لكم فريق Optoacademy بقيادة أخصائية البصريات رشا حسن. يغطي هذا النظام قياسات الحدقة العيارية (Photopic, Mesopic, Scotopic)، معادلات الانعكاس الضوئي (qPLR)، تخطيط عمليات تصحيح النظر (LASIK/SMILE)، والتقييم العصبي الرقمي (NPi & IPA).
                        </p>
                        <div class="flex flex-wrap gap-3 pt-2">
                            <button onclick="switchTab('calculators')" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white rounded-xl text-xs font-bold transition shadow flex items-center gap-2">
                                <i class="fa-solid fa-calculator"></i> بدء الحسابات السريرية
                            </button>
                            <button onclick="switchTab('pathways')" class="px-4 py-2 bg-slate-800 hover:bg-slate-700 border border-slate-700 text-slate-200 rounded-xl text-xs font-bold transition shadow flex items-center gap-2">
                                <i class="fa-solid fa-stethoscope"></i> استعراض المصفوفة التشخيصية
                            </button>
                        </div>
                    </div>
                    <div class="bg-slate-900/80 border border-slate-800 rounded-xl p-4 flex flex-col items-center text-center space-y-3 shadow-inner">
                        <div class="w-16 h-16 rounded-full bg-emerald-600/20 text-emerald-400 border border-emerald-500/40 flex items-center justify-center text-2xl">
                            <i class="fa-solid fa-user-doctor"></i>
                        </div>
                        <div>
                            <h3 class="text-sm font-bold text-white">أخصائية البصريات: رشا حسن</h3>
                            <p class="text-xs text-emerald-400 font-medium">Optometrist & Clinical Instructor</p>
                        </div>
                        <div class="text-xs text-slate-400 border-t border-slate-800 pt-2 w-full">
                            تخصص: قياسات الحدقة المتقدمة والجراحة الانكسارية والعصبية
                        </div>
                    </div>
                </div>
            </div>

            <!-- Standard Pupil Sizes Grid -->
            <div>
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-lg font-bold text-white flex items-center gap-2">
                        <i class="fa-solid fa-ruler-combined text-emerald-400"></i> الأبعاد القياسية للحدقة ومستويات الإضاءة (Standard Pupil Sizes)
                    </h3>
                    <span class="text-xs text-slate-400">مستويات الإضاءة الثلاثة والهدف البصري</span>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <!-- Photopic -->
                    <div class="bg-slate-900/80 border border-slate-800 rounded-xl p-5 hover:border-emerald-500/50 transition group">
                        <div class="flex justify-between items-start mb-3">
                            <span class="px-2.5 py-1 bg-amber-500/20 text-amber-400 text-xs font-bold rounded-lg border border-amber-500/30">الإضاءة الساطعة النهارية</span>
                            <span class="text-lg font-black text-amber-400">2.0 - 3.0 مم</span>
                        </div>
                        <h4 class="text-white font-bold mb-1 text-sm">Photopic (الإضاءة النهارية)</h4>
                        <p class="text-xs text-slate-300 leading-relaxed">
                            رؤية نهارية دقيقة، زيادة عمق التركيز البصري (Depth of Focus)، وحماية الشبكية من الإجهاد الضوئي الشديد.
                        </p>
                        <div class="mt-4 pt-3 border-t border-slate-800 text-xs text-slate-400 flex justify-between">
                            <span>العضلة الفعالة:</span>
                            <span class="text-emerald-400 font-semibold">Ciliary / Sphincter (Miosis)</span>
                        </div>
                    </div>

                    <!-- Mesopic -->
                    <div class="bg-slate-900/80 border border-slate-800 rounded-xl p-5 hover:border-emerald-500/50 transition group">
                        <div class="flex justify-between items-start mb-3">
                            <span class="px-2.5 py-1 bg-blue-500/20 text-blue-400 text-xs font-bold rounded-lg border border-blue-500/30">الإضاءة المتوسطة الداخلية</span>
                            <span class="text-lg font-black text-blue-400">4.0 - 5.0 مم</span>
                        </div>
                        <h4 class="text-white font-bold mb-1 text-sm">Mesopic (الإضاءة المتوسطة)</h4>
                        <p class="text-xs text-slate-300 leading-relaxed">
                            النطاق المتوازن المعتاد للرؤية في ظروف الإضاءة الداخلية والمكاتب، يوازن بين كمية الضوء الواصل وعمق التركيز.
                        </p>
                        <div class="mt-4 pt-3 border-t border-slate-800 text-xs text-slate-400 flex justify-between">
                            <span>الحالة الوظيفية:</span>
                            <span class="text-blue-400 font-semibold">استجابة متوازنة</span>
                        </div>
                    </div>

                    <!-- Scotopic -->
                    <div class="bg-slate-900/80 border border-slate-800 rounded-xl p-5 hover:border-emerald-500/50 transition group">
                        <div class="flex justify-between items-start mb-3">
                            <span class="px-2.5 py-1 bg-purple-500/20 text-purple-400 text-xs font-bold rounded-lg border border-purple-500/30">الظلام التام / الليل</span>
                            <span class="text-lg font-black text-purple-400">6.0 - 8.0 مم</span>
                        </div>
                        <h4 class="text-white font-bold mb-1 text-sm">Scotopic (الظلام الكامل)</h4>
                        <p class="text-xs text-slate-300 leading-relaxed">
                            اتساع أقصى لدخول الضوء في الظلام لتأمين الرؤية الليلية، وقد يسبب الهالات والوهج الليلي إذا لم توضع بالحسبان في الليزر.
                        </p>
                        <div class="mt-4 pt-3 border-t border-slate-800 text-xs text-slate-400 flex justify-between">
                            <span>المعيار الجراحي:</span>
                            <span class="text-purple-400 font-semibold">أساس حساب منطقة العلاج</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Quick Charts Row -->
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Chart 1: Pupil Sizes Comparison -->
                <div class="bg-slate-900/80 border border-slate-800 rounded-xl p-5 shadow-lg">
                    <h3 class="text-sm font-bold text-white mb-4 flex items-center gap-2">
                        <i class="fa-solid fa-chart-bar text-emerald-400"></i> مقارنة قياسات الحدقة ومنطقة العلاج الليلي
                    </h3>
                    <div class="h-64 relative">
                        <canvas id="pupilBarChart"></canvas>
                    </div>
                </div>

                <!-- Chart 2: Manual vs Automated Accuracy -->
                <div class="bg-slate-900/80 border border-slate-800 rounded-xl p-5 shadow-lg">
                    <h3 class="text-sm font-bold text-white mb-4 flex items-center gap-2">
                        <i class="fa-solid fa-chart-line text-emerald-400"></i> أداء الفحص اليدوي مقابل القياس الآلي بالأشعة تحت الحمراء
                    </h3>
                    <div class="h-64 relative">
                        <canvas id="accuracyChart"></canvas>
                    </div>
                </div>
            </div>
        </div>

        <!-- ================= TAB 2: CLINICAL CALCULATORS ================= -->
        <div id="tab-calculators" class="space-y-6 tab-content hidden">
            <div class="bg-slate-900/90 border border-slate-800 rounded-2xl p-6 shadow-xl">
                <div class="border-b border-slate-800 pb-4 mb-6 flex justify-between items-center">
                    <div>
                        <h2 class="text-xl font-black text-white flex items-center gap-2">
                            <i class="fa-solid fa-calculator text-emerald-400"></i> الحاسبات السريرية المتقدمة للحدقة (Clinical Calculators)
                        </h2>
                        <p class="text-xs text-slate-400 mt-1">حسابات ديناميكية منعكس الضوء (qPLR) وتخطيط منطقة الإزالة القرنية لجراحات الليزك و SMILE</p>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                    <!-- Calculator 1: qPLR & Amplitude -->
                    <div class="bg-slate-950/60 border border-slate-800/80 rounded-xl p-5 space-y-4">
                        <h3 class="text-sm font-bold text-emerald-400 flex items-center gap-2">
                            <i class="fa-solid fa-bolt"></i> 1. حاسبة سعة الانقباض الفعلي والنسبة المئوية (qPLR Calculator)
                        </h3>
                        <p class="text-xs text-slate-400">أدخل أقطار الحدقة قبل وبعد التعرض للوميض الضوئي لحساب سعة الانقباض المئوية والتصنيف السريري.</p>
                        
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1">القطر الأقصى في الظلام (D_max مم):</label>
                                <input type="number" id="dMaxInput" value="6.0" step="0.1" min="1" max="9" class="w-full bg-slate-900 border border-slate-700 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-emerald-500">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1">القطر الأدنى بعد الوميض (D_min مم):</label>
                                <input type="number" id="dMinInput" value="3.8" step="0.1" min="0.5" max="8" class="w-full bg-slate-900 border border-slate-700 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-emerald-500">
                            </div>
                        </div>

                        <button onclick="calculateQPLR()" class="w-full py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white rounded-lg text-xs font-bold transition shadow">
                            حساب qPLR والتقييم السريري
                        </button>

                        <!-- qPLR Results Box -->
                        <div id="qplrResultBox" class="bg-slate-900 border border-slate-800 rounded-lg p-4 space-y-2 text-xs">
                            <div class="flex justify-between">
                                <span class="text-slate-400">سعة الانقباض الفعلي (AMP):</span>
                                <span id="resAmp" class="font-bold text-white">-- مم</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-slate-400">نسبة الانقباض المئوية (qPLR %):</span>
                                <span id="resPercent" class="font-bold text-emerald-400">-- %</span>
                            </div>
                            <div class="flex justify-between items-center pt-2 border-t border-slate-800">
                                <span class="text-slate-400">التصنيف السريري:</span>
                                <span id="resClassification" class="px-2.5 py-1 rounded-full font-bold text-xs bg-slate-800 text-slate-300"
