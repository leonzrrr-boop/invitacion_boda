<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bodas de Plata - Esthela & Enrique</title>
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Josefin+Sans:wght@100;300;400&family=Great+Vibes&display=swap" rel="stylesheet">
    <style>
        :root {
            --rosa:   #D6339A; 
            --rosa2:  #E879C5;
            --morado: #8A2BE2;
            --lila:   #B08AB0;
            --fondo:  #FAF5F0; 
            --texto:  #4A2A4A; 
            --suave:  #705070; 
            --crema:  #4A2A4A; 
            --tarjeta: rgba(214, 51, 154, 0.04); 
            --oro: #D4AF37;
        }

        * { margin:0; padding:0; box-sizing:border-box; }
        html { scroll-behavior:smooth; }

        body {
            background: var(--fondo);
            font-family: 'Josefin Sans', sans-serif;
            color: var(--texto);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* ── CANVAS PÉTALOS ── */
        #petals { position:fixed; inset:0; z-index:0; pointer-events:none; }

        /* ── ORBES FLOTANTES ── */
        .orbs { position:fixed; inset:0; z-index:0; pointer-events:none; overflow:hidden; }
        .orb  { position:absolute; border-radius:50%; filter:blur(90px); opacity:.08; } 
        .orb1 { width:520px;height:520px;background:#D6339A;top:-120px;left:-120px;
                 animation:orb-drift1 18s ease-in-out infinite alternate; }
        .orb2 { width:420px;height:420px;background:#8A2BE2;bottom:-100px;right:-100px;
                 animation:orb-drift2 22s ease-in-out infinite alternate; }
        .orb3 { width:320px;height:320px;background:#D6339A;top:42%;left:50%;
                 transform:translate(-50%,-50%);
                 animation:orb-drift3 14s ease-in-out infinite alternate; }
        @keyframes orb-drift1 { from{transform:translate(0,0) scale(1)} to{transform:translate(60px,40px) scale(1.15)} }
        @keyframes orb-drift2 { from{transform:translate(0,0) scale(1)} to{transform:translate(-50px,-30px) scale(1.2)} }
        @keyframes orb-drift3 { from{transform:translate(-50%,-50%) scale(1)} to{transform:translate(-45%,-55%) scale(1.3)} }

        /* ── ESTRELLAS ── */
        .stars-layer { position:fixed; inset:0; z-index:0; pointer-events:none; overflow:hidden; }
        .star {
            position:absolute; border-radius:50%; background:var(--rosa); 
            animation: twinkle var(--dur) ease-in-out infinite var(--delay);
        }
        @keyframes twinkle {
            0%,100%{ opacity:0; transform:scale(.5); }
            50%    { opacity:calc(var(--op) / 2); transform:scale(1); } 
        }

        /* ── WRAPPER ── */
        .page-wrapper { position:relative; z-index:1; display:flex; justify-content:center; padding:20px 16px 60px; }
        .container    { max-width:640px; width:100%; }

        /* ── REVEAL ── */
        .reveal { opacity:0; transform:translateY(40px); transition:opacity 1s cubic-bezier(.22,1,.36,1),transform 1s cubic-bezier(.22,1,.36,1); }
        .reveal.visible { opacity:1; transform:translateY(0); }
        .reveal-delay-1{transition-delay:.1s} .reveal-delay-2{transition-delay:.3s}
        .reveal-delay-3{transition-delay:.5s} .reveal-delay-4{transition-delay:.7s}
        .reveal-delay-5{transition-delay:.9s}

        /* ── HERO ── */
        .hero { text-align:center; padding:70px 20px 40px; position:relative; }

        .hero-ring {
            position:absolute; top:50%; left:50%; width:340px; height:340px;
            transform:translate(-50%,-45%); border-radius:50%;
            border:1px solid rgba(214, 51, 154, 0.2);
            animation:ring-spin 30s linear infinite; pointer-events:none;
        }
        .hero-ring::before {
            content:''; position:absolute; inset:-22px; border-radius:50%;
            border:1px dashed rgba(214, 51, 154, 0.1);
            animation:ring-spin 20s linear infinite reverse;
        }
        @keyframes ring-spin { to{transform:rotate(360deg)} }

        .aniversario-badge {
            display:inline-flex; align-items:center; gap:12px;
            font-size:.65rem; font-weight:300; letter-spacing:6px;
            color:var(--rosa); margin-bottom:8px;
            animation:badge-glow 3s ease-in-out infinite;
        }
        .aniversario-badge::before,.aniversario-badge::after {
            content:''; display:block; width:30px; height:1px;
            background:var(--rosa); opacity:.6;
        }
        @keyframes badge-glow {
            0%,100%{text-shadow:0 0 8px rgba(214, 51, 154,.3)}
            50%    {text-shadow:0 0 15px rgba(214, 51, 154,.5), 0 0 30px rgba(214, 51, 154,.2)}
        }

        .titulo-boda {
            font-size:.65rem; font-weight:100; letter-spacing:8px;
            color:var(--suave); margin-bottom:30px;
        }
        .typewriter-wrap {
            display:inline-block; overflow:hidden; border-right:2px solid var(--rosa);
            white-space:nowrap; max-width:0;
            animation:type-in 2.5s steps(22,end) 1.2s forwards, blink-caret .75s step-end infinite;
        }
        @keyframes type-in    { to{max-width:300px} }
        @keyframes blink-caret{ 50%{border-color:transparent} }

        .nombres {
            font-family:'Great Vibes',cursive;
            font-size:clamp(3.2rem,11vw,5.2rem); line-height:1.1; margin:10px 0;
            background:linear-gradient(135deg,var(--suave) 0%,var(--rosa) 35%,var(--texto) 55%,var(--rosa2) 80%,var(--morado) 100%);
            -webkit-background-clip:text; -webkit-text-fill-color:transparent;
            background-clip:text; background-size:300% auto;
            animation:shimmer-text 5s ease-in-out infinite;
            filter:drop-shadow(0 0 10px rgba(214, 51, 154,.2));
        }
        @keyframes shimmer-text {
            0%  {background-position:0% center}
            50% {background-position:100% center}
            100%{background-position:0% center}
        }

        .musica-link {
            display:inline-flex; align-items:center; gap:8px;
            margin:20px 0 10px; text-decoration:none;
            font-size:.65rem; letter-spacing:4px; font-weight:300; color:var(--suave);
            transition:color .3s,gap .3s,text-shadow .3s;
            position:relative; padding-bottom:6px;
            background: none; border: none; cursor: pointer;
            font-family: 'Josefin Sans', sans-serif;
        }
        .musica-link::after {
            content:''; position:absolute; bottom:0; left:50%;
            transform:translateX(-50%); width:0; height:1px;
            background:var(--rosa); transition:width .4s ease;
        }
        .musica-link:hover{color:var(--rosa);gap:14px;text-shadow:0 0 10px rgba(214, 51, 154,.4)}
        .musica-link:hover::after{width:100%}

        /* ── ORNAMENTO ── */
        .ornament { display:flex; align-items:center; gap:16px; margin:28px auto; max-width:320px; }
        .ornament-line {
            flex:1; height:1px;
            background:linear-gradient(90deg,transparent,var(--lila),transparent);
            animation:line-pulse 3s ease-in-out infinite;
        }
        @keyframes line-pulse { 0%,100%{opacity:.4} 50%{opacity:1} }
        .ornament-symbol { font-size:1.1rem; color:var(--rosa); animation:rotate-symbol 10s linear infinite; }
        @keyframes rotate-symbol { to{transform:rotate(360deg)} }

        /* ── PADRES ── */
        .padres-seccion { text-align:center; padding:10px 20px 30px; }
        .padres-label { font-size:.6rem; letter-spacing:5px; color:var(--suave); font-weight:300; margin-bottom:20px; font-style:italic; }
        .padres-grid  { display:flex; justify-content:center; gap:40px; flex-wrap:wrap; }
        .padre-item   { text-align:center; font-size:.75rem; color:var(--texto); line-height:1.8; font-weight:300; font-style:italic; }
        .padre-item strong { display:block; color:var(--rosa2); font-style:normal; font-weight:300; letter-spacing:2px; font-size:.65rem; margin-bottom:4px; }

        /* ── FECHA ── */
        .fecha-section { text-align:center; padding:40px 20px; }
        .fecha-grande { font-family:'Cormorant Garamond',serif; font-size:clamp(2rem,8vw,3.2rem); font-weight:300; letter-spacing:4px; color:var(--texto); line-height:1.3; }
        .fecha-numero {
            font-size:clamp(4rem,16vw,7rem); font-weight:600; line-height:.9; display:block;
            background:linear-gradient(180deg,rgba(214, 51, 154,.4) 0%,transparent 100%);
            -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text;
            -webkit-text-stroke:1px rgba(214, 51, 154,.4);
            animation:year-float 4s ease-in-out infinite;
        }
        @keyframes year-float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-8px)} }
        .horarios-row { display:flex; justify-content:center; gap:30px; margin-top:20px; flex-wrap:wrap; }
        .horario-item { font-size:.65rem; letter-spacing:4px; color:var(--suave); font-weight:300; position:relative; padding:0 15px; }
        .horario-item:not(:last-child)::after { content:'·'; position:absolute; right:-4px; top:50%; transform:translateY(-50%); color:var(--rosa); }

        /* ── COUNTDOWN ── */
        .countdown-strip { display:flex; justify-content:center; gap:10px; padding:20px 16px 30px; flex-wrap:wrap; }
        .countdown-item {
            text-align:center; min-width:68px; padding:16px 12px;
            border:1px solid rgba(214, 51, 154,.2); background:var(--tarjeta);
            position:relative; overflow:hidden;
            transition:border-color .3s,box-shadow .3s;
        }
        .countdown-item:hover { border-color:rgba(214, 51, 154,.4); box-shadow:0 0 15px rgba(214, 51, 154,.1); }
        .countdown-item::before {
            content:''; position:absolute; top:-50%; left:-50%; width:200%; height:200%;
            background:conic-gradient(transparent 270deg,rgba(214, 51, 154,.1) 360deg);
            animation:countdown-spin 4s linear infinite;
        }
        @keyframes countdown-spin { to{transform:rotate(360deg)} }
        .countdown-num {
            font-family:'Cormorant Garamond',serif; font-size:2rem; font-weight:300;
            color:var(--texto); line-height:1; display:block; position:relative; z-index:1;
            transition:transform .2s,color .2s;
        }
        .countdown-num.flip { animation:num-flip .35s ease; }
        @keyframes num-flip {
            0%  {transform:rotateX(0)}
            50% {transform:rotateX(90deg);color:var(--rosa)}
            100%{transform:rotateX(0)}
        }
        .countdown-label { font-size:.5rem; letter-spacing:3px; color:var(--suave); font-weight:300; display:block; margin-top:4px; position:relative; z-index:1; }

        /* ── NUEVAS UBICACIONES: SOBRE ELEGANTE ── */
        .ubicaciones { 
            display:grid; 
            grid-template-columns:1fr 1fr; 
            gap:40px; 
            padding:60px 16px 100px; 
        }

        .envelope-container {
            position: relative;
            height: 160px;
            width: 100%;
            cursor: pointer;
        }

        .envelope-base {
            position: relative;
            width: 100%;
            height: 100%;
            background: #fff;
            border-radius: 4px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.05);
            display: flex;
            align-items: flex-end;
            justify-content: center;
            padding-bottom: 20px;
            z-index: 2;
            border: 1px solid rgba(214, 51, 154, 0.1);
        }

        /* Solapas internas inferiores */
        .envelope-base::before {
            content: "";
            position: absolute;
            inset: 0;
            z-index: 5;
            background: 
                linear-gradient(35deg, #fff 48%, #f9f9f9 50%, transparent 50%),
                linear-gradient(-35deg, #fff 48%, #f9f9f9 50%, transparent 50%);
            background-size: 100% 100%;
            border-radius: 4px;
        }

        /* La solapa de arriba (triángulo) */
        .envelope-flap {
            position: absolute;
            top: 0;
            width: 100%;
            height: 100%;
            background: #fff;
            clip-path: polygon(0 0, 50% 60%, 100% 0);
            z-index: 10;
            transition: transform 0.6s ease, z-index 0.2s 0.3s;
            transform-origin: top;
            border-top: 1px solid rgba(214, 51, 154, 0.1);
        }

        /* Sello de lacre */
        .wax-seal {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -10%);
            width: 35px;
            height: 35px;
            background: radial-gradient(circle at 30% 30%, #f1d592, var(--oro));
            border-radius: 50%;
            z-index: 11;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2), inset 0 0 5px rgba(0,0,0,0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            color: rgba(255,255,255,0.6);
            font-size: 0.8rem;
            transition: opacity 0.3s, transform 0.6s ease;
        }

        /* Tarjeta interna */
        .letter-card {
            position: absolute;
            bottom: 10%;
            left: 5%;
            width: 90%;
            height: 120%;
            background: #fff;
            z-index: 1;
            padding: 20px 10px;
            text-align: center;
            transition: transform 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: 0 -5px 15px rgba(0,0,0,0.03);
            border: 1px solid rgba(214, 51, 154, 0.05);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
        }

        /* Animación Hover */
        .envelope-container:hover .envelope-flap {
            transform: rotateX(180deg);
            z-index: 0;
        }
        
        .envelope-container:hover .wax-seal {
            opacity: 0;
            transform: translate(-50%, -100%) rotateX(180deg);
        }

        .envelope-container:hover .letter-card {
            transform: translateY(-90px);
        }

        .envelope-base span {
            font-size: 0.6rem;
            letter-spacing: 3px;
            color: var(--suave);
            position: relative;
            z-index: 6;
        }

        .letter-card h3 {
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.1rem;
            color: var(--rosa);
            margin-bottom: 5px;
        }

        .letter-card p {
            font-size: 0.65rem;
            color: var(--suave);
            margin-bottom: 15px;
        }

        .btn-mapa {
            padding: 8px 15px;
            border: 1px solid var(--oro);
            color: var(--oro);
            text-decoration: none;
            font-size: 0.55rem;
            letter-spacing: 2px;
            transition: all 0.3s;
        }

        .btn-mapa:hover {
            background: var(--oro);
            color: #fff;
        }

        /* ── SORTEO ── */
        .sorteo-card {
            margin:0 16px 30px; padding:28px 24px;
            border:1px solid rgba(214, 51, 154,.15); text-align:center;
            position:relative; overflow:hidden;
            background:linear-gradient(135deg,rgba(214, 51, 154,.04),rgba(138, 43, 226,.04));
            animation:sorteo-pulse 4s ease-in-out infinite;
        }
        @keyframes sorteo-pulse {
            0%,100%{box-shadow:0 0 0 rgba(214, 51, 154,0);border-color:rgba(214, 51, 154,.15)}
            50%    {box-shadow:0 0 25px rgba(214, 51, 154,.1);border-color:rgba(214, 51, 154,.3)}
        }
        .sorteo-card::before {
            content:''; position:absolute; top:0; left:-100%; width:100%; height:100%;
            background:linear-gradient(90deg,transparent,rgba(214, 51, 154,.05),transparent);
            animation:sorteo-sweep 5s ease-in-out infinite;
        }
        @keyframes sorteo-sweep { 0%,100%{left:-100%} 50%{left:100%} }
        .sorteo-card h4 { font-weight:300; letter-spacing:6px; font-size:.7rem; color:var(--rosa); margin-bottom:12px; position:relative; z-index:1; }
        .sorteo-card p  { font-size:.8rem; color:var(--suave); font-weight:300; line-height:1.9; font-style:italic; position:relative; z-index:1; }

        /* ── DETALLES ── */
        .detalles { padding:0 16px 30px; display:flex; flex-direction:column; gap:12px; }
        .detalle-row {
            display:flex; align-items:flex-start; gap:16px; padding:14px 20px;
            border-left:2px solid rgba(214, 51, 154,.2); background:var(--tarjeta);
            transition:border-color .3s,background .3s,transform .3s;
        }
        .detalle-row:hover { border-color:rgba(214, 51, 154,.5); background:rgba(214, 51, 154,.06); transform:translateX(5px); }
        .detalle-label { font-size:.6rem; letter-spacing:4px; color:var(--rosa); font-weight:300; min-width:80px; }
        .detalle-valor { font-size:.78rem; color:var(--texto); font-weight:300; font-style:italic; }

        /* ── RSVP ── */
        .rsvp-section {
            margin:0 16px 30px; padding:36px 28px;
            border:1px solid rgba(214, 51, 154,.1); background:var(--tarjeta);
            position:relative; overflow:hidden;
        }
        .rsvp-section::before,.rsvp-section::after {
            content:''; position:absolute; width:40px; height:40px;
            transition:width .4s,height .4s;
        }
        .rsvp-section::before { top:0;left:0; border-top:2px solid rgba(214, 51, 154, .4); border-left:2px solid rgba(214, 51, 154, .4); }
        .rsvp-section::after  { bottom:0;right:0; border-bottom:2px solid rgba(138, 43, 226, .3); border-right:2px solid rgba(138, 43, 226, .3); }
        .rsvp-section:hover::before,.rsvp-section:hover::after { width:65px; height:65px; }
        .rsvp-section h3 { font-weight:100; letter-spacing:7px; font-size:.7rem; color:var(--suave); text-align:center; margin-bottom:24px; }
        .input-nombre {
            width:100%; padding:14px 16px; background:rgba(255,255,255,.5);
            border:1px solid rgba(214, 51, 154,.15); color:var(--texto);
            font-family:'Josefin Sans'; font-weight:300; font-size:.8rem; letter-spacing:2px;
            outline:none; transition:border-color .3s,box-shadow .3s; margin-bottom:16px;
        }
        .input-nombre::placeholder{color:rgba(112, 80, 112,.4)}
        .input-nombre:focus{border-color:rgba(214, 51, 154,.4);box-shadow:0 0 15px rgba(214, 51, 154, .08)}
        .btn-whatsapp {
            width:100%; padding:16px; background:transparent;
            border:1px solid rgba(37,211,102,.5); color:#25D366;
            font-family:'Josefin Sans'; font-weight:300; font-size:.65rem; letter-spacing:5px;
            cursor:pointer; position:relative; overflow:hidden;
            transition:letter-spacing .3s,box-shadow .3s,color .3s;
        }
        .btn-whatsapp::before {
            content:''; position:absolute; inset:0;
            background:linear-gradient(135deg,rgba(37,211,102,.08),rgba(37,211,102,.03));
            transform:scaleX(0); transform-origin:left; transition:transform .4s ease;
        }
        .btn-whatsapp:hover{letter-spacing:7px;color:#128C7E;box-shadow:0 0 20px rgba(37,211,102,.15)}
        .btn-whatsapp:hover::before{transform:scaleX(1)}

        /* ── FOOTER ── */
        footer { text-align:center; padding:20px; font-size:.65rem; letter-spacing:4px; color:rgba(112, 80, 112,.5); font-weight:100; font-style:italic; animation:footer-fade 6s ease-in-out infinite; }
        @keyframes footer-fade { 0%,100%{opacity:.5} 50%{opacity:1} }

        @media(max-width:420px){
            .ubicaciones{grid-template-columns:1fr; gap:120px;}
        }
    </style>
</head>
<body>

    <div class="orbs"><div class="orb orb1"></div><div class="orb orb2"></div><div class="orb orb3"></div></div>
    <div class="stars-layer" id="stars"></div>
    <canvas id="petals"></canvas>

    <div class="page-wrapper">
      <div class="container">

        <header class="hero reveal reveal-delay-1">
            <div class="hero-ring"></div>
            <div class="aniversario-badge">25 ANIVERSARIO</div>
            <div class="titulo-boda"><span class="typewriter-wrap">BODAS DE PLATA</span></div>
            <div class="nombres">Esthela & Enrique</div>
            
            <button id="play-btn" class="musica-link">
                <span id="btn-icon">▶</span>   <span id="btn-text">NUESTRA CANCIÓN</span>
            </button>
            <div id="player" style="display:none;"></div>
        </header>

        <div class="ornament reveal reveal-delay-2">
            <div class="ornament-line"></div><div class="ornament-symbol">✦</div><div class="ornament-line"></div>
        </div>

        <div class="padres-seccion reveal reveal-delay-2">
            <p class="padres-label">Con la bendición de nuestros padres</p>
            <div class="padres-grid">
                <div class="padre-item"><strong>Padres de Esthela</strong>Josefina y Pedro</div>
                <div class="padre-item"><strong>Padres de Enrique</strong>Amalia y Enrique</div>
            </div>
        </div>

        <section class="fecha-section reveal reveal-delay-3">
            <div class="fecha-grande">17 DE ABRIL</div>
            <span class="fecha-numero">2027</span>
            <div class="horarios-row">
                <span class="horario-item">MISA   5:00 PM</span>
                <span class="horario-item">RECEPCIÓN   6:30 PM</span>
            </div>
        </section>

        <div class="countdown-strip reveal reveal-delay-3">
            <div class="countdown-item"><span class="countdown-num" id="cd-dias">--</span><span class="countdown-label">DÍAS</span></div>
            <div class="countdown-item"><span class="countdown-num" id="cd-horas">--</span><span class="countdown-label">HORAS</span></div>
            <div class="countdown-item"><span class="countdown-num" id="cd-min">--</span><span class="countdown-label">MIN</span></div>
            <div class="countdown-item"><span class="countdown-num" id="cd-seg">--</span><span class="countdown-label">SEG</span></div>
        </div>

        <div class="ornament reveal reveal-delay-3">
            <div class="ornament-line"></div><div class="ornament-symbol">◈</div><div class="ornament-line"></div>
        </div>

        <div class="ubicaciones reveal reveal-delay-4">
            
            <div class="envelope-container">
                <div class="envelope-flap"></div>
                <div class="wax-seal">E&E</div>
                <div class="letter-card">
                    <h3>La Misa</h3>
                    <p>Acompáñanos a dar gracias</p>
                    <a href="https://maps.google.com" target="_blank" class="btn-mapa">ABRIR MAPA</a>
                </div>
                <div class="envelope-base">
                    <span>CEREMONIA</span>
                </div>
            </div>

            <div class="envelope-container">
                <div class="envelope-flap"></div>
                <div class="wax-seal">E&E</div>
                <div class="letter-card">
                    <h3>La Fiesta</h3>
                    <p>Celebremos juntos esta noche</p>
                    <a href="https://maps.google.com" target="_blank" class="btn-mapa">ABRIR MAPA</a>
                </div>
                <div class="envelope-base">
                    <span>RECEPCIÓN</span>
                </div>
            </div>

        </div>

        <div class="sorteo-card reveal reveal-delay-4">
            <h4>✦   SORTEO ESPECIAL   ✦</h4>
            <p>Habrá un sorteo con un premio sorpresa. Los boletos se otorgarán individualmente al inicio de la celebración eucarística en el templo. ¡No falten!</p>
        </div>

        <div class="detalles reveal reveal-delay-4">
            <div class="detalle-row"><span class="detalle-label">Vestimenta</span><span class="detalle-valor">Sin especificaciones — Siéntanse cómodos</span></div>
            <div class="detalle-row"><span class="detalle-label">Presente</span><span class="detalle-valor">Mesa de regalos o lluvia de sobres</span></div>
        </div>

        <section class="rsvp-section reveal reveal-delay-5">
            <h3>Confirmar Asistencia</h3>
            <input class="input-nombre" type="text" id="nombre_invitado" placeholder="Tu nombre completo...">
            <button class="btn-whatsapp" onclick="enviarWA()">Confirmar por WhatsApp</button>
        </section>

        <footer class="reveal reveal-delay-5">— Una historia de amor que continúa —</footer>

      </div>
    </div>

<script>
/* ESTRELLAS */
(function(){
    const layer=document.getElementById('stars');
    for(let i=0;i<90;i++){
        const s=document.createElement('div'); s.className='star';
        const sz=(Math.random()*2+.5).toFixed(1);
        const op=(Math.random()*.55+.15).toFixed(2);
        const dur=(Math.random()*4+2).toFixed(1)+'s';
        const del=(Math.random()*7).toFixed(1)+'s';
        s.style.cssText=`width:${sz}px;height:${sz}px;top:${Math.random()*100}%;left:${Math.random()*100}%;--dur:${dur};--delay:${del};--op:${op};`;
        layer.appendChild(s);
    }
})();

/* PÉTALOS */
(function(){
    const canvas=document.getElementById('petals');
    const ctx=canvas.getContext('2d');
    let W,H;
    const resize=()=>{W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight;};
    resize(); window.addEventListener('resize',resize);
    const COLS=['rgba(214, 51, 154,OP)','rgba(232, 121, 197,OP)','rgba(176, 138, 176,OP)','rgba(138, 43, 226,OP)','rgba(112, 80, 112,OP)'];
    class Petal{
        constructor(){this.reset(true);}
        reset(init){
            this.x=Math.random()*W; this.y=init?Math.random()*H:-20;
            this.r=Math.random()*6+3; this.vy=Math.random()*.7+.25;
            this.vx=(Math.random()-.5)*.5; this.rot=Math.random()*360;
            this.rv=(Math.random()-.5)*1.4; this.op=Math.random()*.2+.05; 
            this.color=COLS[Math.floor(Math.random()*COLS.length)].replace('OP',this.op);
            this.swing=Math.random()*Math.PI*2; this.swingS=Math.random()*.02+.005;
        }
        update(){
            this.swing+=this.swingS;
            this.x+=this.vx+Math.sin(this.swing)*.4; this.y+=this.vy; this.rot+=this.rv;
            if(this.y>H+20) this.reset(false);
        }
        draw(){
            ctx.save(); ctx.translate(this.x,this.y); ctx.rotate(this.rot*Math.PI/180);
            ctx.beginPath(); ctx.ellipse(0,0,this.r,this.r*.5,0,0,Math.PI*2);
            ctx.fillStyle=this.color; ctx.fill(); ctx.restore();
        }
    }
    const petals=Array.from({length:60},()=>new Petal());
    (function loop(){ ctx.clearRect(0,0,W,H); petals.forEach(p=>{p.update();p.draw();}); requestAnimationFrame(loop); })();
})();

/* SCROLL REVEAL */
const obs=new IntersectionObserver(entries=>{
    entries.forEach(e=>{if(e.isIntersecting)e.target.classList.add('visible');});
},{threshold:.1});
document.querySelectorAll('.reveal').forEach(el=>{
    obs.observe(el);
    if(el.getBoundingClientRect().top<window.innerHeight) el.classList.add('visible');
});

/* COUNTDOWN FLIP */
const prev={d:'',h:'',m:'',s:''};
function updateCountdown(){
    const diff=new Date('2027-04-17T17:00:00')-new Date();
    if(diff<=0){['cd-dias','cd-horas','cd-min','cd-seg'].forEach(id=>document.getElementById(id).textContent='00');return;}
    const d=String(Math.floor(diff/86400000)).padStart(2,'0');
    const h=String(Math.floor(diff%86400000/3600000)).padStart(2,'0');
    const m=String(Math.floor(diff%3600000/60000)).padStart(2,'0');
    const s=String(Math.floor(diff%60000/1000)).padStart(2,'0');
    [{id:'cd-dias',v:d,k:'d'},{id:'cd-horas',v:h,k:'h'},{id:'cd-min',v:m,k:'m'},{id:'cd-seg',v:s,k:'s'}].forEach(({id,v,k})=>{
        const el=document.getElementById(id);
        if(v!==prev[k]){ el.classList.remove('flip'); void el.offsetWidth; el.classList.add('flip'); el.textContent=v; prev[k]=v; }
    });
}
updateCountdown(); setInterval(updateCountdown,1000);

/* RSVP */
function enviarWA(){
    const tel="523121340598";
    const nombre=document.getElementById('nombre_invitado').value.trim();
    if(!nombre){
        const inp=document.getElementById('nombre_invitado');
        inp.style.borderColor='rgba(255,80,80,.5)'; inp.style.boxShadow='0 0 16px rgba(255,80,80,.2)';
        setTimeout(()=>{inp.style.borderColor='';inp.style.boxShadow='';},2000); return;
    }
    window.open(`https://wa.me/${tel}?text=${encodeURIComponent(`¡Hola Esthela y Enrique! Soy *${nombre}*. Confirmo mi asistencia para celebrar con ustedes sus Bodas de Plata. 🥂`)}`,'_blank');
}

/* --- INTEGRACIÓN DE MÚSICA --- */
var player;
var isPlaying = false;

var tag = document.createElement('script');
tag.src = "https://www.youtube.com/iframe_api";
var firstScriptTag = document.getElementsByTagName('script')[0];
firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

function onYouTubeIframeAPIReady() {
    player = new YT.Player('player', {
        height: '0',
        width: '0',
        videoId: 'm86SrMsjgP0',
        playerVars: {
            'autoplay': 0,
            'controls': 0
        },
        events: {
            'onReady': onPlayerReady
        }
    });
}

function onPlayerReady(event) {
    const playBtn = document.getElementById('play-btn');
    const btnIcon = document.getElementById('btn-icon');
    const btnText = document.getElementById('btn-text');

    playBtn.addEventListener('click', function() {
        if (!isPlaying) {
            player.playVideo();
            btnIcon.textContent = '⏸';
            btnText.textContent = 'PAUSAR MÚSICA';
            isPlaying = true;
        } else {
            player.pauseVideo();
            btnIcon.textContent = '▶';
            btnText.textContent = 'REPRODUCIR';
            isPlaying = false;
        }
    });
}
</script>
</body>
</html>
