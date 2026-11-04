# Selfe-Hackathon
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Mine Safety &amp; Rescue Rover</title>
<style>
:root{--bg:#07121f;--side:#091729;--card:#0d1f35;--line:#1a3350;--ink:#e8f0f8;--mut:#8aa0b8;--blue:#1f7bff;--green:#19c37d;--red:#ef4444;--amber:#f5b73b;--vio:#8b5cf6}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:14px/1.4 "Segoe UI",system-ui,sans-serif}
.app{display:grid;grid-template-columns:200px 1fr;min-height:100vh}
aside{background:var(--side);border-right:1px solid var(--line);padding:12px 10px}
.nav{all:unset;box-sizing:border-box;display:block;width:100%;padding:11px 14px;margin-bottom:4px;border-radius:6px;color:var(--mut);cursor:pointer}
.nav.on{background:var(--blue);color:#fff}.nav:focus-visible{outline:2px solid #fff}
main{padding:0 16px 20px;min-width:0}
header{display:flex;flex-wrap:wrap;gap:14px;align-items:center;justify-content:space-between;padding:12px 0;border-bottom:1px solid var(--line);margin-bottom:14px}
h1{font-size:21px;margin:0}.tag{color:var(--mut);font-size:13px}
.hs{display:flex;gap:22px;align-items:center;font-size:13px;flex-wrap:wrap}.hs small{display:block;color:var(--mut)}
.dot{display:inline-block;width:9px;height:9px;border-radius:50%;background:var(--green);margin-right:7px}.dot.bad{background:var(--red)}.dot.warn{background:var(--amber)}
.row{display:grid;gap:12px;margin-bottom:12px}
.r1{grid-template-columns:repeat(4,1fr)}.r2{grid-template-columns:1fr 1.2fr}.r3{grid-template-columns:1fr 1fr 1fr}.r4{grid-template-columns:2fr 1fr}
.card{background:var(--card);border:1px solid var(--line);border-radius:8px;padding:14px;min-width:0}
.card h2{font-size:16px;margin:0 0 10px;font-weight:600;display:flex;justify-content:space-between;align-items:center}
.st .l{color:var(--mut);font-size:13px}.st .v{font-size:27px;font-weight:600;font-variant-numeric:tabular-nums}.st .v small{font-size:14px;color:var(--mut);font-weight:400}
.pg{height:6px;background:#12304d;border-radius:3px;margin-top:8px;overflow:hidden}.pg i{display:block;height:100%;width:0;background:var(--green);transition:width .6s,background .3s}
.ok{color:var(--green)}.wn{color:var(--amber)}.dg{color:var(--red)}
.live{font-size:12px;color:var(--green);font-weight:400}
canvas.v{width:100%;aspect-ratio:16/9;border-radius:6px;display:block;background:#000}
svg{width:100%;display:block;border-radius:6px;background:#0a1626}
.btn{font:inherit;color:var(--ink);background:#102842;border:1px solid var(--line);border-radius:6px;padding:9px 12px;cursor:pointer}
.btn:hover{border-color:var(--blue)}.btn:focus-visible{outline:2px solid #fff}.btn.on{background:var(--blue);border-color:var(--blue)}
.btn.stop{color:#ff9a9a;border-color:#6b2631;background:#2a1220;width:100%}
.modes{display:grid;grid-template-columns:1fr 1fr;margin-bottom:12px}.modes .btn{border-radius:0}
.pad{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.pad .btn{text-align:center}
ul{list-style:none;margin:0;padding:0}
.ss li{display:flex;justify-content:space-between;padding:7px 0;border-bottom:1px solid var(--line);font-size:13px}
.al{max-height:250px;overflow:auto}.al li{padding:8px 0 8px 12px;border-bottom:1px solid var(--line);border-left:3px solid var(--blue);margin-bottom:4px;font-size:13px}
.al li.dg{border-left-color:var(--red)}.al li.wn{border-left-color:var(--amber)}.al small{display:block;color:var(--mut)}
.gr{display:grid;grid-template-columns:repeat(4,1fr);gap:10px}.gr b{font-size:12px;font-weight:500}
.gr canvas{width:100%;height:110px;display:block}
.rg .btn{padding:3px 9px;font-size:12px;border-radius:4px}.rg{display:flex;gap:4px}
.info{display:grid;grid-template-columns:1fr 1fr;gap:6px 14px;font-size:13px}.info span{color:var(--mut)}
.pill{display:inline-block;border:1px solid #6b2631;color:#ff9a9a;border-radius:5px;padding:2px 9px;font-size:12px;margin-bottom:10px}
code{background:#12304d;padding:1px 5px;border-radius:4px}
@media(max-width:980px){.app{grid-template-columns:1fr}aside{display:none}.r1{grid-template-columns:1fr 1fr}.r2,.r3,.r4{grid-template-columns:1fr}}
@media(max-width:560px){.r1{grid-template-columns:1fr}.gr{grid-template-columns:1fr 1fr}}
</style>
</head>
<body>
<div class="app">
<aside>
  <div style="font-weight:700;padding:8px 14px 16px">⛑ Rescue Rover</div>
  <button class="nav on">🏠 Dashboard</button><button class="nav">📹 Live video</button><button class="nav">🧊 3D mine view</button><button class="nav">📈 Sensor data</button><button class="nav">🕹 Rover control</button><button class="nav">🔔 Alerts &amp; logs</button><button class="nav">⚙ Settings</button>
</aside>
<main>
<header>
  <div><h1>Mine Safety &amp; Rescue Rover</h1><div class="tag">Safer mines · Smarter rescue</div></div>
  <div class="hs">
    <div><span class="dot" id="cdot"></span><b id="ctxt">Rover online</b><small id="cmode">Simulation mode</small></div>
    <div><b id="ipt">192.168.4.1</b><small>Wi-Fi</small></div>
    <div><b id="bat">78%</b><small>Battery</small></div>
    <div><b id="clk">--</b><small id="dte"></small></div>
  </div>
</header>

<section class="row r1">
  <div class="card st"><div class="l">Gas level (MQ-2)</div><div class="v"><span id="gas">–</span> <small>ppm</small></div><div id="gasS" class="ok">Normal</div><div class="pg"><i id="gasB"></i></div></div>
  <div class="card st"><div class="l">Humidity (DHT11)</div><div class="v"><span id="hum">–</span> <small>%</small></div><div id="humS" class="ok">Normal</div><div class="pg"><i id="humB" style="background:var(--blue)"></i></div></div>
  <div class="card st"><div class="l">Tilt (MPU6050)</div><div class="v"><span id="tilt">–</span><small>°</small></div><div id="tiltS" class="ok">Stable</div><div class="pg"><i id="tiltB" style="background:var(--vio)"></i></div></div>
  <div class="card st"><div class="l">Environment</div><div class="v" id="env">Good</div><div id="envS" class="ok">Air quality: Normal</div><div class="pg"><i id="envB"></i></div></div>
</section>

<section class="row r2">
  <div class="card"><h2>Live video <span class="live">● Simulated feed</span></h2><canvas class="v" id="vid" width="640" height="360"></canvas></div>
  <div class="card"><h2>3D mine visualization</h2>
    <svg viewBox="0 0 400 225" id="map" role="img" aria-label="Mine map with rover position, hazard, worker and water markers">
      <g fill="none" stroke="#2a4a6e" stroke-width="22" stroke-linecap="round" stroke-linejoin="round" opacity=".55"><path id="path" d="M40 190 L130 150 L210 170 L290 110 L360 130"/><path d="M130 150 L110 80 L170 40"/><path d="M290 110 L320 50"/></g>
      <g fill="none" stroke="#3f6a99" stroke-width="2" stroke-dasharray="5 5"><path d="M40 190 L130 150 L210 170 L290 110 L360 130"/></g>
      <g font-size="10" fill="#fff"><circle cx="170" cy="40" r="11" fill="#ef4444"/><text x="165" y="44">!</text><text x="186" y="44" fill="#ff9a9a">Hazard (gas)</text>
      <circle cx="320" cy="50" r="11" fill="#19c37d"/><text x="316" y="54">W</text><text x="258" y="30" fill="#7cf0b8">Worker detected</text>
      <circle cx="210" cy="170" r="11" fill="#1f7bff"/><text x="206" y="174">~</text><text x="225" y="196" fill="#8cc0ff">Water (flood risk)</text></g>
      <circle id="rv" r="8" fill="#f5b73b" stroke="#fff" stroke-width="2" cx="40" cy="190"/>
    </svg>
  </div>
</section>

<section class="row r3">
  <div class="card"><h2>Rover control</h2>
    <div class="modes"><button class="btn on" id="mMan">Manual mode</button><button class="btn" id="mAuto">Auto mode</button></div>
    <div class="pad">
      <span></span><button class="btn" data-c="Forward">▲ Forward</button><span></span>
      <button class="btn" data-c="Left">◀ Left</button><button class="btn" data-c="Backward">▼ Backward</button><button class="btn" data-c="Right">Right ▶</button>
    </div>
    <div style="margin-top:8px"><button class="btn stop" data-c="Stop">■ Stop</button></div>
    <div class="tag" style="margin-top:8px">Arrow keys and space also work in manual mode.</div>
  </div>
  <div class="card"><h2>System status</h2><ul class="ss" id="sys"></ul></div>
  <div class="card"><h2>Alerts &amp; logs <button class="btn" id="test" style="padding:3px 9px;font-size:12px">Simulate gas leak</button></h2><ul class="al" id="log"></ul></div>
</section>

<section class="row r4">
  <div class="card"><h2>Sensor graphs <span class="rg" id="rg"><button class="btn on" data-n="30">1H</button><button class="btn" data-n="60">6H</button><button class="btn" data-n="90">12H</button><button class="btn" data-n="120">24H</button></span></h2>
    <div class="gr"><div><b style="color:var(--green)">Gas (ppm)</b><canvas id="g0"></canvas></div><div><b style="color:var(--blue)">Humidity (%)</b><canvas id="g1"></canvas></div><div><b style="color:var(--vio)">Tilt (°)</b><canvas id="g2"></canvas></div><div><b style="color:var(--amber)">Battery (%)</b><canvas id="g3"></canvas></div></div>
  </div>
  <div class="card"><span class="pill">Rover ID: MR-001</span>
    <div class="info"><span>Mode</span><b id="iMode">Manual</b><span>Speed</span><b id="iSpd">0.0 m/s</b><span>Location</span><b id="iLoc">Tunnel B · 12 m</b><span>Mission</span><b>Rescue</b><span>Last command</span><b id="iCmd">–</b></div>
    <p class="tag" style="margin-top:12px">Data is simulated. To use the real rover, set <code>CONFIG.live = true</code> and the ESP32 address in the script.</p>
  </div>
</section>
</main>
</div>

<script>
// ===== Settings: switch to the real ESP32 when hardware is ready =====
const CONFIG={live:false,baseUrl:"http://192.168.4.1",pollMs:2000,gasWarn:200,gasDanger:300};
// Live mode: GET {baseUrl}/data -> {"gas":187,"humidity":62,"tilt":2.4,"battery":78}
//            GET {baseUrl}/cmd?d=Forward   (Forward, Backward, Left, Right, Stop, Auto, Manual)
const $=id=>document.getElementById(id),pad=n=>String(n).padStart(2,"0");
const S={gas:[],hum:[],tilt:[],bat:[]},MAX=120;let rangeN=30,auto=false,moving=false,speed=0,leak=0,online=true;
const sensors=[["Rover motors","Running"],["Camera","Streaming"],["Gas sensor (MQ-2)","Normal"],["DHT11 (humidity)","Normal"],["MPU6050 (tilt)","Stable"],["L298N driver","Connected"],["ESP32-WROOM","Online"],["Battery","78%"]];
$("sys").innerHTML=sensors.map((s,i)=>`<li><span><i class="dot" id="sd${i}"></i>${s[0]}</span><span class="ok" id="sv${i}">${s[1]}</span></li>`).join("");

function log(t,sub,cls){const li=document.createElement("li");li.className=cls||"";const d=new Date();li.innerHTML=`<b>${t}</b><small>${pad(d.getDate())}/${pad(d.getMonth()+1)} ${pad(d.getHours())}:${pad(d.getMinutes())}:${pad(d.getSeconds())}${sub?" · "+sub:""}</small>`;$("log").prepend(li);while($("log").children.length>30)$("log").lastChild.remove()}
log("Rover connected","Simulation mode");

function setState(id,txt,cls){const e=$(id);e.textContent=txt;e.className=cls}
function update(r){
  const push=(a,v)=>{a.push(v);if(a.length>MAX)a.shift()};
  push(S.gas,r.gas);push(S.hum,r.humidity);push(S.tilt,r.tilt);push(S.bat,r.battery);
  $("gas").textContent=Math.round(r.gas);$("hum").textContent=Math.round(r.humidity);$("tilt").textContent=r.tilt.toFixed(1);$("bat").textContent=Math.round(r.battery)+"%";
  const gc=r.gas>=CONFIG.gasDanger?"dg":r.gas>=CONFIG.gasWarn?"wn":"ok",gt={ok:"Normal",wn:"Elevated",dg:"Danger"}[gc];
  setState("gasS",gt,gc);$("gasB").style.width=Math.min(100,r.gas/4)+"%";$("gasB").style.background=gc==="ok"?"var(--green)":gc==="wn"?"var(--amber)":"var(--red)";
  setState("humS",r.humidity>85?"High":"Normal",r.humidity>85?"wn":"ok");$("humB").style.width=r.humidity+"%";
  const tc=Math.abs(r.tilt)>15?"dg":Math.abs(r.tilt)>8?"wn":"ok";setState("tiltS",tc==="ok"?"Stable":tc==="wn"?"Leaning":"Tipping risk",tc);$("tiltB").style.width=Math.min(100,Math.abs(r.tilt)*5+10)+"%";
  const ec=gc==="dg"||tc==="dg"?"dg":gc==="wn"||tc==="wn"?"wn":"ok";$("env").textContent={ok:"Good",wn:"Caution",dg:"Unsafe"}[ec];setState("envS","Air quality: "+gt,ec);$("envB").style.width=ec==="ok"?"80%":ec==="wn"?"50%":"20%";$("envB").style.background=ec==="ok"?"var(--green)":ec==="wn"?"var(--amber)":"var(--red)";
  const sv=[moving?"Running":"Idle","Streaming",gt,"Normal",tc==="ok"?"Stable":"Check","Connected","Online",Math.round(r.battery)+"%"],sc=[ok2(moving||1),"ok",gc,"ok",tc,"ok","ok",r.battery<20?"dg":r.battery<40?"wn":"ok"];
  sv.forEach((v,i)=>{setState("sv"+i,v,sc[i]);$("sd"+i).className="dot"+(sc[i]==="dg"?" bad":sc[i]==="wn"?" warn":"")});
  if(gc!==update.last){if(gc!=="ok")log(gc==="dg"?"Dangerous gas level!":"High gas level detected",Math.round(r.gas)+" ppm (limit "+CONFIG.gasWarn+" ppm)",gc);update.last=gc}
  drawAll();
}
function ok2(){return"ok"}

// simulated sensor source
let ph=0;function sim(){ph+=.15;const g=150+30*Math.sin(ph/3)+Math.random()*10+leak;leak=Math.max(0,leak-25);
  return{gas:g,humidity:62+6*Math.sin(ph/4)+Math.random(),tilt:2.4+(moving?2:0)*Math.sin(ph)+Math.random()*.6,battery:Math.max(5,(S.bat.length?S.bat[S.bat.length-1]:78)-.01)}}
async function poll(){
  if(!CONFIG.live){update(sim());return}
  try{const r=await (await fetch(CONFIG.baseUrl+"/data",{cache:"no-store"})).json();setOnline(true);update({gas:+r.gas,humidity:+r.humidity,tilt:+r.tilt,battery:+r.battery})}
  catch(e){setOnline(false)}
}
function setOnline(v){if(v===online)return;online=v;$("cdot").className="dot"+(v?"":" bad");$("ctxt").textContent=v?"Rover online":"Rover offline";log(v?"Rover reconnected":"Connection lost","Check Wi-Fi and IP",v?"":"dg")}
$("ipt").textContent=CONFIG.baseUrl.replace("http://","");$("cmode").textContent=CONFIG.live?"Live mode":"Simulation mode";

// controls
function send(c){
  $("iCmd").textContent=c;log("Command: "+c,auto?"ignored in auto mode":"Manual","");
  if(c==="Stop"){moving=false;speed=0}else if(!auto){moving=true;speed=c==="Backward"?-.3:.3}
  $("iSpd").textContent=Math.abs(speed).toFixed(1)+" m/s";
  if(CONFIG.live)fetch(CONFIG.baseUrl+"/cmd?d="+c).catch(()=>{});
}
document.querySelectorAll("[data-c]").forEach(b=>b.onclick=()=>send(b.dataset.c));
addEventListener("keydown",e=>{const m={ArrowUp:"Forward",ArrowDown:"Backward",ArrowLeft:"Left",ArrowRight:"Right"," ":"Stop"}[e.key];if(m&&!auto){e.preventDefault();send(m)}});
function mode(a){auto=a;$("mAuto").classList.toggle("on",a);$("mMan").classList.toggle("on",!a);$("iMode").textContent=a?"Auto":"Manual";log(a?"Auto mode enabled":"Manual mode enabled","");if(a){moving=true;speed=.3;$("iSpd").textContent="0.3 m/s"}else{moving=false;speed=0;$("iSpd").textContent="0.0 m/s"}if(CONFIG.live)fetch(CONFIG.baseUrl+"/cmd?d="+(a?"Auto":"Manual")).catch(()=>{})}
$("mMan").onclick=()=>mode(false);$("mAuto").onclick=()=>mode(true);
$("test").onclick=()=>{leak=170};
$("rg").onclick=e=>{const b=e.target.closest("button");if(!b)return;rangeN=+b.dataset.n;document.querySelectorAll("#rg .btn").forEach(x=>x.classList.toggle("on",x===b));drawAll()};

// graphs
function spark(id,data,col,lo,hi){
  const c=$(id),r=c.getBoundingClientRect(),d=devicePixelRatio||1;c.width=r.width*d;c.height=r.height*d;const g=c.getContext("2d");g.scale(d,d);
  const W=r.width,H=r.height,L=26,B=14,a=data.slice(-rangeN);g.font="10px system-ui";g.fillStyle="#8aa0b8";g.strokeStyle="#1a3350";g.lineWidth=1;
  for(let i=0;i<=2;i++){const y=4+(H-B-4)*i/2,v=hi-(hi-lo)*i/2;g.beginPath();g.moveTo(L,y);g.lineTo(W,y);g.stroke();g.textAlign="right";g.fillText(Math.round(v),L-4,y+3)}
  if(a.length<2)return;const X=i=>L+i/(a.length-1)*(W-L),Y=v=>4+(1-(Math.min(hi,Math.max(lo,v))-lo)/(hi-lo))*(H-B-4);
  g.beginPath();a.forEach((v,i)=>i?g.lineTo(X(i),Y(v)):g.moveTo(X(i),Y(v)));g.strokeStyle=col;g.lineWidth=2;g.stroke();
  g.lineTo(W,H-B);g.lineTo(L,H-B);g.globalAlpha=.15;g.fillStyle=col;g.fill();g.globalAlpha=1;
}
function drawAll(){spark("g0",S.gas,"#19c37d",0,400);spark("g1",S.hum,"#1f7bff",0,100);spark("g2",S.tilt,"#8b5cf6",-10,10);spark("g3",S.bat,"#f5b73b",0,100)}
addEventListener("resize",drawAll);

// simulated camera feed
const vc=$("vid"),vg=vc.getContext("2d");
function video(t){
  const W=640,H=360;vg.fillStyle="#0a0b0d";vg.fillRect(0,0,W,H);
  for(let i=14;i>0;i--){const k=((i+(t/700)%1)/14),s=Math.pow(k,2.1),w=W*1.1*s,h=H*1.0*s;vg.strokeStyle=`rgba(150,120,90,${.75*(1-k)+.08})`;vg.lineWidth=1+k*7;vg.strokeRect(W/2-w/2,H*.48-h/2,w,h)}
  const gr=vg.createRadialGradient(W/2,H*.48,10,W/2,H*.48,W*.5);gr.addColorStop(0,"rgba(255,235,190,.5)");gr.addColorStop(1,"rgba(0,0,0,.85)");vg.fillStyle=gr;vg.fillRect(0,0,W,H);
  vg.fillStyle="rgba(255,255,255,.7)";vg.font="12px monospace";vg.fillText("1920 x 1080 · ESP32-CAM (simulated)",14,H-14);
}
// map rover
const pth=$("path"),len=pth.getTotalLength();let pos=0;
function frame(t){video(t);if(moving){pos=(pos+speed*.6+len)%len;const p=pth.getPointAtLength(pos);$("rv").setAttribute("cx",p.x);$("rv").setAttribute("cy",p.y)}requestAnimationFrame(frame)}

function clock(){const d=new Date();$("clk").textContent=pad(d.getHours())+":"+pad(d.getMinutes())+":"+pad(d.getSeconds());$("dte").textContent=d.toLocaleDateString([],{day:"numeric",month:"short",year:"numeric"})}
for(let i=0;i<MAX;i++)if(!CONFIG.live){const r=sim();["gas","hum","tilt","bat"].forEach((k,j)=>S[k].push([r.gas,r.humidity,r.tilt,r.battery][j]))}
clock();setInterval(clock,1000);poll();setInterval(poll,CONFIG.pollMs);requestAnimationFrame(frame);
</script>
</body>
</html>
