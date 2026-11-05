

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<title>Jumping Nemo - 202292022 문강빈</title>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    background: #e8e8e8;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    min-height: 100vh; font-family: sans-serif;
    overflow: hidden; user-select: none;
  }
  .game-wrapper { display: flex; flex-direction: column; align-items: center; gap: 8px; }
  canvas { display: block; border-radius: 8px; border: 2px solid #aaa; cursor: pointer; touch-action: none; }
  .hint { color: #666; font-size: 0.75rem; }
  .credit { color: #111; font-size: 0.82rem; font-weight: bold; margin-top: 2px; }
</style>
</head>
<body>
<div class="game-wrapper">
  <canvas id="gameCanvas"></canvas>
  <div class="hint">클릭 / 탭 = 점프 (2단 점프) &nbsp;|&nbsp; SPACE = 재시작</div>
  <div class="credit">[프로그래밍기초와실습 - 기말프로젝트] 전주대학교 인공지능학과 1학년 문강빈</div>
</div>

<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');
const BASE_W = 500, BASE_H = 300;
canvas.width = BASE_W; canvas.height = BASE_H;
const sc = Math.min(window.innerWidth / BASE_W, (window.innerHeight - 80) / BASE_H, 1.2);
canvas.style.width = Math.floor(BASE_W * sc) + 'px';
canvas.style.height = Math.floor(BASE_H * sc) + 'px';
const W = BASE_W, H = BASE_H, GROUND = H;

// ── 랭크별 시간대 테마 ──────────────────────────────────
const THEMES = [
  { rank:'E',   sky1:'#87ceeb', sky2:'#c9e8f5', ground:'#5a9e3a', groundStroke:'#3a7a1a',
    sunX:380, sunY:50, sunR:28, sunColor:'#fff176', isMoon:false, stars:false, label:'낮' },
  { rank:'D',   sky1:'#4fc3f7', sky2:'#81d4fa', ground:'#4a8e2a', groundStroke:'#2a6a0a',
    sunX:250, sunY:38, sunR:34, sunColor:'#ffee58', isMoon:false, stars:false, label:'점심' },
  { rank:'C',   sky1:'#ff7043', sky2:'#ffb74d', ground:'#6d4c41', groundStroke:'#4e342e',
    sunX:420, sunY:180, sunR:38, sunColor:'#ff8a65', isMoon:false, stars:false, label:'해질녘' },
  { rank:'B',   sky1:'#283593', sky2:'#1a237e', ground:'#263238', groundStroke:'#90a4ae',
    sunX:380, sunY:55, sunR:22, sunColor:'#e8eaf6', isMoon:true, stars:true, label:'밤' },
  { rank:'A',   sky1:'#0d0d1a', sky2:'#1a1a2e', ground:'#1c1c1c', groundStroke:'#78909c',
    sunX:350, sunY:60, sunR:20, sunColor:'#cfd8dc', isMoon:true, stars:true, label:'늦은 밤' },
  { rank:'A+',  sky1:'#0a0a0f', sky2:'#12102a', ground:'#111', groundStroke:'#546e7a',
    sunX:100, sunY:80, sunR:18, sunColor:'#b0bec5', isMoon:true, stars:true, label:'새벽' },
  { rank:'S',   sky1:'#ff9a9e', sky2:'#fecfef', ground:'#5c6bc0', groundStroke:'#3949ab',
    sunX:80, sunY:120, sunR:30, sunColor:'#ffcc80', isMoon:false, stars:false, label:'이른 아침' },
  { rank:'SS',  sky1:'#ffecd2', sky2:'#fcb69f', ground:'#8d6e63', groundStroke:'#5d4037',
    sunX:60, sunY:90, sunR:35, sunColor:'#ffb74d', isMoon:false, stars:false, label:'새벽빛' },
  { rank:'SSS', sky1:'#fff176', sky2:'#ffcc02', ground:'#a5d6a7', groundStroke:'#388e3c',
    sunX:250, sunY:30, sunR:45, sunColor:'#ffd600', isMoon:false, stars:false, label:'황금빛 아침' },
];

function getRankIdx(score) {
  if (score <= 15)  return 0;
  if (score <= 30) return 1;
  if (score <= 45) return 2;
  if (score <= 75) return 3;
  if (score <= 105) return 4;
  if (score <= 120) return 5;
  if (score <= 150) return 6;
  if (score <= 180) return 7;
  return 8;
}
function getObsVel(score) {
  if (score <= 15)  return 4;
  if (score <= 30) return 5;
  if (score <= 45) return 7;
  if (score <= 72) return 10;
  if (score <= 75) return 9;
  if (score <= 105) return 6;
  if (score <= 120) return 9;
  if (score <= 150) return 11;
  if (score <= 180) return 13;
  return 15;
}

// ── 별 ─────────────────────────────────────────────────
const stars = Array.from({length:40}, () => ({
  x: Math.random()*W, y: Math.random()*H*0.75,
  r: Math.random()*1.2+0.3, phase: Math.random()*Math.PI*2
}));
const clouds = [
  {x:60,  y:40, w:80, h:22},
  {x:220, y:28, w:100,h:26},
  {x:380, y:50, w:70, h:18},
];

// ── 테마 전환 ───────────────────────────────────────────
let prevThemeIdx = 0, curThemeIdx = 0, themeAlpha = 0, themeTransiting = false;

function drawTheme(t, alpha, tick) {
  ctx.globalAlpha = alpha;
  const grad = ctx.createLinearGradient(0, 0, 0, H);
  grad.addColorStop(0, t.sky1);
  grad.addColorStop(1, t.sky2);
  ctx.fillStyle = grad;
  ctx.fillRect(0, 0, W, H);

  if (t.stars) {
    ctx.fillStyle = '#ffffff';
    stars.forEach(s => {
      ctx.globalAlpha = alpha * 0.6;
      ctx.beginPath();
      ctx.arc(s.x, s.y, s.r, 0, Math.PI*2);
      ctx.fill();
    });
    ctx.globalAlpha = alpha;
  }

  // 태양/달
  ctx.fillStyle = t.sunColor;
  ctx.beginPath();
  ctx.arc(t.sunX, t.sunY, t.sunR, 0, Math.PI*2);
  ctx.fill();
  if (t.isMoon) {
    ctx.fillStyle = t.sky1;
    ctx.beginPath();
    ctx.arc(t.sunX + t.sunR*0.35, t.sunY - t.sunR*0.2, t.sunR*0.75, 0, Math.PI*2);
    ctx.fill();
  }

  // 구름
  if (!t.stars) {
    ctx.fillStyle = 'rgba(255,255,255,0.6)';
    clouds.forEach((c, i) => {
      const cx = ((c.x + tick * (0.1 + i*0.04)) % (W + 120)) - 60;
      ctx.beginPath();
      ctx.arc(cx, c.y, c.h/2, 0, Math.PI*2);
      ctx.arc(cx + c.w*0.3, c.y - c.h*0.25, c.h*0.4, 0, Math.PI*2);
      ctx.arc(cx - c.w*0.2, c.y - c.h*0.1, c.h*0.35, 0, Math.PI*2);
      ctx.fill();
    });
  }

  // 땅
  ctx.fillStyle = t.ground;
  ctx.fillRect(0, GROUND-4, W, 4);
  ctx.strokeStyle = t.groundStroke;
  ctx.lineWidth = 2;
  ctx.beginPath();
  ctx.moveTo(0, GROUND); ctx.lineTo(W, GROUND);
  ctx.stroke();

  ctx.globalAlpha = 1;
}

function drawBackground(tick) {
  if (themeTransiting) {
    drawTheme(THEMES[prevThemeIdx], 1, tick);
    drawTheme(THEMES[curThemeIdx], 1 - themeAlpha, tick);
    themeAlpha -= 0.025;
    if (themeAlpha <= 0) { themeAlpha = 0; themeTransiting = false; }
  } else {
    drawTheme(THEMES[curThemeIdx], 1, tick);
  }
}

// ── Nemo ────────────────────────────────────────────────
const nemo = {
  x:60, y:GROUND-20, w:20, h:20,
  vel:0, jumpCnt:0, clicked:false,
  reset() { this.y=GROUND-this.h; this.vel=0; this.jumpCnt=0; this.clicked=false; },
  tryJump() {
    if (!this.clicked) {
      this.clicked = true;
      const maxJump = tripleJump > 0 ? 3 : 2;
      if (this.jumpCnt < maxJump) { this.vel = -15; this.jumpCnt++; }
    }
  },
  releaseJump() { this.clicked = false; },
  update() {
    this.vel += 1;
    if (this.vel > 10) this.vel = 10;
    this.y += this.vel;
    if (this.y >= GROUND - this.h) { this.y = GROUND-this.h; this.jumpCnt=0; }
  },
  draw() {
    const blink = (n) => Math.floor(n/6) % 2 === 0;
    if (invincible > 0 && blink(invincible)) ctx.fillStyle = '#00cfff';
    else if (doubleScore > 0 && blink(doubleScore)) ctx.fillStyle = '#ff4444';
    else if (tripleJump > 0 && blink(tripleJump)) ctx.fillStyle = '#44ff88';
    else ctx.fillStyle = '#ff0000';
    ctx.fillRect(this.x, this.y, this.w, this.h);
  },
  collides(o) {
    const p = 2;
    return !(this.x+this.w-p < o.x || this.x+p > o.x+o.w ||
             this.y+this.h-p < o.y || this.y+p > o.y+o.h);
  }
};

// ── 장애물 ───────────────────────────────────────────────
let obstacles = [];
function spawnObstacle() {
  const h = 25 + Math.floor(Math.random()*46);
  const r = Math.floor(Math.random()*256);
  const g = Math.floor(Math.random()*256);
  const b = Math.floor(Math.random()*256);
  obstacles.push({
    x: W, y: GROUND-h, w: 20, h,
    vel: getObsVel(score),
    color: `rgb(${r},${g},${b})`,
    update() { this.x -= this.vel; },
    draw() {
      ctx.fillStyle = this.color;
      ctx.beginPath();
      ctx.moveTo(this.x + this.w/2, this.y);
      ctx.lineTo(this.x, this.y + this.h);
      ctx.lineTo(this.x + this.w, this.y + this.h);
      ctx.closePath();
      ctx.fill();
    }
  });
}

// ── 코인 ─────────────────────────────────────────────────
let coins = [];
let coinCombo = 0;
let particles = [];

function spawnCoin() {
  const floatY = GROUND - 40 - Math.floor(Math.random() * 80);
  coins.push({
    x: W, y: floatY, r: 7,
    vel: getObsVel(score),
    angle: 0,
    update() { this.x -= this.vel; this.angle += 0.08; },
    draw() {
      ctx.save();
      ctx.translate(this.x, this.y);
      ctx.rotate(this.angle);
      ctx.fillStyle = '#ffd700';
      ctx.strokeStyle = '#ffa500';
      ctx.lineWidth = 2;
      ctx.beginPath();
      ctx.arc(0, 0, this.r, 0, Math.PI*2);
      ctx.fill();
      ctx.stroke();
      ctx.fillStyle = '#fff8dc';
      ctx.font = 'bold 7px sans-serif';
      ctx.textAlign = 'center';
      ctx.fillText('C', 0, 2.5);
      ctx.restore();
    },
    collides() {
      const dx = this.x - (nemo.x + nemo.w/2);
      const dy = this.y - (nemo.y + nemo.h/2);
      return Math.sqrt(dx*dx + dy*dy) < this.r + 10;
    }
  });
}

function spawnParticles(x, y, combo) {
  const color = combo ? '#ff4444' : '#ffd700';
  for (let i = 0; i < (combo ? 20 : 8); i++) {
    const angle = (Math.PI * 2 / (combo ? 20 : 8)) * i;
    const spd = combo ? 3 + Math.random()*3 : 1.5 + Math.random()*2;
    particles.push({
      x, y,
      vx: Math.cos(angle) * spd,
      vy: Math.sin(angle) * spd,
      life: combo ? 50 : 30,
      maxLife: combo ? 50 : 30,
      color,
      r: combo ? 4 : 2.5
    });
  }
}

function updateParticles() {
  particles = particles.filter(p => p.life > 0);
  particles.forEach(p => {
    p.x += p.vx; p.y += p.vy;
    p.vy += 0.1;
    p.life--;
    ctx.globalAlpha = p.life / p.maxLife;
    ctx.fillStyle = p.color;
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.r, 0, Math.PI*2);
    ctx.fill();
  });
  ctx.globalAlpha = 1;
}

// 콤보 텍스트
let comboText = { msg:'', timer:0, x:0, y:0 };
function drawComboText() {
  if (comboText.timer <= 0) return;
  ctx.globalAlpha = Math.min(1, comboText.timer / 20);
  ctx.font = 'bold 20px Gothic, sans-serif';
  ctx.fillStyle = '#ff4444';
  ctx.textAlign = 'center';
  ctx.fillText(comboText.msg, comboText.x, comboText.y - (30 - comboText.timer));
  ctx.textAlign = 'left';
  ctx.globalAlpha = 1;
  comboText.timer--;
}

// ── HUD ─────────────────────────────────────────────────
const RANK_COLORS = ['#999','#00ff33','#00ffff','#ff9966','#ff6666','#ff0099','#ffff66','#ffff99','#ffffcc'];
function drawHUD() {
  const ri = getRankIdx(score);
  ctx.font = 'bold 28px Gothic, sans-serif';
  ctx.fillStyle = '#ff3333';
  ctx.fillText(`Score : ${score}`, 8, 34);
  ctx.fillStyle = RANK_COLORS[ri];
  ctx.fillText(`Rank : ${THEMES[ri].rank}`, 330, 34);
  // 코인 콤보
  ctx.font = 'bold 15px Gothic, sans-serif';
  if (invincible > 0) {
    ctx.fillStyle = '#00cfff';
    ctx.fillText(`무적 ${Math.ceil(invincible/60)}초`, 8, 56);
  } else if (doubleScore > 0) {
    ctx.fillStyle = '#ff4444';
    ctx.fillText(`2배 ${Math.ceil(doubleScore/60)}초`, 8, 56);
  } else if (tripleJump > 0) {
    ctx.fillStyle = '#44ff88';
    ctx.fillText(`3단점프 ${Math.ceil(tripleJump/60)}초`, 8, 56);
  } else if (coinCombo > 0) {
    ctx.fillStyle = '#ffd700';
    ctx.fillText(`Coin x${coinCombo}`, 8, 56);
  }
}

// ── 랭크업 알림 제거됨 ──────────────────────────────────
function drawEffectBanner() {
  let label = '', color = '', seconds = 0;
  if (invincible > 0)       { label = '무적 !';     color = '#00cfff'; seconds = Math.ceil(invincible/60); }
  else if (doubleScore > 0) { label = '점수 2배 !!'; color = '#ff4444'; seconds = Math.ceil(doubleScore/60); }
  else if (tripleJump > 0)  { label = '점프 3회 !'; color = '#44ff88'; seconds = Math.ceil(tripleJump/60); }
  else return;

  ctx.textAlign = 'center';
  ctx.font = 'bold 24px Gothic, sans-serif';
  ctx.fillStyle = color;
  ctx.fillText(`${label}  ${seconds}초`, W/2, H/2);
  ctx.textAlign = 'left';
}

function drawRankUp() {}

// ── Game Over ────────────────────────────────────────────
function drawGameOver() {
  ctx.fillStyle = 'rgba(0,0,0,0.5)';
  ctx.fillRect(0,0,W,H);
  ctx.font = 'bold 60px Gothic, sans-serif';
  ctx.fillStyle = '#00ffff';
  ctx.textAlign = 'center';
  ctx.fillText('Game Over', W/2, H/3);
  ctx.font = 'bold 24px Gothic, sans-serif';
  ctx.fillStyle = '#ccccff';
  ctx.fillText(`Score : ${score}  |  Rank : ${THEMES[getRankIdx(score)].rank}`, W/2, H/2);
  ctx.font = '18px Gothic, sans-serif';
  ctx.fillStyle = '#aaaacc';
  ctx.fillText('클릭 / SPACE = 다시 시작', W/2, H*0.72);
  ctx.textAlign = 'left';
}

// ── 상태 ────────────────────────────────────────────────
let invincible = 0;
let doubleScore = 0;
let tripleJump = 0;
let score = 0, gameOver = false, tTick = -1, lastRankIdx = 0;
let nextSpawn = randSpawn();
function randSpawn() { return 25 + Math.floor(Math.random()*36); }

function restartGame() {
  score = 0; gameOver = false; tTick = -1;
  obstacles = []; coins = []; particles = []; coinCombo = 0;
  invincible = 0; doubleScore = 0; tripleJump = 0; nemo.reset();
  nextSpawn = randSpawn();
  lastRankIdx = 0; curThemeIdx = 0; prevThemeIdx = 0;
  themeAlpha = 0; themeTransiting = false;
}

// ── 입력 ────────────────────────────────────────────────
function onPress() { if (gameOver) { restartGame(); return; } nemo.tryJump(); }
function onRelease() { nemo.releaseJump(); }
canvas.addEventListener('mousedown', onPress);
canvas.addEventListener('mouseup', onRelease);
canvas.addEventListener('touchstart', e => { e.preventDefault(); onPress(); }, {passive:false});
canvas.addEventListener('touchend',   e => { e.preventDefault(); onRelease(); }, {passive:false});
document.addEventListener('keydown', e => { if (e.code==='Space') { e.preventDefault(); onPress(); } });
document.addEventListener('keyup',   e => { if (e.code==='Space') onRelease(); });

// ── 메인 루프 ────────────────────────────────────────────
let lastTs = 0;
function loop(ts) {
  requestAnimationFrame(loop);
  if (ts - lastTs < 1000/60) return;
  lastTs = ts;
  tTick++;

  drawBackground(tTick);

  if (gameOver) {
    nemo.draw();
    obstacles.forEach(o => o.draw());
    drawHUD();
    drawGameOver();
    return;
  }

  // 원본 코드 그대로: t_tick % random.randint(25,60) == 0
  if (tTick % nextSpawn === 0) {
    tTick = 0;
    nextSpawn = randSpawn();
    spawnObstacle();
    // 50% 확률로 코인 스폰
    if (Math.random() < 0.5) spawnCoin();
  }

  if (invincible > 0) invincible--;
  if (doubleScore > 0) doubleScore--;
  if (tripleJump > 0) tripleJump--;
  nemo.update();
  obstacles.forEach(o => o.update());
  coins.forEach(c => c.update());

  // 장애물 충돌
  if (invincible === 0) {
    for (const o of obstacles) {
      if (nemo.collides(o)) { gameOver = true; break; }
    }
  }

  // 코인 충돌
  coins = coins.filter(c => {
    if (c.collides()) {
      coinCombo++;
      if (coinCombo >= 3) {
        score += 3;
        const roll = Math.floor(Math.random() * 3);
        let effectMsg = '';
        if (roll === 0) { invincible = 120; effectMsg = '무적 2초!'; }
        else if (roll === 1) { doubleScore = 180; effectMsg = '점수 2배 3초!'; }
        else { tripleJump = 180; effectMsg = '3단점프 3초!'; }
        spawnParticles(nemo.x + nemo.w/2, nemo.y, true);
        comboText = { msg: '3 COMBO! +3점', timer: 60, x: nemo.x + nemo.w/2, y: nemo.y - 10 };
        coinCombo = 0;
      } else {
        spawnParticles(c.x, c.y, false);
        comboText = { msg: `Coin x${coinCombo}`, timer: 25, x: c.x, y: c.y - 5 };
      }
      return false;
    }
    if (c.x + c.r < 0) { coinCombo = 0; return false; }
    return true;
  });

  // 점수 & 장애물 제거
  obstacles = obstacles.filter(o => {
    if (o.x + o.w < 0) { score += doubleScore > 0 ? 2 : 1; return false; }
    return true;
  });

  // 랭크 체크 — 1등급마다 테마 변경 (전환 느리게)
  const newRankIdx = getRankIdx(score);
  if (newRankIdx !== lastRankIdx) {
    prevThemeIdx = curThemeIdx;
    curThemeIdx = newRankIdx;
    themeAlpha = 1;
    themeTransiting = true;
    lastRankIdx = newRankIdx;
  }

  obstacles.forEach(o => o.draw());
  coins.forEach(c => c.draw());
  updateParticles();
  nemo.draw();
  drawHUD();
  drawComboText();
  drawEffectBanner();
  drawRankUp();
}
requestAnimationFrame(loop);
</script>
</body>
</html>
