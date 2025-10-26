

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta name="theme-color" content="#ffabc0">
  <title>Asude için</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg1:#ffd7e6;
      --bg2:#ffb6d0;
      --card:#ffffffee;
      --accent:#ff6f9a;
      --text:#5a2a3a;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
      background: linear-gradient(180deg,var(--bg1) 0%, var(--bg2) 100%);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      overflow-x:hidden;
      color:var(--text);
      display:flex;
      align-items:center;
      justify-content:center;
      padding:24px;
    }

    /* Floating hearts container - full screen */
    .hearts {
      position:fixed;
      inset:0;
      pointer-events:none;
      overflow:hidden;
      z-index:0;
    }
    .heart{
      position:absolute;
      bottom:-80px;
      width:28px;
      height:28px;
      transform:translateX(0) rotate(0deg);
      opacity:0.9;
      animation: floatUp linear infinite;
      will-change:transform,opacity;
      filter:drop-shadow(0 6px 12px rgba(0,0,0,0.06));
    }
    .heart svg{width:100%;height:100%;display:block}

    @keyframes floatUp{
      0%{transform:translateY(0) scale(0.9) rotate(0deg);opacity:0}
      5%{opacity:1}
      50%{transform:translateY(-45vh) scale(1) rotate(15deg)}
      100%{transform:translateY(-120vh) scale(1.15) rotate(-10deg);opacity:0}
    }

    /* Card */
    .card{
      position:relative;
      z-index:2;
      width:100%;
      max-width:520px;
      background:var(--card);
      border-radius:18px;
      padding:20px 18px;
      box-shadow:0 8px 30px rgba(107,17,58,0.12);
      backdrop-filter: blur(6px);
      border:1px solid rgba(255,255,255,0.6);
    }
    .heading{
      font-family:'Playfair Display', serif;
      font-size:28px;
      margin:6px 0 2px;
      color: #3d1224;
      letter-spacing:0.2px;
    }
    .sub{
      font-size:14px;
      color:#6a3341;
      margin-bottom:14px;
    }
    .poem{
      background:linear-gradient(180deg, rgba(255,255,255,0.6), rgba(255,255,255,0.45));
      padding:14px;
      border-radius:12px;
      border:1px solid rgba(255,255,255,0.6);
      font-style:italic;
      line-height:1.5;
      color:#4a1e2b;
      box-shadow: inset 0 -6px 18px rgba(255,182,199,0.08);
    }
    .poem p{margin:0 0 10px}

    .cta{
      display:flex;
      gap:10px;
      margin-top:14px;
    }
    .btn{
      flex:1;
      text-align:center;
      padding:12px 14px;
      border-radius:12px;
      font-weight:600;
      font-size:15px;
      cursor:pointer;
      border:0;
      color:white;
      background: linear-gradient(90deg,var(--accent),#ff3b7a);
      box-shadow:0 8px 20px rgba(255,105,150,0.18);
    }

    .note{font-size:12px;color:#7b4350;margin-top:10px}

    /* Responsive text sizing for small phones */
    @media (max-width:360px){
      .heading{font-size:22px}
      .card{padding:16px}
      .poem{font-size:14px}
    }
  </style>
</head>
<body>
  <div class="hearts" aria-hidden="true"></div>

  <main class="card" role="main">
    <h1 class="heading">Asude'ye</h1>
    <div class="sub">Gözlerde bahar, kalpte huzur. Yumuşacık bir pembe günün ortasında sana birkaç kelime...</div>

    <div class="poem" id="poem">
      <p>Asude, adın rüzgârda saklı bir melodi;
      Gülüşün sabahın en tatlı vaadi.
      Ellerim ellerinde durur sevinçle,
      Her bakışın kalbimde yeni bir şenlikle.</p>

      <p>Gecenin pembe düşlerinde sen olurken,
      Beyaz kalpler göğe doğru uçar, usul usul.
      Sen yanımda olmasan bile, bir umutla,
      Her adımda senin adını fısıldar dudaklarım — usul usul.</p>
    </div>

    <div class="cta">
    </button>
    </div>
    <div class="note"> </div>
  </main>

  <script>
    // --- Hearts generator ---
    const heartsContainer = document.querySelector('.hearts');
    const heartSVG = (color = '#fff') => `
      <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <path fill="${color}" d="M12 21s-7.5-4.9-9.5-8.3C-0.4 8.3 4.2 3 8.7 5.3 10.6 6.4 12 8.2 12 8.2s1.4-1.8 3.3-2.9c4.5-2.3 9.1 3 6.2 7.4C19.5 16.1 12 21 12 21z"/>
      </svg>`;

    // Create a bunch of hearts with randomized size, left position and speed
    function spawnHearts(count = 18){
      const colors = ['#ffffff','#fff1f5','#ffeef6','#fff'];
      for(let i=0;i<count;i++){
        const el = document.createElement('div');
        el.className = 'heart';
        const size = Math.round(18 + Math.random()*50); // 18 - 68px
        el.style.width = size + 'px';
        el.style.height = size + 'px';
        const left = Math.round(Math.random()*110) - 5; // -5% .. 105%
        el.style.left = left + '%';
        const delay = (Math.random()*6).toFixed(2);
        const dur = (8 + Math.random()*12).toFixed(2);
        el.style.animationDelay = `${delay}s`;
        el.style.animationDuration = `${dur}s`;
        el.style.opacity = (0.6 + Math.random()*0.4).toFixed(2);
        el.innerHTML = heartSVG(colors[Math.floor(Math.random()*colors.length)]);
        heartsContainer.appendChild(el);

        // Remove after animation cycle to keep DOM light
        setTimeout(()=>{
          if(el && el.parentNode) el.parentNode.removeChild(el);
        }, (parseFloat(delay) + parseFloat(dur) + 0.5) * 1000);
      }
    }

    // Initial spawn and repeated spawns to keep animation lively
    spawnHearts(22);
    setInterval(()=>spawnHearts(8), 3500);

    // --- Poem toggle ---
    function togglePoem(){
      const p = document.getElementById('poem');
      if(p.style.display === 'none') p.style.display = '';
      else p.style.display = 'block';
      // small haptic-like effect on supporting devices
      if (navigator.vibrate) navigator.vibrate(30);
    }

    // --- Simple share: copy poem text to clipboard ---
    async function share(){
      const text = document.getElementById('poem').innerText.trim();
      try{
        await navigator.clipboard.writeText(text);
        alert('Şiir panoya kopyalandı — istediğin yerde paylaşabilirsin.');
      }catch(e){
        // fallback
        const ta = document.createElement('textarea');
        ta.value = text; document.body.appendChild(ta); ta.select();
        try{ document.execCommand('copy'); alert('Şiir panoya kopyalandı — istediğin yerde paylaşabilirsin.'); }
        catch(err){ alert('Kopyalama başarısız. Şiiri seçip manuel kopyalayabilirsin.'); }
        ta.remove();
      }
    }

    // Accessibility: reduce motion respect
    const mq = window.matchMedia('(prefers-reduced-motion: reduce)');
    if(mq.matches){
      document.querySelectorAll('.heart').forEach(h=>h.style.animationDuration='0s');
    }
  </script>
</body>
</html>
