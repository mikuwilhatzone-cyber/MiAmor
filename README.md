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
      transition: transform 1.3s cubic-bezier(0.4, 0, 0.2, 1);
      transform-style: preserve-3d;
    }
    .door-opened {
      transform: rotateY(-115deg);
    }
    
    /* Coraline Tunnel Vortex Animation */
    @keyframes vortexSpin {
      0% { transform: rotate(0deg) scale(0.85); opacity: 0.6; }
      50% { transform: rotate(180deg) scale(1.15); opacity: 1; }
      100% { transform: rotate(360deg) scale(0.85); opacity: 0.6; }
    }
    .vortex-swirl {
      animation: vortexSpin 8s linear infinite;
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
        <p class="text-zinc-400 text-xs max-w-xs mx-auto leading-relaxed">
          Detrás de esta pared se esconde algo hecho a tu medida. Usa la llave para abrir la pequeña puerta secreta.
        </p>
      </div>

      <!-- ================= CORALINE 3D SECRET DOOR ================= -->
      <div class="relative w-44 h-60 my-2 coraline-door-frame cursor-pointer select-none" onclick="unlockSecretDoor()">
        
        <!-- Wall/Tunnel Portal Background behind door -->
        <div class="absolute inset-0 rounded-t-full bg-gradient-to-b from-[#090b20] to-[#04040a] border-4 border-[#1f2038] shadow-[0_0_35px_rgba(79,70,229,0.45)] overflow-hidden flex items-center justify-center">
          
          <!-- Swirling Tunnel Vortex (Visible through the open door) -->
          <div id="tunnelVortex" class="absolute w-60 h-60 rounded-full bg-[radial-gradient(circle_at_center,_#818cf8_0%,_#4f46e5_30%,_#312e81_60%,_#05050f_90%)] vortex-swirl opacity-90 blur-[1px]"></div>
          
          <!-- Swirling spiderweb / spiral lines -->
          <svg class="absolute inset-0 w-full h-full opacity-40 mix-blend-screen pointer-events-none" viewBox="0 0 200 300">
            <path d="M100 150 Q130 90 100 30 Q70 90 100 150 Q160 170 180 230 Q120 220 100 150 Q40 210 20 230 Q50 170 100 150" fill="none" stroke="#c7d2fe" stroke-width="1.2" />
          </svg>

          <!-- Floating keyhole hint inside -->
          <span class="relative z-10 text-2xl filter drop-shadow-[0_0_10px_#a5b4fc]">✨</span>
        </div>

        <!-- The Door Leaf (Hinged 3D element) -->
        <div id="secretDoorLeaf" class="coraline-door-leaf absolute inset-0 rounded-t-full bg-gradient-to-b from-[#211d2e] via-[#161424] to-[#0c0b16] border-4 border-[#352f4a] shadow-2xl flex flex-col items-center justify-between p-4 z-20">
          
          <!-- Ornate upper carving -->
          <div class="w-12 h-12 rounded-full border border-purple-400/20 flex items-center justify-center mt-2 bg-black/40">
            <span class="text-xs text-indigo-300">🗝️</span>
          </div>

          <!-- Door Details / Peeling Vintage Wallpaper Vibe -->
          <div class="w-full flex flex-col items-center gap-2">
            <div class="w-24 h-1 bg-white/5 rounded-full"></div>
            <div class="w-16 h-1 bg-white/5 rounded-full"></div>
          </div>

          <!-- Door Handle & Black Keyhole with Key -->
          <div class="w-full flex justify-end pr-3 pb-8 relative">
            <div class="relative flex items-center">
              <!-- Keyhole plate -->
              <div class="w-8 h-12 rounded-lg bg-[#0e0c17] border border-amber-500/30 flex flex-col items-center justify-center shadow-inner">
                <div class="w-2 h-2 rounded-full bg-black shadow-inner"></div>
                <div class="w-1 h-3 bg-black"></div>
              </div>
              <!-- Glowing Button Key Attached -->
              <div class="absolute -right-3 -top-1 animate-pulse">
                <span class="text-2xl filter drop-shadow-[0_0_6px_rgba(244,63,94,0.8)]">🗝️</span>
              </div>
            </div>
          </div>

          <!-- Base Step -->
          <div class="text-[9px] tracking-widest uppercase font-mono text-zinc-500 mb-1">
            SECRET DOOR
          </div>
        </div>

      </div>

      <!-- Action Button / Door Trigger -->
      <button onclick="unlockSecretDoor()" class="group relative mt-4 px-8 py-3.5 rounded-2xl bg-gradient-to-r from-indigo-950 via-purple-900 to-rose-950 hover:from-indigo-900 hover:to-rose-900 border border-indigo-500/40 text-white font-medium text-sm tracking-wide shadow-[0_0_25px_rgba(99,102,241,0.35)] active:scale-95 transition-all duration-300 flex items-center space-x-2.5">
        <span class="text-base">🗝️</span>
        <span>Abrir la puerta secreta</span>
        <i data-lucide="sparkles" class="w-4 h-4 text-indigo-300 group-hover:rotate-12 transition-transform"></i>
      </button>

      <p class="text-[11px] text-zinc-500 mt-4 tracking-wide animate-pulse">
        (Toca la puerta o el botón para cruzar al otro mundo)
      </p>
    </section>

    <!-- ==================== SCREEN 2: MAIN EXPERIENCE ==================== -->
    <main id="mainContent" class="hidden opacity-0 flex-col space-y-12 transition-opacity duration-700 pt-2">
      
      <!-- Section 1: Intro Banner -->
      <div class="text-center pt-2">
        <span class="inline-flex items-center px-3 py-1 rounded-full text-[11px] font-medium bg-rose-500/10 text-rose-300 border border-rose-500/20 mb-3">
          <i data-lucide="sparkle" class="w-3 h-3 mr-1 text-rose-400"></i> Una cajita de sorpresas
        </span>
        <h2 class="text-2xl font-bold text-white tracking-tight">Mis facetas para ti</h2>
        <p class="text-xs text-zinc-400 mt-1 max-w-xs mx-auto">
          Toca cada tarjeta para voltearla y descubrir lo que hay detrás.
        </p>
      </div>

      <!-- Section 2: 3D Flip Card Collage (Facets Grid) -->
      <section class="grid grid-cols-2 gap-3.5 perspective-1000">

        <!-- Card 1: Coraline / La Puerta Secreta (Col-Span-2 for special emphasis) -->
        <div class="flip-card col-span-2 h-44 cursor-pointer" onclick="handleFlipCard(this, 'chime4')">
          <div class="flip-card-inner relative w-full h-full duration-500 transform-style-3d transition-transform rounded-2xl">
            <!-- Front -->
            <div class="flip-front absolute inset-0 backface-hidden glass-card rounded-2xl p-4 flex flex-col justify-between border border-indigo-500/30 hover:border-indigo-400/60 shadow-lg bg-gradient-to-br from-[#0c0d1e]/85 to-[#070712]/90">
              <div class="flex items-center justify-between">
                <div class="w-10 h-10 rounded-xl bg-indigo-500/15 border border-indigo-500/30 flex items-center justify-center text-indigo-300 text-xl shadow-inner">
                  🗝️
                </div>
                <span class="text-[10px] tracking-widest uppercase font-semibold text-indigo-300/80 bg-indigo-500/10 px-2.5 py-0.5 rounded-full border border-indigo-500/20">
                  El Otro Mundo
                </span>
              </div>
              <div>
                <p class="text-[11px] font-semibold text-indigo-400 uppercase tracking-wider">Misterio & Conexión</p>
                <h3 class="text-sm font-semibold text-zinc-100 mt-0.5">Nuestra Puerta Secreta</h3>
              </div>
              <span class="text-[10px] text-zinc-400 flex items-center gap-1">
                <i data-lucide="touchpad" class="w-3 h-3"></i> Toca para descubrir el secreto
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
              <div class="w-10 h-10 rounded-xl bg-rose-500/10 border border-rose-500/20 flex items-center justify-center text-rose-400 text-xl">
                🎸
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
              <div class="w-10 h-10 rounded-xl bg-amber-500/10 border border-amber-500/20 flex items-center justify-center text-amber-400 text-xl">
                🍳
              </div>
              <div>
                <p class="text-[11px] font-semibold text-amber-400 uppercase tracking-wider">El Arte Culinario</p>
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
              <div class="w-10 h-10 rounded-xl bg-cyan-500/10 border border-cyan-500/20 flex items-center justify-center text-cyan-400 text-xl">
                💻
              </div>
              <div>
                <p class="text-[11px] font-semibold text-cyan-400 uppercase tracking-wider">Lógica & Creación</p>
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
              <div class="w-10 h-10 rounded-xl bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-emerald-400 text-xl">
                🏋️‍♂️
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
              <div class="w-10 h-10 rounded-xl bg-purple-500/10 border border-purple-500/20 flex items-center justify-center text-purple-400 text-xl">
                🎨
              </div>
              <div>
                <p class="text-[11px] font-semibold text-purple-400 uppercase tracking-wider">Trazo a Trazo</p>
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

        <!-- Card 7: Brindis & Buena Vibra -->
        <div class="flip-card col-span-2 sm:col-span-1 h-44 cursor-pointer" onclick="handleFlipCard(this, 'chime2')">
          <div class="flip-card-inner relative w-full h-full duration-500 transform-style-3d transition-transform rounded-2xl">
            <!-- Front -->
            <div class="flip-front absolute inset-0 backface-hidden glass-card rounded-2xl p-4 flex flex-col justify-between border border-pink-500/20 hover:border-pink-400/50 shadow-lg">
              <div class="w-10 h-10 rounded-xl bg-pink-500/10 border border-pink-500/20 flex items-center justify-center text-pink-400 text-xl">
                🥂
              </div>
              <div>
                <p class="text-[11px] font-semibold text-pink-400 uppercase tracking-wider">Momentos Chidos</p>
                <h3 class="text-sm font-semibold text-zinc-100 mt-0.5">El Brindis</h3>
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
      <section class="glass-card rounded-3xl p-6 text-center border border-white/10 relative overflow-hidden shadow-2xl">
        <div class="w-12 h-12 mx-auto rounded-2xl bg-rose-500/10 border border-rose-500/30 flex items-center justify-center text-rose-400 mb-3">
          <i data-lucide="heart-handshake" class="w-6 h-6"></i>
        </div>

        <h3 class="text-xl font-bold text-white mb-1.5 font-serif">¿Quieres ser mi novia?</h3>
        <p class="text-xs text-zinc-400 mb-6 max-w-xs mx-auto leading-relaxed">
          (Aunque posiblemente ya te lo haya dicho en persona el día en que veas esto, aún así quiero preguntártelo por aquí también ❤️)
        </p>

        <!-- Buttons Container (With runaway "No" button) -->
        <div id="btnContainer" class="relative min-h-[90px] flex items-center justify-center gap-4">
          
          <!-- YES Button -->
          <button id="yesBtn" onclick="handleYesClick()" class="px-7 py-3 rounded-2xl bg-gradient-to-r from-rose-600 to-pink-600 hover:from-rose-500 hover:to-pink-500 text-white font-semibold text-sm shadow-neon-rose active:scale-95 transition-all flex items-center gap-2">
            <span>¡Sí, obvio!</span>
            <i data-lucide="heart" class="w-4 h-4 fill-white"></i>
          </button>

          <!-- NO Button (Dodging Button) -->
          <button id="noBtn" onmouseover="dodgeButton()" onclick="dodgeButton()" class="px-6 py-3 rounded-2xl bg-zinc-800/80 hover:bg-zinc-800 text-zinc-400 font-medium text-sm border border-zinc-700/50 transition-transform duration-200 select-none touch-none">
            No 🙈
          </button>

        </div>

        <!-- Success Modal / Coraline Themed Celebration Box -->
        <div id="successBox" class="hidden mt-6 p-6 rounded-3xl bg-gradient-to-b from-[#121124] via-[#0b0a17] to-[#06060c] border border-indigo-500/40 text-center relative overflow-hidden shadow-[0_0_40px_rgba(99,102,241,0.35)] animate-fade-in">
          
          <!-- Mystical Portal Background Swirl -->
          <div class="absolute -top-10 -right-10 w-44 h-44 rounded-full bg-indigo-600/20 blur-3xl pointer-events-none"></div>
          <div class="absolute -bottom-10 -left-10 w-44 h-44 rounded-full bg-rose-500/15 blur-3xl pointer-events-none"></div>

          <!-- Stitched Button & Key Badge -->
          <div class="relative flex items-center justify-center gap-3 mb-3">
            <!-- Coraline Small Stitched Button -->
            <div class="w-12 h-12 rounded-full black-button-eye border border-indigo-400/50 p-1 flex items-center justify-center shadow-lg relative">
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
            <div class="w-12 h-12 rounded-2xl bg-indigo-500/15 border border-indigo-400/40 flex items-center justify-center text-2xl shadow-inner animate-bounce">
              🗝️
            </div>

            <!-- Heart Badge -->
            <div class="w-12 h-12 rounded-full bg-rose-500/20 border border-rose-400/40 flex items-center justify-center text-rose-300 text-xl shadow-lg">
              🖤
            </div>
          </div>

          <span class="inline-block px-3 py-1 rounded-full text-[10px] tracking-widest font-mono uppercase bg-indigo-500/20 text-indigo-300 border border-indigo-500/30 mb-2">
            🗝️ Bienvenido a Nuestro Mundo
          </span>

          <h4 class="text-lg font-bold text-white font-serif tracking-tight">¡Bienvenida a nuestro propio mundo!</h4>
          
          <p class="text-xs text-indigo-200 mt-2 leading-relaxed px-1 font-light">
            Sin botones en los ojos, sin trampas de la Otra Madre... solo nosotros dos. Oficialmente eres mi novia y mi niña favorita. 🖤
          </p>

          <!-- Quote Block -->
          <div class="my-3.5 p-3 rounded-xl bg-indigo-950/40 border border-indigo-500/30 text-indigo-100 text-xs italic">
            "De todos los mundos posibles detrás de la puerta secreta, me quedo en este contigo para siempre." ✨
          </div>

          <div class="flex items-center justify-center gap-2 text-xs font-semibold text-rose-300">
            <span>Ya estás 100% enamorada conmigo</span>
            <span>🗝️✨</span>
          </div>

        </div>

      </section>

      <!-- Footer Sign -->
      <footer class="text-center pt-4 pb-8 text-zinc-500 text-xs">
        <p>Hecho con código, café y mucho cariño para Citlali</p>
      </footer>

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

      // Play unlocking door creak / mystical chords
      if (audioCtx && !isMuted) {
        [440, 554.37, 659.25, 880, 1108.73].forEach((f, i) => {
          setTimeout(() => playNote(f, 1.2, 'sine', 0.15), i * 110);
        });
      }

      const doorLeaf = document.getElementById('secretDoorLeaf');
      doorLeaf.classList.add('door-opened');

      if (navigator.vibrate) {
        navigator.vibrate([40, 80, 60]);
      }

      // Confetti tunnel burst
      confetti({
        particleCount: 45,
        spread: 80,
        origin: { y: 0.55 },
        colors: ['#818cf8', '#a855f7', '#ec4899', '#38bdf8']
      });

      // After door swing animation, transition to main content
      setTimeout(() => {
        revealContent();
      }, 1100);
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
