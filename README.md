<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>OBBY NEXUS - MEGA ULTIMATE EDITION (EASY MODE V8.0)</title>
    <style>
        /* ========================================
           CORE UI DESIGN & THEME ENGINE (ORIGINAL)
           ======================================== */
        :root {
            --bg-dark: #0f172a; --bg-light: #1e293b; --accent: #38bdf8;
            --panel-bg: rgba(30, 41, 59, 0.98); --text-main: #f8fafc;
            --text-muted: #94a3b8; --danger: #ef4444; --success: #22c55e;
            --gold: #fbbf24;
            --term-green: #00ff41; --term-bg: rgba(0, 5, 10, 0.95);
        }

        body {
            background: radial-gradient(circle at top right, var(--bg-light) 0%, var(--bg-dark) 100%);
            color: var(--text-main); font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex; flex-direction: column; align-items: center; justify-content: flex-start;
            margin: 0; height: 100vh; overflow: hidden; transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            touch-action: none;
        }

        #game-canvas { position: absolute; top: 0; left: 0; z-index: 1; display: none; }

        /* --- MATRIX INTRO & HACKER CONSOLE --- */
        #intro-screen {
            position: fixed; inset: 0; background: #000; z-index: 99999;
            display: flex; flex-direction: column; align-items: flex-start; justify-content: flex-end;
            padding: 40px; font-family: 'Courier New', Courier, monospace; color: var(--term-green);
        }
        .intro-log { font-size: 22px; margin-bottom: 10px; text-shadow: 0 0 10px var(--term-green); }

        #dev-console {
            position: fixed; top: -100%; left: 0; width: 100%; height: 50vh;
            background: var(--term-bg); border-bottom: 4px solid var(--term-green);
            z-index: 50000; transition: top 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex; flex-direction: column; font-family: 'Courier New', Courier, monospace;
            box-shadow: 0 20px 50px rgba(0,0,0,0.8);
        }
        #console-output {
            flex: 1; padding: 20px; overflow-y: auto; color: var(--term-green);
            font-size: 18px; text-shadow: 0 0 5px var(--term-green); display: flex; flex-direction: column; gap: 5px;
        }
        .console-input-line { display: flex; padding: 10px 20px; background: rgba(0,255,65,0.1); border-top: 1px solid var(--term-green); }
        .console-prefix { color: #fff; margin-right: 10px; font-size: 20px; font-weight: bold; }
        #console-input { background: transparent; border: none; color: #fff; font-size: 20px; width: 100%; outline: none; font-family: 'Courier New', Courier, monospace; }
        .sys-msg { color: var(--accent); } .err-msg { color: var(--danger); text-shadow: 0 0 5px var(--danger); } .success-msg { color: var(--gold); }
        .dev-trigger { position: fixed; bottom: 10px; right: 10px; color: rgba(255,255,255,0.2); font-size: 14px; cursor: pointer; z-index: 10000; font-family: monospace; font-weight: bold; }
        .dev-trigger:hover { color: rgba(255,255,255,0.8); text-shadow: 0 0 10px #fff; }

        /* --- RANK UI --- */
        .rank-container {
            background: rgba(15, 23, 42, 0.9); border: 3px solid var(--accent); padding: 15px 40px; 
            border-radius: 20px; text-align: center; box-shadow: 0 0 25px rgba(56, 189, 248, 0.3); width: 350px; z-index: 20;
        }
        .rank-title { color: var(--accent); font-size: 14px; font-weight: bold; letter-spacing: 3px; margin-bottom: 5px; text-transform: uppercase; }
        #rank-name-ui { font-size: 32px; font-weight: 900; color: #fff; text-shadow: 0 0 10px #fff; margin-bottom: 10px; letter-spacing: 2px;}
        .xp-bar-bg { width: 100%; height: 12px; background: #334155; border-radius: 6px; overflow: hidden; border: 1px solid #64748b; }
        #xp-bar-fill { width: 0%; height: 100%; background: var(--gold); transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1); box-shadow: 0 0 15px var(--gold); }
        #xp-text-ui { font-size: 14px; color: #94a3b8; margin-top: 8px; font-weight: bold; }

        /* --- MENÜ SİSTEMİ EKRANLARI --- */
        .screen { display: none; width: 100%; height: 100%; flex-direction: column; align-items: center; padding-top: 40px; position: absolute; inset: 0; background: rgba(15, 23, 42, 0.95); backdrop-filter: blur(25px); overflow-y: auto; z-index: 10; }
        #main-menu { display: flex; z-index: 20; }

        .menu-header { text-align: center; margin-bottom: 30px; animation: slideDown 0.5s ease; }
        @keyframes slideDown { from { transform: translateY(-30px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        .menu-title { font-size: 60px; color: var(--accent); letter-spacing: 5px; text-shadow: 0 0 20px var(--accent); margin: 0; font-weight: 900; }
        .menu-sub { color: var(--text-muted); font-size: 18px; text-transform: uppercase; letter-spacing: 5px; font-weight: bold; }

        /* BUTONLAR */
        .big-btn { background: var(--panel-bg); border: 3px solid var(--accent); border-radius: 20px; color: #fff; padding: 20px 40px; font-size: 24px; font-weight: 900; letter-spacing: 2px; cursor: pointer; transition: 0.3s; width: 400px; margin-bottom: 15px; text-transform: uppercase; box-shadow: 0 8px 0 rgba(0,0,0,0.3); }
        .big-btn:hover { background: var(--accent); color: #000; box-shadow: 0 0 30px var(--accent); transform: translateY(-5px); }
        .big-btn:active { transform: translateY(2px); box-shadow: none; }
        .back-btn { background: transparent; border: 2px solid #64748b; color: #94a3b8; margin-top: 20px; width: 300px; box-shadow: none; }
        .back-btn:hover { background: #64748b; color: #fff; box-shadow: 0 0 15px #64748b; transform: none; }

        .settings-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; max-width: 600px; width: 100%; }
        .mod-btn { background: #1e293b; border: 2px solid var(--accent); border-radius: 15px; color: #fff; padding: 20px; cursor: pointer; font-weight: 900; font-size: 18px; transition: 0.3s; text-transform: uppercase; }
        .mod-btn:hover, .mod-btn.active { background: var(--accent); color: #000; box-shadow: 0 0 20px var(--accent); }

        /* --- OYUN İÇİ ARAYÜZ (HUD) --- */
        #game-ui { display: none; position: absolute; inset: 0; z-index: 5; pointer-events: none; }
        .ui-top { position: absolute; top: 25px; left: 25px; display: flex; gap: 15px; pointer-events: auto;}
        .nav-btn { padding: 12px 25px; border-radius: 12px; border: none; font-weight: 900; cursor: pointer; transition: 0.2s; background: #475569; color: white;}
        .nav-btn:hover { background: var(--danger); }
        
        .hud-stats { position: absolute; top: 20px; right: 20px; background: rgba(0, 0, 0, 0.7); padding: 15px 25px; border-radius: 12px; border: 2px solid #f39c12; color: white; font-size: 18px; font-weight: bold;}
        .hud-stats span { color: #f1c40f; }

        #crosshair { position: absolute; top: 50%; left: 50%; width: 8px; height: 8px; background-color: rgba(255, 255, 255, 0.9); border-radius: 50%; transform: translate(-50%, -50%); }

        /* MOBİL KONTROLLER (YAN EKRAN VE DOKUNMATİK DESTEĞİ DÜZELTİLDİ) */
        #mobile-controls { display: none; position: absolute; bottom: 20px; left: 0; width: 100%; pointer-events: none; z-index: 60; }
        .d-pad { position: absolute; left: 20px; bottom: 10px; width: 150px; height: 150px; }
        .m-btn {
            position: absolute; width: 50px; height: 50px; background: rgba(255,255,255,0.2);
            border: 2px solid rgba(255,255,255,0.5); border-radius: 10px;
            display: flex; align-items: center; justify-content: center; font-size: 20px;
            color: #fff; pointer-events: auto; user-select: none;
        }
        .m-btn:active { background: rgba(255,255,255,0.5); }
        #btn-up { top: 0; left: 50px; } #btn-down { bottom: 0; left: 50px; }
        #btn-left { top: 50px; left: 0; } #btn-right { top: 50px; right: 0; }
        #btn-jump { position: absolute; right: 30px; bottom: 30px; width: 70px; height: 70px; border-radius: 50%; font-weight: bold; background: rgba(34, 197, 94, 0.4); border-color: var(--success); pointer-events: auto; }

        @media (max-width: 1024px), (max-height: 500px), (hover: none) and (pointer: coarse) { 
            #mobile-controls { display: block; } 
            #crosshair { display: none; } 
        }

        /* RANK UP MODAL */
        #rank-up-modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.95); z-index: 99999; flex-direction: column; align-items: center; justify-content: center; text-align: center; padding: 50px; }
        .end-title { font-size: 90px; color: var(--gold); text-shadow: 0 0 50px var(--gold); animation: popOut 0.5s reverse forwards; margin-bottom: 20px; }
        #new-rank-text { font-size: 60px; color: #fff; font-weight: 900; margin-bottom: 30px; text-transform: uppercase; }
        @keyframes popOut { 0% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.5); filter: brightness(2); } 100% { transform: scale(0); opacity: 0; } }

        /* SHARHACK */
        #sharhack-top-btn {
            display: none; position: fixed; top: 10px; left: 50%; transform: translateX(-50%);
            background: #000; border: 2px solid #e74c3c; color: #e74c3c; padding: 10px 30px;
            font-family: 'Courier New', Courier, monospace; font-weight: bold; font-size: 20px;
            border-radius: 5px; cursor: pointer; z-index: 10000; box-shadow: 0 0 20px rgba(231, 76, 60, 0.5);
            pointer-events: auto; animation: pulseRed 2s infinite;
        }
        #sharhack-top-btn:hover { background: #e74c3c; color: #000; }
        @keyframes pulseRed { 0% { box-shadow: 0 0 10px #e74c3c; } 50% { box-shadow: 0 0 30px #e74c3c; } 100% { box-shadow: 0 0 10px #e74c3c; } }

        #hackMenu {
            position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%);
            background: rgba(10, 10, 10, 0.95); border: 2px solid #e74c3c; border-radius: 8px;
            color: #e74c3c; display: none; z-index: 10001; width: 350px; font-family: 'Courier New', Courier, monospace;
            box-shadow: 0 0 50px rgba(231, 76, 60, 0.8); pointer-events: auto; backdrop-filter: blur(5px);
        }
        #hackMenu .header { background: #e74c3c; color: #000; padding: 15px; text-align: center; font-weight: bold; font-size: 22px; }
        #hackMenu .content { padding: 20px; text-align: left; }
        #hackMenu label { display: block; margin-bottom: 15px; font-size: 18px; cursor: pointer; color: #fff;}
        #hackMenu input[type="checkbox"] { transform: scale(1.5); margin-right: 10px; accent-color: #e74c3c; }
        #closeHackBtn { width: 100%; padding: 10px; margin-top: 10px; background: #c0392b; color: white; border: none; font-size: 16px; cursor: pointer; font-weight: bold; border-radius: 5px; }

        /* Toast Bildirimi */
        #toast { position: fixed; top: 30%; left: 50%; transform: translate(-50%, -50%); background: transparent; color: var(--gold); font-size: 60px; font-weight: 900; text-shadow: 0 0 20px #000; display: none; z-index: 9999; text-align: center; }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

<canvas id="game-canvas"></canvas>

<div id="intro-screen">
    <div id="intro-container"></div>
</div>

<div id="dev-console">
    <div id="console-output"></div>
    <div class="console-input-line" id="console-line">
        <span class="console-prefix">root@nexus:~#</span>
        <input type="text" id="console-input" autocomplete="off" spellcheck="false" placeholder="Enter command...">
    </div>
</div>
<div class="dev-trigger" onclick="toggleConsole()">v8.0.0_build(OBBY_FIXED)</div>

<div id="main-menu" class="screen">
    <div class="menu-header">
        <h1 class="menu-title">OBBY NEXUS</h1>
        <span class="menu-sub">EASY MEGA EDITION</span>
    </div>
    
    <div class="rank-container" style="margin-bottom: 30px;">
        <div class="rank-title">CS2 RANK SYSTEM</div>
        <div id="rank-name-ui">🥈 SILVER I</div>
        <div class="xp-bar-bg"><div id="xp-bar-fill"></div></div>
        <div id="xp-text-ui">0 / 400 XP</div>
    </div>

    <button class="big-btn" onclick="showScreen('level-menu')">▶ START GAME</button>
    <button class="big-btn" onclick="showScreen('settings-menu')">⚙️ SETTINGS</button>
    <button class="big-btn" onclick="toggleConsole()" style="border-color: var(--term-green); color: var(--term-green);">💻 SECRET CONSOLE</button>
    
    <button class="big-btn" onclick="toggleFullScreen()" style="border-color: #22c55e; color: #22c55e; margin-top: 15px;">🔲 FULLSCREEN</button>
    
    <p style="color: var(--text-muted); margin-top: 20px; font-weight: bold; text-align: center;">
        When you complete the game 5 times, the system will give you<br>a special secret cheat code from the console.
    </p>
</div>

<div id="level-menu" class="screen">
    <div class="menu-header"><h1 class="menu-title">LEVEL SELECTION</h1></div>
    <button class="big-btn" onclick="startGame(1)">🟩 CLASSIC OBBY</button>
    <button class="big-btn" onclick="startGame(2)" style="border-color: #ef4444; color: #ef4444;">🌋 LAVA RUN (NEED HACK)</button>
    <button class="big-btn" onclick="startGame(3)" style="border-color: #a855f7; color: #a855f7;">🌌 NEON PARKOUR (NEED HACK)</button>
    <button class="big-btn" onclick="startGame(4)" style="border-color: #fbbf24; color: #fbbf24;">🗼 THE TOWER</button>
    <button class="big-btn back-btn" onclick="showScreen('main-menu')">GO BACK</button>
</div>

<div id="settings-menu" class="screen">
    <div class="menu-header"><h1 class="menu-title">SYSTEM SETTINGS</h1></div>
    <div class="settings-grid">
        <button class="mod-btn active" id="btn-sens-low" onclick="setSens(0.002, 'low')">🖱️ Low Sensitivity</button>
        <button class="mod-btn" id="btn-sens-high" onclick="setSens(0.005, 'high')">🖱️ High Sensitivity</button>
        <button class="mod-btn active" id="btn-shadow-on" onclick="setShadow(true)">💡 Shadows ON</button>
        <button class="mod-btn" id="btn-shadow-off" onclick="setShadow(false)">💡 Shadows OFF</button>
    </div>
    <button class="big-btn back-btn" onclick="showScreen('main-menu')" style="margin-top: 40px;">GO BACK</button>
</div>

<div id="game-ui">
    <div class="ui-top">
        <button class="nav-btn" onclick="exitGame()">ESC - QUIT</button>
        <button class="nav-btn" onclick="toggleFullScreen()">🔲 FULLSCREEN</button>
    </div>
    <div class="hud-stats">Wins: <span id="ui-wins">0</span>/5 | Coins: <span id="ui-coins">0</span></div>
    <div id="crosshair"></div>
</div>

<div id="mobile-controls">
    <div class="d-pad">
        <div class="m-btn" id="btn-up">W</div>
        <div class="m-btn" id="btn-down">S</div>
        <div class="m-btn" id="btn-left">A</div>
        <div class="m-btn" id="btn-right">D</div>
    </div>
    <div class="m-btn" id="btn-jump">JUMP</div>
</div>

<div id="rank-up-modal">
    <h1 class="end-title">RANK UP!</h1>
    <div id="new-rank-text">🌟 GOLD NOVA I</div>
    <button class="big-btn" onclick="document.getElementById('rank-up-modal').style.display='none'" style="border-color: var(--gold); color: var(--gold);">CONTINUE</button>
</div>

<button id="sharhack-top-btn" onclick="toggleHackMenu()">☢️ DİCKHACK V1.1 ☢️</button>
<div id="hackMenu">
    <div class="header">☢️ DİCKHACK V1.1 ☢️</div>
    <div class="content">
        <label><input type="checkbox" id="cbGodMode"> God Mode (Disable Lava Damage)</label>
        <label><input type="checkbox" id="cbFlyMode"> Fly Mode (Fly - Space/Shift)</label>
        <label><input type="checkbox" id="cbSpeed"> Speed Hack (x3 Speed)</label>
        <label><input type="checkbox" id="cbJump"> Mega Jump (Jump Hack)</label>
        <button id="closeHackBtn" onclick="toggleHackMenu()">Hide / Back to Game</button>
    </div>
</div>

<div id="toast">Notification!</div>

<script>
    /* ========================================
       FULLSCREEN SYSTEM
       ======================================== */
    function toggleFullScreen() {
        if (!document.fullscreenElement) {
            document.documentElement.requestFullscreen().catch(err => {
                console.log(`Error attempting to enable full-screen mode: ${err.message}`);
            });
        } else {
            if (document.exitFullscreen) {
                document.exitFullscreen();
            }
        }
    }

    /* ========================================
       RANK SYSTEM (CS2)
       ======================================== */
    const RANKS = [
        { name: "SILVER I", icon: "🥈", xp: 0 },
        { name: "SILVER II", icon: "🥈", xp: 400 },
        { name: "SILVER III", icon: "🥈", xp: 800 },
        { name: "SILVER IV", icon: "🥈", xp: 1200 },
        { name: "SILVER ELITE", icon: "🥈", xp: 1600 },
        { name: "GOLD NOVA I", icon: "🌟", xp: 2000 }
    ];
    let RANK_STATE = { xp: 0, level: 0 };

    function addXP(amount) {
        if(RANK_STATE.level >= RANKS.length - 1) return;
        RANK_STATE.xp += amount;
        
        let nextRank = RANKS[RANK_STATE.level + 1];
        if(RANK_STATE.xp >= nextRank.xp) {
            RANK_STATE.level++;
            showRankUpModal();
        }
        updateRankUI();
    }

    function updateRankUI() {
        let current = RANKS[RANK_STATE.level];
        let next = RANKS[RANK_STATE.level + 1];
        document.getElementById('rank-name-ui').innerText = current.icon + " " + current.name;
        
        if(!next) {
            document.getElementById('xp-bar-fill').style.width = "100%";
            document.getElementById('xp-text-ui').innerText = "MAX RANK!";
            document.getElementById('xp-text-ui').style.color = "var(--gold)";
        } else {
            let range = next.xp - current.xp;
            let progress = RANK_STATE.xp - current.xp;
            let pct = (progress / range) * 100;
            document.getElementById('xp-bar-fill').style.width = pct + "%";
            document.getElementById('xp-text-ui').innerText = `${progress} / ${range} XP`;
        }
    }

    function showRankUpModal() {
        document.getElementById('rank-up-modal').style.display = 'flex';
        document.getElementById('new-rank-text').innerText = RANKS[RANK_STATE.level].icon + " " + RANKS[RANK_STATE.level].name;
    }

    /* ========================================
       UI, CONSOLE AND PASSWORD LOGIC
       ======================================== */
    let SYS = { open: false };

    function playIntro() {
        const c = document.getElementById('intro-container');
        const msgs = ["[SYSTEM]: Obby Engine Booting...", "[SYSTEM]: Physics calibrated to Easy Mode...", "[SYSTEM]: Integrating Rank Network...", "[OK]: Ready Player One."];
        let delay = 0;
        msgs.forEach(m => { setTimeout(() => { let p = document.createElement('div'); p.className='intro-log'; p.innerText=m; c.appendChild(p); }, delay); delay += 400; });
        setTimeout(() => { document.getElementById('intro-screen').style.display = 'none'; document.getElementById('main-menu').style.display = 'flex'; updateRankUI(); }, delay + 500);
    }

    function showScreen(id) { document.querySelectorAll('.screen').forEach(el => el.style.display = 'none'); document.getElementById(id).style.display = 'flex'; }

    function toggleConsole() {
        SYS.open = !SYS.open;
        const con = document.getElementById('dev-console');
        const inp = document.getElementById('console-input');
        if(SYS.open) { con.style.top = '0'; inp.focus(); if(isGameRunning) document.exitPointerLock(); } 
        else { con.style.top = '-100%'; inp.blur(); }
    }

    function printConsole(txt, cls="") {
        const out = document.getElementById('console-output');
        const div = document.createElement('div'); div.className = cls; div.innerText = "> " + txt;
        out.appendChild(div); out.scrollTop = out.scrollHeight;
    }

    document.addEventListener('keydown', (e) => {
        if((e.key === '`' || e.key === 'é' || e.key === 'Dead') && !isGameRunning) { e.preventDefault(); toggleConsole(); }
    });

    document.getElementById('console-input').addEventListener('keydown', function(e) {
        if(e.key === 'Enter') {
            let val = this.value.trim(); this.value = ''; if(val === "") return;
            printConsole(val, "");
            if(val === "/attribute game=generic[baseset=devmod] @s") {
                printConsole("PASSWORD ACCEPTED! SHARHACK V1.1 ACTIVE.", "success-msg");
                document.getElementById('sharhack-top-btn').style.display = 'block'; 
                showToast("HACK ACTIVE!");
            } else if (val === "clear") { document.getElementById('console-output').innerHTML = '';
            } else { printConsole("Invalid password or command.", "err-msg"); }
        }
    });

    function toggleHackMenu() {
        const hm = document.getElementById('hackMenu');
        if(hm.style.display === 'block') { hm.style.display = 'none'; if(isGameRunning) document.body.requestPointerLock(); } 
        else { document.exitPointerLock(); hm.style.display = 'block'; }
    }

    function showToast(msg) {
        const t = document.getElementById('toast');
        t.innerText = msg; t.style.display = 'block'; t.style.animation = 'popOut 1.5s forwards';
        setTimeout(() => { t.style.display = 'none'; t.style.animation = ''; }, 1500);
    }

    /* ========================================
       SETTINGS
       ======================================== */
    let GAME_SETTINGS = { sens: 0.002, shadows: true };
    function setSens(val, id) { GAME_SETTINGS.sens = val; document.getElementById('btn-sens-low').classList.remove('active'); document.getElementById('btn-sens-high').classList.remove('active'); document.getElementById('btn-sens-'+id).classList.add('active'); }
    function setShadow(val) { GAME_SETTINGS.shadows = val; renderer.shadowMap.enabled = val; document.getElementById('btn-shadow-on').classList.remove('active'); document.getElementById('btn-shadow-off').classList.remove('active'); if(val) document.getElementById('btn-shadow-on').classList.add('active'); else document.getElementById('btn-shadow-off').classList.add('active'); }

    /* ========================================
       THREE.JS GAME ENGINE & CONTROLS
       ======================================== */
    const canvas = document.getElementById('game-canvas');
    const scene = new THREE.Scene();
    scene.fog = new THREE.FogExp2(0x0f172a, 0.015);
    scene.background = new THREE.Color(0x0f172a); 

    const camera = new THREE.PerspectiveCamera(70, window.innerWidth / window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.shadowMap.enabled = true; renderer.shadowMap.type = THREE.PCFSoftShadowMap;

    const ambientLight = new THREE.AmbientLight(0xffffff, 0.6); scene.add(ambientLight);
    const dirLight = new THREE.DirectionalLight(0xffffff, 0.8); dirLight.position.set(20, 60, 20); dirLight.castShadow = true; dirLight.shadow.mapSize.width = 2048; dirLight.shadow.mapSize.height = 2048; scene.add(dirLight);

    const playerSize = 1;
    const playerGeo = new THREE.BoxGeometry(playerSize, playerSize, playerSize);
    const playerMat = new THREE.MeshStandardMaterial({ color: 0x38bdf8, roughness: 0.4 });
    const player = new THREE.Mesh(playerGeo, playerMat);
    player.castShadow = true; scene.add(player);

    let isGameRunning = false; let currentLevel = 1; 
    let gameWins = 0; let coinsCollected = 0;
    let velocity = { x: 0, y: 0, z: 0 }; let isGrounded = false; let isOnMovingPlatform = false; let platformVelocity = { x: 0, y: 0, z: 0 };
    
    let cameraYaw = 0; let cameraPitch = 0; let cameraDistance = 5; 

    // EASY MODE PHYSICS:
    const baseSpeed = 0.16;
    const baseJump = 0.36;  
    const gravity = -0.015; 
    
    let platforms = []; let coins = [];

    const keys = { W:false, A:false, S:false, D:false, Space:false };
    
    // PC Keyboard
    document.addEventListener('keydown', (e) => {
        if(e.code==='KeyW'||e.code==='ArrowUp') keys.W = true;
        if(e.code==='KeyS'||e.code==='ArrowDown') keys.S = true;
        if(e.code==='KeyA'||e.code==='ArrowLeft') keys.A = true;
        if(e.code==='KeyD'||e.code==='ArrowRight') keys.D = true;
        if(e.code==='Space') keys.Space = true;
    });
    document.addEventListener('keyup', (e) => {
        if(e.code==='KeyW'||e.code==='ArrowUp') keys.W = false;
        if(e.code==='KeyS'||e.code==='ArrowDown') keys.S = false;
        if(e.code==='KeyA'||e.code==='ArrowLeft') keys.A = false;
        if(e.code==='KeyD'||e.code==='ArrowRight') keys.D = false;
        if(e.code==='Space') keys.Space = false;
    });

    // MOBILE TOUCH CONTROLS
    const bindBtn = (id, key) => {
        const btn = document.getElementById(id);
        btn.addEventListener('touchstart', (e) => { e.preventDefault(); keys[key] = true; btn.style.background='rgba(255,255,255,0.6)'; });
        btn.addEventListener('touchend', (e) => { e.preventDefault(); keys[key] = false; btn.style.background='rgba(255,255,255,0.2)'; });
    };
    bindBtn('btn-up', 'W'); bindBtn('btn-down', 'S');
    bindBtn('btn-left', 'A'); bindBtn('btn-right', 'D');
    
    const jumpBtn = document.getElementById('btn-jump');
    jumpBtn.addEventListener('touchstart', (e) => { e.preventDefault(); keys.Space = true; jumpBtn.style.transform='scale(0.9)'; });
    jumpBtn.addEventListener('touchend', (e) => { e.preventDefault(); keys.Space = false; jumpBtn.style.transform='scale(1)'; });

    // PC Mouse (Pointer Lock)
    document.addEventListener('mousemove', (e) => {
        if (isGameRunning && document.pointerLockElement === document.body) {
            cameraYaw -= e.movementX * GAME_SETTINGS.sens;
            cameraPitch += e.movementY * GAME_SETTINGS.sens; 
            cameraPitch = Math.max(-1.5, Math.min(1.5, cameraPitch)); 
        }
    });
    document.addEventListener('wheel', (e) => {
        if (isGameRunning && document.pointerLockElement === document.body) {
            cameraDistance += e.deltaY * 0.01; cameraDistance = Math.max(0, Math.min(15, cameraDistance)); 
            if(cameraDistance < 1) document.getElementById('crosshair').style.display = 'block';
            else document.getElementById('crosshair').style.display = 'none';
        }
    });
    document.addEventListener('pointerlockchange', () => {
        if (document.pointerLockElement === document.body) { isGameRunning = true; } 
        else { if(document.getElementById('hackMenu').style.display !== 'block' && !SYS.open) exitGame(); }
    });

    // Mobile Camera Drag
    let lastTouchX = 0, lastTouchY = 0;
    document.addEventListener('touchstart', (e) => {
        if(e.target.tagName !== 'DIV' && !e.target.classList.contains('m-btn') && isGameRunning) { lastTouchX = e.touches[0].clientX; lastTouchY = e.touches[0].clientY; }
    });
    document.addEventListener('touchmove', (e) => {
        if(e.target.tagName !== 'DIV' && !e.target.classList.contains('m-btn') && isGameRunning && !SYS.open) {
            let dx = e.touches[0].clientX - lastTouchX; let dy = e.touches[0].clientY - lastTouchY;
            cameraYaw -= dx * 0.005; cameraPitch += dy * 0.005;
            cameraPitch = Math.max(-1.5, Math.min(1.5, cameraPitch));
            lastTouchX = e.touches[0].clientX; lastTouchY = e.touches[0].clientY;
        }
    });

    // --- LEVEL MANAGEMENT ---
    function clearLevel() { platforms.forEach(p => scene.remove(p.mesh)); coins.forEach(c => scene.remove(c.mesh)); platforms = []; coins = []; coinsCollected = 0; updateUI(); }

    function createPlatform(x, y, z, w, h, d, color, type, moveRange = 0, moveAxis = 'x', moveSpeed = 2) {
        const mat = new THREE.MeshStandardMaterial({ color: color, roughness: 0.7, metalness: 0.1 });
        if(color === 0xa855f7 || color === 0x00ffff) mat.emissive = new THREE.Color(color).multiplyScalar(0.3); 
        const mesh = new THREE.Mesh(new THREE.BoxGeometry(w, h, d), mat);
        mesh.position.set(x, y, z); mesh.receiveShadow = true; mesh.castShadow = true; scene.add(mesh);
        platforms.push({ mesh: mesh, type: type, yTop: y + (h/2), moveRange: moveRange, moveAxis: moveAxis, moveSpeed: moveSpeed, startX: x, startZ: z });
    }
    function createCoin(x, y, z) {
        const mesh = new THREE.Mesh(new THREE.CylinderGeometry(0.3, 0.3, 0.1, 16), new THREE.MeshStandardMaterial({ color: 0xfbbf24, metalness: 0.8 }));
        mesh.position.set(x, y, z); mesh.rotation.x = Math.PI / 2; mesh.castShadow = true; scene.add(mesh); coins.push({ mesh: mesh, collected: false });
    }

    function loadLevel(levelId) {
        clearLevel(); currentLevel = levelId;
        scene.background = new THREE.Color(0x0f172a); scene.fog.color.setHex(0x0f172a);

        if(levelId === 1) { 
            // CLASSIC OBBY
            createPlatform(0, 0, 0, 6, 1, 6, 0x1e293b, 'normal'); 
            createPlatform(0, 1, -8, 4, 1, 4, 0x334155, 'normal'); createCoin(0, 2, -8);
            createPlatform(0, 2, -15, 3, 1, 3, 0x334155, 'normal');
            createPlatform(0, 3, -22, 3, 1, 3, 0x334155, 'normal'); createCoin(0, 4, -22);
            
            createPlatform(0, 3, -32, 5, 1, 5, 0x38bdf8, 'moving', 5, 'x', 1.0);
            createPlatform(0, 3, -42, 5, 1, 5, 0x38bdf8, 'moving', -5, 'x', 1.0); createCoin(0, 4, -42);
            
            createPlatform(0, 3, -56, 2.5, 1, 16, 0x1e293b, 'normal'); createCoin(0, 4, -56);
            
            createPlatform(0, 4.5, -68, 3, 1, 3, 0x334155, 'normal');
            createPlatform(0, 6.0, -76, 3, 1, 3, 0x334155, 'normal');
            createPlatform(0, 7.5, -84, 3, 1, 3, 0x334155, 'normal');
            
            createPlatform(0, 7.5, -95, 8, 1, 8, 0x22c55e, 'finish');
            createPlatform(0, -5, -45, 150, 1, 150, 0xef4444, 'lava');

        } else if(levelId === 2) { 
            // LAVA RUN
            scene.background = new THREE.Color(0x2a0808); scene.fog.color.setHex(0x2a0808);
            createPlatform(0, 0, 0, 6, 1, 6, 0x1e293b, 'normal');
            createPlatform(0, 0, -12, 4, 1, 4, 0xd97706, 'moving', 6, 'x', 1.5); createCoin(0, 1, -12);
            createPlatform(-6, 1, -24, 3, 1, 3, 0xd97706, 'moving', 5, 'z', 1.2);
            createPlatform(6, 2, -36, 3, 1, 3, 0xd97706, 'moving', 5, 'z', 1.2);
            createPlatform(0, 3, -48, 3, 1, 3, 0x334155, 'normal');
            createPlatform(0, 3, -62, 4, 1, 4, 0xef4444, 'moving', 8, 'x', 2.0); 
            createPlatform(0, 3, -76, 8, 1, 8, 0x22c55e, 'finish');
            createPlatform(0, -2, -40, 150, 1, 150, 0xef4444, 'lava'); 

        } else if(levelId === 3) { 
            // NEON PARKOUR
            scene.background = new THREE.Color(0x000000); scene.fog.color.setHex(0x000000);
            createPlatform(0, 0, 0, 5, 1, 5, 0x1e293b, 'normal');
            createPlatform(0, 2, -10, 3, 0.5, 3, 0xa855f7, 'normal'); createCoin(0, 3, -10);
            createPlatform(-5, 4, -18, 3, 0.5, 3, 0x00ffff, 'normal');
            createPlatform(5, 6, -26, 3, 0.5, 3, 0xa855f7, 'normal');
            createPlatform(0, 8, -34, 3, 0.5, 3, 0x00ffff, 'normal');
            createPlatform(0, 8, -46, 4, 0.5, 4, 0xa855f7, 'moving', 6, 'x', 1.2); createCoin(0, 9, -46);
            
            createPlatform(-5, 9, -58, 3, 0.5, 3, 0x00ffff, 'moving', 4, 'z', 1.5);
            createPlatform(5, 10, -70, 3, 0.5, 3, 0xa855f7, 'moving', 4, 'z', 1.5);
            createPlatform(0, 11, -82, 4, 0.5, 4, 0x00ffff, 'normal');
            
            createPlatform(0, 11, -95, 6, 1, 6, 0x22c55e, 'finish');

        } else if(levelId === 4) { 
            // THE TOWER
            createPlatform(0, 0, 0, 10, 1, 10, 0x1e293b, 'normal'); 
            let height = 0;
            for(let i=1; i<=20; i++) { 
                let angle = i * 0.5; let radius = 7; 
                let px = Math.cos(angle) * radius; let pz = Math.sin(angle) * radius; 
                height = i * 1.0; 
                createPlatform(px, height, pz, 3.5, 0.5, 3.5, 0xfbbf24, 'normal');
                if(i % 5 === 0) createCoin(px, height + 1, pz);
            }
            createPlatform(0, height + 2, 0, 8, 1, 8, 0x22c55e, 'finish'); 
            createPlatform(0, -5, 0, 150, 1, 150, 0xef4444, 'lava');
        }
        respawnPlayer();
    }

    function startGame(levelId) { document.querySelectorAll('.screen').forEach(el => el.style.display = 'none'); document.getElementById('game-ui').style.display = 'block'; canvas.style.display = 'block'; loadLevel(levelId); isGameRunning = true; if(window.innerWidth > 768) document.body.requestPointerLock(); }
    function exitGame() { document.exitPointerLock(); isGameRunning = false; document.getElementById('game-ui').style.display = 'none'; canvas.style.display = 'none'; document.getElementById('hackMenu').style.display = 'none'; showScreen('main-menu'); }
    function updateUI() { document.getElementById('ui-coins').innerText = coinsCollected; document.getElementById('ui-wins').innerText = gameWins; }
    function respawnPlayer() { player.position.set(0, 3, 0); velocity = { x: 0, y: 0, z: 0 }; cameraYaw = 0; cameraPitch = 0; coins.forEach(c => { c.collected = false; c.mesh.visible = true; }); coinsCollected = 0; updateUI(); }

    function handleWin() {
        gameWins++; updateUI();
        addXP(200); 
        
        if(gameWins === 5) {
            printConsole("🏆 GAME COMPLETED 5 TIMES! PASSWORD UNLOCKED.", "log-ok");
            printConsole("SECRET CHEAT CODE: /attribute game=generic[baseset=devmod] @s", "log-ok");
            showToast("Password in Console!");
        } else {
            showToast("LEVEL CLEARED!");
        }
        exitGame();
    }

    const HACK = {
        get isGodMode() { return document.getElementById('cbGodMode').checked; },
        get isFlyMode() { return document.getElementById('cbFlyMode').checked; },
        get speed() { return document.getElementById('cbSpeed').checked ? baseSpeed * 3 : baseSpeed; },
        get jump() { return document.getElementById('cbJump').checked ? baseJump * 2 : baseJump; }
    };

    // --- GAME LOOP ---
    const clock = new THREE.Clock();

    function animate() {
        requestAnimationFrame(animate);
        const time = clock.getElapsedTime();

        coins.forEach(c => { if (!c.collected) c.mesh.rotation.z += 0.04; });
        platforms.forEach(p => {
            if (p.type === 'moving') {
                if (p.moveAxis === 'x') {
                    const oldX = p.mesh.position.x;
                    p.mesh.position.x = p.startX + Math.sin(time * p.moveSpeed) * p.moveRange;
                    p.currentVel = { x: p.mesh.position.x - oldX, y: 0, z: 0 }; 
                } else if (p.moveAxis === 'z') {
                    const oldZ = p.mesh.position.z;
                    p.mesh.position.z = p.startZ + Math.sin(time * p.moveSpeed) * p.moveRange;
                    p.currentVel = { x: 0, y: 0, z: p.mesh.position.z - oldZ }; 
                }
            }
        });

        if (isGameRunning && !SYS.open) {
            let moveForward = 0; let moveRight = 0;
            if (keys.W) moveForward = 1; if (keys.S) moveForward = -1;
            if (keys.A) moveRight = -1; if (keys.D) moveRight = 1;

            const length = Math.sqrt(moveForward * moveForward + moveRight * moveRight);
            if (length > 0) { moveForward /= length; moveRight /= length; }

            player.rotation.y = cameraYaw;
            velocity.x = (moveForward * -Math.sin(cameraYaw) + moveRight * Math.cos(cameraYaw)) * HACK.speed;
            velocity.z = (moveForward * -Math.cos(cameraYaw) + moveRight * -Math.sin(cameraYaw)) * HACK.speed;

            if (HACK.isFlyMode) {
                velocity.y = 0;
                if (keys.Space) velocity.y = HACK.speed;
            } else {
                if (keys.Space && isGrounded) { velocity.y = HACK.jump; isGrounded = false; isOnMovingPlatform = false; }
                velocity.y += gravity;
            }

            if (isOnMovingPlatform) { player.position.x += platformVelocity.x; player.position.z += platformVelocity.z; }
            player.position.x += velocity.x; player.position.y += velocity.y; player.position.z += velocity.z;

            isGrounded = false; isOnMovingPlatform = false; platformVelocity = {x: 0, y: 0, z: 0};
            const playerBox = new THREE.Box3().setFromObject(player);

            for (let i = 0; i < platforms.length; i++) {
                const plat = platforms[i]; const platBox = new THREE.Box3().setFromObject(plat.mesh);
                if (playerBox.intersectsBox(platBox)) {
                    if (plat.type === 'lava' && !HACK.isGodMode) { respawnPlayer(); } 
                    else if (plat.type === 'finish') { handleWin(); } 
                    else {
                        if (velocity.y < 0 && player.position.y > plat.yTop) {
                            player.position.y = plat.yTop + (playerSize / 2); velocity.y = 0; isGrounded = true;
                            if (plat.type === 'moving') { isOnMovingPlatform = true; platformVelocity = plat.currentVel; }
                        }
                    }
                }
            }

            coins.forEach(c => {
                if (!c.collected) {
                    const coinBox = new THREE.Box3().setFromObject(c.mesh);
                    if (playerBox.intersectsBox(coinBox)) { c.collected = true; c.mesh.visible = false; coinsCollected++; updateUI(); }
                }
            });

            if (player.position.y < -25 && !HACK.isGodMode) respawnPlayer();
        }

        const camOffsetX = cameraDistance * Math.sin(cameraYaw) * Math.cos(cameraPitch);
        const camOffsetY = cameraDistance * Math.sin(cameraPitch);
        const camOffsetZ = cameraDistance * Math.cos(cameraYaw) * Math.cos(cameraPitch);

        camera.position.x = player.position.x + camOffsetX;
        camera.position.y = player.position.y + 0.8 + camOffsetY; 
        camera.position.z = player.position.z + camOffsetZ;
        camera.lookAt(player.position.x, player.position.y + 0.8, player.position.z);

        renderer.render(scene, camera);
    }

    window.addEventListener('resize', () => { renderer.setSize(window.innerWidth, window.innerHeight); camera.aspect = window.innerWidth / window.innerHeight; camera.updateProjectionMatrix(); });
    window.onload = () => { playIntro(); animate(); };
</script>
</body>
</html>
