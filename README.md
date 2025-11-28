[shoeb @.txt](https://github.com/user-attachments/files/23826122/shoeb.%40.txt)
<!doctype html>
<html lang="hi">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Kali GPT — AI Terminal</title>
<link rel="stylesheet" href="styles.css">
<link rel="manifest" href="manifest.json">
<meta name="theme-color" content="#071023">
</head>
<body>
<div class="app-shell">
  <aside class="sidebar">
    <div class="brand">
      <div class="logo">🐉</div>
      <div class="name">Kali GPT</div>
    </div>
    <nav class="nav">
      <button class="nav-btn active" data-view="terminal">Terminal</button>
      <button class="nav-btn" data-view="chat">AI Chat</button>
      <button class="nav-btn" data-view="tictactoe">Tic-Tac-Toe</button>
      <button class="nav-btn" data-view="settings">Settings</button>
    </nav>
    <div class="install-box" id="installBox">
      <button id="installBtn" class="install-btn">Install App</button>
    </div>
    <footer class="sb-footer">© Kali GPT</footer>
  </aside>

  <main class="main">
    <!-- Terminal view -->
    <section class="view view-active" id="terminalView">
      <header class="view-header">Terminal Mode</header>
      <div class="terminal" id="terminal" tabindex="0" aria-live="polite">
        <div class="term-lines" id="termLines"></div>
        <div class="term-input">
          <span class="prompt">kali$</span>
          <input id="termInput" placeholder="कमांड लिखें — उदाहारण: hello, help, ping" />
          <button id="termSend" class="small">Send</button>
        </div>
      </div>
    </section>

    <!-- Chat view -->
    <section class="view" id="chatView">
      <header class="view-header">AI Chat</header>
      <div class="chat-wrap">
        <div class="chat-messages" id="chatMessages" aria-live="polite"></div>
        <div class="chat-controls">
          <input id="chatInput" placeholder="AI से पूछें... (हिंदी में लिखें)" />
          <button id="voiceBtn" title="Voice input">🎤</button>
          <button id="sendChat" class="small">Send</button>
        </div>
      </div>
    </section>

    <!-- Tic-Tac-Toe view -->
    <section class="view" id="tictactoeView">
      <header class="view-header">Tic-Tac-Toe</header>
      <div class="ttt-card">
        <div class="status" id="tttStatus">खिलाड़ी X की बारी</div>
        <div class="board" id="tttBoard">
          <button class="cell" data-index="0"></button>
          <button class="cell" data-index="1"></button>
          <button class="cell" data-index="2"></button>
          <button class="cell" data-index="3"></button>
          <button class="cell" data-index="4"></button>
          <button class="cell" data-index="5"></button>
          <button class="cell" data-index="6"></button>
          <button class="cell" data-index="7"></button>
          <button class="cell" data-index="8"></button>
        </div>
        <div class="controls">
          <button id="tttRestart" class="small">रीस्टार्ट</button>
          <button id="tttReset" class="small ghost">स्कोर रीसेट</button>
        </div>
        <div class="scoreboard">
          <div><strong>X:</strong> <span id="scoreX">0</span></div>
          <div><strong>O:</strong> <span id="scoreO">0</span></div>
          <div><strong>ड्रा:</strong> <span id="scoreDraw">0</span></div>
        </div>
      </div>
    </section>

    <!-- Settings view -->
    <section class="view" id="settingsView">
      <header class="view-header">Settings</header>
      <div class="settings-card">
        <label>Language:
          <select id="langSelect">
            <option value="hi" selected>हिन्दी</option>
            <option value="en">English</option>
          </select>
        </label>
        <label><input type="checkbox" id="prefVoice" /> Voice input enabled</label>
        <label><input type="checkbox" id="prefDark" checked /> Dark theme</label>
        <button id="clearStorage" class="small ghost">Clear Local Data</button>
      </div>
    </section>
  </main>
</div>

<!-- Install prompt for PWA -->
<script>
let deferredPrompt;
window.addEventListener('beforeinstallprompt', (e) => {
  e.preventDefault();
  deferredPrompt = e;
  document.getElementById('installBox').style.display = 'block';
});
document.getElementById('installBtn').addEventListener('click', async () => {
  if(!deferredPrompt) return;
  deferredPrompt.prompt();
  const choice = await deferredPrompt.userChoice;
  deferredPrompt = null;
  document.getElementById('installBox').style.display = 'none';
});
</script>

<script src="app.js"></script>
</body>
</html>


/* Kali GPT PWA styles - Hindi UI, dark theme */
:root{
  --bg:#071023;
  --card:#0b1220;
  --accent:#06b6d4;
  --muted:#9aa8b3;
  --glass:rgba(255,255,255,0.03);
  --success:#10b981;
}
*{box-sizing:border-box}
html,body{height:100%;margin:0;font-family:Inter,system-ui,-apple-system,"Segoe UI",Roboto,"Noto Sans",Arial;color:#e6eef6;background:linear-gradient(180deg,var(--bg),#031220)}
.app-shell{display:flex;min-height:100vh}
.sidebar{width:220px;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);padding:16px;display:flex;flex-direction:column;gap:12px;border-right:1px solid rgba(255,255,255,0.03)}
.brand{display:flex;gap:10px;align-items:center}
.logo{font-size:28px}
.name{font-weight:700;color:var(--accent)}
.nav{display:flex;flex-direction:column;gap:6px}
.nav-btn{background:transparent;border:none;color:var(--muted);padding:8px 10px;text-align:left;border-radius:8px;cursor:pointer}
.nav-btn.active{background:linear-gradient(90deg,var(--accent),#7dd3fc);color:#042024;font-weight:700}
.install-box{margin-top:auto;display:none}
.install-btn{width:100%;padding:8px;border-radius:8px;border:none;background:linear-gradient(90deg,var(--accent),#7dd3fc);color:#042024;font-weight:700;cursor:pointer}
.sb-footer{font-size:12px;color:rgba(255,255,255,0.25);margin-top:8px}

/* main area */
.main{flex:1;padding:18px;display:flex;flex-direction:column;gap:14px}
.view{display:none}
.view-active{display:block}
.view-header{font-size:1.1rem;margin-bottom:8px;color:var(--accent)}

/* Terminal */
.terminal{background:var(--card);padding:12px;border-radius:12px;min-height:260px;display:flex;flex-direction:column;gap:8px;outline:none}
.term-lines{flex:1;overflow:auto;font-family:monospace;font-size:13px}
.term-line{padding:6px 0}
.term-input{display:flex;gap:8px;align-items:center}
.prompt{font-family:monospace;color:var(--muted);padding-right:6px}
.term-input input{flex:1;padding:8px;border-radius:8px;border:1px solid rgba(255,255,255,0.03);background:transparent;color:inherit}
.small{padding:6px 10px;border-radius:8px;border:none;background:linear-gradient(90deg,var(--accent),#7dd3fc);color:#042024;cursor:pointer}
.small.ghost{background:transparent;border:1px solid rgba(255,255,255,0.04);color:var(--muted)}

/* Chat */
.chat-wrap{display:flex;flex-direction:column;height:360px}
.chat-messages{flex:1;overflow:auto;padding:10px;display:flex;flex-direction:column;gap:8px}
.msg{max-width:80%;padding:8px 10px;border-radius:8px;background:var(--glass);font-size:14px}
.msg.user{align-self:flex-end;background:linear-gradient(90deg,var(--accent),#7dd3fc);color:#042024}
.msg.ai{align-self:flex-start;background:rgba(255,255,255,0.02)}
.chat-controls{display:flex;gap:8px;padding-top:8px}
.chat-controls input{flex:1;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.03);background:transparent;color:inherit}

/* Tic-Tac-Toe */
.ttt-card{background:var(--card);padding:12px;border-radius:12px}
.board{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;padding:8px}
.cell{aspect-ratio:1/1;border-radius:10px;background:var(--glass);border:none;font-size:2rem;font-weight:700;display:flex;align-items:center;justify-content:center}
.status{text-align:center;color:var(--muted);margin-bottom:6px}
.controls{display:flex;gap:8px;justify-content:space-between;margin-top:8px}
.scoreboard{display:flex;gap:10px;justify-content:space-around;margin-top:8px;color:var(--muted)}

/* Settings */
.settings-card{background:var(--card);Padding:12px;border-radius:12px;display:flex;flex-direction:column;gap:8px}
label{display:flex;gap:8px;align-items:center}

/* responsive */
@media (max-width:800px){
  .sidebar{display:none}
  .app-shell{flex-direction:column}
  .main{padding:12px}
}


/* Kali GPT frontend-only app.js
   - Terminal: local command interpreter (simulated)
   - AI Chat: local simulated AI replies (no external API)
   - Tic-Tac-Toe: full game with scoreboard (localStorage)
   - Settings persisted to localStorage
   - Service Worker registration handled in index
*/

(() => {
  // Navigation
  const navBtns = document.querySelectorAll('.nav-btn');
  const views = document.querySelectorAll('.view');
  navBtns.forEach(btn => btn.addEventListener('click', () => {
    navBtns.forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    const view = btn.dataset.view;
    views.forEach(v=> v.classList.toggle('view-active', v.id === view + 'View'));
  }));

  // Terminal functionality
  const termLines = document.getElementById('termLines');
  const termInput = document.getElementById('termInput');
  const termSend = document.getElementById('termSend');

  function appendLine(text, cls='term-line'){
    const el = document.createElement('div');
    el.className = cls;
    el.textContent = text;
    termLines.appendChild(el);
    termLines.scrollTop = termLines.scrollHeight;
  }

  function runCommand(cmd){
    appendLine('kali$ ' + cmd);
    cmd = cmd.trim().toLowerCase();
    if(!cmd) return;
    // built-in commands
    if(cmd === 'help'){
      appendLine('मदद: available commands — help, echo, ping, date, clear, about, tictactoe');
    } else if(cmd.startsWith('echo ')){
      appendLine(cmd.slice(5));
    } else if(cmd === 'ping'){
      appendLine('pong');
    } else if(cmd === 'date'){
      appendLine(new Date().toString());
    } else if(cmd === 'clear'){
      termLines.innerHTML = '';
    } else if(cmd === 'about'){
      appendLine('Kali GPT — Local PWA demo. No external AI used unless configured.');
    } else if(cmd === 'tictactoe'){
      document.querySelector('[data-view="tictactoe"]').click();
    } else {
      // fallback: simulate an AI-like reply locally
      appendLine('Unknown command. Trying simulated AI reply...');
      simulateAIReply('Terminal', cmd);
    }
  }

  termSend.addEventListener('click', () => { runCommand(termInput.value); termInput.value=''; });
  termInput.addEventListener('keydown', (e)=> { if(e.key==='Enter'){ runCommand(termInput.value); termInput.value=''; } });

  // Simple simulated AI for chat and terminal fallback
  const chatMessages = document.getElementById('chatMessages');
  const chatInput = document.getElementById('chatInput');
  const sendChat = document.getElementById('sendChat');
  const voiceBtn = document.getElementById('voiceBtn');

  function appendChat(text, who='ai'){
    const el = document.createElement('div');
    el.className = 'msg ' + (who === 'user' ? 'user' : 'ai');
    el.textContent = text;
    chatMessages.appendChild(el);
    chatMessages.scrollTop = chatMessages.scrollHeight;
  }

  function simulateAIReply(mode, prompt){
    // Basic canned/intelligent-ish responses without external API.
    const p = prompt.toLowerCase();
    return new Promise(res => {
      setTimeout(() => {
        let reply = '';
        if(p.includes('नमस्ते') || p.includes('hello')) reply = 'नमस्ते! मैं आपकी किस तरह मदद कर सकता हूँ?';
        else if(p.includes('समय') || p.includes('time')) reply = 'वर्तमान समय: ' + new Date().toLocaleString();
        else if(p.includes('तुम कौन') || p.includes('who are')) reply = 'मैं Kali GPT — एक local PWA demo AI assistant हूँ।';
        else if(p.includes('help')) reply = 'आप help कमांड में उपलब्ध निर्देशों को टाइप कर सकते हैं।';
        else if(p.includes('tic') || p.includes('tictactoe')) { document.querySelector('[data-view="tictactoe"]').click(); reply = 'Tic-Tac-Toe पर ले जा रहा हूँ।'; }
        else reply = 'माफ़ कीजिए — यह एक स्थानिक उत्तर है। (यहाँ कोई बाहरी API नहीं जुड़ा)।';
        // deliver
        if(mode === 'Chat'){ appendChat(reply, 'ai'); }
        else { appendLine('AI: ' + reply); }
        res(reply);
      }, 700 + Math.random()*700);
    });
  }

  sendChat.addEventListener('click', ()=> {
    const txt = chatInput.value.trim();
    if(!txt) return;
    appendChat(txt, 'user');
    chatInput.value = '';
    simulateAIReply('Chat', txt);
  });
  chatInput.addEventListener('keydown', (e)=> { if(e.key === 'Enter'){ sendChat.click(); } });

  // Voice input (optional)
  let recognition;
  if('webkitSpeechRecognition' in window || 'SpeechRecognition' in window){
    const Rec = window.SpeechRecognition || window.webkitSpeechRecognition;
    recognition = new Rec();
    recognition.lang = 'hi-IN';
    recognition.onresult = (e) => {
      const text = e.results[0][0].transcript;
      chatInput.value = text;
      sendChat.click();
    };
    recognition.onerror = console.warn;
    voiceBtn.addEventListener('click', ()=> {
      try { recognition.start(); } catch(e){ console.warn(e); }
    });
  } else {
    voiceBtn.style.display = 'none';
  }

  // Tic-Tac-Toe logic (from provided code, adapted)
  const tttBoard = document.getElementById('tttBoard');
  const tttStatus = document.getElementById('tttStatus');
  const tttRestart = document.getElementById('tttRestart');
  const tttReset = document.getElementById('tttReset');
  const scoreXEl = document.getElementById('scoreX');
  const scoreOEl = document.getElementById('scoreO');
  const scoreDrawEl = document.getElementById('scoreDraw');

  let board = Array(9).fill('');
  let currentPlayer = 'X';
  let isGameActive = true;
  const SCORE_KEY = 'ttt_scores_v1';
  let scores = loadScores();

  const WINNING_COMBOS = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];

  function initTTT(){
    tttBoard.querySelectorAll('.cell').forEach(c=>{
      c.textContent = '';
      c.classList.remove('win','draw');
      c.disabled = false;
      c.addEventListener('click', tttClick);
    });
    updateScoreboard();
    setTTTStatus(`${currentPlayer} की बारी`);
  }
  function tttClick(e){
    const idx = Number(e.target.dataset.index);
    if(!isGameActive || board[idx]) return;
    board[idx] = currentPlayer;
    e.target.textContent = currentPlayer;
    e.target.disabled = true;
    checkResult();
    if(isGameActive){
      currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
      setTTTStatus(`${currentPlayer} की बारी`);
    }
  }
  function checkResult(){
    for(const combo of WINNING_COMBOS){
      const [a,b,c] = combo;
      if(board[a] && board[a] === board[b] && board[a] === board[c]){
        isGameActive = false;
        highlightWin(combo);
        setTTTStatus(`खेला ख़त्म — ${board[a]} जीता!`);
        scores[board[a]] = (scores[board[a]]||0) + 1;
        saveScores(); updateScoreboard();
        return;
      }
    }
    if(board.every(cell=>cell !== '')){
      isGameActive = false;
      setTTTStatus('खींचा (Draw)');
      scores.draw = (scores.draw||0) + 1;
      saveScores(); updateScoreboard();
    }
  }
  function highlightWin(combo){
    combo.forEach(i=>{
      const cell = tttBoard.querySelector(`.cell[data-index='${i}']`);
      if(cell) cell.classList.add('win');
    });
    tttBoard.querySelectorAll('.cell').forEach(c=>c.disabled=true);
  }
  function restartGame(){
    board = Array(9).fill('');
    isGameActive = true;
    currentPlayer = 'X';
    setTTTStatus(`${currentPlayer} की बारी`);
    tttBoard.querySelectorAll('.cell').forEach((c,i)=>{ c.textContent=''; c.disabled=false; c.classList.remove('win','draw'); c.dataset.index = i; });
  }
  function resetScores(){
    if(!confirm('क्या आप स्कोर रीसेट करना चाहते हैं?')) return;
    scores = { X:0, O:0, draw:0 };
    saveScores(); updateScoreboard();
  }
  function updateScoreboard(){
    scoreXEl.textContent = scores.X || 0;
    scoreOEl.textContent = scores.O || 0;
    scoreDrawEl.textContent = scores.draw || 0;
  }
  function saveScores(){ localStorage.setItem(SCORE_KEY, JSON.stringify(scores)); }
  function loadScores(){ try{ return JSON.parse(localStorage.getItem(SCORE_KEY)) || {X:0,O:0,draw:0}; }catch(e){ return {X:0,O:0,draw:0}; } }
  function setTTTStatus(t){ tttStatus.textContent = t; }

  tttRestart.addEventListener('click', restartGame);
  tttReset.addEventListener('click', resetScores);

  // Settings
  const langSelect = document.getElementById('langSelect');
  const prefVoice = document.getElementById('prefVoice');
  const prefDark = document.getElementById('prefDark');
  const clearStorage = document.getElementById('clearStorage');

  function loadSettings(){
    const s = JSON.parse(localStorage.getItem('kali_settings')||'{}');
    if(s.lang) langSelect.value = s.lang;
    prefVoice.checked = !!s.voice;
    prefDark.checked = s.dark !== false;
    document.documentElement.style.filter = prefDark.checked ? '':'invert(0)';
  }
  function saveSettings(){
    const s = { lang: langSelect.value, voice: prefVoice.checked, dark: prefDark.checked };
    localStorage.setItem('kali_settings', JSON.stringify(s));
  }
  langSelect.addEventListener('change', saveSettings);
  prefVoice.addEventListener('change', saveSettings);
  prefDark.addEventListener('change', ()=>{ saveSettings(); document.documentElement.style.filter = prefDark.checked ? '':'invert(0)'; });

  clearStorage.addEventListener('click', ()=>{ if(confirm('Clear all local data?')){ localStorage.clear(); location.reload(); } });

  // Simulated AI welcome
  appendLine('Kali GPT Terminal — Welcome!');
  appendChat('Kali GPT तैयार है — नमस्ते!', 'ai');

  loadSettings();
  initTTT();

  // Service worker register (best-effort)
  if('serviceWorker' in navigator){
    navigator.serviceWorker.register('sw.js').then(()=>console.log('SW registered')).catch(()=>console.warn('SW failed'));
  }

})();

{
  "name": "Kali GPT - AI Terminal",
  "short_name": "KaliGPT",
  "start_url": "index.html",
  "display": "standalone",
  "background_color": "#071023",
  "theme_color": "#071023",
  "icons": [
    {"src":"icon-192.png","sizes":"192x192","type":"image/png"},
    {"src":"icon-512.png","sizes":"512x512","type":"image/png"}
  ]
}


const CACHE_NAME = 'kali-gpt-cache-v1';
const ASSETS = ['index.html','styles.css','app.js','manifest.json','icon.svg','icon-192.png','icon-512.png'];

self.addEventListener('install', e=>{
  self.skipWaiting();
  e.waitUntil(
    caches.open(CACHE_NAME).then(cache => cache.addAll(ASSETS).catch(()=>{}))
  );
});
self.addEventListener('activate', e=>{
  e.waitUntil(self.clients.claim());
});
self.addEventListener('fetch', e=>{
  e.respondWith(
    caches.match(e.request).then(res => res || fetch(e.request).catch(()=>caches.match('index.html')))
  );
});

<svg xmlns='http://www.w3.org/2000/svg' width='512' height='512'>
  <rect width='100%' height='100%' fill='#071023'/>
  <text x='50%' y='50%' font-size='200' fill='#06b6d4' text-anchor='middle' dominant-baseline='central'>🐉</text>
</svg>

Kali GPT — Frontend PWA (Local Demo)

यह एक frontend-only PWA demo है जो नीचे चीजें देती है:
- Terminal mode (local commands)
- AI Chat (simulated replies, no external API)
- Tic-Tac-Toe game with scoreboard (localStorage)
- Settings & voice input (browser support पर निर्भर)
- Installable PWA with service worker (offline caching)

