<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="mobile-web-app-capable" content="yes">
<meta name="theme-color" content="#0d0f12">
<title>Fitness Tracker</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@2.44.0/tabler-icons.min.css">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
html,body{width:100%;height:100%;background:#0d0f12;}
body{font-family:'Inter',sans-serif;color:#fff;}
.app{width:100%;max-width:480px;margin:0 auto;background:#0d0f12;min-height:100vh;min-height:100dvh;display:flex;flex-direction:column;}
.topbar{background:#0d0f12;padding:16px 20px 0;display:flex;justify-content:space-between;align-items:center;flex-shrink:0;}
.greeting{font-size:20px;font-weight:800;color:#fff;}
.greeting span{color:#00e5cc;}
.streak{background:#1a1d22;border-radius:999px;padding:6px 14px;font-size:12px;font-weight:600;color:#00e5cc;display:flex;align-items:center;gap:5px;}
.nav-pills{display:flex;gap:8px;padding:14px 20px 0;overflow-x:auto;scrollbar-width:none;flex-shrink:0;}
.nav-pills::-webkit-scrollbar{display:none;}
.npill{flex-shrink:0;padding:10px 18px;border-radius:999px;border:none;font-family:'Inter',sans-serif;font-size:13px;font-weight:600;cursor:pointer;transition:all 0.18s;background:#1a1d22;color:#555;}
.npill.on{color:#0d0f12;}
.npill:active{transform:scale(0.94);}
.page{display:none;flex:1;overflow-y:auto;padding:0 20px 100px;-webkit-overflow-scrolling:touch;}
.page.show{display:block;}
.big-card{background:#1a1d22;border-radius:20px;padding:20px;margin-top:16px;}
.big-card-title{font-size:12px;font-weight:600;color:#444;text-transform:uppercase;letter-spacing:1px;margin-bottom:6px;}
.hero-num{font-size:56px;font-weight:800;line-height:1;letter-spacing:-2px;}
.hero-unit{font-size:16px;font-weight:600;color:#555;margin-top:4px;}
.row{display:flex;gap:10px;margin-top:12px;}
.half{flex:1;}
.big-btn{width:100%;padding:16px;border-radius:16px;border:none;font-family:'Inter',sans-serif;font-size:18px;font-weight:800;cursor:pointer;transition:transform 0.12s;color:#0d0f12;}
.big-btn:active{transform:scale(0.93);}
.sm-btn{width:100%;padding:12px;border-radius:12px;border:none;font-family:'Inter',sans-serif;font-size:14px;font-weight:700;cursor:pointer;transition:transform 0.12s;}
.sm-btn:active{transform:scale(0.93);}
.ghost-btn{background:#1a1d22;border:1.5px solid #2a2d32;color:#aaa;}
.progress-wrap{background:#111316;border-radius:999px;height:10px;overflow:hidden;margin-top:12px;}
.progress-bar{height:100%;border-radius:999px;transition:width 0.5s;}
.macro-row{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-top:12px;}
.macro-box{background:#111316;border-radius:14px;padding:12px;text-align:center;}
.macro-num{font-size:20px;font-weight:800;}
.macro-lbl{font-size:11px;font-weight:600;color:#444;margin-top:2px;text-transform:uppercase;}
.macro-bar-wrap{height:4px;background:#0d0f12;border-radius:999px;margin-top:8px;overflow:hidden;}
.macro-bar-fill{height:100%;border-radius:999px;transition:width 0.4s;}
.hint{font-size:13px;color:#444;text-align:center;margin-top:8px;font-weight:500;}
.food-search-wrap{position:relative;margin-top:16px;}
.food-search{width:100%;padding:14px 14px 14px 42px;border-radius:14px;border:none;background:#111316;color:#fff;font-size:15px;font-family:'Inter',sans-serif;font-weight:500;}
.food-search::placeholder{color:#333;}
.search-ic{position:absolute;left:14px;top:50%;transform:translateY(-50%);font-size:18px;color:#444;}
.results-drop{background:#111316;border-radius:14px;margin-top:6px;overflow:hidden;display:none;}
.result-row{padding:13px 16px;cursor:pointer;border-bottom:1px solid #1a1d22;display:flex;justify-content:space-between;align-items:center;}
.result-row:last-child{border-bottom:none;}
.result-row:active{background:#0d0f12;}
.result-name{font-size:14px;font-weight:600;color:#fff;}
.result-meta{font-size:12px;color:#444;margin-top:2px;}
.result-cal{font-size:14px;font-weight:700;color:#00e5cc;}
.quick-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:12px;}
.quick-item{background:#111316;border-radius:14px;padding:14px;cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:6px;transition:transform 0.12s,background 0.12s;border:1.5px solid transparent;}
.quick-item:active{transform:scale(0.93);}
.quick-item.tapped{border-color:#00e5cc;}
.qi-emoji{font-size:28px;}
.qi-name{font-size:12px;font-weight:700;color:#aaa;text-align:center;}
.qi-cal{font-size:11px;color:#444;font-weight:600;}
.log-item{background:#1a1d22;border-radius:14px;padding:14px 16px;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center;}
.log-name{font-size:14px;font-weight:700;}
.log-meta{font-size:12px;color:#444;margin-top:2px;}
.del-btn{background:#111316;border:none;border-radius:999px;width:32px;height:32px;display:flex;align-items:center;justify-content:center;cursor:pointer;color:#444;font-size:14px;flex-shrink:0;}
.del-btn:active{color:#ff4444;}
.timer-circle{display:flex;justify-content:center;margin-top:8px;}
.rep-display{font-size:72px;font-weight:800;text-align:center;margin-top:8px;line-height:1;}
.rep-sub{font-size:14px;color:#444;font-weight:600;text-align:center;margin-top:4px;}
.set-dots{display:flex;justify-content:center;gap:8px;margin-top:12px;}
.sdot{width:10px;height:10px;border-radius:50%;background:#1a1d22;border:2px solid #2a2d32;transition:all 0.2s;}
.sdot.done{border-color:#00e5cc;background:#00e5cc;}
.stat-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:12px;}
.stat-box{background:#1a1d22;border-radius:16px;padding:16px;}
.stat-num{font-size:28px;font-weight:800;}
.stat-lbl{font-size:12px;font-weight:600;color:#444;margin-top:4px;text-transform:uppercase;letter-spacing:0.5px;}
.mode-toggle{display:flex;background:#111316;border-radius:14px;padding:4px;gap:4px;margin-top:12px;}
.mode-opt{flex:1;padding:12px;border-radius:10px;border:none;font-family:'Inter',sans-serif;font-size:14px;font-weight:700;cursor:pointer;background:transparent;color:#444;transition:all 0.18s;}
.mode-opt:active{transform:scale(0.95);}
.tip-box{background:#1a1d22;border-radius:14px;padding:14px 16px;margin-top:10px;display:flex;align-items:flex-start;gap:10px;}
.tip-text{font-size:13px;color:#aaa;font-weight:500;line-height:1.5;}
.bmi-bands{display:flex;border-radius:999px;overflow:hidden;height:8px;margin-top:14px;}
.bmi-band{flex:1;}
.badge{display:inline-block;padding:8px 18px;border-radius:999px;font-size:16px;font-weight:700;}
.scan-placeholder{border:2px dashed #2a2d32;border-radius:14px;padding:24px;text-align:center;cursor:pointer;margin-top:8px;}
.spin{display:inline-block;width:16px;height:16px;border:2px solid #333;border-top-color:#00e5cc;border-radius:50%;animation:sp 0.7s linear infinite;vertical-align:middle;}
@keyframes sp{to{transform:rotate(360deg)}}
.bottom-nav{position:sticky;bottom:0;background:#0d0f12;border-top:1px solid #1a1d22;display:flex;padding:10px 0;padding-bottom:max(10px,env(safe-area-inset-bottom));flex-shrink:0;z-index:10;}
.bnav{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;cursor:pointer;padding:4px;}
.bnav-ic{font-size:24px;color:#333;transition:color 0.15s,transform 0.12s;}
.bnav-lbl{font-size:10px;font-weight:700;color:#333;letter-spacing:0.3px;text-transform:uppercase;}
.bnav.on .bnav-ic,.bnav.on .bnav-lbl{color:#00e5cc;}
.bnav:active .bnav-ic{transform:scale(0.82);}
input[type=range]{width:100%;margin-top:6px;accent-color:#00e5cc;}
</style>
</head>
<body>
<div class="app">

<div class="topbar">
  <div class="greeting">Hey there <span>👋</span></div>
  <div class="streak"><i class="ti ti-flame"></i> <span>3</span> day streak</div>
</div>

<div class="nav-pills">
  <button class="npill on" id="pill-workout" onclick="goPage('workout',this)" style="background:#00e5cc;color:#0d0f12;">💪 Workout</button>
  <button class="npill" id="pill-food" onclick="goPage('food',this)">🍽️ Food</button>
  <button class="npill" id="pill-bmi" onclick="goPage('bmi',this)">⚖️ My Body</button>
  <button class="npill" id="pill-progress" onclick="goPage('progress',this)">📈 Progress</button>
</div>

<!-- WORKOUT -->
<div id="page-workout" class="page show">
  <div class="big-card">
    <div class="big-card-title">Rest timer — take a break between sets</div>
    <div class="timer-circle">
      <svg width="160" height="160" viewBox="0 0 160 160">
        <circle fill="none" stroke="#111316" stroke-width="10" cx="80" cy="80" r="68"/>
        <circle fill="none" stroke="#00e5cc" stroke-width="10" stroke-linecap="round" cx="80" cy="80" r="68"
          stroke-dasharray="427.3" stroke-dashoffset="0" id="tArc"
          style="transform-origin:80px 80px;transform:rotate(-90deg);transition:stroke-dashoffset 1s linear;"/>
        <text x="80" y="72" text-anchor="middle" dominant-baseline="middle" font-family="Inter" font-size="28" font-weight="800" fill="#fff" id="tTxt">1:30</text>
        <text x="80" y="98" text-anchor="middle" font-family="Inter" font-size="11" font-weight="600" fill="#444" letter-spacing="1">REST TIME</text>
      </svg>
    </div>
    <div class="row">
      <div class="half"><button class="big-btn" id="tBtn" onclick="tAction('start')" style="background:#00e5cc;">▶ Start</button></div>
      <div class="half"><button class="big-btn ghost-btn" onclick="tAction('reset')">↺ Reset</button></div>
    </div>
    <div style="margin-top:10px;"><button class="sm-btn" onclick="tAction('add')" style="background:#111316;color:#00e5cc;border:1.5px solid #00e5cc33;width:100%;">+ Add 30 more seconds</button></div>
  </div>

  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">Rep counter — count every rep you do</div>
    <div class="rep-display" id="repNum">0</div>
    <div class="rep-sub">reps · Set <span id="setCur">1</span> of 4</div>
    <div class="set-dots" id="setDots">
      <div class="sdot"></div><div class="sdot"></div><div class="sdot"></div><div class="sdot"></div>
    </div>
    <div class="row" style="margin-top:16px;">
      <div class="half"><button class="big-btn" onclick="adjRep(1)" style="background:#00e5cc;font-size:24px;">+ Rep</button></div>
      <div class="half"><button class="big-btn ghost-btn" onclick="adjRep(-1)" style="font-size:24px;">- Rep</button></div>
    </div>
    <div class="hint" id="repHint">Tap + Rep every time you finish one rep!</div>
  </div>

  <div class="stat-grid">
    <div class="stat-box"><div class="stat-num" id="totalRepsS">0</div><div class="stat-lbl">Total Reps</div></div>
    <div class="stat-box"><div class="stat-num" id="totalSetsS">0</div><div class="stat-lbl">Sets Done</div></div>
    <div class="stat-box"><div class="stat-num" id="volS">0</div><div class="stat-lbl">Volume lbs</div></div>
    <div class="stat-box"><div class="stat-num" id="timeS">0m</div><div class="stat-lbl">Active Time</div></div>
  </div>
</div>

<!-- FOOD -->
<div id="page-food" class="page">
  <div class="mode-toggle">
    <button class="mode-opt" id="mBulk" onclick="setMode('bulk')" style="background:#1D9E75;color:#fff;">🏋️ Bulking</button>
    <button class="mode-opt" id="mCut" onclick="setMode('cut')">✂️ Cutting</button>
  </div>
  <div class="tip-box" id="modeTip">
    <span style="font-size:20px;">💡</span>
    <span class="tip-text" id="tipText">You are in <strong>Bulking</strong> mode! Eat more to build muscle. Your goal is <strong>3000 calories</strong> today.</span>
  </div>
  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">Calories today</div>
    <div style="display:flex;justify-content:space-between;align-items:flex-end;">
      <div><div class="hero-num" id="calEaten" style="color:#00e5cc;">0</div><div class="hero-unit">of <span id="calGoalLbl">3000</span> kcal eaten</div></div>
      <div style="text-align:right;"><div style="font-size:28px;font-weight:800;" id="calLeftNum">3000</div><div style="font-size:12px;color:#444;font-weight:600;" id="calLeftLbl">left to eat</div></div>
    </div>
    <div class="progress-wrap"><div class="progress-bar" id="calBar" style="width:0%;background:#1D9E75;"></div></div>
    <div class="macro-row">
      <div class="macro-box"><div class="macro-num" id="protNum" style="color:#378ADD;">0g</div><div class="macro-lbl">Protein</div><div class="macro-bar-wrap"><div class="macro-bar-fill" id="protBar" style="background:#378ADD;width:0%;"></div></div></div>
      <div class="macro-box"><div class="macro-num" id="carbNum" style="color:#EF9F27;">0g</div><div class="macro-lbl">Carbs</div><div class="macro-bar-wrap"><div class="macro-bar-fill" id="carbBar" style="background:#EF9F27;width:0%;"></div></div></div>
      <div class="macro-box"><div class="macro-num" id="fatNum" style="color:#D85A30;">0g</div><div class="macro-lbl">Fat</div><div class="macro-bar-wrap"><div class="macro-bar-fill" id="fatBar" style="background:#D85A30;width:0%;"></div></div></div>
    </div>
  </div>

  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">📷 Scan food photo</div>
    <div id="scanPlaceholder" class="scan-placeholder" onclick="document.getElementById('fInput').click()">
      <div style="font-size:40px;">📷</div>
      <div style="font-size:15px;font-weight:700;color:#aaa;margin-top:8px;">Tap to take a photo of your food</div>
      <div style="font-size:12px;color:#333;margin-top:4px;">App will guess what food it is!</div>
    </div>
    <img id="scanImg" style="width:100%;border-radius:12px;margin-top:8px;display:none;max-height:160px;object-fit:cover;" alt="Food photo">
    <div id="scanStatus" style="text-align:center;padding:12px;font-size:14px;color:#00e5cc;display:none;"></div>
    <div id="scanResultBox" style="display:none;margin-top:8px;background:#111316;border-radius:12px;padding:14px;">
      <div style="font-size:16px;font-weight:800;" id="scanName"></div>
      <div style="display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:6px;margin-top:10px;">
        <div style="text-align:center;"><div style="font-size:16px;font-weight:800;" id="sCal"></div><div style="font-size:10px;color:#444;font-weight:600;">KCAL</div></div>
        <div style="text-align:center;"><div style="font-size:16px;font-weight:800;color:#378ADD;" id="sProt"></div><div style="font-size:10px;color:#444;font-weight:600;">PROT</div></div>
        <div style="text-align:center;"><div style="font-size:16px;font-weight:800;color:#EF9F27;" id="sCarb"></div><div style="font-size:10px;color:#444;font-weight:600;">CARBS</div></div>
        <div style="text-align:center;"><div style="font-size:16px;font-weight:800;color:#D85A30;" id="sFat"></div><div style="font-size:10px;color:#444;font-weight:600;">FAT</div></div>
      </div>
      <button class="big-btn" onclick="addScan()" style="background:#1D9E75;margin-top:12px;font-size:15px;">✅ Add this food to my log</button>
    </div>
    <input type="file" id="fInput" accept="image/*" style="display:none;" onchange="handleScan(event)">
  </div>

  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">🔍 Search for any food</div>
    <div class="food-search-wrap">
      <i class="ti ti-search search-ic"></i>
      <input class="food-search" id="foodSearch" placeholder="Type a food name e.g. chicken…" oninput="doSearch(this.value)">
    </div>
    <div class="results-drop" id="resultsBox"></div>
  </div>

  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">⚡ Quick add — tap any food</div>
    <div class="quick-grid">
      <div class="quick-item" onclick="quickAdd('banana',this)"><div class="qi-emoji">🍌</div><div class="qi-name">Banana</div><div class="qi-cal">89 kcal</div></div>
      <div class="quick-item" onclick="quickAdd('chicken breast',this)"><div class="qi-emoji">🍗</div><div class="qi-name">Chicken</div><div class="qi-cal">165 kcal</div></div>
      <div class="quick-item" onclick="quickAdd('white rice',this)"><div class="qi-emoji">🍚</div><div class="qi-name">Rice</div><div class="qi-cal">206 kcal</div></div>
      <div class="quick-item" onclick="quickAdd('egg',this)"><div class="qi-emoji">🥚</div><div class="qi-name">Egg</div><div class="qi-cal">77 kcal</div></div>
      <div class="quick-item" onclick="quickAdd('oats',this)"><div class="qi-emoji">🥣</div><div class="qi-name">Oats</div><div class="qi-cal">307 kcal</div></div>
      <div class="quick-item" onclick="quickAdd('salmon',this)"><div class="qi-emoji">🐟</div><div class="qi-name">Salmon</div><div class="qi-cal">208 kcal</div></div>
      <div class="quick-item" onclick="quickAdd('biryani',this)"><div class="qi-emoji">🍛</div><div class="qi-name">Biryani</div><div class="qi-cal">380 kcal</div></div>
      <div class="quick-item" onclick="quickAdd('roti',this)"><div class="qi-emoji">🫓</div><div class="qi-name">Roti x2</div><div class="qi-cal">210 kcal</div></div>
      <div class="quick-item" onclick="quickAdd('avocado',this)"><div class="qi-emoji">🥑</div><div class="qi-name">Avocado</div><div class="qi-cal">240 kcal</div></div>
      <div class="quick-item" onclick="quickAdd('greek yogurt',this)"><div class="qi-emoji">🥛</div><div class="qi-name">Yogurt</div><div class="qi-cal">130 kcal</div></div>
    </div>
  </div>

  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">📋 Today's food log</div>
    <div id="foodLog"><div style="text-align:center;padding:20px;font-size:14px;color:#333;font-weight:600;">Nothing logged yet — start eating! 🍴</div></div>
  </div>
</div>

<!-- MY BODY -->
<div id="page-bmi" class="page">
  <div class="big-card" style="margin-top:16px;">
    <div class="big-card-title">Your weight — press + or - to change</div>
    <div style="display:flex;align-items:center;gap:16px;margin-top:8px;">
      <button class="big-btn" onclick="adjW(-1)" style="background:#1a1d22;color:#00e5cc;width:64px;height:64px;border-radius:50%;font-size:28px;padding:0;flex-shrink:0;border:1.5px solid #00e5cc44;">−</button>
      <div style="text-align:center;flex:1;"><div class="hero-num" id="wNum">185</div><div class="hero-unit">lbs</div></div>
      <button class="big-btn" onclick="adjW(1)" style="background:#00e5cc;width:64px;height:64px;border-radius:50%;font-size:28px;padding:0;flex-shrink:0;">+</button>
    </div>
  </div>

  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">BMI — Body Mass Index</div>
    <div style="display:flex;justify-content:space-between;align-items:center;margin-top:8px;">
      <div style="font-size:48px;font-weight:800;" id="bmiNum">25.2</div>
      <div class="badge" id="bmiBadge">Normal</div>
    </div>
    <div class="bmi-bands">
      <div class="bmi-band" style="background:#378ADD;"></div>
      <div class="bmi-band" style="background:#1D9E75;"></div>
      <div class="bmi-band" style="background:#EF9F27;"></div>
      <div class="bmi-band" style="background:#D85A30;"></div>
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr 1fr 1fr;margin-top:6px;">
      <div style="font-size:10px;color:#378ADD;font-weight:700;">Under</div>
      <div style="font-size:10px;color:#1D9E75;font-weight:700;">Normal</div>
      <div style="font-size:10px;color:#EF9F27;font-weight:700;">Over</div>
      <div style="font-size:10px;color:#D85A30;font-weight:700;">Obese</div>
    </div>
    <div class="tip-box" style="margin-top:12px;">
      <span style="font-size:20px;" id="bmiEmoji">✅</span>
      <span class="tip-text" id="bmiTip">Your BMI is in the healthy range! Keep it up.</span>
    </div>
  </div>

  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">What is your height?</div>
    <input type="range" min="55" max="80" value="68" id="heightSlider" oninput="updateHeight(this.value)">
    <div style="display:flex;justify-content:space-between;margin-top:4px;">
      <span style="font-size:13px;color:#444;">4'7"</span>
      <span style="font-size:15px;font-weight:700;color:#00e5cc;" id="heightLbl">5'8"</span>
      <span style="font-size:13px;color:#444;">6'8"</span>
    </div>
    <div style="margin-top:12px;background:#111316;border-radius:12px;padding:16px;text-align:center;">
      <div style="font-size:13px;color:#444;font-weight:600;">Your healthy weight range</div>
      <div style="font-size:24px;font-weight:800;color:#00e5cc;margin-top:6px;" id="idealRange">—</div>
      <div style="font-size:12px;color:#333;margin-top:4px;">Based on BMI 18.5 – 24.9</div>
    </div>
  </div>
</div>

<!-- PROGRESS -->
<div id="page-progress" class="page">
  <div class="big-card" style="margin-top:16px;">
    <div class="big-card-title">Today's summary</div>
    <div class="stat-grid" style="margin-top:10px;">
      <div class="stat-box"><div class="stat-num" id="pCal" style="color:#00e5cc;">0</div><div class="stat-lbl">Calories eaten</div></div>
      <div class="stat-box"><div class="stat-num" id="pReps">0</div><div class="stat-lbl">Total reps</div></div>
      <div class="stat-box"><div class="stat-num" id="pSets">0</div><div class="stat-lbl">Sets done</div></div>
      <div class="stat-box"><div class="stat-num" id="pVol">0</div><div class="stat-lbl">Volume lbs</div></div>
    </div>
  </div>
  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">Calorie goal progress</div>
    <div style="margin-top:10px;">
      <div style="display:flex;justify-content:space-between;margin-bottom:6px;">
        <span style="font-size:13px;color:#444;font-weight:600;">Eaten so far</span>
        <span style="font-size:13px;font-weight:700;" id="pPct">0%</span>
      </div>
      <div class="progress-wrap"><div class="progress-bar" id="pBar" style="width:0%;background:#1D9E75;"></div></div>
    </div>
    <div class="tip-box" style="margin-top:12px;">
      <span style="font-size:20px;" id="progressEmoji">🎯</span>
      <span class="tip-text" id="progressTip">Log your food and workout to see your progress here!</span>
    </div>
  </div>
  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">Protein goal</div>
    <div style="margin-top:10px;">
      <div style="display:flex;justify-content:space-between;margin-bottom:6px;">
        <span style="font-size:13px;color:#444;font-weight:600;"><span id="pProtEaten">0</span>g eaten</span>
        <span style="font-size:13px;font-weight:700;color:#378ADD;"><span id="pProtGoal">180</span>g goal</span>
      </div>
      <div class="progress-wrap"><div class="progress-bar" id="pProtBar" style="width:0%;background:#378ADD;"></div></div>
    </div>
  </div>
  <div class="big-card" style="margin-top:12px;">
    <div class="big-card-title">Reset today's data</div>
    <button class="big-btn" onclick="resetAll()" style="background:#D85A30;margin-top:10px;font-size:15px;">🗑️ Clear everything and start fresh</button>
  </div>
</div>

<div class="bottom-nav">
  <div class="bnav on" id="bnav-workout" onclick="goPage('workout',null,this)"><i class="ti ti-barbell bnav-ic"></i><span class="bnav-lbl">Workout</span></div>
  <div class="bnav" id="bnav-food" onclick="goPage('food',null,this)"><i class="ti ti-salad bnav-ic"></i><span class="bnav-lbl">Food</span></div>
  <div class="bnav" id="bnav-bmi" onclick="goPage('bmi',null,this)"><i class="ti ti-scale bnav-ic"></i><span class="bnav-lbl">My Body</span></div>
  <div class="bnav" id="bnav-progress" onclick="goPage('progress',null,this)"><i class="ti ti-chart-bar bnav-ic"></i><span class="bnav-lbl">Progress</span></div>
</div>

</div>
<script>
const DB={'banana':{name:'Banana',e:'🍌',cal:89,p:1,c:23,f:0},'apple':{name:'Apple',e:'🍎',cal:52,p:0,c:14,f:0},'orange':{name:'Orange',e:'🍊',cal:47,p:1,c:12,f:0},'mango':{name:'Mango',e:'🥭',cal:60,p:1,c:15,f:0},'chicken breast':{name:'Chicken breast',e:'🍗',cal:165,p:31,c:0,f:4},'chicken':{name:'Chicken breast',e:'🍗',cal:165,p:31,c:0,f:4},'salmon':{name:'Salmon',e:'🐟',cal:208,p:20,c:0,f:13},'tuna':{name:'Tuna',e:'🐟',cal:132,p:28,c:0,f:1},'egg':{name:'Egg',e:'🥚',cal:77,p:6,c:1,f:5},'eggs':{name:'Eggs x2',e:'🥚',cal:154,p:12,c:2,f:10},'beef':{name:'Beef',e:'🥩',cal:250,p:26,c:0,f:15},'white rice':{name:'White rice',e:'🍚',cal:206,p:4,c:45,f:0},'rice':{name:'Rice',e:'🍚',cal:206,p:4,c:45,f:0},'brown rice':{name:'Brown rice',e:'🍚',cal:218,p:5,c:46,f:2},'oats':{name:'Oats',e:'🥣',cal:307,p:11,c:55,f:5},'oatmeal':{name:'Oatmeal',e:'🥣',cal:307,p:11,c:55,f:5},'bread':{name:'Bread x2',e:'🍞',cal:132,p:4,c:25,f:2},'pasta':{name:'Pasta',e:'🍝',cal:220,p:8,c:43,f:1},'potato':{name:'Potato',e:'🥔',cal:163,p:4,c:37,f:0},'sweet potato':{name:'Sweet potato',e:'🍠',cal:130,p:2,c:30,f:0},'avocado':{name:'Avocado',e:'🥑',cal:240,p:3,c:13,f:22},'almonds':{name:'Almonds',e:'🥜',cal:164,p:6,c:6,f:14},'peanut butter':{name:'Peanut butter',e:'🥜',cal:188,p:8,c:6,f:16},'cheese':{name:'Cheese',e:'🧀',cal:113,p:7,c:0,f:9},'milk':{name:'Milk',e:'🥛',cal:122,p:8,c:12,f:5},'greek yogurt':{name:'Greek yogurt',e:'🥛',cal:130,p:17,c:9,f:0},'yogurt':{name:'Yogurt',e:'🥛',cal:130,p:17,c:9,f:0},'whey protein':{name:'Whey protein',e:'💪',cal:120,p:25,c:3,f:1},'broccoli':{name:'Broccoli',e:'🥦',cal:55,p:4,c:11,f:1},'spinach':{name:'Spinach',e:'🥬',cal:23,p:3,c:4,f:0},'salad':{name:'Salad',e:'🥗',cal:35,p:2,c:7,f:0},'pizza':{name:'Pizza slice',e:'🍕',cal:285,p:12,c:36,f:10},'burger':{name:'Burger',e:'🍔',cal:540,p:30,c:45,f:25},'sandwich':{name:'Sandwich',e:'🥪',cal:350,p:18,c:38,f:14},'biryani':{name:'Biryani',e:'🍛',cal:380,p:18,c:50,f:12},'roti':{name:'Roti x2',e:'🫓',cal:210,p:6,c:42,f:3},'dal':{name:'Dal',e:'🍲',cal:130,p:9,c:22,f:1},'paratha':{name:'Paratha',e:'🫓',cal:260,p:5,c:36,f:10},'chocolate':{name:'Chocolate',e:'🍫',cal:235,p:3,c:26,f:13},'ice cream':{name:'Ice cream',e:'🍦',cal:207,p:4,c:24,f:11},'coffee':{name:'Coffee',e:'☕',cal:5,p:0,c:0,f:0},'water':{name:'Water',e:'💧',cal:0,p:0,c:0,f:0}};
const VMAP=[{k:['banana'],f:'banana'},{k:['apple'],f:'apple'},{k:['chicken','breast','grilled'],f:'chicken breast'},{k:['rice'],f:'white rice'},{k:['egg'],f:'egg'},{k:['salmon','fish'],f:'salmon'},{k:['oat'],f:'oats'},{k:['avocado'],f:'avocado'},{k:['pizza'],f:'pizza'},{k:['burger'],f:'burger'},{k:['salad'],f:'salad'},{k:['broccoli'],f:'broccoli'},{k:['biryani'],f:'biryani'},{k:['roti','paratha'],f:'roti'},{k:['chocolate'],f:'chocolate'},{k:['yogurt'],f:'greek yogurt'},{k:['almond'],f:'almonds'},{k:['sandwich'],f:'sandwich'}];
const goals={bulk:{cal:3000,p:180,c:350,f:80},cut:{cal:2000,p:200,c:180,f:55}};
let mode='bulk',foods=[],pendingScan=null,reps=0,sets=0,totalR=0,weight=185,heightIn=68;
let tTotal=90,tLeft=90,tRunning=false,tIv=null,activeMin=0;

function goPage(id,pillEl,navEl){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('show'));
  document.querySelectorAll('.npill').forEach(p=>{p.classList.remove('on');p.style.background='';p.style.color='';});
  document.querySelectorAll('.bnav').forEach(b=>b.classList.remove('on'));
  document.getElementById('page-'+id).classList.add('show');
  const np=document.getElementById('pill-'+id);
  if(np){np.classList.add('on');np.style.background='#00e5cc';np.style.color='#0d0f12';}
  const bn=document.getElementById('bnav-'+id);
  if(bn)bn.classList.add('on');
  if(id==='progress')updateProgress();
}

function setMode(m){
  mode=m;
  document.getElementById('mBulk').style.background=m==='bulk'?'#1D9E75':'';
  document.getElementById('mBulk').style.color=m==='bulk'?'#fff':'#444';
  document.getElementById('mCut').style.background=m==='cut'?'#D85A30':'';
  document.getElementById('mCut').style.color=m==='cut'?'#fff':'#444';
  const g=goals[mode];
  document.getElementById('tipText').innerHTML=m==='bulk'
    ?`You are in <strong>Bulking</strong> mode! Eat more to build muscle. Your goal is <strong>${g.cal} calories</strong> today.`
    :`You are in <strong>Cutting</strong> mode! Eat less to lose fat. Your goal is <strong>${g.cal} calories</strong> today.`;
  updateFood();
}

function updateFood(){
  const g=goals[mode];
  const tc=Math.round(foods.reduce((s,f)=>s+f.cal,0));
  const tp=Math.round(foods.reduce((s,f)=>s+f.p,0));
  const tcb=Math.round(foods.reduce((s,f)=>s+f.c,0));
  const tf=Math.round(foods.reduce((s,f)=>s+f.f,0));
  document.getElementById('calEaten').textContent=tc;
  document.getElementById('calGoalLbl').textContent=g.cal;
  const left=g.cal-tc;
  document.getElementById('calLeftNum').textContent=Math.abs(left);
  document.getElementById('calLeftLbl').textContent=left>=0?'left to eat':'over goal!';
  document.getElementById('calBar').style.width=Math.min(100,Math.round(tc/g.cal*100))+'%';
  document.getElementById('calBar').style.background=mode==='bulk'?'#1D9E75':'#D85A30';
  document.getElementById('protNum').textContent=tp+'g';
  document.getElementById('carbNum').textContent=tcb+'g';
  document.getElementById('fatNum').textContent=tf+'g';
  document.getElementById('protBar').style.width=Math.min(100,Math.round(tp/g.p*100))+'%';
  document.getElementById('carbBar').style.width=Math.min(100,Math.round(tcb/g.c*100))+'%';
  document.getElementById('fatBar').style.width=Math.min(100,Math.round(tf/g.f*100))+'%';
  const log=document.getElementById('foodLog');
  if(!foods.length){log.innerHTML='<div style="text-align:center;padding:20px;font-size:14px;color:#333;font-weight:600;">Nothing logged yet — start eating! 🍴</div>';return;}
  log.innerHTML=foods.map((f,i)=>`<div class="log-item"><div style="flex:1;min-width:0;"><div class="log-name">${f.e||'🍽️'} ${f.name}</div><div class="log-meta">${f.cal} kcal · Protein ${f.p}g · Carbs ${f.c}g · Fat ${f.f}g</div></div><button class="del-btn" onclick="delFood(${i})"><i class="ti ti-x"></i></button></div>`).join('');
}
function delFood(i){foods.splice(i,1);updateFood();}
function quickAdd(key,el){const f=DB[key];if(!f)return;foods.push(Object.assign({},f));updateFood();if(el){el.classList.add('tapped');setTimeout(()=>el.classList.remove('tapped'),600);}}
function doSearch(q){const box=document.getElementById('resultsBox');if(!q||q.length<2){box.style.display='none';return;}const matches=Object.entries(DB).filter(([k,v])=>k.includes(q.toLowerCase())||v.name.toLowerCase().includes(q.toLowerCase())).slice(0,6);if(!matches.length){box.style.display='none';return;}box.style.display='block';box.innerHTML=matches.map(([k,v])=>`<div class="result-row" onclick="addFromSearch('${k}')"><div><div class="result-name">${v.e} ${v.name}</div><div class="result-meta">Protein ${v.p}g · Carbs ${v.c}g · Fat ${v.f}g</div></div><div class="result-cal">${v.cal} kcal</div></div>`).join('');}
function addFromSearch(key){const f=DB[key];if(!f)return;foods.push(Object.assign({},f));document.getElementById('foodSearch').value='';document.getElementById('resultsBox').style.display='none';updateFood();}
function guessFood(fname){for(const e of VMAP){if(e.k.some(k=>fname.includes(k)))return DB[e.f];}const keys=Object.keys(DB);return DB[keys[Math.floor(Math.random()*keys.length)]];}
function handleScan(e){const file=e.target.files[0];if(!file)return;const reader=new FileReader();reader.onload=ev=>{const img=document.getElementById('scanImg');img.src=ev.target.result;img.style.display='block';document.getElementById('scanPlaceholder').style.display='none';document.getElementById('scanResultBox').style.display='none';document.getElementById('scanStatus').style.display='block';document.getElementById('scanStatus').innerHTML='<span class="spin"></span> Looking at your food…';setTimeout(()=>{const food=guessFood(file.name.toLowerCase());pendingScan=Object.assign({},food);document.getElementById('scanStatus').style.display='none';document.getElementById('scanName').textContent=food.e+' '+food.name;document.getElementById('sCal').textContent=food.cal;document.getElementById('sProt').textContent=food.p+'g';document.getElementById('sCarb').textContent=food.c+'g';document.getElementById('sFat').textContent=food.f+'g';document.getElementById('scanResultBox').style.display='block';},1600);};reader.readAsDataURL(file);e.target.value='';}
function addScan(){if(pendingScan){foods.push(pendingScan);pendingScan=null;updateFood();}document.getElementById('scanResultBox').style.display='none';document.getElementById('scanImg').style.display='none';document.getElementById('scanPlaceholder').style.display='block';}
function updateTimer(){const m=Math.floor(tLeft/60),s=tLeft%60;document.getElementById('tTxt').textContent=m+':'+String(s).padStart(2,'0');document.getElementById('tArc').style.strokeDashoffset=(427.3*(1-tLeft/tTotal)).toFixed(1);}
function tAction(a){if(a==='start'){if(tRunning){clearInterval(tIv);tRunning=false;document.getElementById('tBtn').textContent='▶ Start';}else{if(tLeft<=0)tLeft=tTotal;tRunning=true;document.getElementById('tBtn').textContent='⏸ Pause';tIv=setInterval(()=>{if(tLeft<=0){clearInterval(tIv);tRunning=false;document.getElementById('tBtn').textContent='▶ Start';return;}tLeft--;updateTimer();},1000);}}else if(a==='reset'){clearInterval(tIv);tRunning=false;tLeft=tTotal;document.getElementById('tBtn').textContent='▶ Start';updateTimer();}else if(a==='add'){tTotal+=30;tLeft+=30;updateTimer();}}
function adjRep(d){reps=Math.max(0,reps+d);if(d>0&&reps>0&&reps%12===0){sets=Math.min(4,sets+1);totalR+=12;reps=0;updateDots();}else if(d>0)totalR++;else totalR=Math.max(0,totalR-1);document.getElementById('repNum').textContent=reps;document.getElementById('repHint').textContent=reps===0?'Tap + Rep every time you finish one rep!':reps<6?'Keep going! You got this 💪':reps<12?'Almost there! Push through! 🔥':'Great set! Take a rest ✅';updateWorkoutStats();}
function updateDots(){document.querySelectorAll('.sdot').forEach((d,i)=>d.className='sdot'+(i<sets?' done':''));document.getElementById('setCur').textContent=Math.min(4,sets+1);}
function updateWorkoutStats(){document.getElementById('totalRepsS').textContent=totalR;document.getElementById('totalSetsS').textContent=sets;document.getElementById('volS').textContent=totalR*weight;}
function adjW(d){weight=Math.max(80,Math.min(400,weight+d));document.getElementById('wNum').textContent=weight;updateBMI();}
function updateBMI(){const h=heightIn*0.0254,b=(weight*0.453592)/(h*h);document.getElementById('bmiNum').textContent=b.toFixed(1);let label,color,emoji,tip;if(b<18.5){label='Underweight';color='#378ADD';emoji='⚠️';tip='You are underweight. Try to eat more nutritious food to gain healthy weight.';}else if(b<25){label='Normal ✅';color='#1D9E75';emoji='✅';tip='Your BMI is in the healthy range! Keep eating well and exercising.';}else if(b<30){label='Overweight';color='#EF9F27';emoji='⚠️';tip='You are slightly overweight. Try to eat fewer calories and exercise more.';}else{label='Obese';color='#D85A30';emoji='🚨';tip='Please speak to a doctor. Try to eat healthier and exercise daily.';}const badge=document.getElementById('bmiBadge');badge.textContent=label;badge.style.background=color+'33';badge.style.color=color;document.getElementById('bmiEmoji').textContent=emoji;document.getElementById('bmiTip').textContent=tip;updateIdeal();}
function updateHeight(v){heightIn=parseInt(v);const ft=Math.floor(heightIn/12),inch=heightIn%12;document.getElementById('heightLbl').textContent=ft+"'"+inch+'"';updateIdeal();updateBMI();}
function updateIdeal(){const h=heightIn*0.0254;document.getElementById('idealRange').textContent=Math.round(18.5*h*h/0.453592)+' – '+Math.round(24.9*h*h/0.453592)+' lbs';}
function updateProgress(){const g=goals[mode];const tc=Math.round(foods.reduce((s,f)=>s+f.cal,0));const tp=Math.round(foods.reduce((s,f)=>s+f.p,0));const pct=Math.min(100,Math.round(tc/g.cal*100));document.getElementById('pCal').textContent=tc;document.getElementById('pReps').textContent=totalR;document.getElementById('pSets').textContent=sets;document.getElementById('pVol').textContent=totalR*weight;document.getElementById('pPct').textContent=pct+'%';document.getElementById('pBar').style.width=pct+'%';document.getElementById('pBar').style.background=mode==='bulk'?'#1D9E75':'#D85A30';document.getElementById('pProtEaten').textContent=tp;document.getElementById('pProtGoal').textContent=g.p;document.getElementById('pProtBar').style.width=Math.min(100,Math.round(tp/g.p*100))+'%';let emoji='🎯',tip='Log your food and workout to see your progress here!';if(tc>0&&totalR>0){emoji='🔥';tip='Amazing! You ate and worked out today. Keep it up!';}else if(tc>0){emoji='🍽️';tip='Food logged! Now go workout to complete your day!';}else if(totalR>0){emoji='💪';tip='Great workout! Now log your food to hit your goals!';}document.getElementById('progressEmoji').textContent=emoji;document.getElementById('progressTip').textContent=tip;}
function resetAll(){if(!confirm('Clear all data and start fresh?'))return;foods=[];reps=0;sets=0;totalR=0;updateFood();updateWorkoutStats();updateDots();document.getElementById('repNum').textContent='0';document.getElementById('repHint').textContent='Tap + Rep every time you finish one rep!';}
setInterval(()=>{if(tRunning){activeMin+=1/60;document.getElementById('timeS').textContent=Math.floor(activeMin)+'m';}},1000);
updateTimer();updateFood();updateBMI();updateIdeal();
</script>
</body>
</html>
