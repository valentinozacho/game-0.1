# game-0.1
Spillemaskine 
<!DOCTYPE html>
<html lang="da">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>BananaZ – 10K Ways | Gratis Casino Demo</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@500;600;700&family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --wood-dark: #2a160c;
      --wood-mid: #4a2815;
      --wood-light: #6d3d20;
      --gold-bright: #ffd700;
      --gold-deep: #d97706;
      --jungle-deep: #071c12;
      --jungle-mid: #0f3622;
    }

    * {
      box-sizing: border-box;
      user-select: none;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      margin: 0;
      font-family: 'Inter', sans-serif;
      background: radial-gradient(circle at 50% 15%, #184e32 0%, #0a2417 55%, #04110b 100%);
      color: #fefce8;
      min-height: 100vh;
      overflow-x: hidden;
    }

    .font-display {
      font-family: 'Fredoka', cursive, sans-serif;
    }

    /* Baggrunds-solstråler & jungleatmosfære */
    .sunbeams {
      position: fixed;
      inset: -20%;
      pointer-events: none;
      background: repeating-conic-gradient(
        from 0deg at 50% 0%,
        rgba(253, 224, 71, 0.04) 0deg 10deg,
        transparent 10deg 25deg
      );
      animation: beamSway 18s ease-in-out infinite alternate;
      z-index: 0;
    }

    @keyframes beamSway {
      0% { transform: rotate(-4deg) scale(1.05); }
      100% { transform: rotate(4deg) scale(1.1); }
    }

    /* Udskåret træramme */
    .wood-frame {
      background: linear-gradient(180deg, #5c3219 0%, #3d1f0e 50%, #261207 100%);
      border: 4px solid #854d27;
      box-shadow:
        0 20px 50px rgba(0, 0, 0, 0.75),
        inset 0 2px 4px rgba(255, 215, 0, 0.35),
        inset 0 -4px 10px rgba(0, 0, 0, 0.8);
      position: relative;
    }

    .wood-plaque {
      background: linear-gradient(180deg, #4d2914 0%, #2b1509 100%);
      border: 2px solid #b45309;
      box-shadow: inset 0 1px 2px rgba(254, 240, 138, 0.25), 0 4px 10px rgba(0,0,0,0.5);
    }

    .gold-rim {
      border: 2px solid #f59e0b;
      box-shadow: 0 0 12px rgba(245, 158, 11, 0.35), inset 0 0 8px rgba(253, 224, 71, 0.2);
    }

    /* Spilleplade & Felter */
    .reel-board {
      background: linear-gradient(180deg, #091d13 0%, #0d2b1c 50%, #07170f 100%);
      box-shadow: inset 0 8px 24px rgba(0, 0, 0, 0.85);
    }

    .reel-col {
      background: linear-gradient(180deg, rgba(16, 48, 32, 0.65) 0%, rgba(9, 28, 19, 0.85) 100%);
      border-left: 1px solid rgba(251, 191, 36, 0.14);
      border-right: 1px solid rgba(0, 0, 0, 0.5);
    }

    .top-reel-slot {
      background: linear-gradient(180deg, rgba(45, 24, 12, 0.9) 0%, rgba(23, 12, 6, 0.95) 100%);
      border: 1.5px solid rgba(245, 158, 11, 0.45);
    }

    /* Symbol-celler & Animationer */
    .symbol-cell {
      transition: transform 0.22s cubic-bezier(0.34, 1.56, 0.64, 1), filter 0.2s ease;
      position: relative;
    }

    @keyframes dropIn {
      0% {
        transform: translateY(-130%) scale(0.88);
        opacity: 0.2;
      }
      72% {
        transform: translateY(7%) scale(1.03);
        opacity: 1;
      }
      88% {
        transform: translateY(-3%) scale(0.99);
      }
      100% {
        transform: translateY(0) scale(1);
        opacity: 1;
      }
    }

    .anim-drop {
      animation: dropIn 0.38s cubic-bezier(0.22, 1, 0.36, 1) forwards;
    }

    @keyframes spinBlurPulse {
      0%, 100% { transform: translateY(-4px) scaleY(1.08); filter: blur(1.5px) brightness(1.1); }
      50% { transform: translateY(4px) scaleY(1.12); filter: blur(2.5px) brightness(0.95); }
    }

    .anim-spinning {
      animation: spinBlurPulse 0.12s linear infinite;
    }

    @keyframes winPulse {
      0%, 100% {
        transform: scale(1);
        box-shadow: 0 0 14px rgba(250, 204, 21, 0.85), inset 0 0 12px rgba(250, 204, 21, 0.5);
      }
      50% {
        transform: scale(1.08);
        box-shadow: 0 0 26px rgba(250, 204, 21, 1), inset 0 0 18px rgba(254, 240, 138, 0.8);
      }
    }

    .symbol-win {
      z-index: 15;
      border-radius: 12px;
      background: radial-gradient(circle, rgba(250, 204, 21, 0.32) 0%, rgba(217, 119, 6, 0.12) 70%, transparent 100%);
      outline: 2.5px solid #fde047;
      animation: winPulse 0.65s ease-in-out infinite;
    }

    @keyframes explodeOut {
      0% { transform: scale(1.08); opacity: 1; filter: brightness(1.8); }
      50% { transform: scale(1.32) rotate(8deg); opacity: 0.7; filter: brightness(2.4); }
      100% { transform: scale(0.1) rotate(-15deg); opacity: 0; }
    }

    .symbol-explode {
      animation: explodeOut 0.34s ease-out forwards;
    }

    @keyframes floatUpFade {
      0% { transform: translate(-50%, 10px) scale(0.7); opacity: 0; }
      20% { transform: translate(-50%, -10px) scale(1.15); opacity: 1; }
      80% { transform: translate(-50%, -42px) scale(1); opacity: 1; }
      100% { transform: translate(-50%, -62px) scale(0.95); opacity: 0; }
    }

    .floating-win-pop {
      position: absolute;
      left: 50%;
      top: 45%;
      transform: translate(-50%, -50%);
      pointer-events: none;
      z-index: 40;
      animation: floatUpFade 1.15s cubic-bezier(0.16, 1, 0.3, 1) forwards;
      text-shadow: 0 3px 0 #451a03, 0 0 16px rgba(250, 204, 21, 0.95);
    }

    /* Spin-knap 3D effekt */
    .spin-btn {
      background: radial-gradient(circle at 35% 25%, #4ade80 0%, #16a34a 55%, #14532d 100%);
      border: 4px solid #facc15;
      box-shadow:
        0 8px 0 #052e16,
        0 12px 24px rgba(0, 0, 0, 0.65),
        inset 0 3px 6px rgba(255, 255, 255, 0.45);
      transition: transform 0.1s ease, box-shadow 0.1s ease, filter 0.15s ease;
    }

    .spin-btn:hover:not(:disabled) {
      filter: brightness(1.08);
      transform: translateY(-2px);
    }

    .spin-btn:active:not(:disabled) {
      transform: translateY(4px);
      box-shadow:
        0 3px 0 #052e16,
        0 6px 12px rgba(0, 0, 0, 0.65),
        inset 0 2px 4px rgba(255, 255, 255, 0.35);
    }

    .spin-btn:disabled {
      filter: grayscale(0.45) brightness(0.75);
      cursor: not-allowed;
    }

    .bonus-buy-btn {
      background: linear-gradient(180deg, #fde047 0%, #f59e0b 52%, #b45309 100%);
      border: 2.5px solid #fef08a;
      box-shadow: 0 5px 0 #78350f, 0 8px 18px rgba(0, 0, 0, 0.55);
      transition: transform 0.12s ease, filter 0.15s ease;
    }

    .bonus-buy-btn:hover:not(:disabled) {
      filter: brightness(1.07);
      transform: translateY(-1px);
    }

    .bonus-buy-btn:active:not(:disabled) {
      transform: translateY(3px);
      box-shadow: 0 2px 0 #78350f;
    }

    .bonus-buy-btn:disabled {
      opacity: 0.55;
      cursor: not-allowed;
    }

    /* Ildfluer i baggrunden */
    .firefly {
      position: fixed;
      width: 5px;
      height: 5px;
      border-radius: 50%;
      background: #fde047;
      box-shadow: 0 0 10px #facc15, 0 0 18px #84cc16;
      pointer-events: none;
      opacity: 0;
      z-index: 1;
      animation: fireflyFloat var(--dur, 9s) ease-in-out infinite;
      animation-delay: var(--delay, 0s);
    }

    @keyframes fireflyFloat {
      0%, 100% { transform: translate(0, 0) scale(0.6); opacity: 0; }
      25% { opacity: 0.85; }
      50% { transform: translate(var(--dx, 40px), var(--dy, -60px)) scale(1.2); opacity: 0.4; }
      75% { opacity: 0.9; }
    }

    /* Free Spins gylden glød */
    .freespins-active .wood-frame {
      border-color: #facc15;
      box-shadow:
        0 0 40px rgba(250, 204, 21, 0.45),
        0 20px 50px rgba(0, 0, 0, 0.8),
        inset 0 0 20px rgba(250, 204, 21, 0.3);
    }

    /* Skjul scrollbar pænt */
    ::-webkit-scrollbar { width: 6px; }
    ::-webkit-scrollbar-track { background: #1c0f08; }
    ::-webkit-scrollbar-thumb { background: #92400e; border-radius: 9999px; }
  </style>
</head>
<body class="flex flex-col justify-between min-h-screen relative">

  <!-- Baggrundslys & ildfluer -->
  <div class="sunbeams"></div>
  <div id="fireflies-container"></div>

  <!-- Top HUD-bjælke -->
  <header class="relative z-20 w-full max-w-6xl mx-auto px-3 pt-2.5 pb-1.5 flex flex-wrap items-center justify-between gap-2">
    <div class="flex items-center gap-2">
      <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-extrabold tracking-wide uppercase bg-amber-950/90 border border-amber-400/60 text-amber-200 shadow">
        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
        DEMO-TILSTAND • KUN VIRTUELLE CREDITS
      </span>
      <span class="hidden sm:inline-flex items-center px-2.5 py-1 rounded-full text-xs font-semibold bg-emerald-950/80 border border-emerald-500/40 text-emerald-200">
        4-5-5-5-5-4 • 10.000 WAYS
      </span>
    </div>

    <div class="flex items-center gap-2">
      <button id="btn-sound" type="button" title="Slå lyd til/fra"
        class="wood-plaque px-3 py-1.5 rounded-xl text-xs sm:text-sm font-bold text-amber-100 hover:brightness-110 active:scale-95 transition flex items-center gap-1.5 cursor-pointer">
        <span id="sound-icon">🔊</span>
        <span id="sound-label" class="hidden sm:inline">Lyd: Til</span>
      </button>

      <button id="btn-paytable" type="button" title="Gevinsttabel & Regler"
        class="wood-plaque px-3 py-1.5 rounded-xl text-xs sm:text-sm font-bold text-amber-200 hover:brightness-110 active:scale-95 transition flex items-center gap-1.5 cursor-pointer">
        <span class="inline-flex items-center justify-center w-5 h-5 rounded-full bg-amber-500 text-amber-950 font-black text-xs">i</span>
        <span>Gevinsttabel &amp; Regler</span>
      </button>
    </div>
  </header>

  <!-- Hovedspilleområde -->
  <main class="relative z-10 flex-1 flex flex-col items-center justify-center w-full max-w-6xl mx-auto px-2 sm:px-4 py-1">

    <!-- Titelbanner & Free Spins HUD -->
    <div class="w-full flex flex-col md:flex-row items-center justify-between gap-2 mb-2 px-1">
      <!-- Bonus Buy-knap (venstre på desktop, øverst på mobil) -->
      <div class="order-2 md:order-1 flex items-center gap-2">
        <button id="btn-bonus-buy" type="button"
          class="bonus-buy-btn px-3.5 py-2 rounded-2xl text-amber-950 font-display font-bold flex items-center gap-2.5 cursor-pointer">
          <span class="text-xl leading-none">🍌</span>
          <div class="text-left leading-tight">
            <div class="text-[11px] uppercase tracking-wider font-extrabold text-amber-900">Bonus Buy</div>
            <div class="text-sm sm:text-base font-black" id="bonus-buy-price">1.600,00 kr.</div>
          </div>
        </button>
      </div>

      <!-- Spiltitel i træskilt -->
      <div class="order-1 md:order-2 text-center">
        <div class="inline-block px-5 py-1.5 rounded-2xl wood-plaque gold-rim">
          <h1 class="font-display text-2xl sm:text-3xl md:text-4xl font-bold tracking-tight bg-gradient-to-b from-yellow-200 via-amber-400 to-orange-500 bg-clip-text text-transparent drop-shadow">
            🍌 BananaZ – 10K Ways
          </h1>
        </div>
      </div>

      <!-- Ways / Multiplikator status -->
      <div class="order-3 flex items-center gap-2">
        <div id="ways-badge" class="wood-plaque px-3.5 py-1.5 rounded-2xl text-center min-w-[125px]">
          <div class="text-[10px] uppercase tracking-wider text-amber-300/80 font-bold">Aktive Ways</div>
          <div id="ways-count" class="font-display text-lg sm:text-xl font-bold text-emerald-300">10.000</div>
        </div>

        <div id="multiplier-badge" class="hidden wood-plaque gold-rim px-3.5 py-1.5 rounded-2xl text-center min-w-[115px] bg-gradient-to-b from-amber-800 to-amber-950">
          <div class="text-[10px] uppercase tracking-wider text-yellow-200 font-bold">FS Multiplikator</div>
          <div id="fs-multiplier-val" class="font-display text-lg sm:text-xl font-black text-yellow-300">1x</div>
        </div>
      </div>
    </div>

    <!-- Free Spins Banner (vises kun under gratis spins) -->
    <div id="freespins-banner" class="hidden w-full max-w-3xl mb-2 px-4 py-2 rounded-2xl bg-gradient-to-r from-amber-900/95 via-yellow-700/95 to-amber-900/95 border-2 border-yellow-300 shadow-lg flex items-center justify-between gap-3">
      <div class="flex items-center gap-2">
        <span class="text-2xl">🌴</span>
        <div>
          <div class="font-display font-bold text-yellow-200 text-sm sm:text-base uppercase tracking-wide">BananaZ Free Spins</div>
          <div class="text-xs text-amber-100">Hver kaskade øger gevinstmultiplikatoren med +1!</div>
        </div>
      </div>
      <div class="flex items-center gap-4 text-right">
        <div>
          <div class="text-[10px] uppercase text-yellow-200/80 font-bold">Spins tilbage</div>
          <div id="fs-remaining" class="font-display text-xl font-black text-white">10</div>
        </div>
        <div>
          <div class="text-[10px] uppercase text-yellow-200/80 font-bold">Bonusgevinst</div>
          <div id="fs-total-win" class="font-display text-xl font-black text-emerald-300">0,00 kr.</div>
        </div>
      </div>
    </div>

    <!-- Spillemaskinens Træramme -->
    <div id="machine-frame" class="wood-frame rounded-3xl p-2.5 sm:p-4 w-full max-w-4xl relative">
      <!-- Dekorative jungleblade i hjørnerne (SVG) -->
      <svg class="w-12 h-12 sm:w-16 sm:h-16 absolute -top-4 -left-4 pointer-events-none drop-shadow-lg z-20" viewBox="0 0 64 64">
        <path d="M6 54 C4 26, 24 8, 56 6 C42 22, 34 38, 6 54 Z" fill="#15803d"/>
        <path d="M12 58 C18 34, 34 20, 60 22 C44 32, 30 44, 12 58 Z" fill="#22c55e"/>
        <path d="M8 52 Q30 30 54 8" stroke="#bbf7d0" stroke-width="2" fill="none" opacity="0.6"/>
      </svg>
      <svg class="w-12 h-12 sm:w-16 sm:h-16 absolute -top-4 -right-4 pointer-events-none drop-shadow-lg z-20 scale-x-[-1]" viewBox="0 0 64 64">
        <path d="M6 54 C4 26, 24 8, 56 6 C42 22, 34 38, 6 54 Z" fill="#15803d"/>
        <path d="M12 58 C18 34, 34 20, 60 22 C44 32, 30 44, 12 58 Z" fill="#22c55e"/>
        <path d="M8 52 Q30 30 54 8" stroke="#bbf7d0" stroke-width="2" fill="none" opacity="0.6"/>
      </svg>

      <!-- Øverste vandrette Top Reel over hjul 2, 3, 4 og 5 (giver 4-5-5-5-5-4 = 10.000 Ways) -->
      <div class="grid grid-cols-6 gap-1.5 sm:gap-2 mb-1.5 sm:mb-2 px-0.5">
        <div class="hidden sm:flex items-center justify-center rounded-xl bg-amber-950/50 border border-amber-800/40 text-[11px] font-bold text-amber-300/70 uppercase tracking-wider">
          Hjul 1
        </div>
        <div class="sm:hidden"></div>

        <!-- Top Reel 4 felter (hjul 2,3,4,5) -->
        <div id="top-reel-1" class="top-reel-slot rounded-xl h-14 sm:h-16 md:h-20 flex items-center justify-center p-1 overflow-hidden"></div>
        <div id="top-reel-2" class="top-reel-slot rounded-xl h-14 sm:h-16 md:h-20 flex items-center justify-center p-1 overflow-hidden"></div>
        <div id="top-reel-3" class="top-reel-slot rounded-xl h-14 sm:h-16 md:h-20 flex items-center justify-center p-1 overflow-hidden"></div>
        <div id="top-reel-4" class="top-reel-slot rounded-xl h-14 sm:h-16 md:h-20 flex items-center justify-center p-1 overflow-hidden"></div>

        <div class="hidden sm:flex items-center justify-center rounded-xl bg-amber-950/50 border border-amber-800/40 text-[11px] font-bold text-amber-300/70 uppercase tracking-wider">
          Hjul 6
        </div>
        <div class="sm:hidden"></div>
      </div>

      <!-- Hovedgitter: 6 hjul x 4 rækker -->
      <div id="reels-wrapper" class="reel-board rounded-2xl p-1.5 sm:p-2.5 border-2 border-amber-700/70 relative overflow-hidden">
        <!-- SVG-lag til gevinstlinjer -->
        <svg id="win-lines-svg" class="absolute inset-0 w-full h-full pointer-events-none z-20"></svg>

        <!-- Container til flyvende gevinst-popups & partikler -->
        <div id="effects-layer" class="absolute inset-0 pointer-events-none z-30 overflow-hidden"></div>

        <!-- 6 kolonner -->
        <div id="reels-grid" class="grid grid-cols-6 gap-1.5 sm:gap-2 relative z-10">
          <!-- Genereres dynamisk i JS -->
        </div>
      </div>

      <!-- Status / Kaskade-beskedlinje under hjulene -->
      <div class="mt-2 flex items-center justify-between px-2 text-xs sm:text-sm">
        <div id="status-banner" class="font-semibold text-amber-200 truncate">
          Klar til spin! Tryk på SPIN eller brug mellemrumstasten.
        </div>
        <div id="cascade-badge" class="hidden px-2.5 py-0.5 rounded-full bg-emerald-600/90 text-white font-bold text-xs shadow">
          Kaskade x1
        </div>
      </div>
    </div>

    <!-- Kontrolpanel i udskåret træ -->
    <div class="wood-frame rounded-3xl p-3 sm:p-4 w-full max-w-4xl mt-2.5 flex flex-col md:flex-row items-center justify-between gap-3">

      <!-- Saldo & Indsats -->
      <div class="flex flex-wrap items-center justify-center sm:justify-start gap-2.5 sm:gap-3 w-full md:w-auto">
        <!-- Saldo -->
        <div class="wood-plaque rounded-2xl px-3.5 py-2 min-w-[140px] flex-1 sm:flex-initial">
          <div class="text-[10px] uppercase tracking-wider text-amber-300/80 font-bold">Saldo (Credits)</div>
          <div id="balance-display" class="font-display text-lg sm:text-xl font-bold text-white">10.000,00 kr.</div>
        </div>

        <!-- Samlet Indsats -->
        <div class="wood-plaque rounded-2xl px-2.5 py-1.5 flex items-center gap-2 flex-1 sm:flex-initial justify-between">
          <button id="btn-bet-minus" type="button" aria-label="Sænk indsats"
            class="w-9 h-9 rounded-xl bg-amber-800 hover:bg-amber-700 active:scale-95 border border-amber-400/50 text-amber-100 font-black text-lg flex items-center justify-center cursor-pointer">
            −
          </button>
          <div class="text-center px-1">
            <div class="text-[10px] uppercase tracking-wider text-amber-300/80 font-bold">Samlet Indsats</div>
            <div id="bet-display" class="font-display text-base sm:text-lg font-bold text-amber-200">20,00 kr.</div>
          </div>
          <button id="btn-bet-plus" type="button" aria-label="Øg indsats"
            class="w-9 h-9 rounded-xl bg-amber-800 hover:bg-amber-700 active:scale-95 border border-amber-400/50 text-amber-100 font-black text-lg flex items-center justify-center cursor-pointer">
            +
          </button>
        </div>
      </div>

      <!-- Gevinst-display -->
      <div class="wood-plaque gold-rim rounded-2xl px-4 py-2 text-center w-full md:w-auto min-w-[175px]">
        <div class="text-[10px] uppercase tracking-wider text-yellow-300 font-bold">Gevinst</div>
        <div id="win-display" class="font-display text-xl sm:text-2xl font-black text-emerald-300">0,00 kr.</div>
      </div>

      <!-- Auto-Spin & Stor Spin-knap -->
      <div class="flex items-center justify-center gap-3 w-full md:w-auto">
        <button id="btn-autospin" type="button"
          class="wood-plaque px-3.5 py-3 rounded-2xl text-xs sm:text-sm font-bold text-amber-100 hover:brightness-110 active:scale-95 transition flex flex-col items-center justify-center min-w-[84px] cursor-pointer">
          <span id="autospin-icon" class="text-base leading-none mb-0.5">🔄</span>
          <span id="autospin-label">Auto: Fra</span>
        </button>

        <button id="btn-spin" type="button"
          class="spin-btn w-24 h-16 sm:w-28 sm:h-18 rounded-3xl flex flex-col items-center justify-center text-white font-display cursor-pointer">
          <span class="text-xl sm:text-2xl font-black tracking-wide drop-shadow">SPIN</span>
          <span class="text-[10px] uppercase tracking-widest text-emerald-100 font-bold -mt-1">10K Ways</span>
        </button>
      </div>
    </div>
  </main>

  <!-- Diskret ansvarsfraskrivelse i bunden -->
  <footer class="relative z-10 w-full max-w-5xl mx-auto px-4 py-2.5 text-center">
    <p class="text-[11px] sm:text-xs text-emerald-200/70 leading-relaxed">
      Gratis prototype-demo med virtuelle credits – ingen rigtige penge eller indbetalinger. Spillet anvender sin egen definerede demomatematik og er ikke en certificeret casino-spillemaskine.
    </p>
  </footer>

  <!-- =========================================================
       MODALER & OVERLAYS (Stor gevinst, Free Spins, Bonus Buy, Regler)
       ========================================================= -->

  <!-- Stor Gevinst / Mega Gevinst Fejringsoverlay -->
  <div id="bigwin-overlay" class="hidden fixed inset-0 z-50 bg-black/75 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="wood-frame gold-rim rounded-3xl p-6 sm:p-8 max-w-md w-full text-center relative overflow-hidden transform transition-all scale-100">
      <div class="text-5xl sm:text-6xl mb-2 animate-bounce">🍌👑🍌</div>
      <div id="bigwin-title" class="font-display text-3xl sm:text-5xl font-black uppercase bg-gradient-to-b from-yellow-200 via-amber-400 to-orange-500 bg-clip-text text-transparent drop-shadow">
        STOR GEVINST!
      </div>
      <div id="bigwin-amount" class="font-display text-3xl sm:text-4xl font-black text-emerald-300 mt-3 mb-5">
        0,00 kr.
      </div>
      <button id="btn-close-bigwin" type="button"
        class="bonus-buy-btn px-6 py-2.5 rounded-2xl font-display font-bold text-amber-950 text-base cursor-pointer">
        Fortsæt spil
      </button>
    </div>
  </div>

  <!-- Free Spins Intro / Outro Modal -->
  <div id="freespins-modal" class="hidden fixed inset-0 z-50 bg-black/80 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="wood-frame gold-rim rounded-3xl p-6 sm:p-8 max-w-md w-full text-center">
      <div class="text-5xl mb-2">🌴🍌🎉</div>
      <h2 id="fs-modal-title" class="font-display text-2xl sm:text-3xl font-black text-yellow-300 uppercase">
        BananaZ Free Spins!
      </h2>
      <p id="fs-modal-desc" class="text-sm sm:text-base text-amber-100 mt-2 mb-5 leading-relaxed">
        Du har udløst 10 gratis spins! Under hele bonusrunden stiger gevinstmultiplikatoren med +1 for hver kaskadegevinst.
      </p>
      <button id="btn-fs-modal-ok" type="button"
        class="spin-btn px-8 py-3 rounded-2xl font-display font-black text-white text-lg cursor-pointer">
        Start Free Spins
      </button>
    </div>
  </div>

  <!-- Bonus Buy Bekræftelsesmodal -->
  <div id="bonusbuy-modal" class="hidden fixed inset-0 z-50 bg-black/80 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="wood-frame gold-rim rounded-3xl p-6 max-w-md w-full text-center">
      <div class="text-4xl mb-2">🍌⚡</div>
      <h2 class="font-display text-2xl font-black text-yellow-300">Køb BananaZ Free Spins</h2>
      <p class="text-sm text-amber-100 mt-2 leading-relaxed">
        Garanterer mindst 4 Scatter-symboler på næste spin og starter straks 10 Free Spins med stigende multiplikator.
      </p>
      <div class="wood-plaque rounded-2xl p-3 my-4">
        <div class="text-xs uppercase text-amber-300 font-bold">Pris (80x samlet indsats)</div>
        <div id="modal-buy-cost" class="font-display text-2xl font-black text-yellow-300 mt-0.5">1.600,00 kr.</div>
      </div>
      <div class="flex items-center justify-center gap-3">
        <button id="btn-cancel-buy" type="button"
          class="wood-plaque px-5 py-2.5 rounded-2xl font-bold text-amber-200 hover:brightness-110 cursor-pointer">
          Annuller
        </button>
        <button id="btn-confirm-buy" type="button"
          class="bonus-buy-btn px-6 py-2.5 rounded-2xl font-display font-bold text-amber-950 cursor-pointer">
          Køb Bonus Nu
        </button>
      </div>
    </div>
  </div>

  <!-- Gevinsttabel & Regler Modal -->
  <div id="paytable-modal" class="hidden fixed inset-0 z-50 bg-black/80 backdrop-blur-sm flex items-center justify-center p-3 sm:p-6">
    <div class="wood-frame gold-rim rounded-3xl p-5 sm:p-6 max-w-3xl w-full max-h-[88vh] overflow-y-auto">
      <div class="flex items-center justify-between border-b border-amber-700/70 pb-3 mb-4">
        <h2 class="font-display text-xl sm:text-2xl font-black text-yellow-300">
          🍌 Gevinsttabel &amp; Spilleregler
        </h2>
        <button id="btn-close-paytable" type="button"
          class="w-9 h-9 rounded-xl bg-amber-900 hover:bg-amber-800 text-amber-100 font-black text-lg flex items-center justify-center cursor-pointer">
          ✕
        </button>
      </div>

      <!-- Regelsektion -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-3 mb-5 text-xs sm:text-sm text-amber-100">
        <div class="wood-plaque rounded-2xl p-3.5">
          <h3 class="font-display font-bold text-yellow-300 text-base mb-1">10.000 Ways &amp; Kaskader</h3>
          <p class="leading-relaxed">
            Spillepladen har 6 hjul i opsætningen <strong>4-5-5-5-5-4</strong> (inkl. den øverste vandrette række over hjul 2–5), hvilket giver op til <strong>10.000 gevinstveje</strong>. Ens symboler på tilstødende hjul fra venstre mod højre (hjul 1 og frem) giver gevinst. Vindende symboler eksploderer, og nye falder ned i samme spin.
          </p>
        </div>
        <div class="wood-plaque rounded-2xl p-3.5">
          <h3 class="font-display font-bold text-yellow-300 text-base mb-1">Wild, Scatter &amp; Free Spins</h3>
          <p class="leading-relaxed">
            <strong>Banana Wild</strong> lander på hjul 2, 3, 4 og 5 (inkl. top-rækken) og erstatter alle normale symboler. <strong>4 eller flere Scatter-mønter</strong> udløser <strong>10 Free Spins</strong> (+2 pr. ekstra Scatter) med en ubegrænset gevinstmultiplikator, der stiger med +1 pr. kaskade.
          </p>
        </div>
      </div>

      <!-- Dynamisk symboloversigt -->
      <h3 class="font-display font-bold text-yellow-300 text-base mb-2.5">
        Symboludbetalinger (ved nuværende indsats: <span id="paytable-current-bet">20,00 kr.</span>)
      </h3>
      <div id="paytable-grid" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-2.5 mb-4">
        <!-- Udfyldes af JS -->
      </div>

      <div class="text-xs text-amber-200/75 bg-black/30 rounded-xl p-3 border border-amber-800/50">
        <strong>Bemærk om spilmatematik:</strong> Denne demo bruger sin egen uafhængige demomatematik, symbolvægte og udbetalingstabel udelukkende til underholdning med virtuelle credits.
      </div>
    </div>
  </div>

  <!-- =========================================================
       JAVASCRIPT SPILMOTOR, SVG-GRAFIK & WEB AUDIO API
       ========================================================= -->
  <script>
    (() => {
      'use strict';

      /* ---------------------------------------------------------
         1. LYDSYSTEM (Web Audio API - syntetisk jungle-lyd)
         --------------------------------------------------------- */
      class JungleAudio {
        constructor() {
          this.enabled = true;
          this.ctx = null;
        }

        ensureContext() {
          if (!this.enabled) return null;
          if (!this.ctx) {
            const AudioCtx = window.AudioContext || window.webkitAudioContext;
            if (AudioCtx) this.ctx = new AudioCtx();
          }
          if (this.ctx && this.ctx.state === 'suspended') {
            this.ctx.resume().catch(() => {});
          }
          return this.ctx;
        }

        playTone({ freq = 440, endFreq = null, type = 'sine', duration = 0.12, gain = 0.12, delay = 0 }) {
          const ctx = this.ensureContext();
          if (!ctx) return;

          const now = ctx.currentTime + delay;
          const osc = ctx.createOscillator();
          const vol = ctx.createGain();

          osc.type = type;
          osc.frequency.setValueAtTime(freq, now);
          if (endFreq !== null) {
            osc.frequency.exponentialRampToValueAtTime(Math.max(20, endFreq), now + duration);
          }

          vol.gain.setValueAtTime(0.0001, now);
          vol.gain.linearRampToValueAtTime(gain, now + 0.015);
          vol.gain.exponentialRampToValueAtTime(0.0001, now + duration);

          osc.connect(vol);
          vol.connect(ctx.destination);

          osc.start(now);
          osc.stop(now + duration + 0.02);
        }

        // Jungletromme / spin-start
        playSpinStart() {
          this.playTone({ freq: 150, endFreq: 68, type: 'triangle', duration: 0.16, gain: 0.18 });
          this.playTone({ freq: 240, endFreq: 110, type: 'sine', duration: 0.11, gain: 0.12, delay: 0.05 });
        }

        // Hjul-stop klik
        playReelStop(colIndex) {
          const base = 130 + colIndex * 18;
          this.playTone({ freq: base, endFreq: 55, type: 'triangle', duration: 0.09, gain: 0.14 });
        }

        // Kaskade-eksplosion
        playCascadePop(step = 1) {
          const pitch = Math.min(900, 320 + step * 75);
          this.playTone({ freq: pitch, endFreq: pitch * 1.45, type: 'sine', duration: 0.14, gain: 0.13 });
          this.playTone({ freq: 180, endFreq: 70, type: 'triangle', duration: 0.12, gain: 0.1 });
        }

        // Gevinst-fanfare
        playWin(isBig = false) {
          const notes = isBig
            ? [523.25, 659.25, 783.99, 1046.5, 1318.5]
            : [440, 554.37, 659.25, 880];
          notes.forEach((n, idx) => {
            this.playTone({
              freq: n,
              type: 'triangle',
              duration: isBig ? 0.28 : 0.18,
              gain: 0.14,
              delay: idx * 0.07
            });
          });
        }

        // Scatter-landing
        playScatter(count) {
          const freq = 520 + count * 110;
          this.playTone({ freq, endFreq: freq * 1.25, type: 'sine', duration: 0.22, gain: 0.16 });
        }
      }

      const audio = new JungleAudio();

      /* ---------------------------------------------------------
         2. SYMBOLDEFINITIONER & SPECIALTEGNEDE SVG-IKONER
         --------------------------------------------------------- */
      const SYMBOLS = {
        GORILLA: {
          id: 'GORILLA',
          name: 'Jungle-Gorilla',
          minCount: 2,
          payouts: { 2: 0.5, 3: 1.5, 4: 4.0, 5: 10.0, 6: 25.0 },
          weight: 5,
          svg: `
            <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow">
              <defs>
                <radialGradient id="gGorBg" cx="50%" cy="40%" r="55%">
                  <stop offset="0%" stop-color="#a855f7"/>
                  <stop offset="100%" stop-color="#3b0764"/>
                </radialGradient>
              </defs>
              <rect x="6" y="6" width="88" height="88" rx="20" fill="url(#gGorBg)" stroke="#facc15" stroke-width="3.5"/>
              <!-- Ører -->
              <circle cx="23" cy="48" r="9" fill="#334155"/>
              <circle cx="77" cy="48" r="9" fill="#334155"/>
              <!-- Hoved -->
              <path d="M26 52 C24 26, 76 26, 74 52 C76 74, 64 84, 50 84 C36 84, 24 74, 26 52 Z" fill="#1e293b"/>
              <!-- Pande -->
              <path d="M30 42 Q50 32 70 42 Q66 52 50 49 Q34 52 30 42 Z" fill="#475569"/>
              <!-- Øjne -->
              <circle cx="39" cy="48" r="4.5" fill="#fef08a"/>
              <circle cx="61" cy="48" r="4.5" fill="#fef08a"/>
              <circle cx="39" cy="48" r="2" fill="#0f172a"/>
              <circle cx="61" cy="48" r="2" fill="#0f172a"/>
              <!-- Snude -->
              <ellipse cx="50" cy="66" rx="16" ry="12" fill="#64748b"/>
              <circle cx="45" cy="62" r="2.2" fill="#0f172a"/>
              <circle cx="55" cy="62" r="2.2" fill="#0f172a"/>
              <path d="M39 71 Q50 78 61 71" stroke="#0f172a" stroke-width="3" fill="none" stroke-linecap="round"/>
              <!-- Guldkrone -->
              <path d="M35 26 L40 16 L50 23 L60 16 L65 26 Z" fill="#facc15" stroke="#b45309" stroke-width="1.5"/>
            </svg>`
        },
        TOUCAN: {
          id: 'TOUCAN',
          name: 'Tukan-fugl',
          minCount: 3,
          payouts: { 3: 0.8, 4: 2.0, 5: 5.0, 6: 12.0 },
          weight: 7,
          svg: `
            <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow">
              <defs>
                <radialGradient id="gTouBg" cx="50%" cy="35%" r="60%">
                  <stop offset="0%" stop-color="#0ea5e9"/>
                  <stop offset="100%" stop-color="#0c4a6e"/>
                </radialGradient>
              </defs>
              <rect x="6" y="6" width="88" height="88" rx="20" fill="url(#gTouBg)" stroke="#38bdf8" stroke-width="3"/>
              <!-- Krop -->
              <path d="M26 82 C24 50, 38 28, 56 30 C64 32, 66 56, 56 82 Z" fill="#0f172a"/>
              <!-- Bryst -->
              <path d="M40 44 C52 44, 58 58, 50 76 C38 72, 34 56, 40 44 Z" fill="#fde047"/>
              <!-- Næb -->
              <path d="M54 32 C76 30, 88 40, 86 50 C74 52, 62 50, 52 46 Z" fill="#f97316"/>
              <path d="M76 34 C84 38, 87 44, 86 50 C80 50, 77 44, 76 34 Z" fill="#ef4444"/>
              <path d="M53 45 L84 48" stroke="#7c2d12" stroke-width="2"/>
              <!-- Øje -->
              <circle cx="48" cy="37" r="6" fill="#38bdf8"/>
              <circle cx="49" cy="37" r="3" fill="#0f172a"/>
              <circle cx="50" cy="36" r="1" fill="#fff"/>
            </svg>`
        },
        LEOPARD: {
          id: 'LEOPARD',
          name: 'Jungle-Leopard',
          minCount: 3,
          payouts: { 3: 0.6, 4: 1.5, 5: 3.5, 6: 8.0 },
          weight: 8,
          svg: `
            <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow">
              <defs>
                <radialGradient id="gLeoBg" cx="50%" cy="35%" r="60%">
                  <stop offset="0%" stop-color="#f59e0b"/>
                  <stop offset="100%" stop-color="#78350f"/>
                </radialGradient>
              </defs>
              <rect x="6" y="6" width="88" height="88" rx="20" fill="url(#gLeoBg)" stroke="#fde047" stroke-width="3"/>
              <!-- Ører -->
              <circle cx="30" cy="30" r="9" fill="#d97706"/>
              <circle cx="70" cy="30" r="9" fill="#d97706"/>
              <!-- Hoved -->
              <path d="M25 48 C25 28, 75 28, 75 48 C75 70, 62 82, 50 82 C38 82, 25 70, 25 48 Z" fill="#fbbf24"/>
              <!-- Pletter -->
              <circle cx="36" cy="38" r="3" fill="#451a03"/>
              <circle cx="64" cy="38" r="3" fill="#451a03"/>
              <circle cx="50" cy="34" r="2.8" fill="#451a03"/>
              <!-- Øjne -->
              <ellipse cx="39" cy="50" rx="5" ry="3.5" fill="#10b981"/>
              <ellipse cx="61" cy="50" rx="5" ry="3.5" fill="#10b981"/>
              <circle cx="39" cy="50" r="2" fill="#064e3b"/>
              <circle cx="61" cy="50" r="2" fill="#064e3b"/>
              <!-- Snude -->
              <path d="M40 62 Q50 56 60 62 Q58 75 50 75 Q42 75 40 62 Z" fill="#fef3c7"/>
              <polygon points="46,61 54,61 50,66" fill="#be185d"/>
              <path d="M43 70 Q50 74 57 70" stroke="#451a03" stroke-width="2.5" fill="none" stroke-linecap="round"/>
            </svg>`
        },
        FROG: {
          id: 'FROG',
          name: 'Træfrø',
          minCount: 3,
          payouts: { 3: 0.5, 4: 1.2, 5: 2.5, 6: 6.0 },
          weight: 9,
          svg: `
            <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow">
              <defs>
                <radialGradient id="gFrgBg" cx="50%" cy="35%" r="60%">
                  <stop offset="0%" stop-color="#22c55e"/>
                  <stop offset="100%" stop-color="#14532d"/>
                </radialGradient>
              </defs>
              <rect x="6" y="6" width="88" height="88" rx="20" fill="url(#gFrgBg)" stroke="#86efac" stroke-width="3"/>
              <!-- Øjenbuer -->
              <circle cx="36" cy="36" r="12" fill="#4ade80"/>
              <circle cx="64" cy="36" r="12" fill="#4ade80"/>
              <!-- Hoved -->
              <ellipse cx="50" cy="58" rx="28" ry="21" fill="#22c55e"/>
              <ellipse cx="50" cy="64" rx="22" ry="13" fill="#bef264"/>
              <!-- Røde træfrø-øjne -->
              <circle cx="36" cy="36" r="7.5" fill="#ef4444"/>
              <circle cx="64" cy="36" r="7.5" fill="#ef4444"/>
              <ellipse cx="36" cy="36" rx="2.2" ry="5.5" fill="#0f172a"/>
              <ellipse cx="64" cy="36" rx="2.2" ry="5.5" fill="#0f172a"/>
              <!-- Smil -->
              <path d="M33 60 Q50 72 67 60" stroke="#14532d" stroke-width="3.2" fill="none" stroke-linecap="round"/>
            </svg>`
        },
        A: {
          id: 'A',
          name: 'Es (A)',
          minCount: 3,
          payouts: { 3: 0.3, 4: 0.7, 5: 1.5, 6: 3.5 },
          weight: 12,
          svg: createWoodLetterSVG('A', '#ef4444', '#fca5a5')
        },
        K: {
          id: 'K',
          name: 'Konge (K)',
          minCount: 3,
          payouts: { 3: 0.25, 4: 0.6, 5: 1.3, 6: 3.0 },
          weight: 13,
          svg: createWoodLetterSVG('K', '#f97316', '#fdba74')
        },
        Q: {
          id: 'Q',
          name: 'Dame (Q)',
          minCount: 3,
          payouts: { 3: 0.2, 4: 0.5, 5: 1.1, 6: 2.5 },
          weight: 14,
          svg: createWoodLetterSVG('Q', '#ec4899', '#f9a8d4')
        },
        J: {
          id: 'J',
          name: 'Knægt (J)',
          minCount: 3,
          payouts: { 3: 0.2, 4: 0.45, 5: 1.0, 6: 2.2 },
          weight: 15,
          svg: createWoodLetterSVG('J', '#3b82f6', '#93c5fd')
        },
        T10: {
          id: 'T10',
          name: 'Ti (10)',
          minCount: 3,
          payouts: { 3: 0.15, 4: 0.4, 5: 0.9, 6: 2.0 },
          weight: 16,
          svg: createWoodLetterSVG('10', '#14b8a6', '#5eead4')
        },
        N9: {
          id: 'N9',
          name: 'Ni (9)',
          minCount: 3,
          payouts: { 3: 0.15, 4: 0.35, 5: 0.8, 6: 1.8 },
          weight: 17,
          svg: createWoodLetterSVG('9', '#a3e635', '#d9f99d')
        },
        WILD: {
          id: 'WILD',
          name: 'Banana Wild',
          isWild: true,
          minCount: 0,
          payouts: {},
          weight: 5,
          svg: `
            <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow">
              <defs>
                <radialGradient id="gWildBg" cx="50%" cy="40%" r="58%">
                  <stop offset="0%" stop-color="#fef08a"/>
                  <stop offset="55%" stop-color="#f59e0b"/>
                  <stop offset="100%" stop-color="#92400e"/>
                </radialGradient>
              </defs>
              <rect x="5" y="5" width="90" height="90" rx="20" fill="url(#gWildBg)" stroke="#fef08a" stroke-width="4"/>
              <!-- Bananer -->
              <path d="M26 62 C24 36, 46 20, 72 22 C60 36, 52 54, 26 62 Z" fill="#fde047" stroke="#b45309" stroke-width="2.5"/>
              <path d="M32 68 C34 42, 54 26, 78 30 C66 44, 56 60, 32 68 Z" fill="#facc15" stroke="#b45309" stroke-width="2.5"/>
              <rect x="68" y="19" width="7" height="6" rx="2" fill="#78350f"/>
              <!-- WILD skilt -->
              <rect x="12" y="58" width="76" height="26" rx="8" fill="#14532d" stroke="#fde047" stroke-width="2.5"/>
              <text x="50" y="76" text-anchor="middle" font-family="Fredoka, sans-serif" font-weight="900" font-size="19" fill="#fde047" letter-spacing="1.5">WILD</text>
            </svg>`
        },
        SCATTER: {
          id: 'SCATTER',
          name: 'Banana Scatter',
          isScatter: true,
          minCount: 4,
          payouts: {},
          weight: 4,
          svg: `
            <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow">
              <defs>
                <radialGradient id="gScatCoin" cx="40%" cy="35%" r="60%">
                  <stop offset="0%" stop-color="#fef9c3"/>
                  <stop offset="45%" stop-color="#facc15"/>
                  <stop offset="100%" stop-color="#b45309"/>
                </radialGradient>
              </defs>
              <circle cx="50" cy="48" r="41" fill="url(#gScatCoin)" stroke="#fef08a" stroke-width="4"/>
              <circle cx="50" cy="48" r="33" fill="none" stroke="#92400e" stroke-width="2" stroke-dasharray="5 3"/>
              <!-- Banan ikon i midten -->
              <path d="M30 56 C30 34, 48 22, 70 25 C58 38, 50 50, 30 56 Z" fill="#fffbeb" stroke="#92400e" stroke-width="2.2"/>
              <!-- BONUS banner -->
              <rect x="10" y="64" width="80" height="24" rx="8" fill="#991b1b" stroke="#fde047" stroke-width="2.5"/>
              <text x="50" y="80" text-anchor="middle" font-family="Fredoka, sans-serif" font-weight="900" font-size="15.5" fill="#fef08a" letter-spacing="1">SCATTER</text>
            </svg>`
        }
      };

      function createWoodLetterSVG(label, mainColor, lightColor) {
        return `
          <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow">
            <rect x="8" y="8" width="84" height="84" rx="18" fill="#2b160a" stroke="#78350f" stroke-width="3"/>
            <rect x="13" y="13" width="74" height="74" rx="14" fill="#3f2110" stroke="${mainColor}" stroke-width="2" stroke-opacity="0.6"/>
            <text x="50" y="66" text-anchor="middle" font-family="Fredoka, sans-serif" font-weight="900" font-size="${label.length > 1 ? '44' : '52'}"
              fill="${mainColor}" stroke="${lightColor}" stroke-width="2.2" paint-order="stroke">${label}</text>
          </svg>`;
      }

      const NORMAL_SYMBOL_KEYS = ['GORILLA', 'TOUCAN', 'LEOPARD', 'FROG', 'A', 'K', 'Q', 'J', 'T10', 'N9'];

      /* ---------------------------------------------------------
         3. SPILTILSTAND & KONFIGURATION
         --------------------------------------------------------- */
      const BET_STEPS = [2, 4, 6, 10, 15, 20, 30, 40, 50, 75, 100];
      const BONUS_BUY_MULTIPLIER = 80;

      const state = {
        balance: 10000.00,
        betIndex: 5, // Starter på 20,00 kr.
        currentWin: 0,
        isSpinning: false,
        autoSpin: false,
        freeSpins: {
          active: false,
          remaining: 0,
          multiplier: 1,
          totalWin: 0
        },
        // Gitter-data:
        // mainGrid[col][row] hvor col = 0..5, row = 0..3
        // topReel[idx] hvor idx = 0..3 (svarer til col 1, 2, 3, 4)
        mainGrid: Array.from({ length: 6 }, () => Array(4).fill('GORILLA')),
        topReel: Array(4).fill('WILD'),
        forceBonusNextSpin: false
      };

      function getCurrentBet() {
        return BET_STEPS[state.betIndex];
      }

      function formatDKK(amount) {
        return amount.toLocaleString('da-DK', {
          minimumFractionDigits: 2,
          maximumFractionDigits: 2
        }) + ' kr.';
      }

      /* ---------------------------------------------------------
         4. DOM-REFERENCER & INITIALISERING AF GITTER
         --------------------------------------------------------- */
      const elBalance = document.getElementById('balance-display');
      const elBet = document.getElementById('bet-display');
      const elWin = document.getElementById('win-display');
      const elBonusBuyPrice = document.getElementById('bonus-buy-price');
      const elReelsGrid = document.getElementById('reels-grid');
      const elWinLinesSvg = document.getElementById('win-lines-svg');
      const elEffectsLayer = document.getElementById('effects-layer');
      const elStatusBanner = document.getElementById('status-banner');
      const elCascadeBadge = document.getElementById('cascade-badge');
      const elWaysCount = document.getElementById('ways-count');
      const elMultiplierBadge = document.getElementById('multiplier-badge');
      const elFsMultiplierVal = document.getElementById('fs-multiplier-val');
      const elFsBanner = document.getElementById('freespins-banner');
      const elFsRemaining = document.getElementById('fs-remaining');
      const elFsTotalWin = document.getElementById('fs-total-win');

      const btnSpin = document.getElementById('btn-spin');
      const btnAutoSpin = document.getElementById('btn-autospin');
      const btnBetMinus = document.getElementById('btn-bet-minus');
      const btnBetPlus = document.getElementById('btn-bet-plus');
      const btnBonusBuy = document.getElementById('btn-bonus-buy');
      const btnSound = document.getElementById('btn-sound');
      const btnPaytable = document.getElementById('btn-paytable');

      function initFireflies() {
        const container = document.getElementById('fireflies-container');
        for (let i = 0; i < 18; i++) {
          const fly = document.createElement('div');
          fly.className = 'firefly';
          fly.style.left = `${Math.random() * 100}%`;
          fly.style.top = `${Math.random() * 100}%`;
          fly.style.setProperty('--dur', `${7 + Math.random() * 8}s`);
          fly.style.setProperty('--delay', `${Math.random() * 6}s`);
          fly.style.setProperty('--dx', `${(Math.random() - 0.5) * 140}px`);
          fly.style.setProperty('--dy', `${-40 - Math.random() * 100}px`);
          container.appendChild(fly);
        }
      }

      function buildBoardDOM() {
        elReelsGrid.innerHTML = '';
        for (let col = 0; col < 6; col++) {
          const colEl = document.createElement('div');
          colEl.className = 'reel-col rounded-xl p-1 flex flex-col gap-1.5 sm:gap-2';
          colEl.dataset.col = col;

          for (let row = 0; row < 4; row++) {
            const cell = document.createElement('div');
            cell.id = `cell-main-${col}-${row}`;
            cell.className = 'symbol-cell aspect-square w-full rounded-xl flex items-center justify-center p-1 sm:p-1.5';
            colEl.appendChild(cell);
          }
          elReelsGrid.appendChild(colEl);
        }
      }

      /* ---------------------------------------------------------
         5. TILFÆLDIG SYMBOLGENERATOR (VÆGTET DEMOMATEMATIK)
         --------------------------------------------------------- */
      function pickRandomSymbol({ allowWild = false, allowScatter = true, isFreeSpins = false } = {}) {
        const pool = [];
        for (const key of NORMAL_SYMBOL_KEYS) {
          pool.push({ key, weight: SYMBOLS[key].weight });
        }
        if (allowWild) {
          pool.push({ key: 'WILD', weight: isFreeSpins ? 7 : 5 });
        }
        if (allowScatter) {
          pool.push({ key: 'SCATTER', weight: isFreeSpins ? 3 : 4 });
        }

        const totalWeight = pool.reduce((acc, item) => acc + item.weight, 0);
        let r = Math.random() * totalWeight;
        for (const item of pool) {
          r -= item.weight;
          if (r <= 0) return item.key;
        }
        return 'N9';
      }

      function generateInitialBoard() {
        for (let col = 0; col < 6; col++) {
          const allowWild = col >= 1 && col <= 4;
          for (let row = 0; row < 4; row++) {
            state.mainGrid[col][row] = pickRandomSymbol({
              allowWild,
              allowScatter: true,
              isFreeSpins: state.freeSpins.active
            });
          }
        }
        for (let t = 0; t < 4; t++) {
          state.topReel[t] = pickRandomSymbol({
            allowWild: true,
            allowScatter: false, // Scatters lander på hovedhjulene
            isFreeSpins: state.freeSpins.active
          });
        }

        // Hvis spilleren har købt Bonus Buy, placeres 4 Scatters tilfældigt på hovedgitteret
        if (state.forceBonusNextSpin) {
          state.forceBonusNextSpin = false;
          const coords = [];
          for (let c = 0; c < 6; c++) {
            for (let r = 0; r < 4; r++) {
              coords.push({ c, r });
            }
          }
          // Bland koordinater og sæt 4 Scatters
          for (let i = coords.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [coords[i], coords[j]] = [coords[j], coords[i]];
          }
          for (let k = 0; k < 4; k++) {
            const { c, r } = coords[k];
            state.mainGrid[c][r] = 'SCATTER';
          }
        }
      }

      function renderBoard(animateDrop = false) {
        // Render top reel (over hjul 2, 3, 4, 5 => col 1, 2, 3, 4)
        for (let t = 0; t < 4; t++) {
          const topEl = document.getElementById(`top-reel-${t + 1}`);
          const symKey = state.topReel[t];
          topEl.innerHTML = `<div class="w-12 h-12 sm:w-14 sm:h-14 md:w-16 md:h-16 ${animateDrop ? 'anim-drop' : ''}">${SYMBOLS[symKey].svg}</div>`;
          topEl.classList.remove('symbol-win', 'symbol-explode');
        }

        // Render hovedhjul
        for (let col = 0; col < 6; col++) {
          for (let row = 0; row < 4; row++) {
            const cellEl = document.getElementById(`cell-main-${col}-${row}`);
            const symKey = state.mainGrid[col][row];
            cellEl.innerHTML = `<div class="w-full h-full ${animateDrop ? 'anim-drop' : ''}">${SYMBOLS[symKey].svg}</div>`;
            cellEl.classList.remove('symbol-win', 'symbol-explode');
          }
        }
      }

      /* ---------------------------------------------------------
         6. 10.000 WAYS GEVINSTBEREGNING (4-5-5-5-5-4)
         --------------------------------------------------------- */
      function getColumnSymbols(col) {
        // Returnerer liste over objekter: { symbol, source: 'main'|'top', col, row, topIdx }
        const list = [];
        if (col >= 1 && col <= 4) {
          const topIdx = col - 1;
          list.push({
            symbol: state.topReel[topIdx],
            source: 'top',
            col,
            topIdx
          });
        }
        for (let row = 0; row < 4; row++) {
          list.push({
            symbol: state.mainGrid[col][row],
            source: 'main',
            col,
            row
          });
        }
        return list;
      }

      function evaluate10KWays() {
        const bet = getCurrentBet();
        const multiplier = state.freeSpins.active ? state.freeSpins.multiplier : 1;

        let totalPayout = 0;
        const winningPositions = new Map(); // key -> posObj
        const winDetails = [];

        // Tjek hvert normalt symbol fra hjul 1 og fremefter
        for (const symKey of NORMAL_SYMBOL_KEYS) {
          const symDef = SYMBOLS[symKey];
          let consecutiveReels = 0;
          let waysCount = 1;
          const matchedCellsPerReel = [];

          for (let col = 0; col < 6; col++) {
            const colItems = getColumnSymbols(col);
            const matches = colItems.filter(item =>
              item.symbol === symKey || (item.symbol === 'WILD' && col >= 1 && col <= 4)
            );

            if (matches.length > 0) {
              consecutiveReels++;
              waysCount *= matches.length;
              matchedCellsPerReel.push(matches);
            } else {
              break;
            }
          }

          if (consecutiveReels >= symDef.minCount) {
            const baseMult = symDef.payouts[consecutiveReels] || 0;
            if (baseMult > 0) {
              const winAmount = baseMult * waysCount * bet * multiplier;
              totalPayout += winAmount;
              winDetails.push({
                symbol: symKey,
                name: symDef.name,
                count: consecutiveReels,
                ways: waysCount,
                amount: winAmount
              });

              for (const reelMatches of matchedCellsPerReel) {
                for (const pos of reelMatches) {
                  const uniqueId = pos.source === 'top'
                    ? `top-${pos.topIdx}`
                    : `main-${pos.col}-${pos.row}`;
                  winningPositions.set(uniqueId, pos);
                }
              }
            }
          }
        }

        // Tæl Scatters på hele pladen
        const scatterPositions = [];
        for (let col = 0; col < 6; col++) {
          for (let row = 0; row < 4; row++) {
            if (state.mainGrid[col][row] === 'SCATTER') {
              scatterPositions.push({ source: 'main', col, row });
            }
          }
        }

        return {
          totalPayout: Math.round(totalPayout * 100) / 100,
          winningPositions: Array.from(winningPositions.values()),
          winDetails,
          scatterPositions
        };
      }

      /* ---------------------------------------------------------
         7. VISUELLE EFFEKTER (Highlight, Linjer & Kaskade)
         --------------------------------------------------------- */
      function getCellElement(pos) {
        if (pos.source === 'top') {
          return document.getElementById(`top-reel-${pos.topIdx + 1}`);
        }
        return document.getElementById(`cell-main-${pos.col}-${pos.row}`);
      }

      function highlightWinners(positions) {
        elWinLinesSvg.innerHTML = '';
        const boardRect = document.getElementById('reels-wrapper').getBoundingClientRect();

        // Gruppér vindende felter pr. kolonne for at tegne gyldne forbindelseslinjer
        const byCol = Array.from({ length: 6 }, () => []);
        positions.forEach(pos => {
          const el = getCellElement(pos);
          if (el) {
            el.classList.add('symbol-win');
            const r = el.getBoundingClientRect();
            const cx = r.left - boardRect.left + r.width / 2;
            const cy = Math.max(8, r.top - boardRect.top + r.height / 2);
            byCol[pos.col].push({ cx, cy });
          }
        });

        for (let c = 0; c < 5; c++) {
          if (byCol[c].length > 0 && byCol[c + 1].length > 0) {
            // Tegn linje mellem midtpunkterne i tilstødende hjul
            const p1 = byCol[c][0];
            const p2 = byCol[c + 1][0];
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', p1.cx);
            line.setAttribute('y1', p1.cy);
            line.setAttribute('x2', p2.cx);
            line.setAttribute('y2', p2.cy);
            line.setAttribute('stroke', '#fde047');
            line.setAttribute('stroke-width', '4');
            line.setAttribute('stroke-linecap', 'round');
            line.setAttribute('opacity', '0.75');
            elWinLinesSvg.appendChild(line);
          }
        }
      }

      function spawnFloatingWin(amount) {
        const pop = document.createElement('div');
        pop.className = 'floating-win-pop font-display text-2xl sm:text-4xl font-black text-yellow-300 whitespace-nowrap';
        pop.textContent = `+${formatDKK(amount)}`;
        elEffectsLayer.appendChild(pop);
        setTimeout(() => pop.remove(), 1200);
      }

      async function collapseAndRefill(winningPositions) {
        // 1. Eksplosionsanimation
        elWinLinesSvg.innerHTML = '';
        winningPositions.forEach(pos => {
          const el = getCellElement(pos);
          if (el) {
            el.classList.remove('symbol-win');
            el.classList.add('symbol-explode');
          }
        });

        await sleep(340);

        // 2. Fjern vindende symboler og lad nye falde ned
        const removedTop = new Set();
        const removedMainByCol = Array.from({ length: 6 }, () => new Set());

        winningPositions.forEach(pos => {
          if (pos.source === 'top') {
            removedTop.add(pos.topIdx);
          } else {
            removedMainByCol[pos.col].add(pos.row);
          }
        });

        // Top reel: skub til venstre / fyld op med nye symboler
        if (removedTop.size > 0) {
          const remainingTop = [];
          for (let t = 0; t < 4; t++) {
            if (!removedTop.has(t)) remainingTop.push(state.topReel[t]);
          }
          while (remainingTop.length < 4) {
            remainingTop.push(pickRandomSymbol({
              allowWild: true,
              allowScatter: false,
              isFreeSpins: state.freeSpins.active
            }));
          }
          state.topReel = remainingTop;
        }

        // Hovedhjul: fald ned ovenfra
        for (let col = 0; col < 6; col++) {
          const removedRows = removedMainByCol[col];
          if (removedRows.size > 0) {
            const survivors = [];
            for (let row = 0; row < 4; row++) {
              if (!removedRows.has(row)) {
                survivors.push(state.mainGrid[col][row]);
              }
            }
            const missingCount = 4 - survivors.length;
            const newSyms = [];
            const allowWild = col >= 1 && col <= 4;
            for (let i = 0; i < missingCount; i++) {
              newSyms.push(pickRandomSymbol({
                allowWild,
                allowScatter: true,
                isFreeSpins: state.freeSpins.active
              }));
            }
            state.mainGrid[col] = [...newSyms, ...survivors];
          }
        }

        // Render de opdaterede celler med fald-animation
        for (let t = 0; t < 4; t++) {
          const topEl = document.getElementById(`top-reel-${t + 1}`);
          topEl.classList.remove('symbol-explode', 'symbol-win');
          const symKey = state.topReel[t];
          topEl.innerHTML = `<div class="w-12 h-12 sm:w-14 sm:h-14 md:w-16 md:h-16 ${removedTop.size > 0 ? 'anim-drop' : ''}">${SYMBOLS[symKey].svg}</div>`;
        }

        for (let col = 0; col < 6; col++) {
          const hadCascade = removedMainByCol[col].size > 0;
          for (let row = 0; row < 4; row++) {
            const cellEl = document.getElementById(`cell-main-${col}-${row}`);
            cellEl.classList.remove('symbol-explode', 'symbol-win');
            const symKey = state.mainGrid[col][row];
            cellEl.innerHTML = `<div class="w-full h-full ${hadCascade ? 'anim-drop' : ''}">${SYMBOLS[symKey].svg}</div>`;
          }
        }

        await sleep(360);
      }

      /* ---------------------------------------------------------
         8. SPIN-FLOW, KASKADE-LOOP & FREE SPINS
         --------------------------------------------------------- */
      function sleep(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
      }

      async function animateReelSpin() {
        elWinLinesSvg.innerHTML = '';
        // Start spin-puls på alle hjul
        for (let t = 0; t < 4; t++) {
          document.getElementById(`top-reel-${t + 1}`).classList.add('anim-spinning');
        }
        for (let col = 0; col < 6; col++) {
          for (let row = 0; row < 4; row++) {
            document.getElementById(`cell-main-${col}-${row}`).classList.add('anim-spinning');
          }
        }

        // Generér det nye resultat i baggrunden
        generateInitialBoard();

        // Lad hjulene "flimre" med tilfældige symboler kortvarigt
        const shuffleInterval = setInterval(() => {
          for (let col = 0; col < 6; col++) {
            const colEl = elReelsGrid.children[col];
            if (!colEl.dataset.locked) {
              for (let row = 0; row < 4; row++) {
                const rnd = NORMAL_SYMBOL_KEYS[Math.floor(Math.random() * NORMAL_SYMBOL_KEYS.length)];
                const cellEl = document.getElementById(`cell-main-${col}-${row}`);
                cellEl.innerHTML = `<div class="w-full h-full opacity-85">${SYMBOLS[rnd].svg}</div>`;
              }
            }
          }
        }, 70);

        await sleep(260);

        // Stop hjulene forskudt (staggered stop) fra venstre mod højre
        for (let col = 0; col < 6; col++) {
          elReelsGrid.children[col].dataset.locked = 'true';
          audio.playReelStop(col);

          // Stop evt. tilhørende top-reel felt over hjul 2..5
          if (col >= 1 && col <= 4) {
            const t = col - 1;
            const topEl = document.getElementById(`top-reel-${t + 1}`);
            topEl.classList.remove('anim-spinning');
            const topSym = state.topReel[t];
            topEl.innerHTML = `<div class="w-12 h-12 sm:w-14 sm:h-14 md:w-16 md:h-16 anim-drop">${SYMBOLS[topSym].svg}</div>`;
          }

          for (let row = 0; row < 4; row++) {
            const cellEl = document.getElementById(`cell-main-${col}-${row}`);
            cellEl.classList.remove('anim-spinning');
            const symKey = state.mainGrid[col][row];
            cellEl.innerHTML = `<div class="w-full h-full anim-drop">${SYMBOLS[symKey].svg}</div>`;
          }

          await sleep(95);
        }

        clearInterval(shuffleInterval);
        for (let col = 0; col < 6; col++) {
          delete elReelsGrid.children[col].dataset.locked;
        }
      }

      async function executeSpin() {
        if (state.isSpinning) return;

        const bet = getCurrentBet();
        const isFreeSpin = state.freeSpins.active;

        if (!isFreeSpin) {
          if (state.balance < bet) {
            state.autoSpin = false;
            updateControlsUI();
            elStatusBanner.textContent = 'Ikke nok virtuelle credits til denne indsats. Sænk indsatsen!';
            return;
          }
          state.balance = Math.round((state.balance - bet) * 100) / 100;
        } else {
          state.freeSpins.remaining = Math.max(0, state.freeSpins.remaining - 1);
        }

        state.isSpinning = true;
        state.currentWin = 0;
        elCascadeBadge.classList.add('hidden');
        elStatusBanner.textContent = isFreeSpin
          ? `BananaZ Free Spin i gang (Multiplikator ${state.freeSpins.multiplier}x)...`
          : 'Hjulene drejer... Held og lykke!';
        updateControlsUI();
        audio.playSpinStart();

        await animateReelSpin();

        // Kaskade-loop
        let cascadeStep = 0;
        let spinTotalWin = 0;
        let lastEvaluation = evaluate10KWays();

        while (lastEvaluation.totalPayout > 0) {
          cascadeStep++;
          const stepWin = lastEvaluation.totalPayout;
          spinTotalWin = Math.round((spinTotalWin + stepWin) * 100) / 100;
          state.currentWin = spinTotalWin;

          if (isFreeSpin) {
            state.freeSpins.totalWin = Math.round((state.freeSpins.totalWin + stepWin) * 100) / 100;
          }

          audio.playCascadePop(cascadeStep);
          highlightWinners(lastEvaluation.winningPositions);
          spawnFloatingWin(stepWin);

          if (cascadeStep > 1) {
            elCascadeBadge.textContent = `Kaskade x${cascadeStep}`;
            elCascadeBadge.classList.remove('hidden');
          }

          const topDetail = lastEvaluation.winDetails[0];
          elStatusBanner.textContent = `Gevinst! ${topDetail.count}x ${topDetail.name} (${topDetail.ways} ways) = +${formatDKK(stepWin)}`;
          updateControlsUI();

          await sleep(750);
          await collapseAndRefill(lastEvaluation.winningPositions);

          // I Free Spins stiger multiplikatoren med +1 for hver kaskadegevinst
          if (isFreeSpin) {
            state.freeSpins.multiplier += 1;
            elFsMultiplierVal.textContent = `${state.freeSpins.multiplier}x`;
          }

          lastEvaluation = evaluate10KWays();
        }

        // Læg spin-gevinst til saldo
        if (spinTotalWin > 0) {
          state.balance = Math.round((state.balance + spinTotalWin) * 100) / 100;
          audio.playWin(spinTotalWin >= bet * 15);
          elStatusBanner.textContent = `Samlet spingevinst: ${formatDKK(spinTotalWin)}!`;

          // Stor gevinst / Mega gevinst fejring ved >= 15x indsats
          if (spinTotalWin >= bet * 15) {
            await showBigWinCelebration(spinTotalWin, bet);
          }
        } else {
          elStatusBanner.textContent = isFreeSpin
            ? 'Ingen gevinst på dette gratis spin.'
            : 'Ingen gevinst – prøv igen!';
        }

        // Tjek Scatters (4 eller flere udløser / genudløser Free Spins)
        const scatterCount = lastEvaluation.scatterPositions.length;
        if (scatterCount >= 4) {
          audio.playScatter(scatterCount);
          highlightWinners(lastEvaluation.scatterPositions);
          await sleep(650);

          const awardedSpins = 10 + (scatterCount - 4) * 2;
          if (!state.freeSpins.active) {
            state.freeSpins.active = true;
            state.freeSpins.remaining = awardedSpins;
            state.freeSpins.multiplier = 1;
            state.freeSpins.totalWin = 0;
            document.body.classList.add('freespins-active');
            await showFreeSpinsModal(
              'BananaZ Free Spins!',
              `Du landede ${scatterCount} Scatter-symboler og har vundet ${awardedSpins} Free Spins med stigende kaskade-multiplikator!`,
              'Start Free Spins'
            );
          } else {
            state.freeSpins.remaining += awardedSpins;
            await showFreeSpinsModal(
              'Ekstra Free Spins!',
              `Du landede ${scatterCount} Scatters og vandt +${awardedSpins} ekstra Free Spins!`,
              'Fortsæt Free Spins'
            );
          }
        }

        // Afslut Free Spins hvis der ikke er flere tilbage
        if (state.freeSpins.active && state.freeSpins.remaining === 0) {
          const totalBonusWin = state.freeSpins.totalWin;
          state.freeSpins.active = false;
          state.freeSpins.multiplier = 1;
          document.body.classList.remove('freespins-active');
          updateControlsUI();

          await showFreeSpinsModal(
            'Free Spins Afsluttet!',
            `Tillykke! Du vandt i alt ${formatDKK(totalBonusWin)} i BananaZ Free Spins!`,
            'Tilbage til grundspillet'
          );
        }

        state.isSpinning = false;
        updateControlsUI();

        // Fortsæt automatisk hvis Free Spins er aktive eller Auto-Spin er slået til
        if (state.freeSpins.active && state.freeSpins.remaining > 0) {
          await sleep(550);
          executeSpin();
        } else if (state.autoSpin) {
          if (state.balance >= getCurrentBet()) {
            await sleep(650);
            if (state.autoSpin && !state.isSpinning) executeSpin();
          } else {
            state.autoSpin = false;
            updateControlsUI();
          }
        }
      }

      /* ---------------------------------------------------------
         9. MODALER & UI-OPDATERINGER
         --------------------------------------------------------- */
      function showBigWinCelebration(amount, bet) {
        return new Promise(resolve => {
          const overlay = document.getElementById('bigwin-overlay');
          const title = document.getElementById('bigwin-title');
          const amountEl = document.getElementById('bigwin-amount');
          const closeBtn = document.getElementById('btn-close-bigwin');

          title.textContent = amount >= bet * 40 ? 'MEGA GEVINST!' : 'STOR GEVINST!';
          amountEl.textContent = formatDKK(amount);
          overlay.classList.remove('hidden');

          const cleanup = () => {
            overlay.classList.add('hidden');
            closeBtn.removeEventListener('click', cleanup);
            resolve();
          };
          closeBtn.addEventListener('click', cleanup);
        });
      }

      function showFreeSpinsModal(titleText, descText, btnText) {
        return new Promise(resolve => {
          const modal = document.getElementById('freespins-modal');
          document.getElementById('fs-modal-title').textContent = titleText;
          document.getElementById('fs-modal-desc').textContent = descText;
          const okBtn = document.getElementById('btn-fs-modal-ok');
          okBtn.textContent = btnText;

          modal.classList.remove('hidden');
          const cleanup = () => {
            modal.classList.add('hidden');
            okBtn.removeEventListener('click', cleanup);
            resolve();
          };
          okBtn.addEventListener('click', cleanup);
        });
      }

      function renderPaytable() {
        const bet = getCurrentBet();
        document.getElementById('paytable-current-bet').textContent = formatDKK(bet);
        const grid = document.getElementById('paytable-grid');
        grid.innerHTML = '';

        const orderedKeys = ['GORILLA', 'TOUCAN', 'LEOPARD', 'FROG', 'A', 'K', 'Q', 'J', 'T10', 'N9', 'WILD', 'SCATTER'];
        for (const key of orderedKeys) {
          const sym = SYMBOLS[key];
          const card = document.createElement('div');
          card.className = 'wood-plaque rounded-2xl p-2.5 flex flex-col items-center text-center';

          let payoutHTML = '';
          if (sym.isWild) {
            payoutHTML = `<div class="text-xs text-yellow-200 mt-1">Erstatter alle normale symboler på hjul 2, 3, 4 og 5.</div>`;
          } else if (sym.isScatter) {
            payoutHTML = `<div class="text-xs text-yellow-200 mt-1">4+ Scatters giver 10 Free Spins (+2 pr. ekstra).</div>`;
          } else {
            const entries = Object.entries(sym.payouts)
              .sort((a, b) => Number(b[0]) - Number(a[0]))
              .map(([cnt, mult]) => `<div class="flex justify-between w-full px-1"><span>${cnt}x</span><span class="font-bold text-emerald-300">${formatDKK(mult * bet)}</span></div>`)
              .join('');
            payoutHTML = `<div class="w-full text-xs text-amber-100 mt-1.5 space-y-0.5">${entries}</div>`;
          }

          card.innerHTML = `
            <div class="w-14 h-14 mb-1">${sym.svg}</div>
            <div class="font-display font-bold text-sm text-yellow-300">${sym.name}</div>
            ${payoutHTML}
          `;
          grid.appendChild(card);
        }
      }

      function updateControlsUI() {
        const bet = getCurrentBet();
        const buyPrice = bet * BONUS_BUY_MULTIPLIER;

        elBalance.textContent = formatDKK(state.balance);
        elBet.textContent = formatDKK(bet);
        elWin.textContent = formatDKK(state.currentWin);
        elBonusBuyPrice.textContent = formatDKK(buyPrice);

        const busy = state.isSpinning || state.freeSpins.active;
        btnSpin.disabled = state.isSpinning;
        btnBetMinus.disabled = busy || state.betIndex === 0;
        btnBetPlus.disabled = busy || state.betIndex === BET_STEPS.length - 1;
        btnBonusBuy.disabled = busy || state.balance < buyPrice;

        // Auto-Spin UI
        const autoLabel = document.getElementById('autospin-label');
        const autoIcon = document.getElementById('autospin-icon');
        if (state.autoSpin) {
          btnAutoSpin.classList.add('gold-rim');
          autoLabel.textContent = 'Auto: Til';
          autoIcon.textContent = '⏹️';
        } else {
          btnAutoSpin.classList.remove('gold-rim');
          autoLabel.textContent = 'Auto: Fra';
          autoIcon.textContent = '🔄';
        }

        // Free Spins HUD
        if (state.freeSpins.active) {
          elFsBanner.classList.remove('hidden');
          elMultiplierBadge.classList.remove('hidden');
          elFsRemaining.textContent = state.freeSpins.remaining;
          elFsTotalWin.textContent = formatDKK(state.freeSpins.totalWin);
          elFsMultiplierVal.textContent = `${state.freeSpins.multiplier}x`;
        } else {
          elFsBanner.classList.add('hidden');
          elMultiplierBadge.classList.add('hidden');
        }
      }

      /* ---------------------------------------------------------
         10. EVENT LISTENERS
         --------------------------------------------------------- */
      btnSpin.addEventListener('click', () => {
        executeSpin();
      });

      btnAutoSpin.addEventListener('click', () => {
        state.autoSpin = !state.autoSpin;
        updateControlsUI();
        if (state.autoSpin && !state.isSpinning) {
          executeSpin();
        }
      });

      btnBetMinus.addEventListener('click', () => {
        if (state.isSpinning || state.freeSpins.active) return;
        if (state.betIndex > 0) {
          state.betIndex--;
          updateControlsUI();
        }
      });

      btnBetPlus.addEventListener('click', () => {
        if (state.isSpinning || state.freeSpins.active) return;
        if (state.betIndex < BET_STEPS.length - 1) {
          state.betIndex++;
          updateControlsUI();
        }
      });

      // Bonus Buy flow
      const bonusBuyModal = document.getElementById('bonusbuy-modal');
      btnBonusBuy.addEventListener('click', () => {
        if (state.isSpinning || state.freeSpins.active) return;
        const cost = getCurrentBet() * BONUS_BUY_MULTIPLIER;
        if (state.balance < cost) return;
        document.getElementById('modal-buy-cost').textContent = formatDKK(cost);
        bonusBuyModal.classList.remove('hidden');
      });

      document.getElementById('btn-cancel-buy').addEventListener('click', () => {
        bonusBuyModal.classList.add('hidden');
      });

      document.getElementById('btn-confirm-buy').addEventListener('click', () => {
        const cost = getCurrentBet() * BONUS_BUY_MULTIPLIER;
        if (state.balance < cost || state.isSpinning || state.freeSpins.active) return;

        // Træk bonusprisen (selve udløserspinnet kræver ikke ekstra indsats)
        state.balance = Math.round((state.balance - cost + getCurrentBet()) * 100) / 100;
        state.forceBonusNextSpin = true;
        bonusBuyModal.classList.add('hidden');
        executeSpin();
      });

      // Lyd til/fra
      btnSound.addEventListener('click', () => {
        audio.enabled = !audio.enabled;
        document.getElementById('sound-icon').textContent = audio.enabled ? '🔊' : '🔇';
        document.getElementById('sound-label').textContent = audio.enabled ? 'Lyd: Til' : 'Lyd: Fra';
        if (audio.enabled) audio.playReelStop(2);
      });

      // Gevinsttabel modal
      const paytableModal = document.getElementById('paytable-modal');
      btnPaytable.addEventListener('click', () => {
        renderPaytable();
        paytableModal.classList.remove('hidden');
      });

      document.getElementById('btn-close-paytable').addEventListener('click', () => {
        paytableModal.classList.add('hidden');
      });

      // Mellemrumstast som genvej til SPIN
      window.addEventListener('keydown', (e) => {
        if (e.code === 'Space') {
          const anyModalOpen =
            !document.getElementById('bigwin-overlay').classList.contains('hidden') ||
            !document.getElementById('freespins-modal').classList.contains('hidden') ||
            !bonusBuyModal.classList.contains('hidden') ||
            !paytableModal.classList.contains('hidden');

          if (!anyModalOpen && !state.isSpinning) {
            e.preventDefault();
            executeSpin();
          }
        }
      });

      /* ---------------------------------------------------------
         11. OPSTART AF DEMO
         --------------------------------------------------------- */
      initFireflies();
      buildBoardDOM();
      generateInitialBoard();
      renderBoard(false);
      updateControlsUI();
    })();
- [ ]   </script>
</body>
</html>