<!DOCTYPE html>
<html lang="es" class="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Para Citlali ✨</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;700&family=Dancing+Script:wght@600;700&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>
  <!-- Canvas Confetti -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['"Plus Jakarta Sans"', 'sans-serif'],
            script: ['"Dancing Script"', 'cursive'],
            serif: ['"Cinzel"', 'serif'],
          },
          colors: {
            accent: {
              pink: '#ec4899',
              rose: '#f43f5e',
              violet: '#8b5cf6',
              cyan: '#06b6d4',
            }
          },
          boxShadow: {
            'neon-pink': '0 0 25px -5px rgba(236, 72, 153, 0.45)',
            'neon-rose': '0 0 35px -5px rgba(244, 63, 94, 0.5)',
            'neon-cyan': '0 0 25px -5px rgba(6, 182, 212, 0.45)',
          }
        }
      }
    }
  </script>

  <style>
    /* Custom Scrollbar */
    ::-webkit-scrollbar {
      width: 4px;
    }
    ::-webkit-scrollbar-track {
      background: #09090b;
    }
    ::-webkit-scrollbar-thumb {
      background: #27272a;
      border-radius: 9999px;
    }

    /* 3D Flip Card Styles */
    .perspective-1000 {
      perspective: 1000px;
    }
    .transform-style-3d {
      transform-style: preserve-3d;
    }
    .backface-hidden {
      backface-visibility: hidden;
      -webkit-backface-visibility: hidden;
    }
    .rotate-y-180 {
      transform: rotateY(180deg);
    }

    /* Glassmorphism */
    .glass-card {
      background: rgba(18, 18, 23, 0.72);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }
    
    .glass-envelope {
      background: linear-gradient(135deg, rgba(28, 25, 23, 0.85) 0%, rgba(15, 15, 18, 0.92) 100%);
      backdrop-filter: blur(20px);
      border: 1px solid rgba(244, 63, 94, 0.25);
    }

    /* Keyframes */
    @keyframes pulseGlow {
      0%, 100% {
        box-shadow: 0 0 20px rgba(244, 63, 94, 0.3), 0 0 40px rgba(236, 72, 153, 0.15);
      }
      50% {
        box-shadow: 0 0 35px rgba(244, 63, 94, 0.6), 0 0 60px rgba(236, 72, 153, 0.3);
      }
    }

    .pulse-glow {
      animation: pulseGlow 3s infinite ease-in-out;
    }

    @keyframes floatHeart {
      0% { transform: translateY(0px) scale(1); opacity: 0; }
      50% { opacity: 0.8; }
      100% { transform: translateY(-80px) scale(1.3); opacity: 0; }
    }

    .animate-float-heart {
      animation: floatHeart 2.5s cubic-bezier(0.2, 0.8, 0.2, 1) forwards;
    }

    /* Coraline Door 3D Scene */
    .coraline-door-frame {
      perspective: 1200px;
    }
    .coraline-door-leaf {
      transform-origin: left center;
      transition: transform 1.5s cubic-bezier(0.25, 1, 0.5, 1);
      transform-style: preserve-3d;
    }
    .door-opened {
      transform: rotateY(-118deg);
    }
    
    /* Coraline Tunnel Vortex Animation */
    @keyframes vortexSpin {
      0% { transform: rotate(0deg) scale(0.95); }
      50% { transform: rotate(180deg) scale(1.18); }
      100% { transform: rotate(360deg) scale(0.95); }
    }
    .vortex-swirl {
      animation: vortexSpin 9s linear infinite;
    }

    /* Tunnel zoom dive transition */
    .tunnel-dive-zoom {
      animation: cameraTunnelZoom 1.5s cubic-bezier(0.7, 0, 0.3, 1) forwards;
    }

    @keyframes cameraTunnelZoom {
      0% {
        transform: scale(1) translateZ(0);
        opacity: 1;
        filter: blur(0px);
      }
      65% {
        opacity: 1;
      }
      100% {
        transform: scale(3.4) translateZ(300px);
        opacity: 0;
        filter: blur(8px);
      }
    }

    /* Realistic Stitched Button Badge */
    .black-button-eye {
      background: radial-gradient(circle at 35% 35%, #2a2a38 0%, #0d0d14 65%, #050508 100%);
      box-shadow: inset 0 2px 5px rgba(255, 255, 255, 0.15),
                  inset 0 -3px 6px rgba(0, 0, 0, 0.85),
                  0 8px 25px rgba(99, 102, 241, 0.35);
    }
    .button-inner-rim {
      box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.9), 0 1px 2px rgba(255, 255, 255, 0.1);
    }
  </style>
</head>
<body class="bg-[#050508] text-zinc-100 font-sans selection:bg-rose-500 selection:text-white min-h-screen relative overflow-x-hidden antialiased">

  <!-- Interactive Canvas Background (Floating Constellations & Hearts on Touch) -->
  <canvas id="interactiveCanvas" class="fixed inset-0 pointer-events-auto z-0 w-full h-full"></canvas>

  <!-- Sound Toggle Button (Top Right Floating) -->
  <div class="fixed top-4 right-4 z-50">
    <button id="soundToggleBtn" onclick="toggleAudio()" class="w-11 h-11 rounded-full glass-card flex items-center justify-center text-rose-400 hover:text-white border border-rose-500/30 hover:border-rose-400/60 shadow-lg active:scale-95 transition-all">
      <i id="soundIcon" data-lucide="volume-x" class="w-5 h-5"></i>
    </button>
  </div>

  <!-- MAIN WRAPPER (Mobile Frame / Max Width) -->
  <div class="relative z-10 max-w-md mx-auto min-h-screen flex flex-col justify-between px-4 pb-12 pt-6">

    <!-- ==================== SCREEN 1: COVER / INTRO (CORALINE BUTTON & SECRET DOOR) ==================== -->
    <section id="coverSection" class="min-h-[90vh] flex flex-col items-center justify-center text-center transition-all duration-700">
      
      <!-- Ambient Glow Behind Title -->
      <div class="relative mb-5">
        <div class="absolute -inset-6 bg-gradient-to-r from-indigo-600/25 via-purple-600/20 to-rose-500/20 rounded-full blur-2xl"></div>
        
        <!-- Big Coraline Stitched Button Eye -->
        <div class="relative mx-auto mb-4 w-28 h-28 rounded-full black-button-eye border-2 border-indigo-400/40 p-3 flex items-center justify-center pulse-glow">
          <div class="w-full h-full rounded-full border border-indigo-500/30 button-inner-rim flex items-center justify-center relative">
            <!-- 4 Button Holes & Cross Stitching -->
            <div class="grid grid-cols-2 gap-3 z-10">
              <div class="w-2.5 h-2.5 rounded-full bg-[#050508] border border-white/20 shadow-inner"></div>
              <div class="w-2.5 h-2.5 rounded-full bg-[#050508] border border-white/20 shadow-inner"></div>
              <div class="w-2.5 h-2.5 rounded-full bg-[#050508] border border-white/20 shadow-inner"></div>
              <div class="w-2.5 h-2.5 rounded-full bg-[#050508] border border-white/20 shadow-inner"></div>
            </div>
            <!-- Thread Stitches (Purple/Cyan Neon) -->
            <svg class="absolute inset-0 w-full h-full pointer-events-none" viewBox="0 0 100 100">
              <line x1="38" y1="38" x2="62" y2="62" stroke="#a855f7" stroke-width="2.5" stroke-linecap="round" />
              <line x1="62" y1="38" x2="38" y2="62" stroke="#06b6d4" stroke-width="2.5" stroke-linecap="round" />
            </svg>
          </div>
        </div>

        <p class="text-xs uppercase tracking-[0.3em] font-semibold text-indigo-400/90 mb-1">El Otro Mundo</p>
        <h1 class="text-3xl sm:text-4xl font-bold tracking-tight text-white mb-2 font-serif">
          Para <span class="bg-gradient-to-r from-indigo-300 via-purple-300 to-rose-300 bg-clip-text text-transparent">Citlali</span>
        </h1>
        <p class="text-zinc-300 text-xs max-w-xs mx-auto leading-relaxed font-medium">
          Usa la llave para abrir la pequeña puerta secreta.
        </p>
      </div>

      <!-- ================= CORALINE 3D SECRET DOOR ================= -->
      <div id="doorPortalContainer" class="relative w-48 h-64 my-3 coraline-door-frame cursor-pointer select-none group transition-transform duration-700" onclick="unlockSecretDoor()">
        
        <!-- Mystical Backlight Glow Behind Frame -->
        <div id="doorPortalGlow" class="absolute -inset-5 rounded-full bg-gradient-to-r from-indigo-500/0 via-purple-500/0 to-cyan-400/0 blur-2xl pointer-events-none transition-all duration-1000 z-0"></div>

        <!-- Wall/Tunnel Portal Background behind door -->
        <div class="relative z-10 w-full h-full rounded-t-full bg-gradient-to-b from-[#0b0c26] via-[#060718] to-[#020207] border-4 border-[#2d2a4a] shadow-[0_0_35px_rgba(79,70,229,0.35)] overflow-hidden flex items-center justify-center">
          
          <!-- Swirling Tunnel Vortex (Visible through the open door) -->
          <div id="tunnelVortex" class="absolute w-72 h-72 rounded-full bg-[radial-gradient(circle_at_center,_#c7d2fe_0%,_#6366f1_22%,_#3b0764_50%,_#050512_80%)] vortex-swirl opacity-90 blur-[1px] transition-all duration-1000"></div>
          
          <!-- Spiral / spiderweb tunnel threads -->
          <svg class="absolute inset-0 w-full h-full opacity-40 mix-blend-screen pointer-events-none" viewBox="0 0 200 300">
            <path d="M100 150 Q130 90 100 30 Q70 90 100 150 Q160 170 180 230 Q120 220 100 150 Q40 210 20 230 Q50 170 100 150" fill="none" stroke="#e0e7ff" stroke-width="1.2" />
            <circle cx="100" cy="150" r="18" fill="none" stroke="#a5b4fc" stroke-width="0.8" opacity="0.6" />
            <circle cx="100" cy="150" r="42" fill="none" stroke="#818cf8" stroke-width="0.8" opacity="0.4" />
          </svg>
        </div>

        <!-- The Door Leaf (Hinged 3D element with realistic wooden plank textures & iron hinges) -->
        <div id="secretDoorLeaf" class="coraline-door-leaf absolute inset-0 rounded-t-full bg-[#1c1829] border-4 border-[#3c3654] shadow-2xl flex flex-col justify-between p-3.5 z-20 overflow-hidden" style="background-image: repeating-linear-gradient(90deg, #181523 0px, #181523 38px, #252037 39px, #2e2844 40px, #181523 41px);">
          
          <!-- Subtle wood grain & vignette overlay -->
          <div class="absolute inset-0 bg-gradient-to-b from-black/25 via-transparent to-black/60 pointer-events-none"></div>

          <!-- Iron Hinge Top-Left -->
          <div class="absolute top-12 left-0 w-6 h-3 bg-gradient-to-r from-zinc-800 to-zinc-950 border-y border-r border-amber-600/40 rounded-r shadow-md flex items-center justify-end pr-1 z-30">
            <div class="w-1.5 h-1.5 rounded-full bg-amber-500/60 shadow-inner"></div>
          </div>
          <!-- Iron Hinge Bottom-Left -->
          <div class="absolute bottom-12 left-0 w-6 h-3 bg-gradient-to-r from-zinc-800 to-zinc-950 border-y border-r border-amber-600/40 rounded-r shadow-md flex items-center justify-end pr-1 z-30">
            <div class="w-1.5 h-1.5 rounded-full bg-amber-500/60 shadow-inner"></div>
          </div>

          <!-- Ornate upper arch & carved star emblem -->
          <div class="relative z-10 flex flex-col items-center mt-2">
            <div class="w-11 h-11 rounded-full border-2 border-amber-500/30 bg-[#0d0a17]/80 flex items-center justify-center shadow-inner">
              <span class="text-sm filter drop-shadow-[0_0_4px_rgba(245,158,11,0.6)] text-amber-300">★</span>
            </div>
            <div class="w-20 h-0.5 bg-amber-500/20 rounded-full mt-2.5"></div>
          </div>

          <!-- Horizontal decorative iron brace bars -->
          <div class="relative z-10 w-full flex flex-col items-center gap-7 my-auto">
            <div class="w-11/12 h-1 bg-black/50 border-t border-white/10 rounded-full shadow-inner flex justify-around px-2 items-center">
              <div class="w-1 h-1 rounded-full bg-zinc-600"></div>
              <div class="w-1 h-1 rounded-full bg-zinc-600"></div>
            </div>
            <div class="w-11/12 h-1 bg-black/50 border-t border-white/10 rounded-full shadow-inner flex justify-around px-2 items-center">
              <div class="w-1 h-1 rounded-full bg-zinc-600"></div>
              <div class="w-1 h-1 rounded-full bg-zinc-600"></div>
            </div>
          </div>

          <!-- Ornate Keyhole Plate & Button Skeleton Key -->
          <div class="relative z-10 w-full flex justify-end pr-2.5 pb-6">
            <div class="relative flex items-center">
              <!-- Vintage Ornate Escutcheon / Keyhole plate -->
              <div class="w-7 h-12 rounded-md bg-gradient-to-b from-[#2b2518] to-[#120f0a] border-2 border-amber-500/50 flex flex-col items-center justify-center shadow-[inset_0_1px_3px_rgba(255,255,255,0.2),0_2px_8px_rgba(0,0,0,0.8)]">
                <!-- Tiny screws -->
                <div class="w-1 h-1 rounded-full bg-amber-400/70 mb-1"></div>
                <!-- Keyhole slot -->
                <div class="w-2 h-2 rounded-full bg-black shadow-inner"></div>
                <div class="w-1 h-2.5 bg-black"></div>
                <div class="w-1 h-1 rounded-full bg-amber-400/70 mt-1"></div>
              </div>

              <!-- Button-headed Skeleton Key inserted in lock -->
              <div id="doorKeyObj" class="absolute -right-3.5 -top-1.5 transition-transform duration-500 origin-left">
                <span class="text-2xl filter drop-shadow-[0_0_8px_rgba(244,63,94,0.9)] select-none">🗝️</span>
              </div>
            </div>
          </div>

        </div>

      </div>

      <!-- Action Button / Door Trigger -->
      <button onclick="unlockSecretDoor()" class="group relative mt-4 px-8 py-3.5 rounded-2xl bg-gradient-to-r from-indigo-950 via-purple-900 to-rose-950 hover:from-indigo-900 hover:to-rose-900 border border-indigo-500/40 text-white font-medium text-sm tracking-wide shadow-[0_0_25px_rgba(99,102,241,0.35)] active:scale-95 transition-all duration-300 flex items-center space-x-2.5">
        <span class="text-base">🗝️</span>
        <span>Abrir la puerta secreta</span>
        <i data-lucide="sparkles" class="w-4 h-4 text-indigo-300 group-hover:rotate-12 transition-transform"></i>
      </button>
    </section>

    <!-- ==================== SCREEN 2: MAIN EXPERIENCE ==================== -->
    <main id="mainContent" class="hidden opacity-0 flex-col space-y-12 transition-opacity duration-700 pt-2">
      
      <!-- Section 1: Intro Banner -->
      <div class="text-center pt-4">
        <h2 class="text-3xl sm:text-4xl font-extrabold tracking-tight bg-gradient-to-r from-pink-300 via-rose-300 to-indigo-300 bg-clip-text text-transparent font-serif drop-shadow-[0_0_20px_rgba(244,63,94,0.35)]">
          Una cajita de sorpresas
        </h2>
        <p class="text-xs text-zinc-400 mt-2 max-w-xs mx-auto">
          Toca cada tarjeta para voltearla y descubrir lo que hay detrás.
        </p>
      </div>

      <!-- Section 2: 3D Flip Card Collage (Facets Grid) -->
      <section class="grid grid-cols-2 gap-3.5 perspective-1000">

        <!-- Card 1: Coraline / Misterio y nuestra conexión -->
        <div class="flip-card col-span-2 h-44 cursor-pointer" onclick="handleFlipCard(this, 'chime4')">
          <div class="flip-card-inner relative w-full h-full duration-500 transform-style-3d transition-transform rounded-2xl">
            <!-- Front -->
            <div class="flip-front absolute inset-0 backface-hidden glass-card rounded-2xl p-4 flex flex-col justify-between border border-indigo-500/30 hover:border-indigo-400/60 shadow-lg bg-gradient-to-br from-[#0c0d1e]/85 to-[#070712]/90">
              <div class="flex items-center justify-between">
                <!-- Minimalist Vector Key & Button Icon -->
                <div class="w-10 h-10 rounded-xl bg-indigo-500/10 border border-indigo-500/30 flex items-center justify-center text-indigo-300 shadow-inner">
                  <svg class="w-5 h-5 text-indigo-300" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="7.5" cy="15.5" r="4.5"/>
                    <path d="m10.7 12.3 8.8-8.8"/>
                    <path d="m16 7 2 2"/>
                    <path d="m19 4 2 2"/>
                  </svg>
                </div>
                <span class="text-[10px] tracking-widest uppercase font-semibold text-indigo-300/80 bg-indigo-500/10 px-2.5 py-0.5 rounded-full border border-indigo-500/20">
                  Especial
                </span>
              </div>
              <div>
                <h3 class="text-sm font-semibold text-zinc-100 tracking-wide">Misterio y nuestra conexión</h3>
              </div>
              <span class="text-[10px] text-zinc-400 flex items-center gap-1.5">
                <i data-lucide="sparkles" class="w-3 h-3 text-indigo-400"></i> Toca para descubrir el secreto
              </span>
            </div>
            <!-- Back -->
            <div class="flip-back absolute inset-0 backface-hidden rotate-y-180 bg-gradient-to-br from-indigo-950/90 via-[#0a0a1f] to-zinc-950/90 rounded-2xl p-4 flex flex-col justify-center text-center border border-indigo-500/50 shadow-neon-pink">
              <div class="flex justify-center items-center gap-2 mb-1.5 text-indigo-300">
                <span class="text-lg">🗝️</span>
                <span class="text-sm">🪡</span>
                <span class="text-base">✨</span>
              </div>
              <p class="text-xs text-indigo-100 font-medium leading-relaxed px-1">
                "Dicen que hay que tener cuidado con lo que se desea... pero yo encontré mi mundo perfecto sin necesidad de coserme botones en los ojos. Aunque por ti, cruzo cualquier puerta secreta y me los pongo."
              </p>
            </div>
          </div>
        </div>

        <!-- Card 2: Guitarra & Música -->
        <div class="flip-card h-44 cursor-pointer" onclick="handleFlipCard(this, 'chime1')">
          <div class="flip-card-inner relative w-full h-full duration-500 transform-style-3d transition-transform rounded-2xl">
            <!-- Front -->
            <div class="flip-front absolute inset-0 backface-hidden glass-card rounded-2xl p-4 flex flex-col justify-between border border-rose-500/20 hover:border-rose-400/50 shadow-lg">
              <!-- Minimalist Vector Guitar / Acoustic Notes Icon -->
              <div class="w-10 h-10 rounded-xl bg-rose-500/10 border border-rose-500/20 flex items-center justify-center text-rose-400 shadow-inner">
                <svg class="w-5 h-5 text-rose-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <path d="m11.9 12.1 6.5-6.5"/>
                  <circle cx="6" cy="18" r="4"/>
                  <path d="M9.8 14.2c.4-.4 1-.4 1.4 0l1.4 1.4c.4.4.4 1 0 1.4"/>
                  <path d="M16 4.5 19.5 8"/>
                  <circle cx="18" cy="6" r="1" fill="currentColor"/>
                </svg>
              </div>
              <div>
                <p class="text-[11px] font-semibold text-rose-400 uppercase tracking-wider">Música & Acordes</p>
                <h3 class="text-sm font-semibold text-zinc-100 mt-0.5">La Guitarra</h3>
              </div>
              <span class="text-[10px] text-zinc-400 flex items-center gap-1">
                <i data-lucide="touchpad" class="w-3 h-3"></i> Toca para ver
              </span>
            </div>
            <!-- Back -->
            <div class="flip-back absolute inset-0 backface-hidden rotate-y-180 bg-gradient-to-br from-rose-950/80 to-zinc-950/90 rounded-2xl p-4 flex flex-col justify-center text-center border border-rose-500/40 shadow-neon-pink">
              <span class="text-2xl mb-1">🎶</span>
              <p class="text-xs text-rose-100 font-medium leading-relaxed">
                "Te tocaria todo lo que quieras y cuando quieras y tambien la guitarra."
              </p>
            </div>
          </div>
        </div>

        <!-- Card 3: Cocina & Pan -->
        <div class="flip-card h-44 cursor-pointer" onclick="handleFlipCard(this, 'chime2')">
          <div class="flip-card-inner relative w-full h-full duration-500 transform-style-3d transition-transform rounded-2xl">
            <!-- Front -->
            <div class="flip-front absolute inset-0 backface-hidden glass-card rounded-2xl p-4 flex flex-col justify-between border border-amber-500/20 hover:border-amber-400/50 shadow-lg">
              <!-- Minimalist Vector Chef / Culinary Pan Icon -->
              <div class="w-10 h-10 rounded-xl bg-amber-500/10 border border-amber-500/20 flex items-center justify-center text-amber-400 shadow-inner">
                <svg class="w-5 h-5 text-amber-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M6 13.8V4a2 2 0 0 1 4 0v9.8"/>
                  <path d="M14 4v9.8"/>
                  <path d="M18 4v9.8"/>
                  <path d="M10 13.8a4 4 0 0 0 8 0"/>
                  <path d="M14 17.8V21a1 1 0 0 1-1 1h-2a1 1 0 0 1-1-1v-3.2"/>
                  <path d="M4 10h4"/>
                </svg>
              </div>
              <div>
                <p class="text-[11px] font-semibold text-amber-400 uppercase tracking-wider">Arte de la cocina</p>
                <h3 class="text-sm font-semibold text-zinc-100 mt-0.5">La Cocina & Pan</h3>
              </div>
              <span class="text-[10px] text-zinc-400 flex items-center gap-1">
                <i data-lucide="touchpad" class="w-3 h-3"></i> Toca para ver
              </span>
            </div>
            <!-- Back -->
            <div class="flip-back absolute inset-0 backface-hidden rotate-y-180 bg-gradient-to-br from-amber-950/80 to-zinc-950/90 rounded-2xl p-4 flex flex-col justify-center text-center border border-amber-500/40">
              <span class="text-2xl mb-1">🍞</span>
              <p class="text-xs text-amber-100 font-medium leading-relaxed">
                "Seria tu chef personal dicen que para que esponje un pan debe de estar caliente en un cuarto especial:"
              </p>
            </div>
          </div>
        </div>

        <!-- Card 4: Código & Programación -->
        <div class="flip-card h-44 cursor-pointer" onclick="handleFlipCard(this, 'chime3')">
          <div class="flip-card-inner relative w-full h-full duration-500 transform-style-3d transition-transform rounded-2xl">
            <!-- Front -->
            <div class="flip-front absolute inset-0 backface-hidden glass-card rounded-2xl p-4 flex flex-col justify-between border border-cyan-500/20 hover:border-cyan-400/50 shadow-lg">
              <!-- Minimalist Vector Code Tag Icon -->
              <div class="w-10 h-10 rounded-xl bg-cyan-500/10 border border-cyan-500/20 flex items-center justify-center text-cyan-400 shadow-inner">
                <svg class="w-5 h-5 text-cyan-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <polyline points="16 18 22 12 16 6"/>
                  <polyline points="8 6 2 12 8 18"/>
                  <line x1="14" y1="4" x2="10" y2="20"/>
                </svg>
              </div>
              <div>
                <p class="text-[11px] font-semibold text-cyan-400 uppercase tracking-wider">Creación</p>
                <h3 class="text-sm font-semibold text-zinc-100 mt-0.5">Programar</h3>
              </div>
              <span class="text-[10px] text-zinc-400 flex items-center gap-1">
                <i data-lucide="touchpad" class="w-3 h-3"></i> Toca para ver
              </span>
            </div>
            <!-- Back -->
            <div class="flip-back absolute inset-0 backface-hidden rotate-y-180 bg-gradient-to-br from-cyan-950/80 to-zinc-950/90 rounded-2xl p-4 flex flex-col justify-center text-center border border-cyan-500/40 shadow-neon-cyan">
              <span class="text-2xl mb-1">⚡</span>
              <p class="text-xs text-cyan-100 font-medium leading-relaxed">
                "solo yo te crearia estas paginas dudo que alguien mas lo hiciera funcionar como tu y yo en esta bonita relacion."
              </p>
            </div>
          </div>
        </div>

        <!-- Card 5: Disciplina & Gym -->
        <div class="flip-card h-44 cursor-pointer" onclick="handleFlipCard(this, 'chime4')">
          <div class="flip-card-inner relative w-full h-full duration-500 transform-style-3d transition-transform rounded-2xl">
            <!-- Front -->
            <div class="flip-front absolute inset-0 backface-hidden glass-card rounded-2xl p-4 flex flex-col justify-between border border-emerald-500/20 hover:border-emerald-400/50 shadow-lg">
              <!-- Minimalist Vector Dumbbell Icon -->
              <div class="w-10 h-10 rounded-xl bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-emerald-400 shadow-inner">
                <svg class="w-5 h-5 text-emerald-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <path d="m6.5 6.5 11 11"/>
                  <path d="m21 21-1-1"/>
                  <path d="m3 3 1 1"/>
                  <path d="m18 22 4-4"/>
                  <path d="m2 6 4-4"/>
                  <path d="m3 10 7-7"/>
                  <path d="m14 21 7-7"/>
                </svg>
              </div>
              <div>
                <p class="text-[11px] font-semibold text-emerald-400 uppercase tracking-wider">Fuerza & Dedicación</p>
                <h3 class="text-sm font-semibold text-zinc-100 mt-0.5">El Gimnasio</h3>
              </div>
              <span class="text-[10px] text-zinc-400 flex items-center gap-1">
                <i data-lucide="touchpad" class="w-3 h-3"></i> Toca para ver
              </span>
            </div>
            <!-- Back -->
            <div class="flip-back absolute inset-0 backface-hidden rotate-y-180 bg-gradient-to-br from-emerald-950/80 to-zinc-950/90 rounded-2xl p-4 flex flex-col justify-center text-center border border-emerald-500/40">
              <span class="text-2xl mb-1">💪</span>
              <p class="text-xs text-emerald-100 font-medium leading-relaxed">
                "Fuerza para cuidar y proteger a la que de verdad vale la pena."
              </p>
            </div>
          </div>
        </div>

        <!-- Card 6: El Dibujo & Creatividad -->
        <div class="flip-card h-44 cursor-pointer" onclick="handleFlipCard(this, 'chime1')">
          <div class="flip-card-inner relative w-full h-full duration-500 transform-style-3d transition-transform rounded-2xl">
            <!-- Front -->
            <div class="flip-front absolute inset-0 backface-hidden glass-card rounded-2xl p-4 flex flex-col justify-between border border-purple-500/20 hover:border-purple-400/50 shadow-lg">
              <!-- Minimalist Vector Fine Brush / Pen Icon -->
              <div class="w-10 h-10 rounded-xl bg-purple-500/10 border border-purple-500/20 flex items-center justify-center text-purple-400 shadow-inner">
                <svg class="w-5 h-5 text-purple-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <path d="m14 4 6 6-12 12H2v-6L14 4z"/>
                  <path d="m18 8-4-4"/>
                  <circle cx="6" cy="18" r="1" fill="currentColor"/>
                </svg>
              </div>
              <div>
                <p class="text-[11px] font-semibold text-purple-400 uppercase tracking-wider">Detalle por detalle</p>
                <h3 class="text-sm font-semibold text-zinc-100 mt-0.5">Dibujar</h3>
              </div>
              <span class="text-[10px] text-zinc-400 flex items-center gap-1">
                <i data-lucide="touchpad" class="w-3 h-3"></i> Toca para ver
              </span>
            </div>
            <!-- Back -->
            <div class="flip-back absolute inset-0 backface-hidden rotate-y-180 bg-gradient-to-br from-purple-950/80 to-zinc-950/90 rounded-2xl p-4 flex flex-col justify-center text-center border border-purple-500/40">
              <span class="text-2xl mb-1">🖌️</span>
              <p class="text-xs text-purple-100 font-medium leading-relaxed">
                "Aunque no sea el mejor pintor eso es lo hermoso cada inperfeccion es una perfeccion por eso mis dibujos son genuinos como lo que andamos trayendo."
              </p>
            </div>
          </div>
        </div>

        <!-- Card 7: Momentos para pistear -->
        <div class="flip-card col-span-2 sm:col-span-1 h-44 cursor-pointer" onclick="handleFlipCard(this, 'chime2')">
          <div class="flip-card-inner relative w-full h-full duration-500 transform-style-3d transition-transform rounded-2xl">
            <!-- Front -->
            <div class="flip-front absolute inset-0 backface-hidden glass-card rounded-2xl p-4 flex flex-col justify-between border border-pink-500/20 hover:border-pink-400/50 shadow-lg">
              <!-- Minimalist Vector Cocktail Glass Icon -->
              <div class="w-10 h-10 rounded-xl bg-pink-500/10 border border-pink-500/20 flex items-center justify-center text-pink-400 shadow-inner">
                <svg class="w-5 h-5 text-pink-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <path d="m8 22 8 0"/>
                  <path d="m12 15 0 7"/>
                  <path d="M19 3 5 3l7 8.5Z"/>
                </svg>
              </div>
              <div>
                <p class="text-[11px] font-semibold text-pink-400 uppercase tracking-wider">El Brindis</p>
                <h3 class="text-sm font-semibold text-zinc-100 mt-0.5">Momentos para pistear</h3>
              </div>
              <span class="text-[10px] text-zinc-400 flex items-center gap-1">
                <i data-lucide="touchpad" class="w-3 h-3"></i> Toca para ver
              </span>
            </div>
            <!-- Back -->
            <div class="flip-back absolute inset-0 backface-hidden rotate-y-180 bg-gradient-to-br from-pink-950/80 to-zinc-950/90 rounded-2xl p-4 flex flex-col justify-center text-center border border-pink-500/40">
              <span class="text-2xl mb-1">✨</span>
              <p class="text-xs text-pink-100 font-medium leading-relaxed">
                "Y claroo... echarnos unas tragos para relajarnos con las bebidas que hago ufff."
              </p>
            </div>
          </div>
        </div>

      </section>

      <!-- Section 3: The Wax-Sealed Digital Letter -->
      <section class="space-y-4">
        <div class="text-center">
          <span class="text-xs uppercase tracking-widest text-rose-400 font-semibold">De mí para ti</span>
          <h2 class="text-xl font-bold text-white mt-1">Una carta sincera</h2>
        </div>

        <!-- Envelope / Letter Card -->
        <div class="relative rounded-3xl glass-envelope p-6 sm:p-7 shadow-2xl overflow-hidden border border-rose-500/30">
          
          <!-- Background Watermark Glow -->
          <div class="absolute -top-12 -right-12 w-40 h-40 bg-rose-500/15 rounded-full blur-3xl pointer-events-none"></div>
          
          <!-- Header of the letter with Coraline Key badge -->
          <div class="border-b border-white/10 pb-4 mb-5 flex items-center justify-between">
            <div>
              <p class="font-script text-3xl text-rose-300">Para Citlali,</p>
              <p class="text-[11px] text-zinc-400 mt-0.5 flex items-center gap-1.5">
                <span>🗝️</span> Con dedicación real
              </p>
            </div>
            <div class="w-10 h-10 rounded-full bg-rose-500/20 border border-rose-400/40 flex items-center justify-center text-rose-300 shadow-inner">
              <i data-lucide="heart" class="w-5 h-5 fill-rose-500/40"></i>
            </div>
          </div>

          <!-- Body Text -->
          <div class="space-y-4 text-zinc-300 text-sm leading-relaxed font-light">
            <p>
              La verdad es que si, <strong class="text-rose-200 font-medium">soy una cajita de sorpresas</strong>. Como ya te vas dando cuenta, le entro a todo: me gusta cocinar, Tocar guitarra, dibujar, darle al Gym, meterme a la Investigacion y desvelarme las noches programando y claro, echarme un buen trago de vez en cuando, ¿por qué no? si es mejor contigo a tu lado.
            </p>

            <!-- Highlighted Quote Block -->
            <div class="my-3 p-3.5 rounded-xl bg-gradient-to-r from-rose-950/40 to-purple-950/40 border-l-2 border-rose-500 text-zinc-200 text-xs sm:text-sm italic">
              "Pero hay algo que todavía no te había dicho con todas estas letras, aunque algo me dice que ya lo sabes: <span class="text-rose-300 font-semibold">tengo mis metas bien claras... tan claras como para querer integrarte en ellas💕</span>"
            </div>

            <p>
              Dicen que las cosas que se hacen con cariño siempre se notan, y créeme que todo lo que hago por ti lleva justo a eso😘
            </p>

            <!-- Coraline poetic detail -->
            <div class="pt-1 text-[13px] text-indigo-200 font-medium italic flex items-center gap-1.5">
              <span>🗝️</span>
              <span>Tú eres mi mundo favorito.</span>
            </div>

            <p class="pt-3 text-rose-200 font-medium font-script text-2xl text-right">
              Y esto es para mi Citla Bonita y Hermosa...
            </p>
          </div>

        </div>
      </section>

      <!-- Section 4: The Proposal / Ask Out -->
      <section class="relative rounded-3xl p-7 text-center overflow-hidden border border-rose-500/30 bg-gradient-to-b from-[#131024]/90 via-[#0a0814]/95 to-[#04040a] shadow-[0_0_50px_rgba(244,63,94,0.25)]">
        
        <!-- Animated pulsing ambient aura -->
        <div class="absolute -top-16 -left-16 w-48 h-48 bg-rose-500/25 rounded-full blur-3xl pointer-events-none animate-pulse"></div>
        <div class="absolute -bottom-16 -right-16 w-48 h-48 bg-indigo-500/25 rounded-full blur-3xl pointer-events-none animate-pulse" style="animation-delay: 1.5s;"></div>

        <!-- Stylized Minimalist Heart & Key Icon Badge -->
        <div class="relative w-14 h-14 mx-auto rounded-2xl bg-gradient-to-br from-rose-500/20 via-purple-500/20 to-indigo-500/20 border border-rose-400/50 flex items-center justify-center text-rose-300 mb-4 shadow-[0_0_25px_rgba(244,63,94,0.4)]">
          <svg class="w-7 h-7 text-rose-400 animate-pulse" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
          </svg>
        </div>

        <h3 class="text-2xl sm:text-3xl font-extrabold tracking-tight bg-gradient-to-r from-rose-200 via-pink-200 to-indigo-200 bg-clip-text text-transparent mb-2 font-serif drop-shadow-[0_2px_15px_rgba(244,63,94,0.4)]">
          ¿Quieres ser mi novia?
        </h3>
        
        <p class="text-xs text-zinc-300/90 mb-7 max-w-xs mx-auto leading-relaxed font-light">
          (Aunque posiblemente ya te lo haya dicho en persona el día en que veas esto, aún así quiero preguntártelo por aquí también ❤️)
        </p>

        <!-- Buttons Container (With runaway "No" button) -->
        <div id="btnContainer" class="relative min-h-[95px] flex items-center justify-center gap-4">
          
          <!-- YES Button with high-energy pulsing glow -->
          <button id="yesBtn" onclick="handleYesClick()" class="relative px-8 py-3.5 rounded-2xl bg-gradient-to-r from-rose-600 via-pink-600 to-indigo-600 hover:from-rose-500 hover:to-indigo-500 text-white font-semibold text-sm shadow-[0_0_30px_rgba(244,63,94,0.65)] hover:shadow-[0_0_45px_rgba(236,72,153,0.85)] active:scale-95 transition-all duration-300 flex items-center gap-2.5 z-10 border border-white/20">
            <span>¡Sí, obvio!</span>
            <svg class="w-4 h-4 fill-white" viewBox="0 0 24 24">
              <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
            </svg>
          </button>

          <!-- NO Button (Dodging Button) -->
          <button id="noBtn" onmouseover="dodgeButton()" onclick="dodgeButton()" class="px-6 py-3 rounded-2xl bg-zinc-900/90 hover:bg-zinc-800 text-zinc-400 font-medium text-sm border border-zinc-700/60 transition-transform duration-200 select-none touch-none shadow-inner">
            No 🙈
          </button>

        </div>

        <!-- Success Modal / Coraline Themed Celebration Box -->
        <div id="successBox" class="hidden mt-6 p-7 rounded-3xl bg-gradient-to-b from-[#14122b] via-[#0d0a1d] to-[#040409] border-2 border-indigo-500/50 text-center relative overflow-hidden shadow-[0_0_50px_rgba(99,102,241,0.5)] animate-fade-in">
          
          <!-- Mystical Portal Background Swirl with enhanced brightness -->
          <div class="absolute -top-12 -right-12 w-52 h-52 rounded-full bg-indigo-600/30 blur-3xl pointer-events-none"></div>
          <div class="absolute -bottom-12 -left-12 w-52 h-52 rounded-full bg-rose-500/25 blur-3xl pointer-events-none"></div>

          <!-- Stitched Button & Key Badge with glowing halo -->
          <div class="relative flex items-center justify-center gap-3.5 mb-4">
            <!-- Coraline Small Stitched Button -->
            <div class="w-13 h-13 rounded-full black-button-eye border border-indigo-400/60 p-1 flex items-center justify-center shadow-lg relative">
              <div class="grid grid-cols-2 gap-1.5 z-10">
                <div class="w-1.5 h-1.5 rounded-full bg-[#050508] border border-white/20"></div>
                <div class="w-1.5 h-1.5 rounded-full bg-[#050508] border border-white/20"></div>
                <div class="w-1.5 h-1.5 rounded-full bg-[#050508] border border-white/20"></div>
                <div class="w-1.5 h-1.5 rounded-full bg-[#050508] border border-white/20"></div>
              </div>
              <svg class="absolute inset-0 w-full h-full pointer-events-none" viewBox="0 0 100 100">
                <line x1="38" y1="38" x2="62" y2="62" stroke="#a855f7" stroke-width="3" stroke-linecap="round" />
                <line x1="62" y1="38" x2="38" y2="62" stroke="#06b6d4" stroke-width="3" stroke-linecap="round" />
              </svg>
            </div>

            <!-- The Skeleton Key with Ribbon -->
            <div class="w-13 h-13 rounded-2xl bg-indigo-500/20 border border-indigo-400/50 flex items-center justify-center text-2xl shadow-inner animate-bounce">
              🗝️
            </div>

            <!-- Heart Badge -->
            <div class="w-13 h-13 rounded-full bg-rose-500/25 border border-rose-400/50 flex items-center justify-center text-rose-300 text-xl shadow-lg">
              🖤
            </div>
          </div>

          <span class="inline-block px-3.5 py-1 rounded-full text-[10px] tracking-widest font-mono uppercase bg-indigo-500/25 text-indigo-300 border border-indigo-500/40 mb-2.5">
            🗝️ Bienvenido a Nuestro Mundo
          </span>

          <h4 class="text-xl font-bold text-white font-serif tracking-tight drop-shadow-[0_2px_10px_rgba(255,255,255,0.2)]">
            ¡Bienvenida a nuestro propio mundo!
          </h4>
          
          <p class="text-xs text-indigo-200 mt-2 leading-relaxed px-1 font-light">
            Sin botones en los ojos, sin trampas de la Otra Madre... solo nosotros dos. Oficialmente eres mi novia y mi niña favorita. 🖤
          </p>

          <!-- Quote Block -->
          <div class="my-4 p-3.5 rounded-xl bg-indigo-950/50 border border-indigo-500/40 text-indigo-100 text-xs italic">
            "De todos los mundos posibles detrás de la puerta secreta, me quedo en este contigo para siempre." ✨
          </div>

          <!-- The main requested celebration phrase highlighted with an energetic aura -->
          <div class="mt-2 py-2 px-3 rounded-2xl bg-gradient-to-r from-rose-950/60 via-purple-950/60 to-indigo-950/60 border border-rose-400/50 shadow-[0_0_25px_rgba(244,63,94,0.35)] flex items-center justify-center gap-2 text-sm font-bold text-rose-200">
            <span>Ya estás 100% enamorada conmigo</span>
            <span>🗝️✨</span>
          </div>

        </div>

      </section>

    </main>

  </div>

  <script>
    // Initialize Lucide Icons
    lucide.createIcons();

    // ==========================================
    // 1. Web Audio API Ambient Synthesizer
    // ==========================================
    let audioCtx = null;
    let isMuted = true;
    let synthInterval = null;

    function initAudio() {
      if (!audioCtx) {
        const AudioContext = window.AudioContext || window.webkitAudioContext;
        audioCtx = new AudioContext();
      }
      if (audioCtx.state === 'suspended') {
        audioCtx.resume();
      }
    }

    // Play a gentle bell/chime note
    function playNote(freq, duration = 1.2, type = 'sine', volume = 0.15) {
      if (isMuted || !audioCtx) return;
      try {
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();

        osc.type = type;
        osc.frequency.setValueAtTime(freq, audioCtx.currentTime);

        gain.gain.setValueAtTime(0.001, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(volume, audioCtx.currentTime + 0.05);
        gain.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + duration);

        osc.connect(gain);
        gain.connect(audioCtx.destination);

        osc.start();
        osc.stop(audioCtx.currentTime + duration);
      } catch (e) {
        console.error(e);
      }
    }

    // Chime chords for card flipping
    const chimePresets = {
      chime1: [523.25, 659.25, 783.99], // C5 Major
      chime2: [587.33, 739.99, 880.00], // D5 Major
      chime3: [659.25, 830.61, 987.77], // E5
      chime4: [698.46, 880.00, 1046.50]  // F5
    };

    function playChord(chordKey) {
      if (isMuted) return;
      initAudio();
      const notes = chimePresets[chordKey] || chimePresets.chime1;
      notes.forEach((freq, idx) => {
        setTimeout(() => {
          playNote(freq, 1.4, 'triangle', 0.12);
        }, idx * 70);
      });
    }

    // Ambient dream sequence
    function startAmbientLofi() {
      if (synthInterval) clearInterval(synthInterval);
      const chordProgression = [
        [329.63, 392.00, 493.88], // Em
        [261.63, 329.63, 392.00], // C
        [349.23, 440.00, 523.25], // F
        [392.00, 493.88, 587.33]  // G
      ];
      let step = 0;
      synthInterval = setInterval(() => {
        if (!isMuted && audioCtx) {
          const chord = chordProgression[step % chordProgression.length];
          chord.forEach((n, i) => {
            setTimeout(() => playNote(n * 0.5, 2.8, 'sine', 0.04), i * 140);
          });
          step++;
        }
      }, 3500);
    }

    function toggleAudio() {
      initAudio();
      isMuted = !isMuted;
      const icon = document.getElementById('soundIcon');
      if (isMuted) {
        icon.setAttribute('data-lucide', 'volume-x');
      } else {
        icon.setAttribute('data-lucide', 'volume-2');
        playChord('chime1');
        startAmbientLofi();
      }
      lucide.createIcons();
    }

    // ==========================================
    // 2. Interactive Canvas Particles & Hearts
    // ==========================================
    const canvas = document.getElementById('interactiveCanvas');
    const ctx = canvas.getContext('2d');
    let width, height;
    let particles = [];
    let touchHearts = [];

    function resizeCanvas() {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    }

    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    class Particle {
      constructor() {
        this.x = Math.random() * width;
        this.y = Math.random() * height;
        this.size = Math.random() * 2 + 0.5;
        this.speedX = (Math.random() - 0.5) * 0.4;
        this.speedY = (Math.random() - 0.5) * 0.4;
        this.alpha = Math.random() * 0.5 + 0.1;
      }
      update() {
        this.x += this.speedX;
        this.y += this.speedY;
        if (this.x < 0) this.x = width;
        if (this.x > width) this.x = 0;
        if (this.y < 0) this.y = height;
        if (this.y > height) this.y = 0;
      }
      draw() {
        ctx.fillStyle = `rgba(244, 114, 182, ${this.alpha})`;
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
        ctx.fill();
      }
    }

    // Init background stars
    for (let i = 0; i < 40; i++) {
      particles.push(new Particle());
    }

    class FloatingHeart {
      constructor(x, y) {
        this.x = x;
        this.y = y;
        this.size = Math.random() * 14 + 10;
        this.speedY = -(Math.random() * 2 + 1.2);
        this.speedX = (Math.random() - 0.5) * 1.5;
        this.alpha = 1;
        this.decay = Math.random() * 0.02 + 0.015;
        // Coraline themed symbols: Key, Button, Sparkle, Heart
        const symbols = ['💖', '🗝️', '🔘', '✨', '🖤'];
        this.symbol = symbols[Math.floor(Math.random() * symbols.length)];
      }
      update() {
        this.y += this.speedY;
        this.x += this.speedX;
        this.alpha -= this.decay;
      }
      draw() {
        ctx.save();
        ctx.globalAlpha = Math.max(0, this.alpha);
        ctx.font = `${this.size}px serif`;
        ctx.fillText(this.symbol, this.x, this.y);
        ctx.restore();
      }
    }

    function addHeartTouch(x, y) {
      for (let i = 0; i < 3; i++) {
        touchHearts.push(new FloatingHeart(x + (Math.random() * 20 - 10), y + (Math.random() * 20 - 10)));
      }
    }

    // Touch & Click listeners for particles
    window.addEventListener('click', (e) => {
      addHeartTouch(e.clientX, e.clientY);
      if (!isMuted) {
        playNote(880 + Math.random() * 200, 0.4, 'sine', 0.05);
      }
    });

    window.addEventListener('touchstart', (e) => {
      if (e.touches.length > 0) {
        addHeartTouch(e.touches[0].clientX, e.touches[0].clientY);
      }
    }, { passive: true });

    function renderCanvas() {
      ctx.clearRect(0, 0, width, height);

      // Draw background particles
      for (let i = 0; i < particles.length; i++) {
        particles[i].update();
        particles[i].draw();
      }

      // Draw interactive touch hearts
      for (let i = touchHearts.length - 1; i >= 0; i--) {
        touchHearts[i].update();
        touchHearts[i].draw();
        if (touchHearts[i].alpha <= 0) {
          touchHearts.splice(i, 1);
        }
      }

      requestAnimationFrame(renderCanvas);
    }
    renderCanvas();

    // ==========================================
    // 3. Reveal Experience Flow (Coraline Door)
    // ==========================================
    let doorOpened = false;

    function unlockSecretDoor() {
      if (doorOpened) return;
      doorOpened = true;

      initAudio();
      if (isMuted) {
        toggleAudio(); // Start sound & chords
      }

      // First: Turn the key with animation & subtle glow
      const keyObj = document.getElementById('doorKeyObj');
      if (keyObj) {
        keyObj.style.transform = 'rotate(-90deg) scale(1.15)';
        keyObj.style.filter = 'drop-shadow(0 0 10px rgba(6, 182, 212, 0.9))';
      }

      // Sound sequence for key click & mystical portal opening
      if (audioCtx && !isMuted) {
        playNote(480, 0.35, 'triangle', 0.2);
        setTimeout(() => {
          [440, 554.37, 659.25, 880, 1046.5, 1318.51].forEach((f, i) => {
            setTimeout(() => playNote(f, 1.5, 'sine', 0.16), i * 80);
          });
        }, 180);
      }

      // Second: Open door smoothly & illuminate portal
      setTimeout(() => {
        const doorLeaf = document.getElementById('secretDoorLeaf');
        const portalGlow = document.getElementById('doorPortalGlow');
        const tunnelVortex = document.getElementById('tunnelVortex');
        const container = document.getElementById('doorPortalContainer');

        doorLeaf.classList.add('door-opened');
        
        if (portalGlow) {
          portalGlow.classList.remove('via-purple-500/0');
          portalGlow.classList.add('via-purple-500/50', 'from-indigo-500/40', 'to-cyan-400/40');
        }

        if (tunnelVortex) {
          tunnelVortex.style.filter = 'brightness(1.35) drop-shadow(0 0 20px rgba(129, 140, 248, 0.8))';
        }

        // Spawn Coraline symbols directly emanating from the door center
        const doorRect = container.getBoundingClientRect();
        const doorCenterX = doorRect.left + doorRect.width / 2;
        const doorCenterY = doorRect.top + doorRect.height / 2;

        for (let i = 0; i < 18; i++) {
          setTimeout(() => {
            touchHearts.push(new FloatingHeart(
              doorCenterX + (Math.random() * 40 - 20),
              doorCenterY + (Math.random() * 40 - 20)
            ));
          }, i * 35);
        }

        if (navigator.vibrate) {
          navigator.vibrate([40, 60, 40]);
        }

        // Soft stardust confetti bursting forward
        confetti({
          particleCount: 40,
          spread: 75,
          origin: {
            x: doorCenterX / window.innerWidth,
            y: doorCenterY / window.innerHeight
          },
          colors: ['#818cf8', '#c084fc', '#38bdf8', '#f472b6', '#ffffff'],
          ticks: 180
        });

        // Third: Camera dive-in / absorption zoom into the tunnel
        setTimeout(() => {
          container.classList.add('tunnel-dive-zoom');
          document.getElementById('coverSection').classList.add('opacity-0', 'transition-opacity', 'duration-700');
        }, 550);

        // Transition to main content smoothly
        setTimeout(() => {
          revealContent();
        }, 1400);

      }, 240);
    }

    function revealContent() {
      const cover = document.getElementById('coverSection');
      const main = document.getElementById('mainContent');

      cover.classList.add('opacity-0', '-translate-y-8');
      
      setTimeout(() => {
        cover.style.display = 'none';
        main.classList.remove('hidden');
        requestAnimationFrame(() => {
          main.classList.remove('opacity-0');
          main.classList.add('opacity-100');
        });
      }, 500);
    }

    // ==========================================
    // 4. Flip Card Interaction
    // ==========================================
    function handleFlipCard(cardEl, soundPreset) {
      const inner = cardEl.querySelector('.flip-card-inner');
      inner.classList.toggle('rotate-y-180');
      playChord(soundPreset || 'chime1');

      // Small haptic vibration for mobile if supported
      if (navigator.vibrate) {
        navigator.vibrate(25);
      }
    }

    // ==========================================
    // 5. Playful Dodging "No" Button
    // ==========================================
    function dodgeButton() {
      const btn = document.getElementById('noBtn');
      
      // Calculate random translation offset within bounds
      const randomX = (Math.random() - 0.5) * 160;
      const randomY = (Math.random() - 0.5) * 80;

      btn.style.transform = `translate(${randomX}px, ${randomY}px)`;

      if (!isMuted) {
        playNote(300 + Math.random() * 150, 0.2, 'triangle', 0.1);
      }

      if (navigator.vibrate) {
        navigator.vibrate([15, 30, 15]);
      }
    }

    // ==========================================
    // 6. Handle "YES" Acceptance
    // ==========================================
    // 6. Handle "YES" Acceptance (Coraline Celebration)
    // ==========================================
    function handleYesClick() {
      const successBox = document.getElementById('successBox');
      const btnContainer = document.getElementById('btnContainer');

      successBox.classList.remove('hidden');
      btnContainer.classList.add('pointer-events-none', 'opacity-40');

      // Coraline Music-Box Melody via Web Audio API (Lofi/Dreamy sequence)
      if (!isMuted && audioCtx) {
        // Melodic music box notes (dreamy Coraline vibe)
        const musicBoxNotes = [587.33, 659.25, 783.99, 880.00, 1046.50, 880.00, 783.99, 1174.66];
        musicBoxNotes.forEach((freq, i) => {
          setTimeout(() => {
            playNote(freq, 1.4, 'triangle', 0.16);
          }, i * 160);
        });
      }

      // Add special Coraline symbols burst to interactive canvas
      const centerX = window.innerWidth / 2;
      const centerY = window.innerHeight * 0.65;
      for (let i = 0; i < 24; i++) {
        touchHearts.push(new FloatingHeart(centerX + (Math.random() * 140 - 70), centerY + (Math.random() * 80 - 40)));
      }

      // Grand Confetti Blast (Indigo, Deep Violet, Cyber Cyan, and Rose)
      const duration = 3 * 1000;
      const end = Date.now() + duration;

      (function frame() {
        confetti({
          particleCount: 5,
          angle: 60,
          spread: 60,
          origin: { x: 0 },
          colors: ['#6366f1', '#a855f7', '#06b6d4', '#f43f5e', '#ffffff']
        });
        confetti({
          particleCount: 5,
          angle: 120,
          spread: 60,
          origin: { x: 1 },
          colors: ['#6366f1', '#a855f7', '#06b6d4', '#f43f5e', '#ffffff']
        });

        if (Date.now() < end) {
          requestAnimationFrame(frame);
        }
      }());

      if (navigator.vibrate) {
        navigator.vibrate([100, 50, 100, 50, 150]);
      }

      // Smooth scroll to view celebration card
      successBox.scrollIntoView({ behavior: 'smooth', block: 'center' });
    }
  </script>
</body>
</html>
