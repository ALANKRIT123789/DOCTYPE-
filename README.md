<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Mira — Calm Digital Friend</title>
<style>
  :root{
    --bg:#070b12;
    --card:rgba(15,23,36,.82);
    --line:rgba(140,220,255,.18);
    --cyan:#8fe8ff;
    --pink:#ff9ad5;
    --text:#e8f4ff;
    --muted:#8da6bd;
  }
  *{box-sizing:border-box}
  html,body{height:100%;margin:0}
  body{
    display:grid;place-items:center;min-height:100svh;
    background:
      radial-gradient(circle at 30% 10%, rgba(255,154,213,.10), transparent 35%),
      radial-gradient(circle at 70% 90%, rgba(143,232,255,.12), transparent 40%),
      var(--bg);
    color:var(--text);
    font-family:system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;
    padding:16px;
  }
  .card{
    width:min(92vw,520px);
    background:var(--card);
    border:1px solid var(--line);
    border-radius:24px;
    padding:18px;
    box-shadow:0 25px 80px rgba(0,0,0,.55), inset 0 0 40px rgba(143,232,255,.04);
    backdrop-filter:blur(14px);
  }
  .top{display:flex;align-items:center;gap:14px}
  .avatar{
    width:92px;height:92px;flex:0 0 92px;
    border-radius:50%;
    overflow:hidden;
    border:1px solid rgba(255,255,255,.14);
    box-shadow:0 0 30px rgba(143,232,255,.20);
    animation:breathe 4.8s ease-in-out infinite;
    background:#0b1522;
  }
  .avatar svg{width:100%;height:100%;display:block}
  @keyframes breathe{
    0%,100%{transform:scale(1)}
    50%{transform:scale(1.035)}
  }
  .avatar.talking{animation:breathe 1.1s ease-in-out infinite}
  .who h1{margin:0;font-size:1.25rem;letter-spacing:.02em}
  .who p{margin:4px 0 0;color:var(--muted);font-size:.82rem}
  .status{
    margin-top:8px;font-size:.7rem;color:var(--cyan);
    opacity:.85;word-break:break-word;
  }
  .chat{
    height:220px;overflow:auto;margin:16px 0 12px;
    padding:10px;border-radius:16px;
    background:rgba(0,0,0,.22);
    border:1px solid rgba(255,255,255,.06);
    scroll-behavior:smooth;
  }
  .msg{
    max-width:86%;margin:8px 0;padding:10px 13px;
    border-radius:16px;line-height:1.4;font-size:.9rem;
    white-space:pre-wrap;
  }
  .msg.mira{
    background:linear-gradient(135deg,rgba(143,232,255,.16),rgba(255,154,213,.10));
    border:1px solid rgba(143,232,255,.20);
    border-bottom-left-radius:5px;
  }
  .msg.you{
    margin-left:auto;
    background:rgba(255,255,255,.08);
    border:1px solid rgba(255,255,255,.08);
    border-bottom-right-radius:5px;
  }
  form{display:flex;gap:8px}
  input{
    flex:1;min-width:0;padding:13px 14px;border-radius:14px;
    border:1px solid rgba(255,255,255,.12);
    background:rgba(0,0,0,.28);color:var(--text);
    outline:none;font-size:.95rem;
  }
  input:focus{border-color:rgba(143,232,255,.55);box-shadow:0 0 0 3px rgba(143,232,255,.08)}
  button{
    border:1px solid rgba(143,232,255,.25);
    background:linear-gradient(135deg,rgba(143,232,255,.18),rgba(255,154,213,.14));
    color:var(--text);padding:12px 15px;border-radius:14px;
    font-weight:650;cursor:pointer;
  }
  button:active{transform:translateY(1px)}
  .controls{display:flex;gap:8px;margin-top:10px;flex-wrap:wrap}
  select{
    flex:1;min-width:150px;padding:11px 12px;border-radius:14px;
    background:rgba(0,0,0,.28);color:var(--text);
    border:1px solid rgba(255,255,255,.12);
  }
  .hint{margin:10px 2px 0;color:var(--muted);font-size:.68rem;line-height:1.4}
  @media (prefers-reduced-motion:reduce){
    .avatar,.avatar.talking{animation:none}
  }
</style>
</head>
<body>
<main class="card" aria-label="Mira, a calm digital friend">
  <div class="top">
    <div class="avatar" id="avatar" aria-hidden="true">
      <svg viewBox="0 0 200 200">
        <defs>
          <radialGradient id="bg" cx="50%" cy="35%" r="70%">
            <stop offset="0" stop-color="#14314a"/>
            <stop offset="1" stop-color="#070b12"/>
          </radialGradient>
          <linearGradient id="hair" x1="0" y1="0" x2="1" y2="1">
            <stop offset="0" stop-color="#1a1320"/>
            <stop offset="1" stop-color="#3a2038"/>
          </linearGradient>
          <linearGradient id="skin" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0" stop-color="#f1c7b3"/>
            <stop offset="1" stop-color="#d99a82"/>
          </linearGradient>
        </defs>
        <rect width="200" height="200" fill="url(#bg)"/>
        <circle cx="100" cy="88" r="48" fill="url(#hair)"/>
        <ellipse cx="100" cy="92" rx="35" ry="42" fill="url(#skin)"/>
        <path d="M64 83c5-28 24-42 36-42s31 14 36 42c-9-12-21-17-36-17s-27 5-36 17Z" fill="url(#hair)"/>
        <ellipse cx="86" cy="91" rx="4.2" ry="5" fill="#1a2633"/>
        <ellipse cx="114" cy="91" rx="4.2" ry="5" fill="#1a2633"/>
        <circle cx="87.2" cy="89.2" r="1.1" fill="#fff" opacity=".9"/>
        <circle cx="115.2" cy="89.2" r="1.1" fill="#fff" opacity=".9"/>
        <path d="M88 111c7 6 17 6 24 0" fill="none" stroke="#9d5f58" stroke-width="3" stroke-linecap="round"/>
        <path d="M62 200c3-30 20-47 38-47s35 17 38 47Z" fill="#132536"/>
        <path d="M62 200c3-30 20-47 38-47" fill="none" stroke="rgba(143,232,255,.20)" stroke-width="2"/>
      </svg>
    </div>
    <div class="who">
      <h1>Mira</h1>
      <p>Your calm digital friend</p>
      <div class="status" id="voiceStatus">Loading voices…</div>
    </div>
  </div>

  <div class="chat" id="chat" aria-live="polite">
    <div class="msg mira">Hi. I’m Mira. You don’t have to perform here. Tell me what’s on your mind—or tap “Say hi.”</div>
  </div>

  <form id="chatForm">
    <input id="message" placeholder="Say something…" autocomplete="off" />
    <button type="submit">Send</button>
  </form>

  <div class="controls">
    <select id="accent" aria-label="Voice accent">
      <option value="mixed">Mixed / soothing</option>
      <option value="lithuanian">Lithuanian vibe</option>
      <option value="british">British</option>
      <option value="indian">Indian English</option>
      <option value="american">American</option>
    </select>
    <button type="button" id="hiBtn">Say hi</button>
    <button type="button" id="muteBtn">Mute</button>
  </div>

  <p class="hint">
    Voice uses your browser’s built-in speech engine. Female/accent voices vary by device.
    For a photorealistic talking avatar, you’d need a licensed 3D/video avatar API—not plain HTML.
  </p>
</main>

<script>
  const synth = window.speechSynthesis;
  const chat = document.getElementById("chat");
  const form = document.getElementById("chatForm");
  const input = document.getElementById("message");
  const accent = document.getElementById("accent");
  const voiceStatus = document.getElementById("voiceStatus");
  const avatar = document.getElementById("avatar");
  const muteBtn = document.getElementById("muteBtn");

  let voices = [];
  let currentVoice = null;
  let muted = false;

  const femaleHints = /female|woman|zira|hazel|aria|jenny|sonia|samantha|karen|moira|tessa|victoria|fiona|libby|natasha|susan|allison|ava|serena|veena|kalpana|google uk english female/i;

  const accentMap = {
    mixed: ["en-GB", "en-IN", "en-US", "en-AU", "en-NZ"],
    lithuanian: ["lt-LT", "lt"],
    british: ["en-GB"],
    indian: ["en-IN"],
    american: ["en-US"]
  };

  function loadVoices(){
    voices = synth ? synth.getVoices().filter(v => v.lang) : [];
    pickVoice();
  }

  function pickVoice(){
    const prefs = accentMap[accent.value] || accentMap.mixed;
    let pool = [];

    for (const lang of prefs){
      pool = voices.filter(v => v.lang.toLowerCase().startsWith(lang.toLowerCase()));
      if (pool.length) break;
    }

    const femalePool = pool.filter(v => femaleHints.test(v.name));
    currentVoice =
      femalePool[0] ||
      pool[0] ||
      voices.find(v => femaleHints.test(v.name)) ||
      voices[0] ||
      null;

    voiceStatus.textContent = currentVoice
      ? `Voice: ${currentVoice.name} (${currentVoice.lang})`
      : "No voice loaded yet — tap “Say hi” after interacting.";
  }

  function setTalking(on){
    avatar.classList.toggle("talking", !!on);
  }

  function speak(text){
    if (!synth || muted) return;
    synth.cancel();

    const u = new SpeechSynthesisUtterance(text);
    if (currentVoice) u.voice = currentVoice;
    u.rate = 0.86;      // soothing pace
    u.pitch = 1.08;     // gentle feminine lift
    u.volume = 0.95;
    u.onstart = () => setTalking(true);
    u.onend = () => setTalking(false);
    u.onerror = () => setTalking(false);

    synth.speak(u);
  }

  function addMsg(who, text){
    const div = document.createElement("div");
    div.className = `msg ${who}`;
    div.textContent = text;
    chat.appendChild(div);
    chat.scrollTop = chat.scrollHeight;
  }

  function replyTo(text){
    const s = text.toLowerCase();

    if (/stress|anxious|panic|overwhelm|anxiety/.test(s))
      return "Let’s slow this down. Breathe in for four… hold… out for six. I’m right here. Nothing needs to be solved this second.";

    if (/tired|exhausted|sleep|burn/.test(s))
      return "You sound exhausted. Rest isn’t a reward—it’s maintenance. Can you lie down for ten minutes without fixing anything?";

    if (/sad|lonely|down|empty|cry/.test(s))
      return "I’m sorry it feels like that. You don’t have to carry it alone right now. Tell me the part that hurts most.";

    if (/plan|work|study|goal|business|money/.test(s))
      return "Pick the smallest next action. Not the whole plan—one realistic step you can finish today. I’ll help you keep it honest.";

    if (/angry|mad|frustrated|unfair/.test(s))
      return "That sounds frustrating. You’re allowed to be angry. Let’s separate what happened from what you want to do next.";

    if (/hi|hello|hey|good morning|good evening/.test(s))
      return "Hi. I’m glad you’re here. How are you actually doing—not the polite answer?";

    const fallbacks = [
      "I’m listening. Tell me more, and I won’t rush you.",
      "That makes sense. What would feel like a small kindness to yourself right now?",
      "Okay. Softly now—what do you need most in this moment?",
      "I hear you. You don’t have to have the right words."
    ];
    return fallbacks[Math.floor(Math.random() * fallbacks.length)];
  }

  form.addEventListener("submit", e => {
    e.preventDefault();
    const text = input.value.trim();
    if (!text) return;

    addMsg("you", text);
    input.value = "";

    setTimeout(() => {
      const reply = replyTo(text);
      addMsg("mira", reply);
      speak(reply);
    }, 350);
  });

  document.getElementById("hiBtn").addEventListener("click", () => {
    if (!voices.length) loadVoices();
    const greeting = "Hi. I’m Mira. Take a breath. What’s on your mind?";
    addMsg("mira", greeting);
    speak(greeting);
  });

  muteBtn.addEventListener("click", () => {
    muted = !muted;
    if (muted && synth) synth.cancel();
    setTalking(false);
    muteBtn.textContent = muted ? "Unmute" : "Mute";
  });

  accent.addEventListener("change", () => {
    if (!voices.length) loadVoices();
    pickVoice();
  });

  if ("speechSynthesis" in window){
    loadVoices();
    synth.onvoiceschanged = loadVoices;
  } else {
    voiceStatus.textContent = "Speech synthesis is not supported in this browser.";
  }
</script>
</body>
</html>
