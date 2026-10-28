<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Новогодний Корпоратив в Concert | Restaurant & Karaoke</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&family=Dancing+Script:wght@700&family=Great+Vibes&family=Montserrat:wght@300;400;500;600;700;800;900&family=Playfair+Display:ital,wght@0,700;1,600&display=swap" rel="stylesheet">
  <!-- FontAwesome Icons for festive elements -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- Canvas Confetti -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

  <style>
    :root {
      --gold-primary: #f2c76e;
      --gold-shine: #fff2b2;
      --gold-dark: #b8860b;
      --gold-gradient: linear-gradient(135deg, #eed083 0%, #f7e4a9 25%, #c5973b 50%, #fcf0be 75%, #a67623 100%);
      --red-festive: #c9182b;
      --red-glow: #e6283b;
    }

    body {
      font-family: 'Montserrat', sans-serif;
      background-color: #080709;
      color: #f7f7f7;
      overflow-x: hidden;
      touch-action: manipulation;
    }

    .font-script {
      font-family: 'Great Vibes', cursive;
    }

    .font-dancing {
      font-family: 'Dancing Script', cursive;
    }

    .font-serif-luxury {
      font-family: 'Playfair Display', serif;
    }

    /* Metallic Gold Text Effect matching the logo */
    .text-gold-metallic {
      background: linear-gradient(180deg, #fffbeb 0%, #fae69e 20%, #e0b448 45%, #9b6c16 70%, #fef3c7 85%, #84570d 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      text-shadow: 0 4px 18px rgba(224, 180, 72, 0.35);
      filter: drop-shadow(0 2px 4px rgba(0,0,0,0.6));
    }

    .font-serif-luxury {
      font-family: 'Playfair Display', serif;
    }

    /* Metallic Gold Text Effect */
    .text-gold-metallic {
      background: linear-gradient(180deg, #fff7c2 0%, #f0c365 30%, #bb8928 60%, #fae29c 85%, #8c5d0f 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      text-shadow: 0 0 25px rgba(240, 195, 101, 0.4);
    }

    .gold-border-glow {
      border: 1px solid rgba(242, 199, 110, 0.45);
      box-shadow: 0 0 20px rgba(223, 169, 58, 0.25), inset 0 0 15px rgba(223, 169, 58, 0.1);
    }

    .gold-box-shadow {
      box-shadow: 0 10px 30px -5px rgba(230, 40, 59, 0.4), 0 0 20px rgba(242, 199, 110, 0.35);
    }

    /* Background festive ambient */
    .radial-festive-bg {
      background: radial-gradient(circle at 50% 15%, rgba(184, 25, 41, 0.35) 0%, rgba(20, 10, 15, 0.85) 45%, #070709 80%);
    }

    /* Equalizer Pulse for sound icon */
    .sound-bar {
      transition: height 0.2s ease;
    }
    .playing .bar-1 { animation: soundPulse 0.8s infinite alternate 0.1s; }
    .playing .bar-2 { animation: soundPulse 0.8s infinite alternate 0.3s; }
    .playing .bar-3 { animation: soundPulse 0.8s infinite alternate 0.2s; }
    @keyframes soundPulse {
      0% { height: 4px; }
      100% { height: 18px; }
    }

    /* Subtle shimmer shine on ribbons and buttons */
    @keyframes goldShimmer {
      0% { background-position: -200% 0; }
      100% { background-position: 200% 0; }
    }
    .btn-gold-shimmer {
      background-size: 200% auto;
      background-image: linear-gradient(90deg, #c9182b 0%, #ff3b50 35%, #f2c76e 50%, #ff3b50 65%, #c9182b 100%);
      animation: goldShimmer 4s infinite linear;
    }

    /* Snow canvas overlay */
    #snow-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 40;
    }
  </style>
</head>
<body class="radial-festive-bg min-h-screen relative selection:bg-amber-500 selection:text-black">

  <!-- Interactive Snow Canvas -->
  <canvas id="snow-canvas"></canvas>

  <!-- Background Music Element -->
  <audio id="bgMusic" src="music.mp3" loop preload="auto"></audio>

  <!-- Ambient Light Orbs -->
  <div class="fixed top-0 left-1/2 -translate-x-1/2 w-[480px] h-[360px] bg-red-600/15 rounded-full blur-[110px] pointer-events-none -z-10"></div>
  <div class="fixed bottom-10 left-1/2 -translate-x-1/2 w-[380px] h-[280px] bg-amber-500/15 rounded-full blur-[90px] pointer-events-none -z-10"></div>

  <!-- Mobile Container Wrapper (Centered for desktop, native for smartphone) -->
  <div class="max-w-[480px] mx-auto min-h-screen bg-[#0d0c11]/90 backdrop-blur-md shadow-2xl relative border-x border-amber-500/20 pb-16">

    <!-- TOP BAR: Controls (Audio + Lang) -->
    <header class="sticky top-0 z-50 flex items-center justify-between px-5 py-3.5 bg-[#09080d]/85 backdrop-blur-md border-b border-amber-500/25">
      <!-- Music toggle button -->
      <button id="musicToggleBtn" class="flex items-center gap-2.5 px-3.5 py-1.5 rounded-full bg-gradient-to-r from-neutral-900 to-neutral-800 border border-amber-400/40 text-amber-300 hover:text-white transition-all shadow-md active:scale-95" title="Включить новогоднюю музыку">
        <div id="soundWaves" class="flex items-end gap-1 h-4 w-4 justify-center">
          <span class="sound-bar bar-1 w-1 bg-amber-400 rounded-full h-1"></span>
          <span class="sound-bar bar-2 w-1 bg-amber-400 rounded-full h-3"></span>
          <span class="sound-bar bar-3 w-1 bg-amber-400 rounded-full h-2"></span>
        </div>
        <span id="musicLabel" class="text-xs font-semibold tracking-wider">МУЗЫКА: ВЫКЛ</span>
      </button>

      <!-- Language selector toggle -->
      <div class="flex items-center bg-black/70 rounded-full p-1 border border-amber-500/30 text-xs font-bold">
        <button id="langRu" class="px-2.5 py-1 rounded-full bg-amber-400 text-black shadow transition-all">RU</button>
        <button id="langKz" class="px-2.5 py-1 rounded-full text-zinc-400 hover:text-white transition-all">KZ</button>
      </div>
    </header>

    <!-- HERO SECTION WITH RECREATED CONCERT LOGO -->
    <section class="pt-6 pb-4 px-6 text-center relative overflow-hidden">
      <!-- Garland / Sparkles decorative top -->
      <div class="flex justify-center items-center gap-2 text-amber-300/80 text-xs tracking-widest uppercase mb-4">
        <i class="fa-solid fa-sparkles text-amber-400 animate-pulse"></i>
        <span class="tracking-[0.25em] text-[11px] font-semibold">ПРЕМИАЛЬНЫЙ НОВЫЙ ГОД</span>
        <i class="fa-solid fa-sparkles text-amber-400 animate-pulse"></i>
      </div>

      <!-- ORIGINAL LOGO IMAGE (Direct file from user) -->
      <div class="flex flex-col items-center justify-center my-2 transform hover:scale-[1.02] transition-transform duration-500">
        <div class="w-full max-w-[290px] px-2 py-1 flex items-center justify-center">
          <img 
            src="logo.png" 
            alt="Concert Logo" 
            class="w-full h-auto object-contain drop-shadow-[0_10px_25px_rgba(224,180,72,0.4)]"
            id="mainLogo"
          >
        </div>
      </div>

      <!-- Festive Greeting Script (From poster) -->
      <div class="mt-4 mb-2 relative">
        <span class="text-4xl sm:text-5xl font-script text-white drop-shadow-[0_3px_10px_rgba(255,255,255,0.4)] flex items-center justify-center gap-2" id="greetText">
          Дорогие наши гости!
          <span class="text-red-500 text-3xl animate-bounce">♥</span>
        </span>
      </div>

      <!-- Main Headline with 3D feel and Santa Hat decoration -->
      <div class="bg-gradient-to-b from-black/85 via-neutral-900/90 to-red-950/40 p-5 rounded-3xl border border-amber-500/35 shadow-2xl mt-2 relative">
        
        <!-- Santa Hat SVG Accent positioned stylishly over the headline -->
        <div class="absolute -top-6 left-6 sm:left-10 w-12 h-12 transform -rotate-12 pointer-events-none drop-shadow-lg z-10">
          <svg viewBox="0 0 100 100" class="w-full h-full">
            <!-- Hat cone red -->
            <path d="M 20 80 Q 40 10, 78 30 Q 88 40, 92 60 Q 55 55, 20 80 Z" fill="#d91b2b"/>
            <path d="M 78 30 Q 95 35, 90 60" stroke="#b0101e" stroke-width="3" fill="none"/>
            <!-- Pom pom white ball -->
            <circle cx="92" cy="62" r="9" fill="#ffffff" stroke="#e5e5e5" stroke-width="1.5"/>
            <!-- White fur trim bottom -->
            <rect x="12" y="72" width="70" height="18" rx="9" fill="#ffffff" stroke="#e0e0e0" stroke-width="1"/>
            <circle cx="20" cy="81" r="7" fill="#ffffff"/>
            <circle cx="36" cy="81" r="7" fill="#ffffff"/>
            <circle cx="54" cy="81" r="7" fill="#ffffff"/>
            <circle cx="70" cy="81" r="7" fill="#ffffff"/>
          </svg>
        </div>

        <div class="inline-flex items-center gap-1.5 bg-red-600 text-white text-[11px] font-extrabold px-3.5 py-1 rounded-full uppercase tracking-wider shadow-md mb-2">
          <i class="fa-solid fa-bell text-[10px] animate-pulse"></i>
          <span id="badgeText">Пора бронировать</span>
        </div>
        
        <h2 class="text-2xl sm:text-3xl font-black uppercase text-gold-metallic leading-[1.15] tracking-wide mt-1" id="mainTitle">
          НОВОГОДНИЙ<br>КОРПОРАТИВ!
        </h2>
        
        <p class="text-xs sm:text-sm text-zinc-200 mt-3 font-medium leading-relaxed" id="subTitle">
          Подарите своей команде праздник, который запомнится надолго!
        </p>
      </div>
    </section>

    <!-- REAL-TIME COUNTDOWN TIMER -->
    <section class="px-5 my-4">
      <div class="bg-gradient-to-r from-neutral-900 via-neutral-950 to-neutral-900 rounded-2xl p-4 border border-amber-500/30 text-center shadow-lg relative">
        <p class="text-[11px] font-bold tracking-widest text-amber-300/80 uppercase mb-3 flex items-center justify-center gap-1.5">
          <i class="fa-regular fa-clock text-amber-400"></i>
          <span id="timerTitle">До Нового года осталось:</span>
        </p>
        
        <div class="grid grid-cols-4 gap-2">
          <!-- Days -->
          <div class="bg-black/60 rounded-xl p-2 border border-amber-400/20">
            <span id="t-days" class="text-xl sm:text-2xl font-black text-amber-300 block">00</span>
            <span class="text-[9px] uppercase tracking-wider text-zinc-400" id="lbl-days">Дней</span>
          </div>
          <!-- Hours -->
          <div class="bg-black/60 rounded-xl p-2 border border-amber-400/20">
            <span id="t-hours" class="text-xl sm:text-2xl font-black text-white block">00</span>
            <span class="text-[9px] uppercase tracking-wider text-zinc-400" id="lbl-hours">Часов</span>
          </div>
          <!-- Minutes -->
          <div class="bg-black/60 rounded-xl p-2 border border-amber-400/20">
            <span id="t-minutes" class="text-xl sm:text-2xl font-black text-white block">00</span>
            <span class="text-[9px] uppercase tracking-wider text-zinc-400" id="lbl-mins">Минут</span>
          </div>
          <!-- Seconds -->
          <div class="bg-black/60 rounded-xl p-2 border border-red-500/30 bg-red-950/20">
            <span id="t-seconds" class="text-xl sm:text-2xl font-black text-red-400 block animate-pulse">00</span>
            <span class="text-[9px] uppercase tracking-wider text-zinc-400" id="lbl-secs">Секунд</span>
          </div>
        </div>
      </div>
    </section>

    <!-- 3 KEY HIGHLIGHTS / PILLARS (From Poster) -->
    <section class="px-5 my-5">
      <div class="grid grid-cols-3 gap-2.5 text-center">
        <!-- Item 1: Cloche/Cuisine -->
        <div class="bg-gradient-to-b from-neutral-900 to-black p-3 rounded-2xl border border-amber-500/25 shadow-md flex flex-col items-center group hover:border-amber-400 transition-all">
          <div class="w-13 h-13 w-12 h-12 rounded-full border border-amber-400/70 flex items-center justify-center bg-gradient-to-tr from-amber-600/30 to-amber-300/10 mb-2 shadow-[0_0_12px_rgba(240,195,101,0.25)] group-hover:scale-110 transition-transform">
            <!-- Restaurant cloche icon matching poster -->
            <i class="fa-solid fa-bell-concierge text-amber-300 text-lg"></i>
          </div>
          <h4 class="text-[11px] sm:text-xs font-bold text-white uppercase leading-tight" id="feature1">Вкусная кухня</h4>
        </div>

        <!-- Item 2: Music note/Atmosphere -->
        <div class="bg-gradient-to-b from-neutral-900 to-black p-3 rounded-2xl border border-amber-500/25 shadow-md flex flex-col items-center group hover:border-amber-400 transition-all">
          <div class="w-12 h-12 rounded-full border border-amber-400/70 flex items-center justify-center bg-gradient-to-tr from-amber-600/30 to-amber-300/10 mb-2 shadow-[0_0_12px_rgba(240,195,101,0.25)] group-hover:scale-110 transition-transform">
            <i class="fa-solid fa-music text-amber-300 text-lg"></i>
          </div>
          <h4 class="text-[11px] sm:text-xs font-bold text-white uppercase leading-tight" id="feature2">Яркая атмосфера</h4>
        </div>

        <!-- Item 3: Star/Emotion -->
        <div class="bg-gradient-to-b from-neutral-900 to-black p-3 rounded-2xl border border-amber-500/25 shadow-md flex flex-col items-center group hover:border-amber-400 transition-all">
          <div class="w-12 h-12 rounded-full border border-amber-400/70 flex items-center justify-center bg-gradient-to-tr from-amber-600/30 to-amber-300/10 mb-2 shadow-[0_0_12px_rgba(240,195,101,0.25)] group-hover:scale-110 transition-transform">
            <i class="fa-solid fa-star text-amber-300 text-lg"></i>
          </div>
          <h4 class="text-[11px] sm:text-xs font-bold text-white uppercase leading-tight" id="feature3">Музыка и море эмоций</h4>
        </div>
      </div>
    </section>

    <!-- SPECIAL OFFER GIFT CARD (From Poster) -->
    <section class="px-5 my-5">
      <div class="relative overflow-hidden rounded-2xl bg-gradient-to-br from-red-950 via-neutral-900 to-black border-2 border-red-500/50 p-5 shadow-2xl">
        <!-- Festive Ribbon Tag -->
        <div class="absolute -right-12 top-6 rotate-45 bg-amber-400 text-black text-[9px] font-black uppercase py-1 px-12 tracking-widest shadow-md">
          VIP ПОДАРОК
        </div>

        <div class="flex items-center gap-4">
          <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-amber-400 to-amber-600 flex items-center justify-center text-3xl text-neutral-950 shadow-lg shrink-0 transform -rotate-6">
            🎁
          </div>
          <div>
            <div class="inline-block bg-red-600 text-white text-[10px] font-black px-2 py-0.5 rounded tracking-wide uppercase mb-1">
              СПЕЦИАЛЬНОЕ ПРЕДЛОЖЕНИЕ
            </div>
            <h3 class="text-lg font-black text-amber-300 uppercase leading-snug" id="giftTitle">
              ШОУ-ПРОГРАММА В ПОДАРОК!
            </h3>
            <p class="text-xs text-zinc-300 mt-1 italic font-script text-base text-amber-100" id="giftSub">
              «Мы будем рады вновь стать частью ваших праздничных традиций!»
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- URGENCY WARNING RIBBON -->
    <div class="px-5 mb-5">
      <div class="bg-gradient-to-r from-amber-500/20 via-amber-400/30 to-amber-500/20 border border-amber-400/50 rounded-xl p-3 text-center">
        <p class="text-xs font-bold text-amber-200 flex items-center justify-center gap-2">
          <span>★</span>
          <span id="urgentText">Не откладывайте — самые востребованные даты разбирают первыми!</span>
          <span>★</span>
        </p>
      </div>
    </div>

    <!-- INTERACTIVE RSVP & BOOKING CALCULATOR -->
    <section class="px-5 my-6" id="booking">
      <div class="bg-gradient-to-b from-neutral-900/90 to-black/95 rounded-3xl p-5 border border-amber-500/30 shadow-2xl">
        <div class="text-center mb-5">
          <span class="text-xs uppercase tracking-widest text-amber-400 font-bold">ОНЛАЙН-БРОНИРОВАНИЕ</span>
          <h3 class="text-xl font-black text-white mt-1" id="formHeader">Забронировать корпоратив</h3>
          <p class="text-xs text-zinc-400 mt-1" id="formSubheader">Заполните детали и мы моментально подготовим для вас персональный расчет в WhatsApp</p>
        </div>

        <form id="rsvpForm" class="space-y-4" onsubmit="event.preventDefault(); submitBooking();">
          <!-- Company or Guest Name -->
          <div>
            <label class="block text-xs font-semibold text-zinc-300 mb-1.5" id="lblCompany">Компания / Ваше имя:</label>
            <div class="relative">
              <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center text-zinc-500 text-sm">
                <i class="fa-regular fa-user"></i>
              </span>
              <input type="text" id="companyInput" required placeholder="Например: Kaspi Team или Айдар" 
                class="w-full pl-10 pr-3 py-2.5 bg-black/60 border border-neutral-700 focus:border-amber-400 rounded-xl text-sm text-white focus:outline-none transition-colors">
            </div>
          </div>

          <!-- Phone Number -->
          <div>
            <label class="block text-xs font-semibold text-zinc-300 mb-1.5" id="lblPhone">Номер телефона:</label>
            <div class="relative">
              <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center text-zinc-500 text-sm">
                <i class="fa-solid fa-phone"></i>
              </span>
              <input type="tel" id="phoneInput" required placeholder="+7 (___) ___-__-__" value="+7 "
                class="w-full pl-10 pr-3 py-2.5 bg-black/60 border border-neutral-700 focus:border-amber-400 rounded-xl text-sm text-white focus:outline-none transition-colors">
            </div>
          </div>

          <!-- Select Date -->
          <div>
            <label class="block text-xs font-semibold text-zinc-300 mb-1.5" id="lblDate">Желаемая дата корпоратива:</label>
            <div class="relative">
              <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center text-zinc-500 text-sm">
                <i class="fa-regular fa-calendar-check"></i>
              </span>
              <select id="dateSelect" class="w-full pl-10 pr-3 py-2.5 bg-black/60 border border-neutral-700 focus:border-amber-400 rounded-xl text-sm text-white focus:outline-none appearance-none">
                <option value="15 декабря 2026">15 декабря 2026 (Вторник)</option>
                <option value="16 декабря 2026">16 декабря 2026 (Среда)</option>
                <option value="17 декабря 2026">17 декабря 2026 (Четверг)</option>
                <option value="18 декабря 2026">18 декабря 2026 (Пятница)</option>
                <option value="19 декабря 2026">19 декабря 2026 (Суббота)</option>
                <option value="20 декабря 2026">20 декабря 2026 (Воскресенье)</option>
                <option value="21 декабря 2026">21 декабря 2026 (Понедельник)</option>
                <option value="22 декабря 2026">22 декабря 2026 (Вторник)</option>
                <option value="23 декабря 2026">23 декабря 2026 (Среда)</option>
                <option value="24 декабря 2026">24 декабря 2026 (Четверг)</option>
                <option value="25 декабря 2026">25 декабря 2026 (Пятница - Топ спрос!)</option>
                <option value="26 декабря 2026">26 декабря 2026 (Суббота - Топ спрос!)</option>
                <option value="27 декабря 2026">27 декабря 2026 (Воскресенье)</option>
                <option value="28 декабря 2026">28 декабря 2026 (Понедельник)</option>
                <option value="29 декабря 2026">29 декабря 2026 (Вторник)</option>
                <option value="30 декабря 2026">30 декабря 2026 (Среда)</option>
              </select>
            </div>
          </div>

          <!-- Number of Guests Counter -->
          <div>
            <div class="flex justify-between items-center mb-1.5">
              <label class="text-xs font-semibold text-zinc-300" id="lblGuests">Количество гостей:</label>
              <span id="guestCountDisplay" class="text-xs font-bold text-amber-300 px-2 py-0.5 rounded bg-amber-950/60 border border-amber-500/30">25 персон</span>
            </div>
            <input type="range" id="guestRange" min="1" max="150" step="1" value="25"
              class="w-full h-2 bg-neutral-800 rounded-lg appearance-none cursor-pointer accent-amber-400">
            <div class="flex justify-between text-[10px] text-zinc-500 mt-1">
              <span>от 1 чел.</span>
              <span>до 150 чел.</span>
            </div>
          </div>

          <!-- PRIMARY ACTION BUTTON (From Poster) -->
          <div class="pt-2">
            <button type="submit" 
              class="w-full btn-gold-shimmer py-4 px-5 rounded-2xl font-black text-sm uppercase tracking-wider text-white shadow-xl hover:scale-[1.02] active:scale-95 transition-all flex items-center justify-center gap-3 group">
              <i class="fa-brands fa-whatsapp text-2xl text-emerald-400"></i>
              <div class="text-left leading-tight">
                <div class="text-xs font-black" id="btnMainText">Напишите нам прямо сейчас</div>
                <div class="text-[10px] text-amber-200 font-normal">Забронировать корпоратив в WhatsApp &rarr;</div>
              </div>
            </button>
          </div>
        </form>

        <!-- Direct Phone Call Backup -->
        <div class="mt-3 text-center">
          <a href="tel:+77777772454" class="inline-flex items-center gap-2 text-xs font-semibold text-zinc-400 hover:text-amber-300 transition-colors">
            <i class="fa-solid fa-phone-volume text-amber-400"></i>
            <span>Позвонить банкетному менеджеру: <strong>+7 (777) 777-24-54</strong></span>
          </a>
        </div>
      </div>
    </section>

    <!-- LOCATION & CONTACTS SECTION -->
    <section class="px-5 my-6">
      <div class="bg-neutral-900/80 rounded-2xl p-5 border border-amber-500/20 text-center">
        <h4 class="text-sm font-bold uppercase tracking-wider text-amber-300 mb-2 flex items-center justify-center gap-2">
          <i class="fa-solid fa-location-dot text-red-500"></i>
          <span>Локация и заведение</span>
        </h4>

        <p class="text-base font-extrabold text-white">Ресторан-караоке «CONCERT»</p>
        <p class="text-xs text-zinc-300 mt-1">г. Караганда, пр. Нуркена Абдирова, 15/1</p>
        <p class="text-[11px] text-zinc-400 mt-0.5">Ежедневно: с 12:00 до 02:00</p>

        <!-- Direct 2GIS & Navigation Button -->
        <div class="mt-4 flex flex-col sm:flex-row gap-2">
          <a href="https://2gis.kz/karaganda/firm/70000001074421547" target="_blank" rel="noopener noreferrer" 
            class="flex-1 py-2.5 px-4 bg-emerald-600/20 hover:bg-emerald-600/30 text-emerald-300 border border-emerald-500/40 rounded-xl text-xs font-bold transition-all flex items-center justify-center gap-2">
            <span class="w-2 h-2 rounded-full bg-emerald-400 animate-ping"></span>
            <span>Открыть в 2GIS</span>
          </a>
          
          <a href="https://www.instagram.com/concert_krg/" target="_blank" rel="noopener noreferrer"
            class="py-2.5 px-4 bg-pink-600/20 hover:bg-pink-600/30 text-pink-300 border border-pink-500/40 rounded-xl text-xs font-bold transition-all flex items-center justify-center gap-2">
            <i class="fa-brands fa-instagram"></i>
            <span>Instagram @concert_krg</span>
          </a>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="text-center px-6 pt-4 pb-8 border-t border-white/5 text-zinc-500 text-xs">
      <p class="text-[11px]">© 2026 CONCERT Karaganda. Все права защищены.</p>
      <p class="text-[10px] mt-1 text-zinc-600">Создано для незабываемых новогодних праздников</p>
    </footer>

    <!-- STICKY BOTTOM QUICK ACTION BAR FOR MOBILE -->
    <div class="fixed bottom-0 left-1/2 -translate-x-1/2 w-full max-w-[480px] p-3 bg-neutral-950/90 backdrop-blur-md border-t border-amber-500/30 z-40 flex gap-2">
      <a href="tel:+77777772454" class="p-3 bg-neutral-900 hover:bg-neutral-800 text-amber-300 border border-amber-500/30 rounded-xl flex items-center justify-center text-lg active:scale-95 transition-all">
        <i class="fa-solid fa-phone"></i>
      </a>
      <a href="#booking" class="flex-1 py-3 px-4 btn-gold-shimmer rounded-xl text-white font-bold text-xs uppercase tracking-wider flex items-center justify-center gap-2 shadow-lg active:scale-95 transition-all">
        <i class="fa-brands fa-whatsapp text-emerald-300 text-lg"></i>
        <span>Забронировать дату</span>
      </a>
    </div>

  </div>

  <!-- JAVASCRIPT LOGIC: SNOW, AUDIO SYNTH, COUNTDOWN, TRANSLATION & WHATSAPP -->
  <script>
    /* ==========================================================
       1. MULTI-LANGUAGE DICTIONARY (RU / KZ)
       ========================================================== */
    const translations = {
      ru: {
        greetText: 'Дорогие наши гости! <span class="text-red-500 text-3xl animate-bounce">♥</span>',
        badgeText: 'Пора бронировать',
        mainTitle: 'НОВОГОДНИЙ<br>КОРПОРАТИВ!',
        subTitle: 'Подарите своей команде праздник, который запомнится надолго!',
        timerTitle: 'До Нового года осталось:',
        lblDays: 'Дней',
        lblHours: 'Часов',
        lblMins: 'Минут',
        lblSecs: 'Секунд',
        feature1: 'Вкусная кухня',
        feature2: 'Яркая атмосфера',
        feature3: 'Музыка и море эмоций',
        giftTitle: 'ШОУ-ПРОГРАММА В ПОДАРОК!',
        giftSub: '«Мы будем рады вновь стать частью ваших праздничных традиций!»',
        urgentText: 'Не откладывайте — самые востребованные даты разбирают первыми!',
        formHeader: 'Забронировать корпоратив',
        formSubheader: 'Заполните детали и мы моментально подготовим для вас расчет в WhatsApp',
        lblCompany: 'Компания / Ваше имя:',
        lblPhone: 'Номер телефона:',
        lblDate: 'Желаемая дата корпоратива:',
        lblGuests: 'Количество гостей:',
        btnMainText: 'Напишите нам прямо сейчас',
        musicOn: 'МУЗЫКА: ВКЛ',
        musicOff: 'МУЗЫКА: ВЫКЛ'
      },
      kz: {
        greetText: 'Құрметті қонақтарымыз! <span class="text-red-500 text-3xl animate-bounce">♥</span>',
        badgeText: 'Брондау уақыты келді',
        mainTitle: 'ЖАҢА ЖЫЛДЫҚ<br>КОРПОРАТИВ!',
        subTitle: 'Өз ұжымыңызға ұзақ уақыт есте қалатын ұмытылмас мереке сыйлаңыз!',
        timerTitle: 'Жаңа жылға дейін қалды:',
        lblDays: 'Күн',
        lblHours: 'Сағат',
        lblMins: 'Минут',
        lblSecs: 'Секунд',
        feature1: 'Дәмді асхана',
        feature2: 'Жарқын атмосфера',
        feature3: 'Музыка мен мол эмоция',
        giftTitle: 'ШОУ-БАҒДАРЛАМА СЫЙЛЫҚҚА!',
        giftSub: '«Мерекелік дәстүріңіздің бір бөлшегі болуға әрқашан қуаныштымыз!»',
        urgentText: 'Кейінге қалдырмаңыз — ең сұранысқа ие күндер тез брондалады!',
        formHeader: 'Корпоративті брондау',
        formSubheader: 'Ақпаратты толтырыңыз, менеджеріміз WhatsApp арқылы дереу жауап береді',
        lblCompany: 'Компания немесе Есіміңіз:',
        lblPhone: 'Телефон нөміріңіз:',
        lblDate: 'Мереке өтетін күн:',
        lblGuests: 'Қонақтар саны:',
        btnMainText: 'Дәл қазір жазыңыз',
        musicOn: 'ӘУЕН: ҚОСУЛЫ',
        musicOff: 'ӘУЕН: ӨШІРУЛІ'
      }
    };

    let currentLang = 'ru';

    function setLanguage(lang) {
      currentLang = lang;
      const t = translations[lang];

      document.getElementById('greetText').innerHTML = t.greetText;
      document.getElementById('badgeText').innerText = t.badgeText;
      document.getElementById('mainTitle').innerHTML = t.mainTitle;
      document.getElementById('subTitle').innerText = t.subTitle;
      document.getElementById('timerTitle').innerText = t.timerTitle;
      document.getElementById('lbl-days').innerText = t.lblDays;
      document.getElementById('lbl-hours').innerText = t.lblHours;
      document.getElementById('lbl-mins').innerText = t.lblMins;
      document.getElementById('lbl-secs').innerText = t.lblSecs;
      document.getElementById('feature1').innerText = t.feature1;
      document.getElementById('feature2').innerText = t.feature2;
      document.getElementById('feature3').innerText = t.feature3;
      document.getElementById('giftTitle').innerText = t.giftTitle;
      document.getElementById('giftSub').innerText = t.giftSub;
      document.getElementById('urgentText').innerText = t.urgentText;
      document.getElementById('formHeader').innerText = t.formHeader;
      document.getElementById('formSubheader').innerText = t.formSubheader;
      document.getElementById('lblCompany').innerText = t.lblCompany;
      document.getElementById('lblPhone').innerText = t.lblPhone;
      document.getElementById('lblDate').innerText = t.lblDate;
      document.getElementById('lblGuests').innerText = t.lblGuests;
      document.getElementById('btnMainText').innerText = t.btnMainText;

      const musicLabel = document.getElementById('musicLabel');
      musicLabel.innerText = isPlayingAudio ? t.musicOn : t.musicOff;

      if(lang === 'ru') {
        document.getElementById('langRu').className = "px-2.5 py-1 rounded-full bg-amber-400 text-black shadow transition-all";
        document.getElementById('langKz').className = "px-2.5 py-1 rounded-full text-zinc-400 hover:text-white transition-all";
      } else {
        document.getElementById('langKz').className = "px-2.5 py-1 rounded-full bg-amber-400 text-black shadow transition-all";
        document.getElementById('langRu').className = "px-2.5 py-1 rounded-full text-zinc-400 hover:text-white transition-all";
      }
    }

    document.getElementById('langRu').addEventListener('click', () => setLanguage('ru'));
    document.getElementById('langKz').addEventListener('click', () => setLanguage('kz'));

    /* ==========================================================
       2. COUNTDOWN TIMER LOGIC
       ========================================================== */
    // Targets January 1, 2027 (Midnight)
    const targetDate = new Date(2027, 0, 1, 0, 0, 0).getTime();

    function updateCountdown() {
      const now = new Date().getTime();
      let diff = targetDate - now;

      if (diff <= 0) {
        diff = 0;
      }

      const days = Math.floor(diff / (1000 * 60 * 60 * 24));
      const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((diff % (1000 * 60)) / 1000);

      document.getElementById('t-days').innerText = String(days).padStart(2, '0');
      document.getElementById('t-hours').innerText = String(hours).padStart(2, '0');
      document.getElementById('t-minutes').innerText = String(minutes).padStart(2, '0');
      document.getElementById('t-seconds').innerText = String(seconds).padStart(2, '0');
    }
    setInterval(updateCountdown, 1000);
    updateCountdown();

    /* ==========================================================
       3. GUEST RANGE SLIDER SYNCHRONIZATION
       ========================================================== */
    const guestRange = document.getElementById('guestRange');
    const guestDisplay = document.getElementById('guestCountDisplay');
    guestRange.addEventListener('input', (e) => {
      guestDisplay.innerText = `${e.target.value} персон`;
    });

    /* ==========================================================
       4. WHATSAPP RSVP RESERVATION SUBMISSION
       ========================================================== */
    function submitBooking() {
      const company = document.getElementById('companyInput').value.trim();
      const phone = document.getElementById('phoneInput').value.trim();
      const date = document.getElementById('dateSelect').value;
      const guests = guestRange.value;

      // Confetti celebratory burst
      confetti({
        particleCount: 80,
        spread: 60,
        origin: { y: 0.7 },
        colors: ['#f2c76e', '#e6283b', '#ffffff', '#22c55e']
      });

      // Construct customized WhatsApp message
      const rawMessage = `🎄 *Заявка на Новогодний Корпоратив в Concert!*\n\n` +
        `👤 *Организатор / Компания:* ${company}\n` +
        `📞 *Телефон:* ${phone}\n` +
        `🗓️ *Желаемая дата:* ${date}\n` +
        `👥 *Количество гостей:* ${guests} персон\n` +
        `🎁 *Спецпредложение:* Шоу-программа в подарок!\n\n` +
        `Здравствуйте! Хотим забронировать свободную дату и получить персональный расчет меню.`;
        
      const message = encodeURIComponent(rawMessage);

      // Concert manager phone in Karaganda
      const managerWhatsApp = "77777772454";

      setTimeout(() => {
        window.open(`https://wa.me/${managerWhatsApp}?text=${message}`, '_blank');
      }, 300);
    }

    /* ==========================================================
       5. INTERACTIVE AMBIENT SOUND (MP3 Audio)
       ========================================================== */
    let isPlayingAudio = false;
    const bgMusic = document.getElementById('bgMusic');

    function toggleAudio() {
      const btn = document.getElementById('musicToggleBtn');
      const soundWaves = document.getElementById('soundWaves');
      const label = document.getElementById('musicLabel');

      if (isPlayingAudio) {
        bgMusic.pause();
        isPlayingAudio = false;
        soundWaves.classList.remove('playing');
        label.innerText = currentLang === 'ru' ? 'МУЗЫКА: ВЫКЛ' : 'ӘУЕН: ӨШІРУЛІ';
        btn.classList.remove('border-emerald-400');
      } else {
        bgMusic.play().then(() => {
          isPlayingAudio = true;
          soundWaves.classList.add('playing');
          label.innerText = currentLang === 'ru' ? 'МУЗЫКА: ВКЛ' : 'ӘУЕН: ҚОСУЛЫ';
          btn.classList.add('border-emerald-400');
        }).catch(err => {
          console.error("Ошибка воспроизведения аудио (возможно, заблокировано браузером):", err);
        });
      }
    }

    document.getElementById('musicToggleBtn').addEventListener('click', toggleAudio);

    /* ==========================================================
       6. FALLING SNOW PARTICLES (Smooth Canvas Effect)
       ========================================================== */
    const canvas = document.getElementById('snow-canvas');
    const ctx = canvas.getContext('2d');
    let width = (canvas.width = window.innerWidth);
    let height = (canvas.height = window.innerHeight);

    window.addEventListener('resize', () => {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    });

    const flakes = [];
    const numFlakes = 50;

    for (let i = 0; i < numFlakes; i++) {
      flakes.push({
        x: Math.random() * width,
        y: Math.random() * height,
        r: Math.random() * 2.5 + 1,
        d: Math.random() * numFlakes,
        opacity: Math.random() * 0.7 + 0.3,
        speed: Math.random() * 0.8 + 0.4
      });
    }

    let angle = 0;
    function renderSnow() {
      ctx.clearRect(0, 0, width, height);
      ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';
      angle += 0.01;

      for (let i = 0; i < numFlakes; i++) {
        const p = flakes[i];
        p.y += p.speed;
        p.x += Math.sin(angle + p.d) * 0.4;

        if (p.y > height) {
          flakes[i] = {
            x: Math.random() * width,
            y: -10,
            r: p.r,
            d: p.d,
            opacity: p.opacity,
            speed: p.speed
          };
        }

        ctx.beginPath();
        ctx.fillStyle = `rgba(255, 255, 255, ${p.opacity})`;
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2, false);
        ctx.fill();
      }

      requestAnimationFrame(renderSnow);
    }
    requestAnimationFrame(renderSnow);
  </script>
</body>
</html>
