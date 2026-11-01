<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Kemer Agent Dashboard</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        darkBg: '#0b1120',
                        cardBg: '#182234',
                        cardBorder: '#2a374a',
                        brandYellow: '#facc15',
                        brandYellowDark: '#eab308',
                        brandGreen: '#22c55e',
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        html, body {
            height: 100%;
            margin: 0;
            padding: 0;
            overflow: hidden;
            background-color: #070b14;
            color: #f8fafc;
            font-family: 'Inter', sans-serif;
            -webkit-tap-highlight-color: transparent;
            touch-action: manipulation;
        }
        /* Custom Glowing Effect for Yellow & Green Borders */
        .yellow-glow {
            border-color: #facc15;
            box-shadow: 0 0 15px rgba(250, 204, 21, 0.25);
        }
        .green-glow {
            border-color: #22c55e !important;
            box-shadow: 0 0 15px rgba(34, 197, 94, 0.3) !important;
        }
    </style>
</head>
<body class="w-full h-full flex flex-col items-center justify-center p-1.5 text-slate-200 select-none">

    <!-- Container scaling perfectly to fit mobile screen without scrolling -->
    <div class="w-full max-w-sm h-full max-h-[780px] bg-[#0f172a] rounded-[22px] border border-slate-800/80 shadow-2xl overflow-hidden flex flex-col justify-between">
        
        <!-- Header Bar -->
        <div class="px-4 pt-3 pb-2 flex items-center justify-between border-b border-slate-800/50">
            <!-- Agent Badge -->
            <div class="flex items-center gap-2 px-3 py-1 rounded-full bg-[#182234] border border-slate-700/60 shadow-sm">
                <span id="agentDot" class="w-2 h-2 rounded-full bg-slate-500 transition-all duration-300"></span>
                <span id="agentBadgeText" class="text-xs font-semibold text-slate-400 tracking-wide">Agent #01</span>
            </div>
            
            <!-- Time Indicator -->
            <div class="text-xs font-semibold tracking-wider text-slate-400">
                EAT <span id="clockDisplay">14:41</span>
            </div>
        </div>

        <!-- Main Content -->
        <div class="px-3 py-2 space-y-2 flex-1 flex flex-col justify-between">

            <!-- SECTION 1: Status Card -->
            <div class="bg-[#182234] rounded-xl p-2.5 border border-slate-800/70 relative shadow-lg">
                <!-- Header Title -->
                <div class="flex items-center justify-between mb-1.5">
                    <div class="flex items-center gap-1.5">
                        <span id="statusIndicatorBar" class="w-1.5 h-3.5 bg-slate-500 rounded-full transition-all duration-300"></span>
                        <h2 class="text-xs font-semibold text-slate-200">Your status</h2>
                    </div>
                    <span class="text-[9.5px] text-slate-400 font-normal">tap a duration to go online</span>
                </div>

                <!-- Main Status Banner -->
                <div id="statusBanner" class="text-center py-2.5 rounded-lg bg-[#0f172a]/90 border border-slate-800/80 mb-2 transition-all duration-300">
                    <div class="flex items-center justify-center gap-1.5 mb-0.5">
                        <span id="statusPulseDot" class="w-1.5 h-1.5 rounded-full bg-slate-500 transition-all duration-300"></span>
                        <span id="statusSubHeader" class="text-[9.5px] uppercase tracking-wider font-bold text-slate-400">YOU ARE OFFLINE</span>
                    </div>
                    <h1 id="statusText" class="text-lg font-bold text-white mb-0.5">Offline</h1>
                    <p id="statusSubtitle" class="text-[10.5px] text-slate-400">pick a duration below to come back</p>
                    <div id="timerDisplay" class="hidden mt-0.5 text-sm font-mono font-bold text-emerald-400">00:00:00</div>
                </div>

                <!-- Duration Buttons -->
                <div class="grid grid-cols-5 gap-1.5">
                    <button onclick="setDuration(15)" class="duration-btn relative flex flex-col items-center justify-center py-1.5 bg-[#0f172a]/90 border border-slate-800 hover:border-slate-600 rounded-lg transition duration-150 active:scale-95">
                        <span class="text-xs font-bold text-slate-200">15</span>
                        <span class="text-[7.5px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>
                    
                    <button onclick="setDuration(30)" class="duration-btn relative flex flex-col items-center justify-center py-1.5 bg-[#0f172a]/90 border border-slate-800 hover:border-slate-600 rounded-lg transition duration-150 active:scale-95">
                        <span class="text-xs font-bold text-slate-200">30</span>
                        <span class="text-[7.5px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>

                    <button onclick="setDuration(45)" class="duration-btn relative flex flex-col items-center justify-center py-1.5 bg-[#0f172a]/90 border border-slate-800 hover:border-slate-600 rounded-lg transition duration-150 active:scale-95">
                        <span class="text-xs font-bold text-slate-200">45</span>
                        <span class="text-[7.5px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>

                    <button onclick="setDuration(60)" class="duration-btn relative flex flex-col items-center justify-center py-1.5 bg-[#0f172a]/90 border border-slate-800 hover:border-slate-600 rounded-lg transition duration-150 active:scale-95">
                        <span class="text-xs font-bold text-slate-200">60</span>
                        <span class="text-[7.5px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>

                    <button id="btn120" onclick="setDuration(120)" class="duration-btn yellow-glow relative flex flex-col items-center justify-center py-1.5 bg-[#0f172a]/90 border border-yellow-500/80 rounded-lg transition duration-150 active:scale-95">
                        <i class="fa-solid fa-star text-[7px] text-yellow-400 absolute top-1 right-1"></i>
                        <span class="text-xs font-bold text-slate-200">120</span>
                        <span class="text-[7.5px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>
                </div>
            </div>

            <!-- SECTION 2: Withdrawal Settings Card -->
            <div class="bg-[#182234] rounded-xl p-2.5 border border-slate-800/70 space-y-2 shadow-lg flex-1 flex flex-col justify-between">
                
                <!-- Section Header with Badge -->
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-1.5">
                        <span class="w-1.5 h-3.5 bg-yellow-400 rounded-full"></span>
                        <h2 class
