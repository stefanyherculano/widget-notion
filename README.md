[widget-foco.html](https://github.com/user-attachments/files/28323630/widget-foco.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Foco · Rotina Lucrativa</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400&family=Lato:wght@400&family=Albert+Sans:wght@600&display=swap" rel="stylesheet">
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }

html, body {
height: 100%;
background-color: #f9efe6;
font-family: 'Lato', sans-serif;
color: #472c1c;
overflow: hidden;
-webkit-font-smoothing: antialiased;
}

.rl-widget {
width: 100%;
height: 100vh;
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
padding: 24px 20px;
}

.rl-tabs {
display: flex;
gap: 4px;
background-color: rgba(233, 184, 163, 0.28);
padding: 4px;
border-radius: 10px;
margin-bottom: 28px;
}

.rl-tab {
font-family: 'Albert Sans', sans-serif;
font-weight: 600;
font-size: 11px;
letter-spacing: 1.5px;
text-transform: uppercase;
color: #87695b;
background: transparent;
border: none;
padding: 9px 18px;
border-radius: 8px;
cursor: pointer;
transition: background-color 0.25s ease, color 0.25s ease;
}

.rl-tab.rl-active {
background-color: #d48d6c;
color: #f9efe7;
}

.rl-mode {
display: none;
flex-direction: column;
align-items: center;
}

.rl-mode.rl-show {
display: flex;
}

.rl-phase {
font-family: 'Albert Sans', sans-serif;
font-weight: 600;
font-size: 11px;
letter-spacing: 2px;
text-transform: uppercase;
color: #d48d6c;
margin-bottom: 14px;
min-height: 14px;
}

.rl-display {
font-family: 'Playfair Display', serif;
font-weight: 400;
font-size: 86px;
color: #472c1c;
letter-spacing: -0.03em;
line-height: 1;
font-variant-numeric: tabular-nums;
margin-bottom: 6px;
}

.rl-cycles {
font-family: 'Lato', sans-serif;
font-size: 13px;
color: #87695b;
margin-bottom: 24px;
min-height: 18px;
}

.rl-controls {
display: flex;
gap: 10px;
align-items: center;
}

.rl-btn {
font-family: 'Albert Sans', sans-serif;
font-weight: 600;
font-size: 11px;
letter-spacing: 1.5px;
text-transform: uppercase;
background-color: #d48d6c;
color: #f9efe7;
border: none;
padding: 13px 28px;
border-radius: 8px;
cursor: pointer;
box-shadow:
0 1px 2px rgba(212, 141, 108, 0.20),
0 2px 4px rgba(212, 141, 108, 0.25);
transition: transform 0.15s ease, box-shadow 0.15s ease, background-color 0.25s ease;
}

.rl-btn:hover { transform: translateY(-1px); }
.rl-btn:active { transform: translateY(0); }

.rl-btn-ghost {
background-color: transparent;
color: #87695b;
box-shadow: none;
border: 1px solid rgba(212, 141, 108, 0.35);
padding: 12px 20px;
}

.rl-btn-ghost:hover {
border-color: rgba(212, 141, 108, 0.65);
color: #472c1c;
}

.rl-settings {
margin-top: 32px;
display: flex;
gap: 18px;
flex-wrap: wrap;
justify-content: center;
}

.rl-setting {
display: flex;
flex-direction: column;
align-items: center;
gap: 6px;
}

.rl-setting label {
font-family: 'Albert Sans', sans-serif;
font-weight: 600;
font-size: 9px;
letter-spacing: 1.3px;
text-transform: uppercase;
color: #87695b;
}

.rl-setting input {
width: 56px;
text-align: center;
font-family: 'Lato', sans-serif;
font-size: 14px;
color: #472c1c;
background-color: #faf0e8;
border: 1px solid rgba(212, 141, 108, 0.35);
border-radius: 6px;
padding: 6px 8px;
outline: none;
transition: border-color 0.2s ease;
}

.rl-setting input:focus {
border-color: #d48d6c;
}

@media (max-width: 480px) {
.rl-display { font-size: 64px; }
.rl-btn { padding: 11px 22px; font-size: 10px; }
}
</style>
</head>
<body>

<div class="rl-widget">

<div class="rl-tabs">
<button class="rl-tab rl-active" data-mode="cron" type="button">Cronômetro</button>
<button class="rl-tab" data-mode="pomo" type="button">Pomodoro</button>
</div>

<div class="rl-mode rl-show" id="rl-cron">
<div class="rl-phase">Tempo decorrido</div>
<div class="rl-display" id="rl-cron-display">00:00:00</div>
<div class="rl-cycles"></div>
<div class="rl-controls">
<button class="rl-btn" id="rl-cron-toggle" type="button">Iniciar</button>
<button class="rl-btn rl-btn-ghost" id="rl-cron-reset" type="button">Resetar</button>
</div>
</div>

<div class="rl-mode" id="rl-pomo">
<div class="rl-phase" id="rl-pomo-phase">Foco</div>
<div class="rl-display" id="rl-pomo-display">25:00</div>
<div class="rl-cycles" id="rl-pomo-cycles">Ciclo 1 de 4</div>
<div class="rl-controls">
<button class="rl-btn" id="rl-pomo-toggle" type="button">Iniciar</button>
<button class="rl-btn rl-btn-ghost" id="rl-pomo-skip" type="button">Pular</button>
<button class="rl-btn rl-btn-ghost" id="rl-pomo-reset" type="button">Resetar</button>
</div>
<div class="rl-settings">
<div class="rl-setting">
<label>Foco (min)</label>
<input type="number" id="rl-set-focus" value="25" min="1" max="120">
</div>
<div class="rl-setting">
<label>Pausa curta</label>
<input type="number" id="rl-set-short" value="5" min="1" max="60">
</div>
<div class="rl-setting">
<label>Pausa longa</label>
<input type="number" id="rl-set-long" value="15" min="1" max="60">
</div>
<div class="rl-setting">
<label>Ciclos</label>
<input type="number" id="rl-set-cycles" value="4" min="2" max="10">
</div>
</div>
</div>

</div>

<script>
(function() {

var tabs = document.querySelectorAll('.rl-tab');
var modes = document.querySelectorAll('.rl-mode');
tabs.forEach(function(tab) {
tab.addEventListener('click', function() {
tabs.forEach(function(t) { t.classList.remove('rl-active'); });
tab.classList.add('rl-active');
var target = tab.getAttribute('data-mode');
modes.forEach(function(m) { m.classList.remove('rl-show'); });
document.getElementById('rl-' + target).classList.add('rl-show');
});
});

var cronDisplay = document.getElementById('rl-cron-display');
var cronToggle = document.getElementById('rl-cron-toggle');
var cronReset = document.getElementById('rl-cron-reset');
var cronInterval = null;
var cronElapsed = 0;
var cronStart = 0;

function formatCron(ms) {
var totalSec = Math.floor(ms / 1000);
var h = Math.floor(totalSec / 3600);
var m = Math.floor((totalSec % 3600) / 60);
var s = totalSec % 60;
return String(h).padStart(2, '0') + ':' + String(m).padStart(2, '0') + ':' + String(s).padStart(2, '0');
}

function updateCron() {
var now = Date.now();
cronDisplay.textContent = formatCron(cronElapsed + (now - cronStart));
}

cronToggle.addEventListener('click', function() {
if (cronInterval) {
cronElapsed += Date.now() - cronStart;
clearInterval(cronInterval);
cronInterval = null;
cronToggle.textContent = 'Continuar';
} else {
cronStart = Date.now();
cronInterval = setInterval(updateCron, 200);
cronToggle.textContent = 'Pausar';
}
});

cronReset.addEventListener('click', function() {
clearInterval(cronInterval);
cronInterval = null;
cronElapsed = 0;
cronStart = 0;
cronDisplay.textContent = '00:00:00';
cronToggle.textContent = 'Iniciar';
});

var pomoDisplay = document.getElementById('rl-pomo-display');
var pomoPhase = document.getElementById('rl-pomo-phase');
var pomoCyclesLabel = document.getElementById('rl-pomo-cycles');
var pomoToggle = document.getElementById('rl-pomo-toggle');
var pomoSkip = document.getElementById('rl-pomo-skip');
var pomoReset = document.getElementById('rl-pomo-reset');
var setFocus = document.getElementById('rl-set-focus');
var setShort = document.getElementById('rl-set-short');
var setLong = document.getElementById('rl-set-long');
var setCycles = document.getElementById('rl-set-cycles');

var pomoInterval = null;
var pomoEnd = 0;
var pomoRemaining = 0;
var pomoPhaseIndex = 0;
var pomoCycle = 1;
var pomoRunning = false;

function currentPhaseDuration() {
if (pomoPhaseIndex === 0) return parseInt(setFocus.value, 10) * 60 * 1000;
if (pomoPhaseIndex === 1) {
var totalCycles = parseInt(setCycles.value, 10);
if (pomoCycle === totalCycles) return parseInt(setLong.value, 10) * 60 * 1000;
return parseInt(setShort.value, 10) * 60 * 1000;
}
return 0;
}

function currentPhaseLabel() {
if (pomoPhaseIndex === 0) return 'Foco';
var totalCycles = parseInt(setCycles.value, 10);
if (pomoCycle === totalCycles && pomoPhaseIndex === 1) return 'Pausa longa';
return 'Pausa curta';
}

function formatPomo(ms) {
if (ms < 0) ms = 0;
var totalSec = Math.ceil(ms / 1000);
var m = Math.floor(totalSec / 60);
var s = totalSec % 60;
return String(m).padStart(2, '0') + ':' + String(s).padStart(2, '0');
}

function updatePomoDisplay(remaining) {
pomoDisplay.textContent = formatPomo(remaining);
pomoPhase.textContent = currentPhaseLabel();
var totalCycles = parseInt(setCycles.value, 10);
pomoCyclesLabel.textContent = 'Ciclo ' + pomoCycle + ' de ' + totalCycles;
}

function resetPomo() {
clearInterval(pomoInterval);
pomoInterval = null;
pomoRunning = false;
pomoPhaseIndex = 0;
pomoCycle = 1;
pomoRemaining = currentPhaseDuration();
pomoToggle.textContent = 'Iniciar';
updatePomoDisplay(pomoRemaining);
}

function advancePhase() {
var totalCycles = parseInt(setCycles.value, 10);
if (pomoPhaseIndex === 0) {
pomoPhaseIndex = 1;
} else {
pomoPhaseIndex = 0;
if (pomoCycle >= totalCycles) {
pomoCycle = 1;
} else {
pomoCycle += 1;
}
}
pomoRemaining = currentPhaseDuration();
updatePomoDisplay(pomoRemaining);
try {
if (typeof Audio !== 'undefined') {
var ctx = new (window.AudioContext || window.webkitAudioContext)();
var osc = ctx.createOscillator();
var gain = ctx.createGain();
osc.connect(gain);
gain.connect(ctx.destination);
osc.frequency.value = 660;
gain.gain.setValueAtTime(0.0001, ctx.currentTime);
gain.gain.exponentialRampToValueAtTime(0.15, ctx.currentTime + 0.02);
gain.gain.exponentialRampToValueAtTime(0.0001, ctx.currentTime + 0.4);
osc.start(ctx.currentTime);
osc.stop(ctx.currentTime + 0.42);
}
} catch (e) {}
}

function tickPomo() {
var now = Date.now();
var remaining = pomoEnd - now;
if (remaining <= 0) {
advancePhase();
pomoEnd = Date.now() + pomoRemaining;
} else {
updatePomoDisplay(remaining);
}
}

pomoToggle.addEventListener('click', function() {
if (pomoRunning) {
pomoRemaining = pomoEnd - Date.now();
clearInterval(pomoInterval);
pomoInterval = null;
pomoRunning = false;
pomoToggle.textContent = 'Continuar';
} else {
if (pomoRemaining <= 0) pomoRemaining = currentPhaseDuration();
pomoEnd = Date.now() + pomoRemaining;
pomoInterval = setInterval(tickPomo, 250);
pomoRunning = true;
pomoToggle.textContent = 'Pausar';
}
});

pomoSkip.addEventListener('click', function() {
advancePhase();
if (pomoRunning) {
pomoEnd = Date.now() + pomoRemaining;
} else {
updatePomoDisplay(pomoRemaining);
}
});

pomoReset.addEventListener('click', resetPomo);

[setFocus, setShort, setLong, setCycles].forEach(function(input) {
input.addEventListener('change', function() {
if (!pomoRunning) {
pomoRemaining = currentPhaseDuration();
updatePomoDisplay(pomoRemaining);
}
});
});

resetPomo();

})();
</script>

</body>
</html>
