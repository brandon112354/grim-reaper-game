<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no" />
<title>Grim Reaper — Mobile Harvest of Souls</title>
<style>
html,body{margin:0;padding:0;height:100%;overflow:hidden;font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial;background:#05050a;color:#eafaf5;}
canvas{display:block;width:100%;height:100%;}
#ui{position:absolute;top:6px;left:6px;font-weight:700;text-shadow:0 1px 0 #000;}
#controls{position:absolute;bottom:12px;width:100%;display:flex;justify-content:space-between;align-items:flex-end;padding:0 8px;pointer-events:none;}
.joystick{width:140px;height:140px;border-radius:50%;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.08);backdrop-filter:blur(8px);pointer-events:auto;position:relative;}
.stick{width:70px;height:70px;border-radius:50%;background:rgba(255,255,255,0.15);position:absolute;left:35px;top:35px;pointer-events:none;transition:0.05s;}
.right{display:flex;gap:12px;align-items:center;pointer-events:auto;flex-wrap:wrap;max-width:55%;justify-content:flex-end;}
.btn{width:80px;height:80px;border-radius:16px;background:linear-gradient(180deg,#222,#0f0f0f);border:2px solid #333;display:flex;align-items:center;justify-content:center;font-size:20px;color:#fff;}
#centerMsg{position:absolute;width:100%;text-align:center;top:28%;pointer-events:none;font-size:1.2rem;}
</style>
</head>
<body>
<canvas id="game" width="1280" height="720"></canvas>
<div id="ui">HP: <span id="hp">100</span> &nbsp; Souls: <span id="money">0</span> &nbsp; Level: <span id="lvl">1</span></div>
<div id="centerMsg"></div>
<div id="controls">
<div class="joystick" id="joystick"><div class="stick" id="stick"></div></div>
<div class="right">
<div class="btn" id="swap">Swap</div>
<div class="btn" id="s1">1</div>
<div class="btn" id="s2">2</div>
<div class="btn" id="s3">3</div>
<div class="btn" id="restart">↻</div>
</div>
</div>
<script>
const canvas=document.getElementById('game');const ctx=canvas.getContext('2d');let W=canvas.width,H=canvas.height;
function resize(){canvas.style.width=window.innerWidth+'px';canvas.style.height=window.innerHeight+'px';}
window.addEventListener('resize',resize);resize();
const joystickEl=document.getElementById('joystick'),stickEl=document.getElementById('stick');
let joystick={dx:0,dy:0,active:false};
function joystickLocal(t){const rect=joystickEl.getBoundingClientRect();const cx=rect.left+rect.width/2,cy=rect.top+rect.height/2;let dx=t.clientX-cx,dy=t.clientY-cy;const max=rect.width/2-12;const d=Math.hypot(dx,dy);if(d>max){dx=dx/d*max;dy=dy/d*max;}stickEl.style.left=(rect.width/2-stickEl.offsetWidth/2+dx)+'px';stickEl.style.top=(rect.height/2-stickEl.offsetHeight/2+dy)+'px';joystick.dx=dx/max;joystick.dy=dy/max;}
joystickEl.addEventListener('touchstart',e=>{joystick.active=true;joystickLocal(e.touches[0]);});
joystickEl.addEventListener('touchmove',e=>{e.preventDefault();if(!joystick.active)return;joystickLocal(e.touches[0]);});
joystickEl.addEventListener('touchend',e=>{joystick.active=false;joystick.dx=0;joystick.dy=0;stickEl.style.left='';stickEl.style.top='';});
function loop(){ctx.fillStyle='#05050a';ctx.fillRect(0,0,W,H);ctx.fillStyle='#0f0';ctx.fillRect(W/2-16,H/2-16,32,32);requestAnimationFrame(loop);}
loop();
</script>
</body>
</html>
