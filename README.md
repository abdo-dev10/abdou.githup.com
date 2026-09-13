<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday ♡</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&family=Patrick+Hand&display=swap" rel="stylesheet">

<style>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
html, body {
    width: 100%;
    height: 100%;
    overflow: hidden;
    background: #0d0614;
    color: #ffffff;
    user-select: none;
    font-family: 'Fredoka', sans-serif;
}

.screen {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100dvh;
    display: none;
    overflow: hidden;
}
.screen.active {
    display: flex;
}

/* =====================================================
   1. COUNTDOWN MATRIX HEARTS (PURE CODE)
===================================================== */
#countdown-screen {
    align-items: center;
    justify-content: center;
    background: #0a0312;
}

#matrixCanvas {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
}

#number {
    position: relative;
    z-index: 10;
    font-size: clamp(120px, 24vw, 210px);
    font-weight: 700;
    color: #ff4d94;
    text-shadow: 
        0 0 25px #ff0066,
        0 0 50px #ff3388,
        0 0 90px #e6005c;
    animation: numPop 0.8s cubic-bezier(0.34, 1.56, 0.64, 1);
}

@keyframes numPop {
    0% { opacity: 0; transform: scale(0.2); filter: blur(8px); }
    100% { opacity: 1; transform: scale(1); filter: blur(0); }
}

/* =====================================================
   2. MAIN SCENE & PASTEL NIGHT ATMOSPHERE
===================================================== */
#space-screen {
    align-items: center;
    justify-content: center;
    background: radial-gradient(circle at 50% 35%, #2a1545 0%, #120724 65%, #080212 100%);
}

.stars-container {
    position: absolute;
    inset: 0;
    pointer-events: none;
}
.star {
    position: absolute;
    background: #fff;
    clip-path: polygon(50% 0%, 63% 37%, 100% 50%, 63% 63%, 50% 100%, 37% 63%, 0% 50%, 37% 37%);
    animation: starPulse var(--dur) ease-in-out infinite alternate;
}
@keyframes starPulse {
    0% { opacity: 0.2; transform: scale(0.5); }
    100% { opacity: 1; transform: scale(1.2); filter: drop-shadow(0 0 8px #ffb3d9); }
}

.moon {
    position: absolute;
    top: 6%;
    right: 8%;
    width: 56px;
    height: 56px;
    border-radius: 50%;
    box-shadow: -14px 12px 0 2px #ffe680;
    filter: drop-shadow(0 0 15px rgba(255, 230, 128, 0.85));
}

.saturn-planet {
    position: absolute;
    top: 7%;
    left: 8%;
    width: 68px;
    height: 68px;
    border-radius: 50%;
    background: radial-gradient(circle at 30% 30%, #d4b2ff, #6b26d9);
    box-shadow: 0 0 25px rgba(212, 178, 255, 0.45);
}
.saturn-planet::after {
    content: "";
    position: absolute;
    width: 98px;
    height: 24px;
    border: 4px solid #ebd9ff;
    border-radius: 50%;
    left: -18px;
    top: 22px;
    transform: rotate(-20deg);
}

/* HAPPY BIRTHDAY TITLE */
.hb-title {
    position: absolute;
    top: 5%;
    text-align: center;
    z-index: 20;
    direction: ltr;
}
.hb-word {
    display: flex;
    justify-content: center;
    gap: 8px;
    font-size: clamp(38px, 6.5vw, 70px);
    font-weight: 700;
}
.letter {
    display: inline-block;
    animation: letterBounce 2s ease-in-out infinite alternate;
    text-shadow: 0 6px 0 rgba(0,0,0,0.3);
}
.letter:nth-child(1){ color:#ff77b9; animation-delay:.1s; }
.letter:nth-child(2){ color:#ff99c8; animation-delay:.2s; }
.letter:nth-child(3){ color:#ffb3d9; animation-delay:.3s; }
.letter:nth-child(4){ color:#c299ff; animation-delay:.4s; }
.letter:nth-child(5){ color:#99c2ff; animation-delay:.5s; }
.letter:nth-child(6){ color:#80e5ff; animation-delay:.6s; }
.letter:nth-child(7){ color:#ffe680; animation-delay:.7s; }

@keyframes letterBounce {
    from { transform: translateY(0); }
    to { transform: translateY(-12px); }
}

/* SUPER CUTE DUCK STAGE & SMOOTH RUNNING */
.duck-stage {
    position: absolute;
    bottom: 8%;
    left: 50%;
    transform: translateX(-50%);
    width: 220px;
    height: 230px;
    z-index: 15;
    transition: left 2.2s cubic-bezier(0.25, 1, 0.5, 1);
}
.duck-stage.run-to-gift {
    left: 68%;
}

.duck-inner {
    width: 100%;
    height: 100%;
    animation: duckIdle 3s ease-in-out infinite;
}

.duck-stage.run-to-gift .duck-inner {
    animation: duckSmoothRun 0.35s ease-in-out infinite alternate;
}

@keyframes duckIdle {
    0%, 100% { transform: translateY(0) rotate(0deg); }
    50% { transform: translateY(-7px) rotate(1deg); }
}

@keyframes duckSmoothRun {
    0% { transform: translateY(0) rotate(-4deg); }
    100% { transform: translateY(-12px) rotate(4deg); }
}

/* GIFT BOX STAGE */
.gift-container {
    position: absolute;
    bottom: 9%;
    left: 36%;
    width: 135px;
    height: 135px;
    z-index: 25;
    cursor: pointer;
    opacity: 0;
    transform: scale(0.3) translateY(40px);
    transition: all 1s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.gift-container.show {
    opacity: 1;
    transform: scale(1) translateY(0);
}

.open-text {
    position: absolute;
    top: -48px;
    width: 100%;
    text-align: center;
    font-family: 'Fredoka', sans-serif;
    font-size: 24px;
    font-weight: 700;
    color: #ffe680;
    text-shadow: 0 3px 0 #cc3300, 0 0 12px #ff1a75;
    animation: openBounce 0.8s ease-in-out infinite alternate;
    direction: ltr;
}
@keyframes openBounce {
    from { transform: translateY(0); }
    to { transform: translateY(-6px); }
}

/* =====================================================
   3. BEAUTIFUL & SMOOTH ENVELOPE MODAL
===================================================== */
#envelope-modal {
    position: absolute;
    inset: 0;
    background: rgba(10, 4, 18, 0.88);
    backdrop-filter: blur(12px);
    z-index: 50;
    display: none;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.6s ease;
}
#envelope-modal.active {
    display: flex;
    opacity: 1;
}

.envelope-wrapper {
    position: relative;
    width: min(90%, 410px);
    height: 260px;
    background: linear-gradient(135deg, #ff99c8 0%, #ff80bf 100%);
    border-radius: 20px;
    box-shadow: 0 25px 50px rgba(0,0,0,0.6), 0 0 30px rgba(255, 128, 191, 0.3);
    display: flex;
    justify-content: center;
    align-items: flex-end;
    perspective: 1200px;
}

.envelope-flap {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 140px;
    background: #ff70b5;
    clip-path: polygon(0 0, 100% 0, 50% 100%);
    transform-origin: top;
    transition: transform 0.7s cubic-bezier(0.4, 0, 0.2, 1) 0.1s, z-index 0.1s ease 0.35s;
    z-index: 3;
    border-radius: 20px 20px 0 0;
}
.envelope-wrapper.open .envelope-flap {
    transform: rotateX(180deg);
    z-index: 1;
}

.envelope-pocket {
    position: absolute;
    inset: 0;
    background: linear-gradient(180deg, #ff5c9d 0%, #ff4d94 100%);
    clip-path: polygon(0 100%, 100% 100%, 100% 38%, 50% 72%, 0 38%);
    z-index: 3;
    border-radius: 0 0 20px 20px;
}

.letter-card {
    position: absolute;
    bottom: 12px;
    width: 88%;
    height: 230px;
    background: #ffffff;
    border-radius: 16px;
    padding: 28px 24px;
    box-shadow: 0 8px 25px rgba(0,0,0,0.15);
    z-index: 2;
    transition: transform 0.9s cubic-bezier(0.34, 1.3, 0.64, 1) 0.5s, height 0.6s ease 1.1s;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    color: #3b2233;
    border: 2px solid #fff0f5;
}

.envelope-wrapper.open .letter-card {
    transform: translateY(-115px);
    height: 300px;
    z-index: 4;
}

.card-header-line {
    width: 40px;
    height: 4px;
    background: #ff80bf;
    border-radius: 2px;
    margin-bottom: 12px;
}

.letter-card h2 {
    font-family: 'Patrick Hand', cursive;
    font-size: 40px;
    color: #ff1a75;
    margin-bottom: 10px;
    direction: ltr;
}

.letter-card p {
    font-family: 'Patrick Hand', cursive;
    font-size: 23px;
    line-height: 1.45;
    color: #4a2b40;
    direction: ltr;
}

.letter-card strong {
    color: #e6005c;
}

.fade-out { animation: fadeOut 0.7s forwards; }
@keyframes fadeOut { to { opacity: 0; } }

@media(max-width: 600px) {
    .duck-stage { width: 180px; height: 190px; }
    .duck-stage.run-to-gift { left: 66%; }
    .gift-container { width: 110px; height: 110px; left: 24%; }
    .open-text { font-size: 20px; top: -40px; }
}
</style>
</head>
<body>

<!-- 1. COUNTDOWN SCREEN -->
<section id="countdown-screen" class="screen active">
    <canvas id="matrixCanvas"></canvas>
    <div id="number">3</div>
</section>

<!-- 2. MAIN SPACE SCENE -->
<section id="space-screen" class="screen">
    <div class="stars-container" id="starsContainer"></div>
    <div class="saturn-planet"></div>
    <div class="moon"></div>

    <!-- TITLE -->
    <div class="hb-title">
        <div class="hb-word">
            <span class="letter">H</span><span class="letter">A</span><span class="letter">P</span><span class="letter">P</span><span class="letter">Y</span>
        </div>
        <div class="hb-word">
            <span class="letter">B</span><span class="letter">I</span><span class="letter">R</span><span class="letter">T</span><span class="letter">H</span><span class="letter">D</span><span class="letter">A</span><span class="letter">Y</span>
        </div>
    </div>

    <!-- NEW ULTRA CUTE DUCK WITH GUITAR -->
    <div class="duck-stage" id="duckStage">
        <div class="duck-inner">
            <svg viewBox="0 0 200 220" width="100%" height="100%">
                <defs>
                    <linearGradient id="duckGrad" x1="0%" y1="0%" x2="0%" y2="100%">
                        <stop offset="0%" stop-color="#ffffcc"/>
                        <stop offset="100%" stop-color="#ffeb99"/>
                    </linearGradient>
                    <linearGradient id="beakGrad" x1="0%" y1="0%" x2="0%" y2="100%">
                        <stop offset="0%" stop-color="#ffb366"/>
                        <stop offset="100%" stop-color="#ff8000"/>
                    </linearGradient>
                    <linearGradient id="guitarBody" x1="0%" y1="0%" x2="100%" y2="100%">
                        <stop offset="0%" stop-color="#ffaa55"/>
                        <stop offset="100%" stop-color="#e65c00"/>
                    </linearGradient>
                </defs>

                <!-- Soft Feet -->
                <ellipse cx="65" cy="195" rx="18" ry="10" fill="url(#beakGrad)" stroke="#4a2c1d" stroke-width="3.5"/>
                <ellipse cx="135" cy="195" rx="18" ry="10" fill="url(#beakGrad)" stroke="#4a2c1d" stroke-width="3.5"/>

                <!-- Cute Round Duck Body & Head -->
                <path d="M 50 135 C 30 70, 170 70, 150 135 C 150 188, 50 188, 50 135 Z" 
                      fill="url(#duckGrad)" stroke="#4a2c1d" stroke-width="4" stroke-linejoin="round"/>
                
                <path d="M 52 115 C 40 45, 160 45, 148 115" 
                      fill="url(#duckGrad)" stroke="#4a2c1d" stroke-width="4" stroke-linecap="round"/>

                <!-- Extra Cute Round Beak -->
                <path d="M 72 102 C 70 86, 130 86, 128 102 C 128 118, 72 118, 72 102 Z" 
                      fill="url(#beakGrad)" stroke="#4a2c1d" stroke-width="3.5" stroke-linejoin="round"/>

                <!-- Cute Big Sparkly Eyes -->
                <circle cx="76" cy="88" r="8.5" fill="#361e15"/>
                <circle cx="124" cy="88" r="8.5" fill="#361e15"/>
                <circle cx="73" cy="85" r="3.5" fill="#ffffff"/>
                <circle cx="121" cy="85" r="3.5" fill="#ffffff"/>
                <circle cx="78" cy="91" r="1.5" fill="#ffffff"/>
                <circle cx="126" cy="91" r="1.5" fill="#ffffff"/>

                <!-- Blush Hearts / Cheeks -->
                <ellipse cx="58" cy="105" rx="9" ry="6" fill="#ff77a8" opacity="0.85"/>
                <ellipse cx="142" cy="105" rx="9" ry="6" fill="#ff77a8" opacity="0.85"/>

                <!-- Guitar -->
                <g id="guitarGroup">
                    <rect x="95" y="118" width="60" height="7" rx="3" fill="#593111" stroke="#361e15" stroke-width="2" transform="rotate(-22 95 118)"/>
                    <path d="M 68 146 C 58 132, 78 122, 92 132 C 102 128, 112 138, 107 152 C 102 166, 82 166, 68 146 Z" 
                          fill="url(#guitarBody)" stroke="#361e15" stroke-width="3"/>
                    <circle cx="87" cy="144" r="5" fill="#361e15"/>
                </g>

                <!-- Wings Holding Guitar -->
                <path d="M 46 138 C 40 152, 68 160, 72 148 Z" fill="#ffeb99" stroke="#4a2c1d" stroke-width="3.5"/>
                <path d="M 154 138 C 160 152, 132 160, 128 148 Z" fill="#ffeb99" stroke="#4a2c1d" stroke-width="3.5"/>

                <!-- Small Floating Cute Sparkles -->
                <path d="M 40 40 L 43 47 L 50 50 L 43 53 L 40 60 L 37 53 L 30 50 L 37 47 Z" fill="#ffffff" opacity="0.85"/>
                <path d="M 160 40 L 163 47 L 170 50 L 163 53 L 160 60 L 157 53 L 150 50 L 157 47 Z" fill="#ffe680" opacity="0.9"/>
            </svg>
        </div>
    </div>

    <!-- GIFT BOX -->
    <div class="gift-container" id="giftBox">
        <div class="open-text">
            OPEN IT
            <div style="font-size:14px;">↓</div>
        </div>
        <svg viewBox="0 0 100 100" width="100%" height="100%" filter="drop-shadow(0 8px 15px rgba(0,0,0,0.4))">
            <rect x="15" y="40" width="70" height="50" rx="8" fill="#ff4d88" />
            <rect x="42" y="40" width="16" height="50" fill="#ffe66d" />

            <g id="giftLid">
                <rect x="10" y="26" width="80" height="16" rx="5" fill="#ff6699" />
                <rect x="42" y="26" width="16" height="16" fill="#ffe66d" />
                <path d="M 50 26 C 35 10, 20 24, 42 28 Z" fill="#ffe66d" />
                <path d="M 50 26 C 65 10, 80 24, 58 28 Z" fill="#ffe66d" />
                <circle cx="50" cy="26" r="4" fill="#ffd11a" />
            </g>
        </svg>
    </div>
</section>

<!-- 3. ENVELOPE MODAL WITH LETTER -->
<div id="envelope-modal">
    <div class="envelope-wrapper" id="envelopeWrapper">
        <div class="envelope-flap"></div>
        <div class="envelope-pocket"></div>
        
        <div class="letter-card">
            <div class="card-header-line"></div>
            <h2>Happy Birthday!</h2>
            <p>
                I hope you're always doing well and that life always brings you happiness.
                <br><br>
                <strong>Stay happy and keep smiling!</strong>
            </p>
        </div>
    </div>
</div>

<script>
const $ = id => document.getElementById(id);

/* =====================================================
   HEAVY MATRIX HEARTS RAIN
===================================================== */
const canvas = $("matrixCanvas");
const ctx = canvas.getContext("2d");

function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
resizeCanvas();
window.addEventListener("resize", resizeCanvas);

function drawHeart(ctx, x, y, size, color, alpha) {
    ctx.save();
    ctx.globalAlpha = alpha;
    ctx.beginPath();
    ctx.fillStyle = color;
    const topCurveHeight = size * 0.3;
    ctx.moveTo(x, y + topCurveHeight);
    ctx.bezierCurveTo(x, y, x - size / 2, y, x - size / 2, y + topCurveHeight);
    ctx.bezierCurveTo(x - size / 2, y + (size + topCurveHeight) / 2, x, y + size, x, y + size);
    ctx.bezierCurveTo(x, y + size, x + size / 2, y + (size + topCurveHeight) / 2, x + size / 2, y + topCurveHeight);
    ctx.bezierCurveTo(x + size / 2, y, x, y, x, y + topCurveHeight);
    ctx.closePath();
    ctx.fill();
    ctx.restore();
}

const columns = Math.floor(window.innerWidth / 14);
const drops = [];
for (let i = 0; i < columns; i++) {
    drops[i] = {
        x: i * 15,
        y: Math.random() * -800,
        speed: 4 + Math.random() * 6,
        length: 15 + Math.floor(Math.random() * 12)
    };
}

function renderMatrix() {
    ctx.fillStyle = "rgba(10, 3, 18, 0.22)";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    drops.forEach(drop => {
        for (let j = 0; j < drop.length; j++) {
            const hY = drop.y - (j * 16);
            if (hY > 0 && hY < canvas.height) {
                const alpha = 1 - (j / drop.length);
                const color = (j === 0) ? "#ffffff" : (j % 2 === 0 ? "#ff3385" : "#ff80bf");
                drawHeart(ctx, drop.x, hY, 11, color, alpha);
            }
        }
        drop.y += drop.speed;
        if (drop.y - (drop.length * 16) > canvas.height) {
            drop.y = Math.random() * -150;
            drop.speed = 4 + Math.random() * 6;
        }
    });

    requestAnimationFrame(renderMatrix);
}
renderMatrix();

/* =====================================================
   BACKGROUND STARS
===================================================== */
function generateStars() {
    const container = $("starsContainer");
    for (let i = 0; i < 50; i++) {
        const star = document.createElement("div");
        star.className = "star";
        const size = 4 + Math.random() * 6;
        star.style.width = size + "px";
        star.style.height = size + "px";
        star.style.left = Math.random() * 100 + "%";
        star.style.top = Math.random() * 80 + "%";
        star.style.setProperty("--dur", (1 + Math.random() * 2) + "s");
        container.appendChild(star);
    }
}
generateStars();

/* =====================================================
   SYNTHESIZED AUDIO
===================================================== */
function playMelody() {
    try {
        const AudioCtx = window.AudioContext || window.webkitAudioContext;
        if (!AudioCtx) return;
        const audioCtx = new AudioCtx();

        const notes = [
            { f: 264, d: 0.35 }, { f: 264, d: 0.35 }, { f: 297, d: 0.7 }, { f: 264, d: 0.7 }, { f: 352, d: 0.7 }, { f: 330, d: 1.2 },
            { f: 264, d: 0.35 }, { f: 264, d: 0.35 }, { f: 297, d: 0.7 }, { f: 264, d: 0.7 }, { f: 396, d: 0.7 }, { f: 352, d: 1.2 }
        ];

        let now = audioCtx.currentTime + 0.1;
        notes.forEach(note => {
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.type = "sine";
            osc.frequency.value = note.f;

            gain.gain.setValueAtTime(0, now);
            gain.gain.linearRampToValueAtTime(0.15, now + 0.04);
            gain.gain.exponentialRampToValueAtTime(0.001, now + note.d);

            osc.connect(gain);
            gain.connect(audioCtx.destination);

            osc.start(now);
            osc.stop(now + note.d);
            now += note.d + 0.08;
        });
    } catch(e) {}
}

/* =====================================================
   SCREEN CONTROLS & DUCK RUNNING LOGIC
===================================================== */
function switchScreen(fromId, toId) {
    const from = $(fromId);
    const to = $(toId);
    from.classList.add("fade-out");
    setTimeout(() => {
        from.classList.remove("active", "fade-out");
        to.classList.add("active");
    }, 600);
}

let count = 3;
const numEl = $("number");

const countTimer = setInterval(() => {
    count--;
    if (count > 0) {
        numEl.innerText = count;
        numEl.style.animation = "none";
        void numEl.offsetWidth;
        numEl.style.animation = "numPop 0.8s cubic-bezier(0.34, 1.56, 0.64, 1)";
    } else {
        clearInterval(countTimer);
        switchScreen("countdown-screen", "space-screen");
        playMelody();

        // Smooth Duck Running Animation
        setTimeout(() => {
            const duck = $("duckStage");
            duck.classList.add("run-to-gift");

            setTimeout(() => {
                duck.classList.remove("run-to-gift");
                $("giftBox").classList.add("show");
            }, 2200);
        }, 1200);
    }
}, 1200);

/* =====================================================
   GIFT & ENVELOPE INTERACTION
===================================================== */
$("giftBox").addEventListener("click", () => {
    const modal = $("envelope-modal");
    modal.classList.add("active");

    setTimeout(() => {
        $("envelopeWrapper").classList.add("open");
    }, 400);
});
</script>
</body>
</html>
