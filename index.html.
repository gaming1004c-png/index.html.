
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#050b18">
<title>JARVIS | Personal Assistant</title>
<style>
:root {
  --blue: #39d8ff;
  --bg: #050b18;
  --panel: #0b1830;
}
* { box-sizing: border-box; }
body {
  margin: 0; min-height: 100vh;
  background: radial-gradient(ellipse at 50% 35%,
    #102d50 0%, var(--bg) 68%);
  color: #e6f7ff;
  font-family: system-ui, sans-serif;
}
main {
  width: min(100% - 28px, 560px);
  margin: auto; padding: 28px 0;
}
header { display:flex; justify-content:space-between;
  align-items:center; gap:12px; }
.eyebrow { color:var(--blue); letter-spacing:3px;
  font-size:11px; }
h1 { font-size:25px; letter-spacing:5px; margin:5px 0; }
.status { font-size:12px; color:#9db9d5; }
.pill { border:1px solid #245477; padding:7px 10px;
  border-radius:30px; color:var(--blue); font-size:11px; }
.orb-area { display:grid; place-items:center; padding:42px 0 28px; }
.orb {
  width:180px; height:180px; border-radius:50%;
  display:grid; place-items:center; cursor:pointer;
  background:radial-gradient(circle, #164f79 0%, #0c2343 45%,
    #071225 68%);
  border:1px solid #43dfff;
  box-shadow:0 0 22px #21baff40, inset 0 0 24px #21baff45;
  color:var(--blue); font-size:45px;
  transition:transform .2s, box-shadow .2s;
  animation:pulse 3s infinite;
}
.orb:active { transform:scale(.96); }
.orb.listening {
  box-shadow:0 0 45px #21baff99, inset 0 0 35px #21baff80;
  animation:pulse .8s infinite;
}
@keyframes pulse {
  50% { box-shadow:0 0 35px #21baff65, inset 0 0 30px #21baff65; }
}
.center { text-align:center; }
#state { color:var(--blue); font-size:13px; }
.card {
  background:#09172acc; border:1px solid #183654;
  border-radius:16px; padding:16px; margin-top:14px;
}
.label { font-size:10px; letter-spacing:2px;
  color:#78a7c8; margin-bottom:9px; }
#reply { line-height:1.6; min-height:48px; white-space:pre-wrap; }
.row { display:flex; gap:8px; margin-top:12px; }
input, button {
  font:inherit; border-radius:10px; padding:12px;
}
input {
  min-width:0; flex:1; background:#050d1b;
  color:white; border:1px solid #21415e;
}
button { cursor:pointer; }
.primary {
  background:#103957; color:var(--blue);
  border:1px solid #2b8cb3;
}
.shortcuts { display:grid; grid-template-columns:1fr 1fr; gap:9px; }
.shortcuts button {
  background:#0a1b31; border:1px solid #1a3b58;
  color:#c9eaff; text-align:left; font-size:13px;
}
footer { color:#6686a3; font-size:11px; line-height:1.6;
  text-align:center; padding:22px 4px; }
</style>
</head>
<body>
<main>
<header>
  <div>
    <div class="eyebrow">PERSONAL AI SYSTEM</div>
    <h1>J.A.R.V.I.S.</h1>
    <div class="status">Mobile interface · Prototype 01</div>
  </div>
  <div class="pill">● SYSTEM READY</div>
</header>

<section class="orb-area">
  <button id="orb" class="orb" aria-label="Start voice input">◉</button>
</section>
<div class="center">
  <div id="state">READY WHEN YOU ARE, SIR</div>
  <p class="status">Tap the orb and speak, or type below.</p>
</div>

<section class="card">
  <div class="label">ASSISTANT RESPONSE</div>
  <div id="reply">Good day, sir. JARVIS prototype is online.
How may I assist you?</div>
  <div class="row">
    <input id="question" placeholder="Enter a command..." />
    <button class="primary" id="send">Send</button>
  </div>
</section>

<section class="card">
  <div class="label">QUICK COMMANDS</div>
  <div class="shortcuts">
    <button data-cmd="What time is it?">◷ &nbsp; Time and date</button>
    <button data-cmd="Give me motivation">✦ &nbsp; Motivation</button>
    <button data-cmd="Help me study">▤ &nbsp; Study mode</button>
    <button data-cmd="Tell me a football joke">⚽ &nbsp; Football mode</button>
  </div>
</section>

<footer>
  LOCAL DEMO · Replies are built-in examples, not live AI.
  Voice recognition may require internet and microphone permission.
</footer>
</main>

<script>
const orb = document.querySelector("#orb");
const state = document.querySelector("#state");
const reply = document.querySelector("#reply");
const question = document.querySelector("#question");
const send = document.querySelector("#send");

function speak(text) {
  if (!("speechSynthesis" in window)) return;
  speechSynthesis.cancel();
  const msg = new SpeechSynthesisUtterance(text);
  msg.lang = "en-IN";
  msg.rate = 0.95;
  msg.pitch = 0.95;
  speechSynthesis.speak(msg);
}

function answer(text) {
  const q = text.toLowerCase().trim();
  let result;

  if (q.includes("time") || q.includes("date")) {
    result = "The current time is " +
      new Date().toLocaleTimeString([], {hour:"2-digit",minute:"2-digit"}) +
      ". Today is " + new Date().toLocaleDateString("en-IN",
      {weekday:"long",day:"numeric",month:"long",year:"numeric"}) + ".";
  } else if (q.includes("study") || q.includes("homework")) {
    result = "Study mode initiated, sir. Pick one topic, work for 25 minutes, then take a short break. Which subject are we tackling?";
  } else if (q.includes("football")) {
    result = "Football mode activated. Remember, sir: tactics win matches, but your friends will still blame the referee.";
  } else if (q.includes("motivat")) {
    result = "One task at a time, sir. You do not need to solve the whole week today. Just win the next 20 minutes.";
  } else if (q.includes("hello") || q.includes("hi jarvis")) {
    result = "Hello, sir. All systems are ready. What shall we work on?";
  } else if (q.includes("help")) {
    result = "Available commands: time, date, study mode, motivation, football joke, and hello. This prototype does not have live AI connected yet.";
  } else {
    result = "I received your message: " + text +
      ". Sir, this prototype uses preset responses. A real AI connection is a separate next step.";
  }

  reply.textContent = result;
  state.textContent = "RESPONSE READY";
  speak(result);
}

function listen() {
  const SpeechRecognition =
    window.SpeechRecognition || window.webkitSpeechRecognition;

  if (!SpeechRecognition) {
    state.textContent = "VOICE INPUT UNAVAILABLE";
    reply.textContent = "This browser does not expose speech recognition. Try an updated Chrome browser, or use the text box.";
    return;
  }

  const recognition = new SpeechRecognition();
  recognition.lang = "en-IN";
  recognition.interimResults = false;
  recognition.maxAlternatives = 1;

  recognition.onstart = () => {
    state.textContent = "LISTENING...";
    orb.classList.add("listening");
  };
  recognition.onresult = event => {
    question.value = event.results[0][0].transcript;
    answer(question.value);
  };
  recognition.onerror = () => {
    state.textContent = "VOICE INPUT ERROR";
    reply.textContent = "Please check microphone permission and internet access, then try again.";
  };
  recognition.onend = () => {
    orb.classList.remove("listening");
    if (state.textContent === "LISTENING...") {
      state.textContent = "READY WHEN YOU ARE, SIR";
    }
  };

  try { recognition.start(); }
  catch (e) { state.textContent = "PLEASE TRY AGAIN"; }
}

orb.addEventListener("click", listen);
send.addEventListener("click", () => {
  if (question.value.trim()) answer(question.value.trim());
});
question.addEventListener("keydown", event => {
  if (event.key === "Enter" && question.value.trim()) {
    answer(question.value.trim());
  }
});
document.querySelectorAll("[data-cmd]").forEach(button => {
  button.addEventListener("click", () => answer(button.dataset.cmd));
});
</script>
</body>
</html>
