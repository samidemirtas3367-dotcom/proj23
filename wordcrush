<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ENG GAME (MEGA ULTIMATE EDITION - RANK UP)</title>
    <style>
        /* ========================================
           CORE UI DESIGN & THEME ENGINE
           ======================================== */
        :root {
            --bg-dark: #0f172a; --bg-light: #1e293b; --accent: #38bdf8;
            --panel-bg: rgba(30, 41, 59, 0.98); --text-main: #f8fafc;
            --text-muted: #94a3b8; --danger: #ef4444; --success: #22c55e;
            --gold: #fbbf24; --p1-color: #f87171; --p2-color: #60a5fa;
            --minigame-accent: #a855f7; --wheel-accent: #f43f5e;
            --term-green: #00ff41; --term-bg: rgba(0, 5, 10, 0.95);
        }

        body {
            background: radial-gradient(circle at top right, var(--bg-light) 0%, var(--bg-dark) 100%);
            color: var(--text-main); font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex; flex-direction: column; align-items: center; justify-content: flex-start;
            margin: 0; height: 100vh; overflow: hidden; transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

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
            border-radius: 20px; text-align: center; box-shadow: 0 0 25px rgba(56, 189, 248, 0.3); width: 350px;
        }
        .rank-title { color: var(--accent); font-size: 14px; font-weight: bold; letter-spacing: 3px; margin-bottom: 5px; text-transform: uppercase; }
        #rank-name-ui { font-size: 32px; font-weight: 900; color: #fff; text-shadow: 0 0 10px #fff; margin-bottom: 10px; letter-spacing: 2px;}
        .xp-bar-bg { width: 100%; height: 12px; background: #334155; border-radius: 6px; overflow: hidden; border: 1px solid #64748b; }
        #xp-bar-fill { width: 0%; height: 100%; background: var(--gold); transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1); box-shadow: 0 0 15px var(--gold); }
        #xp-text-ui { font-size: 14px; color: #94a3b8; margin-top: 8px; font-weight: bold; }

        /* --- MENÜ SİSTEMİ EKRANLARI --- */
        .screen { display: none; width: 100%; height: 100%; flex-direction: column; align-items: center; padding-top: 40px; position: absolute; inset: 0; background: rgba(15, 23, 42, 0.95); backdrop-filter: blur(25px); overflow-y: auto; z-index: 10; }
        #main-menu { display: flex; z-index: 20; }
        #game-screen, #quiz-screen, #battle-screen, #bomb-screen, #memory-screen, #rain-screen, #wheel-screen, #voltage-screen, #crate-screen, #air-screen, #tunnel-screen, #chem-screen { background: transparent; backdrop-filter: none; z-index: 5; }

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
        .nav-btn { padding: 12px 25px; border-radius: 12px; border: none; font-weight: 900; cursor: pointer; transition: 0.2s; z-index: 1000;}
        .btn-exit { background: #475569; color: white; } .btn-finish { background: var(--danger); color: white; box-shadow: 0 0 15px rgba(239, 68, 68, 0.4); }

        .minigame-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; max-width: 900px; }
        .locked-game { opacity: 0.4; cursor: not-allowed; border-color: #475569 !important; color: #94a3b8 !important; }
        /* V3.0 KİLİT AÇILMA STİLİ */
        .unlocked-game { opacity: 1 !important; border-color: var(--success) !important; color: var(--success) !important; cursor: pointer !important; text-shadow: 0 0 10px var(--success); box-shadow: 0 0 20px rgba(34, 197, 94, 0.4); }

        /* ÜNİTE KARTLARI & MODLAR */
        .card-container { width: 100%; max-width: 800px; padding: 0 20px; box-sizing: border-box; display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .unit-card { background: var(--panel-bg); border: 2px solid var(--accent); border-radius: 15px; padding: 20px; cursor: pointer; transition: 0.3s ease; position: relative; overflow: hidden; }
        .unit-card:hover { transform: scale(1.05); box-shadow: 0 10px 30px rgba(0,0,0,0.5), 0 0 15px var(--accent); }
        .unit-card h2 { margin: 0 0 10px 0; font-size: 26px; color: #fff; }
        .unit-card hr { border: 0; height: 1px; background: var(--accent); opacity: 0.4; margin-bottom: 10px; }
        .unit-card p { margin: 0; color: var(--text-muted); font-size: 15px; }

        .mods-grid, .settings-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; max-width: 600px; width: 100%; }
        .mod-btn { background: #1e293b; border: 2px solid var(--accent); border-radius: 15px; color: #fff; padding: 20px; cursor: pointer; font-weight: 900; font-size: 18px; transition: 0.3s; text-transform: uppercase; }
        .mod-btn:hover, .mod-btn.active { background: var(--accent); color: #000; box-shadow: 0 0 20px var(--accent); }
        .info-box { background: rgba(0,0,0,0.5); border: 1px solid var(--accent); border-radius: 10px; padding: 20px; margin-top: 30px; max-width: 600px; text-align: center; color: var(--gold); font-size: 18px; }

        /* --- SCOREBOARDS --- */
        .ui-top { position: absolute; top: 25px; left: 25px; display: flex; gap: 15px; z-index: 2000; }
        .scoreboard { display: flex; justify-content: space-around; width: 85%; background: var(--panel-bg); padding: 15px; border-radius: 20px; border: 2px solid rgba(255,255,255,0.1); margin-bottom: 25px; margin-top: 60px; z-index: 100; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
        .stat-box { text-align: center; } .stat-val { display: block; font-size: 36px; font-weight: 900; color: var(--accent); text-shadow: 0 0 10px var(--accent); } .stat-lbl { font-size: 14px; color: var(--text-muted); text-transform: uppercase; font-weight: bold; }

        /* --- QUIZ & BATTLE --- */
        .quiz-container { width: 90%; max-width: 800px; margin-top: 20px; }
        .quiz-question { background: var(--panel-bg); border: 4px solid var(--accent); border-radius: 20px; padding: 50px; font-size: 36px; text-align: center; margin-bottom: 30px; box-shadow: 0 0 20px rgba(0,0,0,0.5); }
        .quiz-options { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        .quiz-opt-btn { background: #1e293b; border: 3px solid #475569; border-radius: 15px; padding: 30px; font-size: 26px; color: #fff; cursor: pointer; transition: 0.2s; font-weight: bold; }
        .quiz-opt-btn:hover { background: var(--accent); color: #000; border-color: var(--accent); transform: translateY(-5px); }

        #battle-screen { flex-direction: row; padding: 0; background: #000; overflow: hidden; }
        .battle-side { flex: 1; display: flex; flex-direction: column; align-items: center; justify-content: center; position: relative; transition: 0.3s; height: 100%; }
        .p1-side { border-right: 5px solid #334155; background: linear-gradient(to right, #1a0505, #000); } .p2-side { background: linear-gradient(to left, #050a1a, #000); }
        .vs-divider { position: absolute; left: 50%; top: 50%; transform: translate(-50%, -50%); font-size: 100px; font-weight: 900; color: #fff; text-shadow: 0 0 30px var(--accent); z-index: 100; font-style: italic; }
        .battle-q-zone { position: absolute; top: 30px; width: 70%; background: var(--panel-bg); padding: 25px; border-radius: 20px; border: 3px solid var(--accent); text-align: center; font-size: 36px; font-weight: bold; z-index: 50; left: 15%; box-shadow: 0 0 20px #000; }
        .battle-options { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; width: 85%; max-width: 600px; }
        .battle-btn { padding: 40px 10px; font-size: 26px; font-weight: bold; border-radius: 15px; border: 4px solid rgba(255,255,255,0.1); cursor: pointer; color: white; transition: 0.2s; background: rgba(255,255,255,0.05); }
        .p1-btn:hover { background: var(--p1-color); color: #000; transform: scale(1.05); } .p2-btn:hover { background: var(--p2-color); color: #000; transform: scale(1.05); }
        .battle-score { font-size: 100px; font-weight: 900; margin-bottom: 30px; text-shadow: 0 0 20px; } .p1-text { color: var(--p1-color); } .p2-text { color: var(--p2-color); }

        /* --- WORD MATCH --- */
        .game-world { display: flex; gap: 50px; margin-top: 10px; }
        .grid-wrap h3 { text-align: center; color: var(--accent); letter-spacing: 4px; margin-bottom: 10px; text-shadow: 0 0 10px var(--accent); }
        .game-grid { display: grid; grid-template-columns: repeat(3, 120px); grid-template-rows: repeat(5, 85px); gap: 12px; background: rgba(0,0,0,0.6); padding: 20px; border-radius: 30px; border: 4px solid #334155; position: relative; box-shadow: inset 0 0 30px #000; }
        .tile { width: 120px; height: 85px; display: flex; align-items: center; justify-content: center; border-radius: 16px; cursor: pointer; font-size: 14px; font-weight: 900; transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275); text-align: center; box-shadow: 0 8px 0 rgba(0,0,0,0.4); text-transform: uppercase; padding: 5px; box-sizing: border-box; position: absolute; z-index: 10; }
        .tile:hover { filter: brightness(1.2); transform: translateY(-5px) scale(1.05); }
        .active-sel { border: 4px solid #fff !important; transform: scale(1.15) !important; z-index: 100; box-shadow: 0 0 30px #fff; }
        .c-0 { background: linear-gradient(135deg, #f87171, #991b1b); } .c-1 { background: linear-gradient(135deg, #60a5fa, #1e40af); } .c-2 { background: linear-gradient(135deg, #4ade80, #14532d); } .c-3 { background: linear-gradient(135deg, #fbbf24, #b45309); color: #000; } .tr-tile { background: #1e293b; color: #94a3b8; border: 1px solid #475569; }

        @keyframes popOut { 0% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.5); filter: brightness(2); } 100% { transform: scale(0); opacity: 0; } }
        @keyframes fire-glow { 0% { box-shadow: 0 0 10px #ff4500, 0 0 20px #ff0000; } 100% { box-shadow: 0 0 20px #ffd700, 0 0 40px #ff4500; } }
        @keyframes gravityDrop { 0% { transform: translateY(-100px); opacity: 0; } 100% { transform: translateY(0); opacity: 1; } }
        .gravity-fall { animation: gravityDrop 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards; }
        .pop { animation: popOut 0.4s forwards; pointer-events: none; }
        .fire-pop { animation: fire-glow 0.4s alternate infinite, popOut 0.4s forwards; border: 4px solid red; z-index: 200; }

        /* --- MINIGAMES: WHEEL OF FORTUNE --- */
        .wheel-box { position: relative; width: 550px; height: 550px; margin-top: 20px; display: flex; align-items: center; justify-content: center; }
        #wheel-canvas { border-radius: 50%; border: 12px solid var(--panel-bg); box-shadow: 0 0 60px rgba(0,0,0,0.8), 0 0 20px var(--wheel-accent); transition: transform 4s cubic-bezier(0.1, 0.8, 0.25, 1); }
        .wheel-pointer { position: absolute; top: -30px; left: 50%; transform: translateX(-50%); width: 0; height: 0; border-left: 35px solid transparent; border-right: 35px solid transparent; border-top: 60px solid #fff; z-index: 100; filter: drop-shadow(0 5px 10px rgba(0,0,0,0.8)); }
        #wheel-result-modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.95); z-index: 9000; flex-direction: column; align-items: center; justify-content: center; text-align: center; padding: 50px; animation: modalIn 0.5s ease; }
        @keyframes modalIn { from { transform: scale(0.5); opacity: 0; } to { transform: scale(1); opacity: 1; } }
        .wheel-task-number { font-size: 40px; color: var(--wheel-accent); letter-spacing: 5px; font-weight: bold; margin-bottom: 25px; text-shadow: 0 0 15px var(--wheel-accent); }
        .wheel-task-text { font-size: 60px; color: #fff; font-weight: 900; max-width: 1000px; line-height: 1.3; text-shadow: 0 5px 30px #000; margin-bottom: 50px; }

        /* --- MINIGAMES: BOMB DEFUSE --- */
        #bomb-screen { background: radial-gradient(circle, #310a0a 0%, #000 100%); }
        .bomb-container { background: #111; border: 10px solid #333; border-radius: 30px; padding: 40px; display: flex; flex-direction: column; align-items: center; box-shadow: inset 0 0 60px #000, 0 20px 60px rgba(0,0,0,0.9); width: 85%; max-width: 800px; margin-top: 50px; border-style: double; }
        .digital-timer { font-family: 'Courier New', Courier, monospace; font-size: 110px; color: #ef4444; background: #050000; padding: 15px 50px; border-radius: 20px; border: 5px solid #222; text-shadow: 0 0 25px #ef4444; margin-bottom: 30px; letter-spacing: 8px; box-shadow: inset 0 0 20px #f00; }
        .bomb-question { font-size: 34px; color: #fff; margin-bottom: 25px; text-align: center; font-weight: bold; background: rgba(255,255,255,0.05); padding: 10px 30px; border-radius: 15px; }
        .wires-container { display: flex; flex-direction: column; gap: 20px; width: 100%; }
        .wire { background: linear-gradient(90deg, #444 0%, #888 50%, #444 100%); height: 70px; border-radius: 35px; display: flex; align-items: center; justify-content: center; font-size: 24px; font-weight: bold; color: white; cursor: pointer; text-shadow: 1px 1px 2px #000; transition: 0.2s; position: relative; overflow: hidden; border: 2px solid #222; box-shadow: 0 10px 15px rgba(0,0,0,0.5); }
        .wire:hover { filter: brightness(1.2); transform: scale(1.02); }
        .wire.cut::after { content: ''; position: absolute; left: 50%; top: -10px; bottom: -10px; width: 15px; background: #000; transform: skewX(-20deg); box-shadow: inset 0 0 15px #000; }
        .wire.cut-wrong { background: #ef4444 !important; animation: shake 0.3s; }
        .w-red { background: #dc2626; } .w-blue { background: #2563eb; } .w-green { background: #16a34a; } .w-yellow { background: #ca8a04; }
        @keyframes massiveExplosion { 0% { background: #fff; transform: scale(1); } 50% { background: #ff4500; transform: scale(1.1); } 100% { background: #000; transform: scale(1); opacity: 0; } }
        .exploded-bg { animation: massiveExplosion 1s forwards; pointer-events: none; }

        /* --- MINIGAMES: MEMORY CARDS (3D) --- */
        .memory-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; max-width: 900px; margin-top: 20px; perspective: 1200px; }
        .mem-card { width: 150px; height: 150px; background: transparent; cursor: pointer; perspective: 1200px; }
        .mem-inner { position: relative; width: 100%; height: 100%; text-align: center; transition: transform 0.6s cubic-bezier(0.4, 0.2, 0.2, 1); transform-style: preserve-3d; border-radius: 20px; box-shadow: 0 8px 15px rgba(0,0,0,0.4); }
        .mem-card.flipped .mem-inner, .mem-card.matched .mem-inner { transform: rotateY(180deg); }
        .mem-front, .mem-back { position: absolute; width: 100%; height: 100%; backface-visibility: hidden; border-radius: 20px; display: flex; align-items: center; justify-content: center; font-size: 20px; font-weight: bold; padding: 15px; box-sizing: border-box; }
        .mem-front { background: linear-gradient(135deg, var(--accent), #1e3a8a); color: white; border: 4px solid #fff; font-size: 60px; box-shadow: inset 0 0 20px rgba(0,0,0,0.5); }
        .mem-back { background: var(--panel-bg); color: var(--gold); transform: rotateY(180deg); border: 4px solid var(--gold); }
        .mem-card.matched .mem-inner { animation: popOut 0.5s 0.3s forwards; }

        /* --- MINIGAMES: WORD RAIN --- */
        #rain-screen { overflow: hidden; position: relative; }
        .rain-catcher { position: absolute; bottom: 30px; left: 50%; transform: translateX(-50%); background: var(--panel-bg); border: 5px solid var(--accent); padding: 25px 50px; border-radius: 30px; font-size: 32px; font-weight: 900; z-index: 100; text-align: center; box-shadow: 0 -15px 40px rgba(0,0,0,0.6); width: 65%; }
        .rain-target-word { color: var(--gold); display: block; font-size: 50px; margin-top: 15px; text-shadow: 0 0 15px var(--gold); }
        .raindrop { position: absolute; top: -120px; background: #1e293b; border: 3px solid #fff; border-radius: 15px; padding: 20px 30px; font-size: 24px; font-weight: bold; cursor: pointer; transition: background 0.2s; box-shadow: 0 15px 30px rgba(0,0,0,0.6); text-align: center; z-index: 50; }
        .raindrop:hover { background: var(--accent); color: #000; transform: scale(1.15); }
        @keyframes rainFall { to { top: 110vh; } }
        .rain-explode { animation: fire-glow 0.3s alternate infinite, popOut 0.3s forwards; pointer-events: none; border-color: var(--success) !important; background: var(--success) !important; color: #000 !important;}

        /* --- MINIGAMES: VOLTAGE CUT --- */
        #voltage-screen { background: radial-gradient(circle, #0a0a2a 0%, #000 100%); }
        .voltage-area { width: 85%; height: 60vh; background: #050510; border: 6px solid #222; border-radius: 30px; position: relative; margin-top: 30px; box-shadow: inset 0 0 60px #000; overflow: hidden; touch-action: none; }
        .voltage-node { position: absolute; width: 100px; height: 100px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 16px; text-align: center; padding: 10px; cursor: pointer; z-index: 10; border: 4px solid #fff; box-shadow: 0 0 20px rgba(255,255,255,0.5); }
        .v-start { background: var(--p2-color); color: #000; left: 30px; top: 40%; }
        .v-end { background: var(--success); color: #000; right: 30px; top: 40%; transition: top 0.5s; }
        .v-wire { position: absolute; background: #444; height: 20px; border-radius: 10px; transform-origin: left center; z-index: 5; pointer-events: none; box-shadow: 0 5px 10px #000; }
        .v-active-wire { background: #00ffff !important; box-shadow: 0 0 20px #00ffff, 0 0 40px #00ffff !important; }
        .zap-effect { animation: zapFlash 0.3s; }
        @keyframes zapFlash { 0%, 100% { background: #050510; } 50% { background: #00ffff; } }

        /* --- MINIGAMES: CRATE BREAKER --- */
        #crate-screen { background: url('https://www.transparenttextures.com/patterns/dark-matter.png'), #111; }
        .crates-container { display: flex; gap: 50px; margin-top: 60px; }
        .crate { width: 220px; height: 220px; background: url('https://www.transparenttextures.com/patterns/wood-pattern.png'), #8b4513; border: 10px solid #3e1f08; border-radius: 15px; cursor: pointer; position: relative; display: flex; align-items: center; justify-content: center; font-size: 30px; font-weight: bold; color: #fff; text-shadow: 2px 2px 5px #000; box-shadow: 0 25px 50px rgba(0,0,0,0.8), inset 0 0 60px rgba(0,0,0,0.5); transition: transform 0.1s; }
        .crate:active { transform: scale(0.92); }
        .crate-cracked-1 { background: url('https://www.transparenttextures.com/patterns/wood-pattern.png'), #70360e; border-color: #2e1605; }
        .crate-cracked-2 { background: url('https://www.transparenttextures.com/patterns/wood-pattern.png'), #542809; border-color: #1a0c03; }
        .crate-broken { background: transparent !important; border: none !important; box-shadow: none !important; pointer-events: none; animation: popOut 0.5s forwards; color: var(--gold); font-size: 50px; text-shadow: 0 0 30px var(--gold); }
        .crate-q { position: absolute; top: -90px; width: 100%; text-align: center; font-size: 45px; color: var(--gold); font-weight: 900; text-shadow: 0 0 25px #000; background: rgba(0,0,0,0.5); padding: 5px; border-radius: 10px; }

        /* ========================================
           V3.0 OYUNLARI STİLLERİ (YENİ)
           ======================================== */
        
        /* AIR DROP */
        #air-screen { background: linear-gradient(to bottom, #0f172a 0%, #000 100%); overflow: hidden; }
        .air-target-box { background: rgba(0,0,0,0.8); border: 4px solid #f59e0b; padding: 20px 40px; border-radius: 20px; font-size: 40px; font-weight: bold; color: #fff; text-shadow: 0 0 20px #f59e0b; margin-top: 50px; z-index: 100; }
        .air-crate { position: absolute; width: 160px; height: 160px; background: url('https://www.transparenttextures.com/patterns/wood-pattern.png'), #b45309; border: 6px solid #78350f; border-radius: 10px; display: flex; align-items: center; justify-content: center; font-size: 24px; font-weight: 900; color: #fff; text-shadow: 2px 2px 4px #000; cursor: pointer; box-shadow: 0 15px 25px rgba(0,0,0,0.8); transition: transform 0.1s; z-index: 50; }
        .air-crate:hover { filter: brightness(1.2); transform: scale(1.05); }
        .parachute { position: absolute; top: -60px; left: 50%; transform: translateX(-50%); width: 100px; height: 60px; background: #ef4444; border-radius: 50px 50px 0 0; }
        .parachute::before, .parachute::after { content: ''; position: absolute; width: 2px; height: 40px; background: #fff; bottom: -40px; }
        .parachute::before { left: 20px; transform: rotate(20deg); } .parachute::after { right: 20px; transform: rotate(-20deg); }
        @keyframes airdropFall { to { top: 120vh; } }

        /* GRAVITY TUNNEL */
        #tunnel-screen { background: #000; perspective: 1000px; overflow: hidden; }
        .tunnel-bg { position: absolute; inset: 0; background: repeating-radial-gradient(circle at center, transparent 0, transparent 40px, rgba(56, 189, 248, 0.1) 41px, rgba(56, 189, 248, 0.1) 50px); animation: tunnelMove 2s linear infinite; z-index: 1; }
        @keyframes tunnelMove { 0% { transform: scale(1); opacity: 0.5; } 100% { transform: scale(2); opacity: 1; } }
        .tunnel-q { position: absolute; top: 15%; width: 80%; text-align: center; font-size: 50px; color: #fff; font-weight: 900; z-index: 100; text-shadow: 0 0 20px var(--accent); background: rgba(0,0,0,0.5); padding: 20px; border-radius: 20px; border: 2px solid var(--accent); }
        .tunnel-doors { display: flex; gap: 40px; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); z-index: 50; }
        .t-door { width: 200px; height: 300px; background: rgba(15, 23, 42, 0.9); border: 8px solid #64748b; border-radius: 20px; display: flex; align-items: center; justify-content: center; font-size: 32px; font-weight: bold; color: #fff; cursor: pointer; transition: 0.2s; box-shadow: inset 0 0 50px #000, 0 0 30px var(--accent); animation: doorApproach 0.5s ease-out forwards; }
        .t-door:hover { border-color: var(--accent); transform: scale(1.1); box-shadow: 0 0 50px var(--accent); }
        @keyframes doorApproach { 0% { transform: scale(0.1) translateZ(-1000px); opacity: 0; } 100% { transform: scale(1) translateZ(0); opacity: 1; } }

        /* CHEM REACTION */
        #chem-screen { background: radial-gradient(circle, #064e3b 0%, #000 100%); }
        .chem-table { display: flex; flex-direction: column; align-items: center; margin-top: 50px; width: 100%; }
        .beaker { width: 150px; height: 200px; border: 6px solid #cbd5e1; border-top: none; border-radius: 0 0 40px 40px; position: relative; display: flex; align-items: flex-end; justify-content: center; background: rgba(255,255,255,0.05); margin-bottom: 50px; box-shadow: inset 0 -20px 50px rgba(0,0,0,0.5); }
        .beaker-liquid { width: 100%; height: 30%; background: #10b981; border-radius: 0 0 34px 34px; transition: height 0.5s, background 0.5s; display: flex; align-items: center; justify-content: center; font-size: 24px; font-weight: bold; color: #000; }
        .chem-q { font-size: 40px; color: #fff; font-weight: 900; margin-bottom: 40px; text-shadow: 0 0 20px #10b981; background: rgba(0,0,0,0.5); padding: 15px 40px; border-radius: 20px; border: 2px solid #10b981; }
        .flasks { display: flex; gap: 40px; }
        .flask { width: 100px; height: 140px; background: rgba(255,255,255,0.1); border: 4px solid #94a3b8; border-radius: 50px 50px 20px 20px; position: relative; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 20px; font-weight: bold; color: #fff; text-shadow: 1px 1px 2px #000; transition: 0.3s; overflow: hidden; }
        .flask::before { content:''; position: absolute; bottom: 0; width: 100%; height: 60%; background: var(--minigame-accent); z-index: -1; }
        .flask:hover { transform: translateY(-15px) rotate(15deg); border-color: #fff; }
        @keyframes explosionChem { 0% { transform: scale(1); background: #fff; } 50% { transform: scale(5); background: #10b981; } 100% { transform: scale(1); opacity: 0; } }
        @keyframes badExplosion { 0% { transform: scale(1); background: #fff; } 50% { transform: scale(5); background: #ef4444; } 100% { transform: scale(1); opacity: 0; } }

        /* --- EFFECTS & MODALS --- */
        .win-flash { animation: winGlow 0.5s infinite alternate; } @keyframes winGlow { from { box-shadow: inset 0 0 50px rgba(34, 197, 94, 0.5); } to { box-shadow: inset 0 0 100px var(--success); } }
        .wrong-flash { background: var(--danger) !important; animation: shake 0.3s; border-color: #fff !important; }
        .correct-flash { background: var(--success) !important; border-color: #fff !important; color: #000 !important; }
        @keyframes shake { 0%, 100% { transform: translateX(0); } 25% { transform: translateX(10px); } 75% { transform: translateX(-10px); } }

        #toast, #msg-popup { position: fixed; top: 30%; font-weight: 900; display: none; z-index: 9999; text-shadow: 0 0 20px #000; text-align: center; }
        #toast { font-size: 70px; color: gold; } #msg-popup { font-size: 50px; }

        .end-screen { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.98); z-index: 9999; flex-direction: column; align-items: center; justify-content: center; text-align: center; padding: 50px; }
        .end-title { font-size: 70px; color: var(--accent); margin-bottom: 25px; text-shadow: 0 0 30px var(--accent); }
        .end-quote { font-size: 28px; color: #fff; font-style: italic; max-width: 900px; margin-bottom: 50px; }
    </style>
</head>
<body>

<div id="intro-screen">
    <div id="intro-container"></div>
</div>

<div id="dev-console">
    <div id="console-output"></div>
    <div class="console-input-line" id="console-line">
        <span class="console-prefix">root@smartboard:~#</span>
        <input type="password" id="console-input" autocomplete="off" spellcheck="false" autofocus>
    </div>
</div>

<div class="dev-trigger" onclick="toggleConsole()">v3.0.0_build(912)</div>

<div id="main-menu" class="screen">
    <div class="menu-header">
        <h1 class="menu-title">ENG GAME</h1>
        <span class="menu-sub">MEGA ULTIMATE EDITION</span>
    </div>
    
    <div class="rank-container" style="margin-bottom: 30px;">
        <div class="rank-title">CS2 RANK SYSTEM</div>
        <div id="rank-name-ui">🥈 SILVER I</div>
        <div class="xp-bar-bg">
            <div id="xp-bar-fill"></div>
        </div>
        <div id="xp-text-ui">0 / 400 XP</div>
    </div>

    <button class="big-btn" onclick="showScreen('mode-menu')">▶ KLASİK MODLAR</button>
    <button class="big-btn" onclick="showScreen('minigames-menu')" style="border-color: var(--minigame-accent); color: var(--minigame-accent); box-shadow: 0 0 20px rgba(168, 85, 247, 0.5);">🎮 MİNİGAMES (12)</button>
    <button class="big-btn" onclick="showScreen('mods-menu')">🎨 TEMALAR</button>
    <button class="big-btn" onclick="showScreen('settings-menu')">⚙️ AYARLAR</button>
</div>

<div id="mode-menu" class="screen">
    <div class="menu-header"><h1 class="menu-title">MOD SEÇİMİ</h1></div>
    <button class="big-btn" onclick="selectMode('wordmatch')">🧩 WORD MATCH (Bonuslu)</button>
    <button class="big-btn" onclick="selectMode('quiz')" style="border-color: #fbbf24; color: #fbbf24;">📝 QUICK QUIZ</button>
    <button class="big-btn" onclick="selectMode('battle')" style="border-color: #ef4444; color: #ef4444;">⚔️ BATTLE MODE (2P)</button>
    <button class="big-btn back-btn" onclick="showScreen('main-menu')">GERİ DÖN</button>
</div>

<div id="minigames-menu" class="screen">
    <div class="menu-header" style="margin-bottom: 20px;"><h1 class="menu-title" style="color:var(--minigame-accent); text-shadow:0 0 20px var(--minigame-accent);">MİNİGAMES</h1><span class="menu-sub">Aksiyon ve Hız</span></div>
    <div class="minigame-grid">
        <button class="big-btn" style="width:100%; font-size: 18px; border-color: var(--wheel-accent); color: var(--wheel-accent);" onclick="selectMinigame('wheel')">🎡 GÖREV ÇARKI (34)</button>
        <button class="big-btn" style="width:100%; font-size: 18px; border-color: #ef4444; color: #ef4444;" onclick="selectMinigame('bomb')">💣 BOMB DEFUSE</button>
        <button class="big-btn" style="width:100%; font-size: 18px; border-color: #38bdf8; color: #38bdf8;" onclick="selectMinigame('memory')">🎴 MEMORY CARDS</button>
        <button class="big-btn" style="width:100%; font-size: 18px; border-color: #22c55e; color: #22c55e;" onclick="selectMinigame('rain')">🌧️ WORD RAIN</button>
        <button class="big-btn" style="width:100%; font-size: 18px; border-color: #00ffff; color: #00ffff;" onclick="selectMinigame('voltage')">⚡ VOLTAGE CUT</button>
        <button class="big-btn" style="width:100%; font-size: 18px; border-color: #d97706; color: #d97706;" onclick="selectMinigame('crate')">📦 CRATE BREAKER</button>
        
        <button class="big-btn locked-game" id="mg-air" data-id="air" data-realname="📡 AIR DROP SCAN" style="width:100%; font-size: 18px;" onclick="if(this.classList.contains('unlocked-game')) selectMinigame('air')">🔒 KİLİTLİ (V3.0)</button>
        <button class="big-btn locked-game" id="mg-tun" data-id="tunnel" data-realname="🚀 GRAVITY TUNNEL" style="width:100%; font-size: 18px;" onclick="if(this.classList.contains('unlocked-game')) selectMinigame('tunnel')">🔒 KİLİTLİ (V3.0)</button>
        <button class="big-btn locked-game" id="mg-chem" data-id="chem" data-realname="🧪 CHEM REACTION" style="width:100%; font-size: 18px; grid-column: span 2;" onclick="if(this.classList.contains('unlocked-game')) selectMinigame('chem')">🔒 KİLİTLİ (V3.0) - GOLD NOVA OL</button>
    </div>
    <button class="big-btn back-btn" onclick="showScreen('main-menu')">GERİ DÖN</button>
</div>

<div id="bomb-settings-menu" class="screen">
    <div class="menu-header"><h1 class="menu-title" style="color:#ef4444;">BOMBA SÜRESİ</h1></div>
    <button class="big-btn" onclick="setBombSettings(10, 2)" style="font-size: 20px;">10 SANİYE (2 SORU)</button>
    <button class="big-btn" onclick="setBombSettings(20, 4)" style="font-size: 20px;">20 SANİYE (4 SORU)</button>
    <button class="big-btn" onclick="setBombSettings(40, 6)" style="font-size: 20px;">40 SANİYE (6 SORU)</button>
    <button class="big-btn" onclick="setBombSettings(50, 10)" style="border-color:#ef4444; color:#ef4444; font-size: 20px; box-shadow: 0 0 20px rgba(239,68,68,0.5);">50 SANİYE (10 SORU) 🔥</button>
    <button class="big-btn back-btn" onclick="showScreen('minigames-menu')">GERİ DÖN</button>
</div>

<div id="unit-menu" class="screen">
    <div class="menu-header"><h1 class="menu-title">ÜNİTE SEÇİMİ</h1></div>
    <div class="card-container" id="unit-root"></div>
    <button class="big-btn back-btn" style="grid-column: span 2; margin: 20px auto;" onclick="showScreen('main-menu')">GERİ DÖN</button>
</div>

<div id="mods-menu" class="screen">
    <div class="menu-header"><h1 class="menu-title">TEMALAR</h1></div>
    <div class="mods-grid">
        <button class="mod-btn" id="btn-theme-classic" onclick="applyTheme('classic')">🌑 Classic</button>
        <button class="mod-btn" id="btn-theme-subnautica" onclick="applyTheme('subnautica')">🌊 Subnautica</button>
        <button class="mod-btn" id="btn-theme-cs2" onclick="applyTheme('cs2')">🔫 CS2 Global</button>
        <button class="mod-btn" id="btn-theme-alastor" onclick="applyTheme('alastor')" style="border-color: #ef4444; color: #ef4444;">📻 Alastor</button>
        <button class="mod-btn" id="btn-theme-vox" onclick="applyTheme('vox')" style="border-color: #06b6d4; color: #06b6d4;">📺 VoxTek</button>
    </div>
    <button class="big-btn back-btn" onclick="showScreen('main-menu')">GERİ DÖN</button>
</div>

<div id="settings-menu" class="screen">
    <div class="menu-header"><h1 class="menu-title">AYARLAR</h1></div>
    <div class="settings-grid">
        <button class="mod-btn" id="btn-dev-pc" onclick="setDevice('pc')">💻 PC</button>
        <button class="mod-btn" id="btn-dev-tahta" onclick="setDevice('tahta')">🏫 Akıllı Tahta</button>
    </div>
    <div id="device-info" class="info-box">Tahta için dokunmatik yüzeyler büyütülmüştür.</div>
    <button class="big-btn back-btn" onclick="showScreen('main-menu')">GERİ DÖN</button>
</div>

<div id="game-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button><button class="nav-btn btn-finish" onclick="triggerFinal(true)">BİTİR</button></div>
    <div class="scoreboard">
        <div class="stat-box"><span class="stat-lbl">Ünite</span><span id="wm-unit" class="stat-val">1</span></div>
        <div class="stat-box"><span class="stat-lbl">Skor</span><span id="wm-score" class="stat-val">0</span></div>
        <div class="stat-box"><span class="stat-lbl">Kalan Eş</span><span id="wm-tiles" class="stat-val">15</span></div>
    </div>
    <div class="game-world"><div class="grid-wrap"><h3>İNGİLİZCE</h3><div id="en-grid" class="game-grid"></div></div><div class="grid-wrap"><h3>TÜRKÇE</h3><div id="tr-grid" class="game-grid"></div></div></div>
</div>

<div id="quiz-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="scoreboard">
        <div class="stat-box"><span class="stat-lbl">Ünite</span><span id="qz-unit" class="stat-val">1</span></div>
        <div class="stat-box"><span class="stat-lbl">Soru</span><span id="qz-progress" class="stat-val">1/10</span></div>
        <div class="stat-box"><span class="stat-lbl">Skor</span><span id="qz-score" class="stat-val">0</span></div>
    </div>
    <div class="quiz-container">
        <div id="quiz-q-text" class="quiz-question">Yükleniyor...</div>
        <div id="quiz-options-container" class="quiz-options">
            <button class="quiz-opt-btn" onclick="checkQuizAnswer(0)" id="q-opt-0">A</button> <button class="quiz-opt-btn" onclick="checkQuizAnswer(1)" id="q-opt-1">B</button>
            <button class="quiz-opt-btn" onclick="checkQuizAnswer(2)" id="q-opt-2">C</button> <button class="quiz-opt-btn" onclick="checkQuizAnswer(3)" id="q-opt-3">D</button>
        </div>
    </div>
</div>

<div id="battle-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="vs-divider">VS</div>
    <div id="battle-q-box" class="battle-q-zone">SORU YÜKLENİYOR...</div>
    <div class="battle-side p1-side" id="p1-side">
        <div class="battle-score p1-text" id="p1-score-ui">0</div>
        <div class="battle-options"><button class="battle-btn p1-btn" onclick="handleBattlePress(1, 0)" id="p1-opt-0">A</button> <button class="battle-btn p1-btn" onclick="handleBattlePress(1, 1)" id="p1-opt-1">B</button> <button class="battle-btn p1-btn" onclick="handleBattlePress(1, 2)" id="p1-opt-2">C</button> <button class="battle-btn p1-btn" onclick="handleBattlePress(1, 3)" id="p1-opt-3">D</button></div>
        <h2 class="p1-text" style="margin-top:20px; font-size: 30px;">PLAYER 1</h2>
    </div>
    <div class="battle-side p2-side" id="p2-side">
        <div class="battle-score p2-text" id="p2-score-ui">0</div>
        <div class="battle-options"><button class="battle-btn p2-btn" onclick="handleBattlePress(2, 0)" id="p2-opt-0">A</button> <button class="battle-btn p2-btn" onclick="handleBattlePress(2, 1)" id="p2-opt-1">B</button> <button class="battle-btn p2-btn" onclick="handleBattlePress(2, 2)" id="p2-opt-2">C</button> <button class="battle-btn p2-btn" onclick="handleBattlePress(2, 3)" id="p2-opt-3">D</button></div>
        <h2 class="p2-text" style="margin-top:20px; font-size: 30px;">PLAYER 2</h2>
    </div>
</div>

<div id="wheel-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="menu-header" style="margin-bottom: 0;">
        <h1 class="menu-title" style="color:var(--wheel-accent); text-shadow:0 0 20px var(--wheel-accent);">GÖREV ÇARKI</h1>
    </div>
    <div class="wheel-box">
        <div class="wheel-pointer"></div>
        <canvas id="wheel-canvas" width="550" height="550"></canvas>
    </div>
    <button class="big-btn" onclick="spinWheel()" id="spin-btn" style="border-color:var(--wheel-accent); color:var(--wheel-accent); margin-top: 40px; width: 450px; font-size: 32px;">ÇEVİR!</button>
</div>

<div id="wheel-result-modal">
    <div class="wheel-task-number" id="wheel-task-num">GÖREV #1</div>
    <div class="wheel-task-text" id="wheel-task-text">Bunu Yap!</div>
    <button class="big-btn" onclick="document.getElementById('wheel-result-modal').style.display='none'" style="border-color:var(--success); color:var(--success);">GÖREVİ ALDIM</button>
</div>

<div id="bomb-screen" class="screen" style="z-index: 8;">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="bomb-container" id="bomb-box">
        <div style="color:white; font-size: 16px; letter-spacing: 3px; margin-bottom: 5px;">TIME REMAINING</div>
        <div class="digital-timer" id="bomb-timer-ui">00.00</div>
        <div style="display:flex; justify-content: space-between; width: 100%; margin-bottom: 15px;">
            <span style="color:var(--text-muted); font-size: 20px; font-weight: bold;">Soru: <span id="bomb-q-count">1/4</span></span>
        </div>
        <div class="bomb-question" id="bomb-q-text">Soru Yükleniyor...</div>
        <div class="wires-container" id="bomb-wires">
            <div class="wire w-red" onclick="cutWire(0)" id="w-opt-0">Kablo 1</div>
            <div class="wire w-blue" onclick="cutWire(1)" id="w-opt-1">Kablo 2</div>
            <div class="wire w-green" onclick="cutWire(2)" id="w-opt-2">Kablo 3</div>
            <div class="wire w-yellow" onclick="cutWire(3)" id="w-opt-3">Kablo 4</div>
        </div>
    </div>
</div>

<div id="memory-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="scoreboard">
        <div class="stat-box"><span class="stat-lbl">Eşleşme</span><span id="mem-score-ui" class="stat-val">0/8</span></div>
        <div class="stat-box"><span class="stat-lbl">Hamle</span><span id="mem-moves-ui" class="stat-val">0</span></div>
    </div>
    <div class="memory-grid" id="memory-grid"></div>
</div>

<div id="rain-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="scoreboard" style="margin-top: 10px; width: 60%;">
        <div class="stat-box"><span class="stat-lbl">Skor</span><span id="rain-score-ui" class="stat-val">0</span></div>
        <div class="stat-box"><span class="stat-lbl">Can</span><span id="rain-hp-ui" class="stat-val" style="color:red;">❤️❤️❤️</span></div>
    </div>
    <div id="rain-area" style="position:absolute; top:150px; left:0; width:100%; height:calc(100vh - 300px);"></div>
    <div class="rain-catcher">YAKALA: <span class="rain-target-word" id="rain-target-ui">APPLE</span></div>
</div>

<div id="voltage-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="menu-header"><h1 class="menu-title" style="color:#00ffff; text-shadow:0 0 20px #00ffff;">VOLTAGE CUT</h1><span class="menu-sub">Kabloyu Koparmadan Bağla!</span></div>
    <div style="font-size: 36px; font-weight: 900; margin-top: 10px; text-shadow: 0 0 10px #fff;" id="voltage-target">Hedef: Yükleniyor...</div>
    <div class="voltage-area" id="voltage-area">
        <div class="v-wire" id="v-wire-main"></div>
        <div class="voltage-node v-start" id="v-start-node">BAŞLA</div>
        <div class="voltage-node v-end" id="v-end-node">HEDEF</div>
    </div>
</div>

<div id="crate-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="menu-header" style="margin-top: 50px;"><h1 class="menu-title" style="color:#d97706; text-shadow:0 0 20px #d97706;">CRATE BREAKER</h1><span class="menu-sub">Doğru Kasayı 3 Kere Vurarak Parçala!</span></div>
    <div style="font-size: 55px; font-weight: 900; margin-top: 40px; color: #fff; text-shadow: 0 0 25px #000;" id="crate-q-text">Soru Yükleniyor...</div>
    <div class="crates-container" id="crates-container">
        <div class="crate" id="crate-0" onclick="hitCrate(0)"><div class="crate-q" id="cq-0">A</div></div>
        <div class="crate" id="crate-1" onclick="hitCrate(1)"><div class="crate-q" id="cq-1">B</div></div>
        <div class="crate" id="crate-2" onclick="hitCrate(2)"><div class="crate-q" id="cq-2">C</div></div>
    </div>
</div>

<div id="air-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="scoreboard" style="margin-top: 10px; width: 60%;">
        <div class="stat-box"><span class="stat-lbl">Hedef Bulundu</span><span id="air-score-ui" class="stat-val">0/5</span></div>
    </div>
    <div class="air-target-box" id="air-target-ui">Sinyal Aranıyor...</div>
    <div id="air-zone" style="position: absolute; top: 200px; left: 0; width: 100%; height: calc(100vh - 200px);"></div>
</div>

<div id="tunnel-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="tunnel-bg"></div>
    <div class="tunnel-q" id="tunnel-q-ui">Soru Yükleniyor...</div>
    <div class="tunnel-doors" id="tunnel-doors-area"></div>
</div>

<div id="chem-screen" class="screen">
    <div class="ui-top"><button class="nav-btn btn-exit" onclick="resetGame()">ÇIKIŞ</button></div>
    <div class="menu-header" style="margin-top:20px; margin-bottom:10px;"><h1 class="menu-title" style="color:#10b981; font-size:40px;">CHEM REACTION</h1></div>
    <div class="chem-table">
        <div class="chem-q" id="chem-q-ui">Analiz Ediliyor...</div>
        <div class="beaker" id="chem-beaker"><div class="beaker-liquid" id="chem-liquid"></div></div>
        <div class="flasks" id="chem-flasks-area"></div>
    </div>
</div>

<div id="toast">BONUS COMBO!</div>
<div id="end-screen" class="end-screen">
    <h1 id="end-header" class="end-title">TEBRİKLER!</h1>
    <p id="end-quote" class="end-quote">"Öğrenenlerin geleceği parlaktır."</p>
    <div style="font-size: 55px; color: var(--accent); font-weight: 900; margin-bottom: 40px; text-shadow: 0 0 20px var(--accent);">FİNAL SKOR: <span id="end-score">0</span></div>
    <button class="nav-btn" style="background:var(--accent); color:#000; padding:25px 60px; font-size:24px;" onclick="resetGame()">ANA MENÜYE DÖN</button>
</div>

<div id="rank-up-modal" class="end-screen" style="z-index: 99999; background: rgba(0,0,0,0.95);">
    <h1 class="end-title" style="color: var(--gold); font-size: 90px; text-shadow: 0 0 50px var(--gold); animation: popOut 0.5s reverse forwards;">RANK UP!</h1>
    <div id="new-rank-text" style="font-size: 60px; color: #fff; font-weight: 900; margin-bottom: 30px; text-transform: uppercase;">🌟 GOLD NOVA I</div>
    <div id="unlock-msg" style="font-size: 28px; color: var(--success); margin-bottom: 50px; font-weight: bold; text-shadow: 0 0 15px var(--success); display: none;">🔓 TEBRİKLER! V3.0 GİZLİ OYUNLARIN KİLİDİ AÇILDI!</div>
    <button class="big-btn" onclick="document.getElementById('rank-up-modal').style.display='none'" style="border-color: var(--gold); color: var(--gold); box-shadow: 0 0 20px rgba(251,191,36,0.4);">DEVAM ET</button>
</div>

<script>
    /* ========================================
       SİSTEM DEĞİŞKENLERİ VE VERİTABANI
       ======================================== */
    const MASTER_DICT = {
        1: { desc: "Daily routines and breakfast habits.", words: [{en:"Routine", tr:"Rutin"}, {en:"Nap", tr:"Kestirmek"}, {en:"Diary", tr:"Günlük"}, {en:"Visit", tr:"Ziyaret"}, {en:"Wake up", tr:"Uyanmak"}, {en:"Arrive", tr:"Varmak"}, {en:"Course", tr:"Kurs"}, {en:"Rest", tr:"Dinlenmek"}] },
        2: { desc: "Food, drinks and healthy life.", words: [{en:"Yummy", tr:"Lezzetli"}, {en:"Healthy", tr:"Sağlıklı"}, {en:"Cheese", tr:"Peynir"}, {en:"Butter", tr:"Tereyağı"}, {en:"Honey", tr:"Bal"}, {en:"Bagel", tr:"Simit"}, {en:"Beverage", tr:"İçecek"}, {en:"Jam", tr:"Reçel"}] },
        3: { desc: "Downtown life, streets and busy cities.", words: [{en:" Downtown", tr:"Şehir Merkezi"}, {en:"Street", tr:"Sokak"}, {en:"Skyscraper", tr:"Gökdelen"}, {en:"Crowded", tr:"Kalabalık"}, {en:"Kiosk", tr:"Büfe"}, {en:"Neighborhood", tr:"Mahalle"}, {en:"Pavement", tr:"Kaldırım"}] },
        4: { desc: "Weather conditions and moods.", words: [{en:"Weather", tr:"Hava Durumu"}, {en:"Stormy", tr:"Fırtınalı"}, {en:"Freezing", tr:"Dondurucu"}, {en:"Lightning", tr:"Şimşek"}, {en:" Mood", tr:"Ruh Hali"}, {en:"Anxious", tr:"Endişeli"}, {en:"Frightened", tr:"Korkmuş"}] },
        5: { desc: "Funfairs, bumper cars and thrill.", words: [{en:"Funfair", tr:"Lunapark"}, {en:"Ferris Wheel", tr:"Dönme Dolap"}, {en:"Bumper cars", tr:"Çarpışan araba"}, {en:"Carousel", tr:"Atlı Karınca"}, {en:"Ticket", tr:"Bilet"}, {en:"Thrilling", tr:"Heyecan verici"}, {en:"Amazing", tr:"Şaşırtıcı"}] },
        6: { desc: "Occupations and working places.", words: [{en:"Mechanic", tr:"Tamirci"}, {en:"Vet", tr:"Veteriner"}, {en:"Tailor", tr:"Terzi"}, {en:"Driver", tr:"Şoför"}, {en:"Architect", tr:"Mimar"}, {en:"Engineer", tr:"Mühendis"}, {en:"Dentist", tr:"Diş Hekimi"}] },
        7: { desc: "Vacation, seaside and sightseeing.", words: [{en:"Vacation", tr:"Tatil"}, {en:"Sightseeing", tr:"Şehir Gezisi"}, {en:" Seaside", tr:"Deniz Kenarı"}, {en:" Forest", tr:"Orman"}, {en:" Tent", tr:"Çadır"}, {en:" Skiing", tr:"Kayak yapmak"}, {en:" Hiking", tr:"Doğa yürüyüşü"}] },
        8: { desc: "Bookworms and library rules.", words: [{en:"Bookworm", tr:"Kitap Kurdu"}, {en:"Novel", tr:"Roman"}, {en:"Poetry", tr:"Şiir"}, {en:"Library", tr:"Kütüphane"}, {en:"Shelf", tr:"Raf"}, {en:"Borrow", tr:"Ödünç almak"}, {en:"Dictionary", tr:"Sözlük"}] },
        9: { desc: "Environment, saving the planet.", words: [{en:"Environment", tr:"Çevre"}, {en:"Recycle", tr:"Geri Dönüşüm"}, {en:" Pollution", tr:"Kirlilik"}, {en:"Save", tr:"Korumak"}, {en:" Litter", tr:"Çöp atmak"}, {en:" Waste", tr:"Atık"}] },
        10:{ desc: "Democracy, elections and voting process.", words: [{en:"Election", tr:"Seçim"}, {en:"Vote", tr:"Oy Vermek"}, {en:"Candidate", tr:"Aday"}, {en:"Ballot box", tr:"Sandık"}, {en:" Democracy", tr:"Demokrasi"}, {en:" Presidential", tr:"Başkanlık"}] }
    };

    let GAME_STATE = { mode: '', unit: 1, theme: 'classic', device: 'pc', score: 0, scoreP1: 0, scoreP2: 0, isBattleLocked: false, activeCount: 15, selectedEN: null, selectedTR: null, bonusActive: false, enData: null, trData: null };
    let MINIGAME = { id: '' };
    
    let QUIZ_STATE = { questions: [], currentIdx: 0 }; let BATTLE_Q = null;
    let BOMB_STATE = { timeLimit: 0, totalQs: 0, currentQ: 0, timeRemaining: 0, interval: null, questions: [], isExploded: false, timeMod: 0 };
    let MEMORY_STATE = { cards: [], firstCard: null, secondCard: null, lockBoard: false, matched: 0, moves: 0 };
    let RAIN_STATE = { targetWord: null, hp: 3, interval: null, spawnInterval: null, fallingDivs: [], speedMod: 1 };
    let VOLTAGE_STATE = { isDragging: false, targetWord: null, currentQ: 0, maxQ: 5 };
    let CRATE_STATE = { currentQ: 0, maxQ: 5, hits: [0,0,0], correctIdx: 0, questions: [] };

    const WHEEL_TASKS = [
        "Tahtada zıplayarak 3 İngilizce kelime söyle!", "Sınıfa dön ve İngilizce olarak kendini tanıt!", "Tahtada tek ayak üstünde 3 İngilizce renk say!", "İngilizce 5 tane hayvan ismi söyle!", "Bomb Defuse modunu 10 saniyede oyna!", "Memory Cards modunda 1 tur oyna!", "Yanındaki arkadaşına İngilizce iltifat et!", "En sevdiğin yemeği İngilizce tarif et!", "Sınıftaki 3 eşyanın İngilizcesini söyle!", "İngilizce 1'den 20'ye kadar geriye doğru say!", "Word Rain modunda 1 tur oyna!", "Bugün ne yaptığını İngilizce 3 cümleyle anlat.", "En sevdiğin rengi İngilizce söyle ve o renkte bir eşya göster.", "Tahtaya İngilizce bir kelime çiz, sınıf tahmin etsin!", "İngilizce 3 tane spor dalı say!", "Öğretmenine İngilizce bir soru sor!", "Hızlıca 5 tane İngilizce meyve say!", "15 saniye boyunca durmadan İngilizce konuş!", "İngilizce haftanın günlerini sırayla say!", "İngilizce ayları say!", "ŞANSLISIN! Görevi pas geçiyorsun! 🎉", "İngilizce 3 tane meslek söyle!", "İngilizce hava durumunu tarif et!", "Tahtaya bir çöp adam çiz ve İngilizce vücut bölümlerini yaz!", "İngilizce 3 tane ulaşım aracı söyle!", "Sınıftan birini seç, onunla İngilizce selamlaş!", "İngilizce 3 tane kıyafet ismi söyle!", "İngilizce bildiğin bir şarkının nakaratını söyle!", "Sınıf kurallarından birini İngilizce söyle!", "Şu an saat kaç? İngilizce olarak söyle!", "En sevdiğin filmi İngilizce 2 cümleyle anlat!", "Alfabeyi İngilizce olarak A'dan Z'ye oku!", "İngilizce 3 tane duygu durumu söyle!", "JOKER! İstediğin bir arkadaşına İngilizce bir görev ver!"
    ];
    let WHEEL_STATE = { isSpinning: false, currentRot: 0 };

    /* ========================================
       YENİ EKLENEN: CS2 RANK SİSTEMİ
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
        if(RANK_STATE.level >= RANKS.length - 1) return; // Zirvedesin kral
        RANK_STATE.xp += amount;
        
        let nextRank = RANKS[RANK_STATE.level + 1];
        if(RANK_STATE.xp >= nextRank.xp) {
            RANK_STATE.level++;
            showRankUpModal();
            if(RANK_STATE.level === 5) { // Gold Nova 1'e ulaştık!
                unlockV3Games();
            }
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
        playSound('bonus');
        setTimeout(() => playSound('win'), 500); // Havalı giriş
        document.getElementById('rank-up-modal').style.display = 'flex';
        document.getElementById('new-rank-text').innerText = RANKS[RANK_STATE.level].icon + " " + RANKS[RANK_STATE.level].name;
        
        if(RANK_STATE.level === 5) {
            document.getElementById('unlock-msg').style.display = 'block';
        }
    }

    function unlockV3Games() {
        document.querySelectorAll('.locked-game').forEach(el => { 
            el.classList.remove('locked-game'); 
            el.classList.add('unlocked-game');
            el.innerText = el.dataset.realname; 
        });
        printConsole("Rank Threshold Hit. All restricted modules unlocked automatically.", "success-msg");
    }

    /* ========================================
       MATRIX INTRO & HACKER CONSOLE
       ======================================== */
    let SYS = { auth: false, open: false };

    function playIntro() {
        const c = document.getElementById('intro-container');
        const msgs = ["[SYSTEM]: Initializing Core Framework...", "[SYSTEM]: Loading English Vocabulary Database...", "[SYSTEM]: Integrating Rank Network...", "[WARN]: Security protocol bypassed by User.", "[OK]: Environment ready. Let the games begin."];
        let delay = 0;
        msgs.forEach(m => {
            setTimeout(() => { let p = document.createElement('div'); p.className='intro-log'; p.innerText=m; c.appendChild(p); playSound('correct'); }, delay);
            delay += 600;
        });
        setTimeout(() => {
            document.getElementById('intro-screen').style.display = 'none';
            document.getElementById('main-menu').style.display = 'flex';
            updateRankUI(); // Intro bitince Rank UI'yi güncelle
            playSound('win');
        }, delay + 800);
    }

    function toggleConsole() {
        SYS.open = !SYS.open;
        const con = document.getElementById('dev-console');
        const inp = document.getElementById('console-input');
        if(SYS.open) {
            con.style.top = '0'; inp.focus();
            if(!SYS.auth) { printConsole("Authentication required. Enter password:", "sys-msg"); inp.type = "password"; }
        } else { con.style.top = '-100%'; inp.blur(); }
    }

    document.getElementById('console-input').addEventListener('keydown', function(e) {
        if(e.key === 'Enter') {
            let val = this.value.trim(); this.value = ''; if(val === "") return;
            if(!SYS.auth) {
                if(val === "LETSBEGİN_") { 
                    SYS.auth = true; this.type = "text"; 
                    printConsole("ACCESS GRANTED. Welcome Admin.", "success-msg"); 
                    printConsole("Type /help for command list.", "sys-msg");
                } else { printConsole("ACCESS DENIED. Incorrect password.", "err-msg"); playSound('wrong'); }
            } else { processCommand(val); }
        }
    });

    function printConsole(txt, cls="") {
        const out = document.getElementById('console-output');
        const div = document.createElement('div'); div.className = cls; div.innerText = "> " + txt;
        out.appendChild(div); out.scrollTop = out.scrollHeight;
    }

    function processCommand(cmd) {
        printConsole(cmd, "");
        let args = cmd.split(' '); let c = args[0].toLowerCase();
        if(c === '/help') {
            printConsole("--- COMMAND LIST ---", "sys-msg");
            printConsole("set_gravity <val> : Word Rain hızını değiştirir", "sys-msg");
            printConsole("add_time <sec>    : Bomb Defuse moduna süre ekler", "sys-msg");
            printConsole("matrix_mode       : Temayı kod akışına çevirir", "sys-msg");
            printConsole("unlock_all        : Kilitli tüm minigameleri açar", "sys-msg");
            printConsole("set_rank <level>  : Rütbeyi hileyle zorlar (0-5)", "sys-msg");
            printConsole("clear             : Konsolu temizler", "sys-msg");
            printConsole("exit              : Konsolu kapatır", "sys-msg");
        } else if(c === 'set_gravity') {
            RAIN_STATE.speedMod = parseFloat(args[1]) || 1; printConsole(`Gravity set to ${RAIN_STATE.speedMod}`, "success-msg");
        } else if(c === 'add_time') {
            let t = parseInt(args[1]) || 0; BOMB_STATE.timeMod += t; BOMB_STATE.timeRemaining += (t*1000); printConsole(`Added ${t} seconds.`, "success-msg");
        } else if(c === 'matrix_mode') {
            document.body.style.background = "#000"; document.documentElement.style.setProperty('--accent', '#00ff41'); document.documentElement.style.setProperty('--panel-bg', 'rgba(0,20,0,0.9)'); printConsole("Matrix loaded.", "success-msg");
        } else if(c === 'unlock_all') { 
            unlockV3Games(); playSound('bonus');
        } else if(c === 'set_rank') {
            let level = parseInt(args[1]);
            if(level >= 0 && level <= 5) {
                RANK_STATE.level = level;
                RANK_STATE.xp = RANKS[level].xp;
                updateRankUI();
                if(level === 5) unlockV3Games();
                printConsole(`Rank set to ${RANKS[level].name}`, "success-msg");
            }
        } else if(c === 'clear') { document.getElementById('console-output').innerHTML = '';
        } else if(c === 'exit') { toggleConsole();
        } else { printConsole(`Command not found: ${c}`, "err-msg"); }
    }

    /* ========================================
       SES VE BİLDİRİM MOTORU
       ======================================== */
    const AUDIO_FILES = {
        classic: { correct: 'https://actions.google.com/sounds/v1/water/splash.ogg', wrong: 'https://actions.google.com/sounds/v1/alarms/beep_short.ogg', win: 'https://actions.google.com/sounds/v1/human_voices/applause.ogg', bonus: 'https://actions.google.com/sounds/v1/cartoon/conga_drum_hit.ogg' },
        cs2: { correct: 'https://actions.google.com/sounds/v1/weapons/firework_rocket_launch.ogg', wrong: 'https://actions.google.com/sounds/v1/alarms/digital_alarm_clock.ogg', win: 'https://actions.google.com/sounds/v1/science_fiction/low_fuzz_explosion.ogg', bonus: 'https://actions.google.com/sounds/v1/weapons/automatic_gun_fire.ogg' }
    };
    function playSound(t) { let src = (AUDIO_FILES[GAME_STATE.theme] || AUDIO_FILES['classic'])[t]; if(src){ let a=new Audio(src); a.volume=0.5; let p=a.play(); if(p!==undefined)p.catch(()=>{}); } }
    function showToast(msg) { const t = document.getElementById('toast'); t.innerText = msg; t.style.display = 'block'; t.style.animation = 'popOut 1.5s forwards'; setTimeout(() => { t.style.display = 'none'; t.style.animation = ''; }, 1500); }
    function showFeedback(txt, cls) { let p = document.getElementById('msg-popup'); if(!p){p=document.createElement('div');p.id='msg-popup';p.style.cssText="position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);font-size:55px;font-weight:900;z-index:9000;text-shadow:0 5px 20px #000;background:rgba(0,0,0,0.9);padding:20px 50px;border-radius:50px;";document.body.appendChild(p);} p.innerText = txt; p.style.display = 'block'; p.style.color = (cls==="correct-flash") ? "#22c55e" : "#ef4444"; setTimeout(() => p.style.display = 'none', 600); }

    /* ========================================
       NAVİGASYON VE AYARLAR
       ======================================== */
    function showScreen(id) { document.querySelectorAll('.screen').forEach(el => el.style.display = 'none'); document.getElementById(id).style.display = 'flex'; }
    function selectMode(m) { GAME_STATE.mode = m; MINIGAME.id = ''; showScreen('unit-menu'); }
    function selectMinigame(id) { MINIGAME.id = id; GAME_STATE.mode = 'minigame'; if(id==='bomb') showScreen('bomb-settings-menu'); else if(id==='wheel') initWheel(); else showScreen('unit-menu'); }
    function setBombSettings(t, q) { BOMB_STATE.timeLimit = t; BOMB_STATE.totalQs = q; showScreen('unit-menu'); }
    
    function resetGame() {
        document.getElementById('end-screen').style.display = 'none'; document.body.classList.remove('exploded-bg');
        clearInterval(BOMB_STATE.interval); clearInterval(RAIN_STATE.interval); clearInterval(RAIN_STATE.spawnInterval);
        RAIN_STATE.fallingDivs.forEach(d => { if(d && d.parentNode) d.parentNode.removeChild(d); }); RAIN_STATE.fallingDivs = [];
        WHEEL_STATE.isSpinning = false; VOLTAGE_STATE.isDragging = false;
        
        // V3 clear intervals if any
        if(window.v3AirInterval) clearTimeout(window.v3AirInterval);
        
        showScreen('main-menu');
    }

    const unitRoot = document.getElementById('unit-root');
    for (let i = 1; i <= 10; i++) {
        if(!MASTER_DICT[i]) continue;
        const card = document.createElement('div'); card.className = 'unit-card';
        card.innerHTML = `<h2>Ünite ${i}</h2><hr><p>${MASTER_DICT[i].desc}</p>`; card.onclick = () => startGame(i); unitRoot.appendChild(card);
    }

    function applyTheme(t) {
        GAME_STATE.theme = t; const s = document.documentElement.style;
        if(t==='subnautica') { s.setProperty('--accent', '#00ffff'); s.setProperty('--bg-dark', '#001a33'); s.setProperty('--panel-bg', 'rgba(0, 26, 51, 0.9)'); }
        else if(t==='cs2') { s.setProperty('--accent', '#fbbf24'); s.setProperty('--bg-dark', '#111'); s.setProperty('--panel-bg', 'rgba(20, 20, 20, 0.95)'); }
        else if(t==='alastor') { s.setProperty('--accent', '#ef4444'); s.setProperty('--bg-dark', '#2a0000'); s.setProperty('--panel-bg', 'rgba(40, 0, 0, 0.9)'); }
        else if(t==='vox') { s.setProperty('--accent', '#06b6d4'); s.setProperty('--bg-dark', '#081c24'); s.setProperty('--panel-bg', 'rgba(0, 30, 45, 0.9)'); }
        else { s.setProperty('--accent', '#38bdf8'); s.setProperty('--bg-dark', '#070b14'); s.setProperty('--panel-bg', 'rgba(15, 23, 42, 0.95)'); }
        document.querySelectorAll('#mods-menu .mod-btn').forEach(b => b.classList.remove('active')); document.getElementById('btn-theme-' + t).classList.add('active');
    }
    function setDevice(type) { GAME_STATE.device = type; document.querySelectorAll('#settings-menu .mod-btn').forEach(b=>b.classList.remove('active')); document.getElementById('btn-dev-'+type).classList.add('active'); }
    applyTheme('classic'); setDevice('pc');

    /* ========================================
       OYUN BAŞLATICI (ROUTER)
       ======================================== */
    function startGame(uId) {
        GAME_STATE.unit = uId; GAME_STATE.score = 0;
        let uWords = MASTER_DICT[uId].words; let aWords = []; Object.values(MASTER_DICT).forEach(u => aWords.push(...u.words));
        
        if (GAME_STATE.mode === 'minigame') {
            if(MINIGAME.id === 'bomb') startBombDefuse(uWords, aWords);
            else if(MINIGAME.id === 'memory') startMemoryCards(uWords);
            else if(MINIGAME.id === 'rain') startWordRain(uWords);
            else if(MINIGAME.id === 'voltage') startVoltageCut(uWords, aWords);
            else if(MINIGAME.id === 'crate') startCrateBreaker(uWords, aWords);
            // V3 YENİ EKLENEN OYUNLARIN YÖNLENDİRMESİ:
            else if(MINIGAME.id === 'air') startAirDrop(uWords, aWords);
            else if(MINIGAME.id === 'tunnel') startTunnel(uWords, aWords);
            else if(MINIGAME.id === 'chem') startChem(uWords, aWords);
            return;
        }

        if (GAME_STATE.mode === 'wordmatch') {
            GAME_STATE.activeCount = 15; GAME_STATE.enData = null; GAME_STATE.trData = null; GAME_STATE.bonusActive = false;
            activeGamePool = []; let att = 0; while(activeGamePool.length < 15 && att < 100) { let r = aWords[Math.floor(Math.random()*aWords.length)]; if(!activeGamePool.find(x => x.en === r.en)) activeGamePool.push(r); att++; }
            showScreen('game-screen'); updateWMUI(); buildGrids(); setTimeout(scanForBonus, 800);
        } else if (GAME_STATE.mode === 'quiz') {
            let sel = [...uWords].sort(()=>Math.random()-0.5).slice(0, 10);
            QUIZ_STATE.questions = sel.map(w => { let o = [w.tr]; while(o.length < 4) { let r = aWords[Math.floor(Math.random()*aWords.length)].tr; if(!o.includes(r)) o.push(r); } return { en: w.en, correct: w.tr, options: o.sort(()=>Math.random()-0.5) }; });
            QUIZ_STATE.currentIdx = 0; showScreen('quiz-screen'); loadQuizQuestion(); updateQuizUI();
        } else if (GAME_STATE.mode === 'battle') {
            GAME_STATE.scoreP1 = 0; GAME_STATE.scoreP2 = 0; document.getElementById('p1-score-ui').innerText = "0"; document.getElementById('p2-score-ui').innerText = "0"; showScreen('battle-screen'); nextBattleQuestion();
        }
    }

    /* ========================================
       V3.0 OYUN MOTORLARI (TAM SÜRÜM)
       ======================================== */

    /* 1. AIR DROP SCAN LOGIC */
    let AIR_STATE = { count: 0, max: 5, currentQ: null };
    function startAirDrop(uWords, aWords) {
        showScreen('air-screen'); AIR_STATE.count = 0; GAME_STATE.score = 0; 
        document.getElementById('air-score-ui').innerText = "0/5"; 
        let zone = document.getElementById('air-zone'); zone.innerHTML = '';
        
        function nextDrop() {
            if(AIR_STATE.count >= AIR_STATE.max) { triggerFinal(false, "SCAN COMPLETE!", "Radyo sinyali tertemiz. Eşyalar senin!"); return; }
            AIR_STATE.currentQ = uWords[Math.floor(Math.random()*uWords.length)];
            document.getElementById('air-target-ui').innerText = `RADAR: ${AIR_STATE.currentQ.tr}`;
            
            zone.innerHTML = '';
            let options = [AIR_STATE.currentQ.en];
            while(options.length < 3) { let r = aWords[Math.floor(Math.random()*aWords.length)].en; if(!options.includes(r)) options.push(r); }
            options.sort(()=>Math.random()-0.5);

            options.forEach((opt, idx) => {
                let d = document.createElement('div'); d.className = 'air-crate'; d.innerText = opt;
                d.style.left = (20 + idx * 30) + "%"; d.style.top = "-200px";
                let p = document.createElement('div'); p.className = 'parachute'; d.appendChild(p);
                
                // Animasyon ekle (hız rastgele)
                let dur = 3 + Math.random()*2;
                d.style.animation = `airdropFall ${dur}s linear forwards`;
                
                d.onclick = () => {
                    if(opt === AIR_STATE.currentQ.en) {
                        playSound('win'); d.style.background = "var(--success)"; d.innerHTML = "GÜVENLİ"; 
                        GAME_STATE.score += 200; addXP(100); showToast("DROP ALINDI!");
                        AIR_STATE.count++; document.getElementById('air-score-ui').innerText = `${AIR_STATE.count}/5`;
                        Array.from(zone.children).forEach(c => c.style.pointerEvents = 'none');
                        window.v3AirInterval = setTimeout(nextDrop, 1000);
                    } else {
                        playSound('wrong'); d.style.background = "var(--danger)"; d.innerHTML = "BOOM!";
                        Array.from(zone.children).forEach(c => c.style.pointerEvents = 'none');
                        setTimeout(() => triggerFinal(false, "SİNYAL KOPTU!", "Yanlış kutuyu açtın, düşman yerini tespit etti."), 1000);
                    }
                };
                zone.appendChild(d);
            });
        }
        nextDrop();
    }

    /* 2. GRAVITY TUNNEL LOGIC */
    let TUNNEL_STATE = { count: 0, max: 5 };
    function startTunnel(uWords, aWords) {
        showScreen('tunnel-screen'); TUNNEL_STATE.count = 0; GAME_STATE.score = 0;
        
        function nextDoor() {
            if(TUNNEL_STATE.count >= TUNNEL_STATE.max) { triggerFinal(false, "TÜNEL AŞILDI!", "Işık hızına ulaştın ve sağ kurtuldun."); return; }
            let q = uWords[Math.floor(Math.random()*uWords.length)];
            document.getElementById('tunnel-q-ui').innerText = `HEDEF: ${q.en}`;
            
            let area = document.getElementById('tunnel-doors-area'); area.innerHTML = '';
            let opts = [q.tr];
            while(opts.length < 3) { let r = aWords[Math.floor(Math.random()*aWords.length)].tr; if(!opts.includes(r)) opts.push(r); }
            opts.sort(()=>Math.random()-0.5);

            opts.forEach(opt => {
                let d = document.createElement('div'); d.className = 't-door'; d.innerText = opt;
                d.onclick = () => {
                    if(opt === q.tr) {
                        playSound('win'); d.style.borderColor = "var(--success)"; d.style.boxShadow = "inset 0 0 50px var(--success)";
                        GAME_STATE.score += 150; addXP(100); showToast("DOĞRU KAPI!");
                        TUNNEL_STATE.count++; setTimeout(nextDoor, 800);
                    } else {
                        playSound('wrong'); d.style.borderColor = "var(--danger)"; d.style.background = "var(--danger)";
                        setTimeout(() => triggerFinal(false, "DUVARA ÇARPTIN!", "Yanlış kapıya girdin, tünel çöktü."), 1000);
                    }
                };
                area.appendChild(d);
            });
        }
        nextDoor();
    }

    /* 3. CHEM REACTION LOGIC */
    let CHEM_STATE = { count: 0, max: 5 };
    function startChem(uWords, aWords) {
        showScreen('chem-screen'); CHEM_STATE.count = 0; GAME_STATE.score = 0;
        
        function nextReaction() {
            if(CHEM_STATE.count >= CHEM_STATE.max) { triggerFinal(false, "FORMÜL TAMAM!", "Mükemmel reaksiyon, yeni elementi buldun."); return; }
            let q = uWords[Math.floor(Math.random()*uWords.length)];
            document.getElementById('chem-q-ui').innerText = `Sentez: ${q.tr}`;
            
            let liq = document.getElementById('chem-liquid');
            liq.style.height = "20%"; liq.style.background = "#10b981"; liq.innerText = "";
            
            let area = document.getElementById('chem-flasks-area'); area.innerHTML = '';
            let opts = [q.en];
            while(opts.length < 3) { let r = aWords[Math.floor(Math.random()*aWords.length)].en; if(!opts.includes(r)) opts.push(r); }
            opts.sort(()=>Math.random()-0.5);

            opts.forEach(opt => {
                let f = document.createElement('div'); f.className = 'flask'; f.innerText = opt;
                f.onclick = () => {
                    if(opt === q.en) {
                        playSound('win'); GAME_STATE.score += 180; addXP(150);
                        liq.style.height = "90%"; liq.style.background = "var(--accent)"; liq.innerText = "SUCCESS";
                        f.style.animation = "explosionChem 0.5s forwards";
                        CHEM_STATE.count++; setTimeout(nextReaction, 1500);
                    } else {
                        playSound('wrong');
                        liq.style.height = "100%"; liq.style.background = "var(--danger)"; liq.innerText = "DANGER";
                        f.style.animation = "badExplosion 0.5s forwards";
                        setTimeout(() => triggerFinal(false, "LABORATUVAR PATLADI!", "Yanlış kimyasal karıştırdın!"), 1000);
                    }
                };
                area.appendChild(f);
            });
        }
        nextReaction();
    }


    /* ========================================
       YENİ MİNİGAME: CRATE BREAKER (Kasa Kırma)
       ======================================== */
    function startCrateBreaker(uWords, aWords) {
        showScreen('crate-screen'); CRATE_STATE.currentQ = 0; GAME_STATE.score = 0;
        CRATE_STATE.questions = []; let pool = [...uWords].sort(()=>Math.random()-0.5);
        for(let i=0; i<CRATE_STATE.maxQ; i++) {
            let q = pool[i % pool.length]; let opts = [q.tr];
            while(opts.length < 3) { let r = aWords[Math.floor(Math.random()*aWords.length)].tr; if(!opts.includes(r)) opts.push(r); }
            CRATE_STATE.questions.push({ en: q.en, correct: q.tr, options: opts.sort(()=>Math.random()-0.5) });
        }
        loadCrateQuestion();
    }
    
    function loadCrateQuestion() {
        if(CRATE_STATE.currentQ >= CRATE_STATE.maxQ) { triggerFinal(false, "KASALAR KIRILDI! 📦", "Tüm ganimeti topladın!"); return; }
        CRATE_STATE.hits = [0,0,0]; let q = CRATE_STATE.questions[CRATE_STATE.currentQ];
        document.getElementById('crate-q-text').innerText = `"${q.en}"`;
        for(let i=0; i<3; i++) {
            let c = document.getElementById('crate-'+i); c.className = 'crate'; c.innerText = ""; c.style.pointerEvents = 'auto';
            let cq = document.createElement('div'); cq.className = 'crate-q'; cq.innerText = q.options[i];
            c.appendChild(cq);
            if(q.options[i] === q.correct) CRATE_STATE.correctIdx = i;
        }
    }

    function hitCrate(idx) {
        let c = document.getElementById('crate-'+idx);
        if(c.classList.contains('crate-broken')) return;
        CRATE_STATE.hits[idx]++; playSound('correct');
        
        if(CRATE_STATE.hits[idx] === 1) c.classList.add('crate-cracked-1');
        else if(CRATE_STATE.hits[idx] === 2) c.classList.add('crate-cracked-2');
        else if(CRATE_STATE.hits[idx] === 3) {
            c.classList.add('crate-broken');
            if(idx === CRATE_STATE.correctIdx) {
                playSound('win'); GAME_STATE.score += 200; addXP(200); c.innerText = "+200 XP"; showToast("CRATE OPENED!");
                for(let i=0;i<3;i++) document.getElementById('crate-'+i).style.pointerEvents='none';
                setTimeout(() => { CRATE_STATE.currentQ++; loadCrateQuestion(); }, 1500);
            } else {
                playSound('wrong'); c.innerText = "BOOM!"; c.style.color = "red"; showFeedback("YANLIŞ KASA!", "wrong-flash");
                for(let i=0;i<3;i++) document.getElementById('crate-'+i).style.pointerEvents='none';
                setTimeout(() => { CRATE_STATE.currentQ++; loadCrateQuestion(); }, 1500);
            }
        }
    }

    /* ========================================
       YENİ MİNİGAME: VOLTAGE CUT (Kablo Bağlama)
       ======================================== */
    function startVoltageCut(uWords, aWords) {
        showScreen('voltage-screen'); VOLTAGE_STATE.currentQ = 0; GAME_STATE.score = 0;
        loadVoltageQuestion(uWords, aWords);
    }

    function loadVoltageQuestion(uWords, aWords) {
        if(VOLTAGE_STATE.currentQ >= VOLTAGE_STATE.maxQ) { triggerFinal(false, "GÜÇ AKTARILDI! ⚡", "Sistemi başarıyla tamir ettin."); return; }
        let q = uWords[Math.floor(Math.random() * uWords.length)];
        document.getElementById('voltage-target').innerText = `Bağla: ${q.en} -> ${q.tr}`;
        
        let area = document.getElementById('voltage-area'); let startNode = document.getElementById('v-start-node'); let endNode = document.getElementById('v-end-node'); let wire = document.getElementById('v-wire-main');
        startNode.innerText = q.en; endNode.innerText = q.tr;
        
        endNode.style.top = (Math.random() * 60 + 20) + "%"; // Rastgele Y ekseni
        wire.style.width = '0px'; wire.classList.remove('v-active-wire'); VOLTAGE_STATE.isDragging = false;

        const handleMove = (x, y) => {
            if(!VOLTAGE_STATE.isDragging) return;
            let dx = x - startNode.offsetLeft - 50; let dy = y - startNode.offsetTop - 50;
            let length = Math.sqrt(dx*dx + dy*dy); let angle = Math.atan2(dy, dx) * 180 / Math.PI;
            wire.style.width = length + 'px'; wire.style.transform = `rotate(${angle}deg)`;

            let endRect = endNode.getBoundingClientRect(); let areaRect = area.getBoundingClientRect();
            let absX = x + areaRect.left; let absY = y + areaRect.top;
            
            if(absX > endRect.left && absX < endRect.right && absY > endRect.top && absY < endRect.bottom) {
                VOLTAGE_STATE.isDragging = false; playSound('correct'); GAME_STATE.score += 150; addXP(150); showToast("BAĞLANTI TAMAM!");
                setTimeout(() => { VOLTAGE_STATE.currentQ++; loadVoltageQuestion(uWords, aWords); }, 1000);
            }
        };

        const handleEnd = () => {
            if(VOLTAGE_STATE.isDragging) {
                VOLTAGE_STATE.isDragging = false; playSound('wrong'); area.classList.add('zap-effect'); setTimeout(()=>area.classList.remove('zap-effect'), 300);
                wire.style.width = '0px'; wire.classList.remove('v-active-wire');
            }
        };

        startNode.onmousedown = (e) => { VOLTAGE_STATE.isDragging = true; wire.classList.add('v-active-wire'); wire.style.left = (startNode.offsetLeft + 50) + 'px'; wire.style.top = (startNode.offsetTop + 50) + 'px'; };
        startNode.ontouchstart = (e) => { e.preventDefault(); VOLTAGE_STATE.isDragging = true; wire.classList.add('v-active-wire'); wire.style.left = (startNode.offsetLeft + 50) + 'px'; wire.style.top = (startNode.offsetTop + 50) + 'px'; };
        
        area.onmousemove = (e) => { let r = area.getBoundingClientRect(); handleMove(e.clientX - r.left, e.clientY - r.top); };
        area.ontouchmove = (e) => { e.preventDefault(); let r = area.getBoundingClientRect(); handleMove(e.touches[0].clientX - r.left, e.touches[0].clientY - r.top); };
        
        area.onmouseup = area.onmouseleave = handleEnd;
        area.ontouchend = area.ontouchcancel = handleEnd;
    }

    /* ========================================
       ÇARKIFELEK (WHEEL OF FORTUNE) MOTORU
       ======================================== */
    function initWheel() { showScreen('wheel-screen'); drawWheelCanvas(); document.getElementById('wheel-canvas').style.transform = `rotate(0deg)`; WHEEL_STATE.currentRot = 0; WHEEL_STATE.isSpinning = false; document.getElementById('spin-btn').innerText = "ÇEVİR!"; }
    function drawWheelCanvas() {
        const ctx = document.getElementById('wheel-canvas').getContext('2d'); const slices = WHEEL_TASKS.length; const ang = (2*Math.PI)/slices; const cols = ["#ef4444", "#3b82f6", "#22c55e", "#eab308", "#a855f7", "#f43f5e"];
        ctx.clearRect(0,0,550,550); ctx.translate(275,275);
        for(let i=0; i<slices; i++) { ctx.beginPath(); ctx.moveTo(0,0); ctx.arc(0,0,275, i*ang, (i+1)*ang); ctx.fillStyle=cols[i%cols.length]; ctx.fill(); ctx.stroke(); ctx.save(); ctx.rotate(i*ang+ang/2); ctx.textAlign="right"; ctx.textBaseline="middle"; ctx.fillStyle="#fff"; ctx.font="bold 16px Arial"; ctx.fillText(i+1, 250, 0); ctx.restore(); } ctx.translate(-275,-275);
    }
    function spinWheel() {
        if(WHEEL_STATE.isSpinning) return; WHEEL_STATE.isSpinning = true; document.getElementById('spin-btn').innerText = "DÖNÜYOR..."; playSound('correct');
        let total = ((5+Math.random()*5)*360) + Math.floor(Math.random()*360); WHEEL_STATE.currentRot += total;
        document.getElementById('wheel-canvas').style.transform = `rotate(${WHEEL_STATE.currentRot}deg)`;
        setTimeout(() => {
            WHEEL_STATE.isSpinning = false; document.getElementById('spin-btn').innerText = "YENİDEN ÇEVİR!"; playSound('win');
            let deg = (360 - (WHEEL_STATE.currentRot % 360) + 270) % 360; let idx = Math.floor(deg / (360/WHEEL_TASKS.length));
            document.getElementById('wheel-task-num').innerText = `GÖREV KARTI #${idx + 1}`; document.getElementById('wheel-task-text').innerText = WHEEL_TASKS[idx]; document.getElementById('wheel-result-modal').style.display = 'flex';
            addXP(100); // Çark çevirdi diye biraz XP ver
        }, 4100);
    }

    /* ========================================
       BOMB DEFUSE MOTORU
       ======================================== */
    function startBombDefuse(uWords, aWords) {
        showScreen('bomb-screen'); document.body.classList.remove('exploded-bg'); BOMB_STATE.isExploded = false; BOMB_STATE.currentQ = 0; BOMB_STATE.timeRemaining = (BOMB_STATE.timeLimit + BOMB_STATE.timeMod) * 1000;
        BOMB_STATE.questions = []; let pool = [...uWords].sort(()=>Math.random()-0.5);
        for(let i=0; i<BOMB_STATE.totalQs; i++) { let q = pool[i%pool.length]; let opts = [q.tr]; while(opts.length<4) { let r = aWords[Math.floor(Math.random()*aWords.length)].tr; if(!opts.includes(r)) opts.push(r); } BOMB_STATE.questions.push({ en: q.en, correct: q.tr, options: opts.sort(()=>Math.random()-0.5) }); }
        loadBombQuestion(); clearInterval(BOMB_STATE.interval); let lastUpdate = Date.now();
        BOMB_STATE.interval = setInterval(() => { if(BOMB_STATE.isExploded) return; let dt = Date.now()-lastUpdate; lastUpdate = Date.now(); BOMB_STATE.timeRemaining -= dt; if(BOMB_STATE.timeRemaining <= 0) { BOMB_STATE.timeRemaining = 0; updateBombTimerUI(); explodeBomb(); } else updateBombTimerUI(); }, 50);
    }
    function updateBombTimerUI() { let secs = Math.floor(BOMB_STATE.timeRemaining/1000), ms = Math.floor((BOMB_STATE.timeRemaining%1000)/10); document.getElementById('bomb-timer-ui').innerText = `${secs.toString().padStart(2,'0')}.${ms.toString().padStart(2,'0')}`; }
    function loadBombQuestion() {
        if(BOMB_STATE.currentQ >= BOMB_STATE.totalQs) { defuseBombWin(); return; }
        let q = BOMB_STATE.questions[BOMB_STATE.currentQ]; document.getElementById('bomb-q-text').innerText = `"${q.en}"`; document.getElementById('bomb-q-count').innerText = `${BOMB_STATE.currentQ + 1}/${BOMB_STATE.totalQs}`;
        for(let i=0; i<4; i++) { let w = document.getElementById('w-opt-'+i); w.innerText = q.options[i]; w.className = 'wire w-' + ['red','blue','green','yellow'][i]; }
    }
    function cutWire(idx) {
        if(BOMB_STATE.isExploded) return; let w = document.getElementById('w-opt-'+idx); if(w.classList.contains('cut')) return; w.classList.add('cut');
        if(w.innerText === BOMB_STATE.questions[BOMB_STATE.currentQ].correct) { playSound('correct'); BOMB_STATE.currentQ++; setTimeout(loadBombQuestion, 400); } else { w.classList.add('cut-wrong'); explodeBomb(); }
    }
    function explodeBomb() { BOMB_STATE.isExploded = true; clearInterval(BOMB_STATE.interval); playSound('wrong'); document.body.classList.add('exploded-bg'); document.getElementById('bomb-timer-ui').innerText="ERR.OR"; document.getElementById('bomb-timer-ui').style.color="#000"; document.getElementById('bomb-timer-ui').style.background="#ef4444"; setTimeout(() => { triggerFinal(false, "BOMBA PATLADI! 💥", "Süre doldu veya yanlış kestin."); }, 1500); }
    function defuseBombWin() { BOMB_STATE.isExploded = true; clearInterval(BOMB_STATE.interval); playSound('win'); GAME_STATE.score += Math.floor(BOMB_STATE.timeLimit*100 + BOMB_STATE.timeRemaining/10); addXP(BOMB_STATE.timeLimit*40); document.getElementById('bomb-timer-ui').style.color="#22c55e"; setTimeout(() => triggerFinal(false, "BOMB DEFUSED! 🛡️", "Şehri kurtardın!"), 1000); }

    /* ========================================
       MEMORY CARDS MOTORU (3D FLIP)
       ======================================== */
    function startMemoryCards(uWords) {
        showScreen('memory-screen'); MEMORY_STATE.matched=0; MEMORY_STATE.moves=0; MEMORY_STATE.firstCard=null; MEMORY_STATE.lockBoard=false; document.getElementById('mem-score-ui').innerText=`0/8`; document.getElementById('mem-moves-ui').innerText=`0`;
        let pool = [...uWords].sort(()=>Math.random()-0.5).slice(0,8); MEMORY_STATE.cards=[]; pool.forEach(w=>{ MEMORY_STATE.cards.push({text:w.en,pair:w.en}); MEMORY_STATE.cards.push({text:w.tr,pair:w.en}); }); MEMORY_STATE.cards.sort(()=>Math.random()-0.5);
        const grid=document.getElementById('memory-grid'); grid.innerHTML='';
        MEMORY_STATE.cards.forEach(c=>{ let d=document.createElement('div'); d.className='mem-card'; d.dataset.pair=c.pair; d.onclick=()=>flipMemoryCard(d); let inn=document.createElement('div'); inn.className='mem-inner'; let f=document.createElement('div'); f.className='mem-front'; f.innerText="?"; let b=document.createElement('div'); b.className='mem-back'; b.innerText=c.text; inn.appendChild(f); inn.appendChild(b); d.appendChild(inn); grid.appendChild(d); });
    }
    function flipMemoryCard(c) {
        if(MEMORY_STATE.lockBoard||c===MEMORY_STATE.firstCard||c.classList.contains('matched')) return; c.classList.add('flipped');
        if(!MEMORY_STATE.firstCard) { MEMORY_STATE.firstCard=c; return; } MEMORY_STATE.secondCard=c; MEMORY_STATE.lockBoard=true; MEMORY_STATE.moves++; document.getElementById('mem-moves-ui').innerText=MEMORY_STATE.moves;
        if(MEMORY_STATE.firstCard.dataset.pair===MEMORY_STATE.secondCard.dataset.pair) { playSound('correct'); GAME_STATE.score+=200; addXP(100); MEMORY_STATE.firstCard.classList.add('matched'); MEMORY_STATE.secondCard.classList.add('matched'); MEMORY_STATE.matched++; document.getElementById('mem-score-ui').innerText=`${MEMORY_STATE.matched}/8`; MEMORY_STATE.firstCard=null; MEMORY_STATE.lockBoard=false; if(MEMORY_STATE.matched===8) setTimeout(()=>triggerFinal(false,"HAFIZA USTASI! 🧠",`${MEMORY_STATE.moves} hamlede bitirdin.`),800); } else { playSound('wrong'); setTimeout(()=>{MEMORY_STATE.firstCard.classList.remove('flipped');MEMORY_STATE.secondCard.classList.remove('flipped');MEMORY_STATE.firstCard=null;MEMORY_STATE.lockBoard=false;},1000); }
    }

    /* ========================================
       WORD RAIN MOTORU
       ======================================== */
    function startWordRain(uWords) {
        showScreen('rain-screen'); RAIN_STATE.hp=3; GAME_STATE.score=0; RAIN_STATE.fallingDivs=[]; updateRainUI(); let aWords=[]; Object.values(MASTER_DICT).forEach(u=>aWords.push(...u.words)); const area=document.getElementById('rain-area'); area.innerHTML='';
        function setTarget() { let r=uWords[Math.floor(Math.random()*uWords.length)]; RAIN_STATE.targetWord=r; document.getElementById('rain-target-ui').innerText=`"${r.en}"`; } setTarget();
        RAIN_STATE.spawnInterval = setInterval(() => { let isT=Math.random()>0.6; let dText=isT?RAIN_STATE.targetWord.tr:aWords[Math.floor(Math.random()*aWords.length)].tr; let d=document.createElement('div'); d.className='raindrop'; d.innerText=dText; d.style.left=Math.floor(Math.random()*80)+10+"%"; d.style.animation=`rainFall ${4/RAIN_STATE.speedMod}s linear forwards`; d.onclick=()=>{ if(isT&&d.innerText===RAIN_STATE.targetWord.tr){ playSound('correct'); d.classList.add('rain-explode'); GAME_STATE.score+=150; addXP(50); updateRainUI(); setTimeout(()=>{area.innerHTML=''; RAIN_STATE.fallingDivs=[]; setTarget();},300); } else { playSound('wrong'); showFeedback("YANLIŞ!","wrong-flash"); d.style.background="red"; RAIN_STATE.hp--; updateRainUI(); if(RAIN_STATE.hp<=0){clearInterval(RAIN_STATE.interval);clearInterval(RAIN_STATE.spawnInterval);triggerFinal(false,"OYUN BİTTİ 🌧️","Kelime kaçtı!");} } }; area.appendChild(d); RAIN_STATE.fallingDivs.push(d); }, 1500 / RAIN_STATE.speedMod);
        RAIN_STATE.interval = setInterval(()=>{ RAIN_STATE.fallingDivs.forEach((d,i)=>{ if(!d)return; if(d.getBoundingClientRect().top>window.innerHeight-150){ if(d.innerText===RAIN_STATE.targetWord.tr){ playSound('wrong'); showFeedback("-1 CAN!","wrong-flash"); RAIN_STATE.hp--; updateRainUI(); if(RAIN_STATE.hp<=0){clearInterval(RAIN_STATE.interval);clearInterval(RAIN_STATE.spawnInterval);triggerFinal(false,"OYUN BİTTİ 🌧️","Kelime kaçtı!");}else setTarget(); } if(d.parentNode)d.parentNode.removeChild(d); RAIN_STATE.fallingDivs[i]=null; } }); RAIN_STATE.fallingDivs=RAIN_STATE.fallingDivs.filter(x=>x!==null); }, 100);
    }
    function updateRainUI() { document.getElementById('rain-score-ui').innerText=GAME_STATE.score; document.getElementById('rain-hp-ui').innerText="❤️".repeat(RAIN_STATE.hp)||"💀"; }

    /* ========================================
       KLASİK OYUN MOTORLARI (ÖZET)
       ======================================== */
    function buildGrids() { renderGrid('en-grid','en'); renderGrid('tr-grid','tr'); }
    function renderGrid(id, type) { const c=document.getElementById(id); c.innerHTML=''; if(!GAME_STATE[type+'Data']){ let p=[...activeGamePool].sort(()=>Math.random()-0.5); GAME_STATE[type+'Data']=[]; for(let i=0;i<15;i++)GAME_STATE[type+'Data'].push(p[i]); } GAME_STATE[type+'Data'].forEach((w,i)=>{ if(!w)return; let row=Math.floor(i/3), col=i%3, colr=w.color!==undefined?w.color:Math.floor(Math.random()*4); w.color=colr; let d=document.createElement('div'); d.innerText=type==='en'?w.en:w.tr; d.dataset.index=i; d.dataset.type=type; d.dataset.pair=w.pair||w.en; d.dataset.color=type==='tr'?'tr':colr; d.onclick=()=>onTileClick(d); d.className=`tile ${type==='tr'?'tr-tile':'c-'+colr}`; d.style.left=(col*132+20)+"px"; d.style.top=(row*97+20)+"px"; c.appendChild(d); }); }
    function onTileClick(t) { if(GAME_STATE.bonusActive)return; if(t.dataset.type==='en'){if(GAME_STATE.selectedEN)GAME_STATE.selectedEN.classList.remove('active-sel');GAME_STATE.selectedEN=t;}else{if(GAME_STATE.selectedTR)GAME_STATE.selectedTR.classList.remove('active-sel');GAME_STATE.selectedTR=t;} t.classList.add('active-sel'); if(GAME_STATE.selectedEN&&GAME_STATE.selectedTR)checkPair(); }
    function checkPair() { let e=GAME_STATE.selectedEN, t=GAME_STATE.selectedTR; if(e.dataset.pair===t.dataset.pair){GAME_STATE.score+=100; addXP(100); playSound('correct');showFeedback("DOĞRU!","correct-flash");removeTilesWM(e,t);}else{playSound('wrong');showFeedback("YANLIŞ!","wrong-flash");e.classList.remove('active-sel');t.classList.remove('active-sel');} GAME_STATE.selectedEN=null;GAME_STATE.selectedTR=null;updateWMUI(); }
    function removeTilesWM(e,t) { let eI=parseInt(e.dataset.index), tI=parseInt(t.dataset.index); e.classList.add('pop'); t.classList.add('pop'); setTimeout(()=>{GAME_STATE.enData[eI]=null;GAME_STATE.trData[tI]=null;applyGravity('en');applyGravity('tr');GAME_STATE.activeCount--;updateWMUI();if(GAME_STATE.activeCount<=0)triggerFinal(false);else scanForBonus();},400); }
    function applyGravity(type) { let d=GAME_STATE[type+'Data']; for(let c=0;c<3;c++){let emp=[];for(let r=4;r>=0;r--){let i=r*3+c;if(d[i]===null)emp.push(i);else if(emp.length>0){let n=emp.shift();d[n]=d[i];d[i]=null;emp.push(i);}}} renderGrid(type+'-grid',type); Array.from(document.getElementById(type+'-grid').children).forEach(c=>{c.classList.remove('gravity-fall');void c.offsetWidth;c.classList.add('gravity-fall');}); }
    function scanForBonus() { if(GAME_STATE.mode!=='wordmatch'||GAME_STATE.bonusActive)return; let d=GAME_STATE.enData; if(!d)return; let m=new Set(); for(let r=0;r<5;r++){if(d[r*3]&&d[r*3+1]&&d[r*3+2]&&d[r*3].color===d[r*3+1].color&&d[r*3+1].color===d[r*3+2].color){m.add(r*3);m.add(r*3+1);m.add(r*3+2);}} for(let c=0;c<3;c++){for(let r=0;r<=2;r++){if(d[r*3+c]&&d[(r+1)*3+c]&&d[(r+2)*3+c]&&d[r*3+c].color===d[(r+1)*3+c].color&&d[(r+1)*3+c].color===d[(r+2)*3+c].color){m.add(r*3+c);m.add((r+1)*3+c);m.add((r+2)*3+c);}}} if(m.size>=3){GAME_STATE.bonusActive=true;GAME_STATE.score+=500; addXP(300); playSound('bonus');showToast("BONUS COMBO!"); let eIdx=Array.from(m), tIdx=[]; eIdx.forEach(i=>{let p=d[i].pair;let ti=GAME_STATE.trData.findIndex(t=>t&&t.pair===p&&!tIdx.includes(GAME_STATE.trData.indexOf(t)));document.querySelector(`#en-grid .tile[data-index="${i}"]`).classList.add('fire-pop');GAME_STATE.enData[i]=null;if(ti!==-1)tIdx.push(ti);}); tIdx.forEach(i=>{document.querySelector(`#tr-grid .tile[data-index="${i}"]`).classList.add('fire-pop');GAME_STATE.trData[i]=null;}); setTimeout(()=>{let a=[];Object.values(MASTER_DICT).forEach(u=>a.push(...u.words));let ne=[],nt=[];for(let i=0;i<eIdx.length;i++){let w=a[Math.floor(Math.random()*a.length)],c=Math.floor(Math.random()*4);ne.push({en:w.en,tr:w.tr,pair:w.en,color:c});nt.push({en:w.en,tr:w.tr,pair:w.en,color:'tr'});}applyGravityWithRefill('en',ne);applyGravityWithRefill('tr',nt);updateWMUI();setTimeout(()=>{GAME_STATE.bonusActive=false;scanForBonus();},600);},400); } }
    function applyGravityWithRefill(type,q) { let d=GAME_STATE[type+'Data']; for(let c=0;c<3;c++){let emp=[];for(let r=4;r>=0;r--){let i=r*3+c;if(d[i]===null)emp.push(i);else if(emp.length>0){let n=emp.shift();d[n]=d[i];d[i]=null;emp.push(i);}} emp.forEach(idx=>{if(q.length>0){let p=q.shift();d[idx]={en:p.en,tr:p.tr,pair:p.pair,color:type==='en'?p.color:'tr'};}});} renderGrid(type+'-grid',type); Array.from(document.getElementById(type+'-grid').children).forEach(c=>{c.classList.remove('gravity-fall');void c.offsetWidth;c.classList.add('gravity-fall');}); }
    function updateWMUI() { document.getElementById('wm-unit').innerText=GAME_STATE.unit; document.getElementById('wm-score').innerText=GAME_STATE.score; document.getElementById('wm-tiles').innerText=GAME_STATE.activeCount; }
    
    function loadQuizQuestion() { if(QUIZ_STATE.currentIdx>=QUIZ_STATE.questions.length){triggerFinal(true);return;} let q=QUIZ_STATE.questions[QUIZ_STATE.currentIdx]; document.getElementById('quiz-q-text').innerText=`"${q.en}" = ?`; for(let i=0;i<4;i++){let b=document.getElementById('q-opt-'+i);b.innerText=q.options[i];b.className='quiz-opt-btn';b.disabled=false;} }
    function checkQuizAnswer(i) { let q=QUIZ_STATE.questions[QUIZ_STATE.currentIdx], b=document.getElementById('q-opt-'+i); for(let j=0;j<4;j++)document.getElementById('q-opt-'+j).disabled=true; if(b.innerText===q.correct){b.classList.add('correct-flash');GAME_STATE.score+=100; addXP(150); playSound('correct');}else{b.classList.add('wrong-flash');playSound('wrong');for(let j=0;j<4;j++)if(document.getElementById('q-opt-'+j).innerText===q.correct)document.getElementById('q-opt-'+j).classList.add('correct-flash');} updateQuizUI(); setTimeout(()=>{QUIZ_STATE.currentIdx++;loadQuizQuestion();updateQuizUI();},1500); }
    function updateQuizUI() { document.getElementById('qz-unit').innerText=GAME_STATE.unit; document.getElementById('qz-score').innerText=GAME_STATE.score; document.getElementById('qz-progress').innerText=(QUIZ_STATE.currentIdx>=10?10:QUIZ_STATE.currentIdx+1)+"/10"; }
    
    function nextBattleQuestion() { GAME_STATE.isBattleLocked=false; document.getElementById('p1-side').classList.remove('win-flash'); document.getElementById('p2-side').classList.remove('win-flash'); let a=[]; Object.values(MASTER_DICT).forEach(u=>a.push(...u.words)); let c=MASTER_DICT[GAME_STATE.unit].words[Math.floor(Math.random()*MASTER_DICT[GAME_STATE.unit].words.length)]; let o=[c.tr]; while(o.length<4){let r=a[Math.floor(Math.random()*a.length)].tr;if(!o.includes(r))o.push(r);} o.sort(()=>Math.random()-0.5); BATTLE_Q={en:c.en,tr:c.tr,options:o}; document.getElementById('battle-q-box').innerText=`"${c.en}"`; for(let i=0;i<4;i++){document.getElementById(`p1-opt-${i}`).innerText=o[i];document.getElementById(`p2-opt-${i}`).innerText=o[i];document.getElementById(`p1-opt-${i}`).style.background="";document.getElementById(`p2-opt-${i}`).style.background="";} }
    function handleBattlePress(p,i) { if(GAME_STATE.isBattleLocked)return; if(BATTLE_Q.options[i]===BATTLE_Q.tr){ GAME_STATE.isBattleLocked=true; playSound('correct'); if(p===1){GAME_STATE.scoreP1+=10; addXP(20); document.getElementById('p1-score-ui').innerText=GAME_STATE.scoreP1;document.getElementById('p1-side').classList.add('win-flash');}else{GAME_STATE.scoreP2+=10; addXP(20); document.getElementById('p2-score-ui').innerText=GAME_STATE.scoreP2;document.getElementById('p2-side').classList.add('win-flash');} setTimeout(nextBattleQuestion,1500); }else{ playSound('wrong'); document.getElementById(`p${p}-opt-${i}`).style.background="var(--danger)"; } }

    /* ========================================
       BİTİŞ EKRANI (Dinamik Final)
       ======================================== */
    function triggerFinal(man, cT=null, cQ=null) {
        playSound('win'); const s=document.getElementById('end-screen'), h=document.getElementById('end-header'), q=document.getElementById('end-quote'); document.getElementById('end-score').innerText=GAME_STATE.score;
        if(cT){h.innerText=cT; q.innerText=`"${cQ}"`;} else {
            if(GAME_STATE.theme==='cs2') { h.innerText=Math.random()>0.5?"COUNTER-TERRORISTS WIN 💣":"TERRORISTS WIN 💥"; q.innerText='"Bomb defused. Good work team."'; }
            else if(GAME_STATE.theme === 'alastor') { h.innerText = "THE SHOW IS OVER! 📻"; q.innerText = '"Smile, my dear! You know you are never fully dressed without one!"'; }
            else { h.innerText="GÖREV TAMAMLANDI! 🏆"; q.innerText='"İngilizce ustası oldun!"'; }
        } s.style.display='flex';
    }

    // Sistemin Matrix modunda başlaması
    window.onload = () => { playIntro(); };
</script>
</body>
</html>
