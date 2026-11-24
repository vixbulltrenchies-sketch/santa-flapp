<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1">
<title>Santa Flap — Tap the bird. Collect Santa Coins.</title>
<meta name="description" content="Tap to flap, collect Santa Coins, complete tasks. Season 1 ends March 31.">
<meta property="og:title" content="Santa Flap">
<meta property="og:description" content="Tap the bird. Collect Santa Coins. Season ends Mar 31.">
<meta property="og:type" content="website">
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'><circle cx='16' cy='18' r='10' fill='%23c81e2b'/><circle cx='16' cy='24' r='6' fill='%23fff'/></svg>">

<!-- ===== PASTE YOUR AD NETWORK SCRIPT TAG HERE (once) ===== -->
<!-- <script async src="https://your-monetag-tag.js"></script> -->

<style>
  *{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
  body{margin:0;background:#070c18;color:#eaf1fa;font-family:ui-sans-serif,system-ui,-apple-system,'Segoe UI',sans-serif;display:flex;justify-content:center;padding:14px 10px 40px}
  .app{width:100%;max-width:375px}
  .hud{display:flex;justify-content:space-between;align-items:center;padding:10px 12px;border:1px solid #263049;border-radius:14px 14px 0 0;background:#131a2c}
  .lab{font-size:10px;letter-spacing:.09em;text-transform:uppercase;color:#8fa0bd}
  .bal{font-size:21px;font-weight:800;line-height:1.1;font-variant-numeric:tabular-nums}
  .erow{display:flex;align-items:center;gap:6px;justify-content:flex-end}
  .etrack{width:52px;height:6px;border-radius:3px;background:#263049;overflow:hidden}
  .efill{height:100%;width:100%;background:#c81e2b;transition:width .3s}
  .etxt{font-size:13px;font-weight:700;font-variant-numeric:tabular-nums}
  .stage{position:relative;height:440px;border-left:1px solid #263049;border-right:1px solid #263049;overflow:hidden}
  canvas{width:100%;height:440px;display:block}
  .overlay{position:absolute;inset:0;display:none;text-align:center;z-index:4}
  #gover{background:rgba(4,8,20,.88);padding:16px}
  #gover .t{font-size:19px;font-weight:800;margin-top:14px}
  #gover .s{font-size:12px;color:#8fa0bd;margin:6px 0 14px}
  .adlabel{font-size:9px;letter-spacing:.1em;color:#6b7d9c;margin-bottom:5px}
  .adslot{display:flex;align-items:center;justify-content:center;border:1px dashed #33405e;border-radius:8px;color:#5d6f8f;font-size:11px;background:rgba(255,255,255,.03)}
  #slot_big{height:250px;margin-bottom:14px}
  #slot_bar{height:50px;border-radius:6px}
  #modal{background:rgba(4,8,20,.88);align-items:center;justify-content:center;padding:22px;z-index:6}
  #modal .box{background:#131a2c;border:1px solid #263049;border-radius:16px;padding:22px 18px;width:100%}
  #modal .h{font-weight:800;font-size:15px;margin-bottom:6px}
  #modal .p{font-size:12px;color:#8fa0bd;margin-bottom:16px}
  #mbig{font-size:34px;font-weight:800;margin-bottom:16px;font-variant-numeric:tabular-nums}
  .btn{width:100%;padding:12px;border-radius:10px;border:none;font-weight:700;font-size:13px;cursor:pointer;font-family:inherit}
  .btn-red{background:#c81e2b;color:#fff}
  .btn-gold{background:#f2b632;color:#1a1205}
  .btn-ghost{background:#1b2437;color:#c8d4e6;border:1px solid #263049}
  .btn:disabled{background:#263049;color:#5d6f8f;cursor:not-allowed}
  .barwrap{border-left:1px solid #263049;border-right:1px solid #263049;padding:7px 12px 9px;background:#131a2c}
  .card{border:1px solid #263049;border-top:none;border-radius:0 0 14px 14px;padding:12px;background:#131a2c}
  .row{display:flex;justify-content:space-between;align-items:center;margin-bottom:7px}
  .row b{font-size:12px}
  .pct{font-size:11px;color:#8fa0bd;font-variant-numeric:tabular-nums}
  .track{height:8px;border-radius:4px;background:#263049;overflow:hidden;margin-bottom:9px}
  .fill{height:100%;width:0;background:linear-gradient(90deg,#16a34a,#22c55e);transition:width .4s}
  .meta{display:flex;justify-content:space-between;font-size:11px;color:#8fa0bd;margin-bottom:10px}
  .sec{font-size:11px;letter-spacing:.09em;text-transform:uppercase;color:#8fa0bd;font-weight:700;margin:14px 2px 7px}
  .task{display:flex;align-items:center;justify-content:space-between;gap:10px;padding:10px 12px;border:1px solid #263049;border-radius:10px;margin-bottom:7px;background:#131a2c}
  .task .l{font-size:12.5px;font-weight:600}
  .task .p{font-size:11px;color:#8fa0bd}
  .task button{flex:0 0 auto;padding:7px 13px;border-radius:8px;border:none;font-size:11.5px;font-weight:700;cursor:pointer;background:#c81e2b;color:#fff;font-family:inherit}
  .task button.done{background:#263049;color:#5d6f8f;cursor:default}
  .note{padding:12px;border:1px solid #263049;border-radius:12px;background:#131a2c;margin-top:14px}
  .note .t{font-size:11px;letter-spacing:.09em;text-transform:uppercase;color:#8fa0bd;font-weight:700;margin-bottom:6px}
  #cd{font-size:16px;font-weight:800;font-variant-numeric:tabular-nums}
  .note .s{font-size:11px;color:#8fa0bd;margin-top:6px;line-height:1.45}
  #toast{font-size:12px;text-align:center;color:#8fa0bd;min-height:16px;margin-top:12px}
  footer{margin-top:18px;font-size:11px;color:#5d6f8f;text-align:center;line-height:1.6}
  footer a{color:#8fa0bd}
</style>
</head>
<body>
<div class="app">

  <div class="hud">
    <div>
      <div class="lab">Santa Coins</div>
      <div class="bal" id="bal">0</div>
    </div>
    <div style="text-align:right">
      <div class="lab">Energy</div>
      <div class="erow">
        <div class="etrack"><div class="efill" id="ebar"></div></div>
        <span class="etxt" id="etxt">100</span>
      </div>
    </div>
  </div>

  <div class="stage">
    <canvas id="c" width="360" height="440"></canvas>

    <div class="overlay" id="gover">
      <div class="t">Run over</div>
      <div class="s" id="gosc">—</div>
      <div class="adlabel">AD</div>
      <div class="adslot" id="slot_big">300 × 250 — paste ad code</div>
      <button class="btn btn-red" id="again">Play again</button>
    </div>

    <div class="overlay" id="modal">
      <div class="box">
        <div class="h">Sponsored ad</div>
        <div class="p">Reward unlocks when the ad finishes.</div>
        <div id="mbig">5</div>
        <button class="btn btn-ghost" id="mbtn" disabled>Claim reward</button>
      </div>
    </div>
  </div>

  <div class="barwrap">
    <div class="adlabel">AD</div>
    <div class="adslot" id="slot_bar">320 × 50 banner — paste ad code</div>
  </div>

  <div class="card">
    <div class="row">
      <b>Withdraw 25,000 SC</b>
      <span class="pct" id="pct">0%</span>
    </div>
    <div class="track"><div class="fill" id="wbar"></div></div>
    <div class="meta">
      <span id="refs">Referrals 0 / 10</span>
      <span>Wallet required</span>
    </div>
    <button class="btn btn-ghost" id="connect">Connect wallet</button>
    <button class="btn btn-ghost" id="wbtn" style="margin-top:7px">Request withdrawal</button>
  </div>

  <div class="sec">Tasks</div>
  <div id="tasks"></div>

  <button class="btn btn-gold" id="adbtn" style="margin-top:8px">Optional: watch ad · +50 SC, +10 energy</button>

  <div class="note">
    <div class="t">Season 1 closes</div>
    <div id="cd">—</div>
    <div class="s">Snapshot Mar 31. Distribution TBD. Points are not money until conversion.</div>
  </div>

  <div id="toast"></div>

  <footer>
    <a href="privacy.html">Privacy</a> · <a href="terms.html">Terms</a><br>
    Contact: you@email.com
  </footer>
</div>

<script>
(function(){
  /* =====================================================================
     EDIT ME: put your real links in the 4th slot of each line below.
     Delete any line you don't want.
     ===================================================================== */
  const TASKS=[
    ['tg1','Join Telegram channel',500,'https://t.me/https://t.me/qwkdjvtkvvdlxvzjsantacoi'],
    ['tg2','Join Telegram group',300,'https://t.me/CHANGE_ME'],
    ['yt','Subscribe on YouTube',600,'https://youtube.com/@https://www.youtube.com/@santacoins?sub_confirmation=1'],
    ['x','Follow on X',400,'https://x.com/CHANGE_ME'],
    ['ig','Follow on Instagram',350,'https://instagram.com/CHANGE_ME'],
    ['fb','Follow on Facebook',350,'https://facebook.com/CHANGE_ME'],
    ['wa','Join WhatsApp channel',400,'https://whatsapp.com/channel/CHANGE_ME'],
    ['qt','Quote-tweet #SantaFlap',800,'https://twitter.com/intent/tweet?text=I%27m%20flapping%20for%20%23SantaFlap'],
    ['ref','Invite a friend',1000,'https://t.me/CHANGE_ME']
  ];

  const $=id=>document.getElementById(id);
  const cvs=$('c'), ctx=cvs.getContext('2d');
  const W=360, H=440, GROUND=H-52, G=0.44, FLAP=-7.2, SPD=2.5;
  const K='sf3_';
  const get=(k,d)=>{try{const v=localStorage.getItem(K+k);return v===null?d:JSON.parse(v)}catch(e){return d}};
  const set=(k,v)=>{try{localStorage.setItem(K+k,JSON.stringify(v))}catch(e){}};

  let santa=get('pts',0), energy=get('energy',100), refs=get('refs',0);
  let claimed=get('claimed',{}), lastRegen=Date.now(), best=get('best',0);
  let state='menu', bird, pipes, gifts, score, runCoins, tick, snow=[];

  for(let i=0;i<36;i++) snow.push({x:Math.random()*W,y:Math.random()*H,r:Math.random()*1.7+.6,s:Math.random()*.6+.2});

  function reset(){
    bird={x:104,y:H/2,vy:0,r:13,rot:0};
    pipes=[]; gifts=[]; score=0; runCoins=0; tick=0;
  }
  reset();

  function paint(){
    $('bal').textContent=santa.toLocaleString();
    $('etxt').textContent=energy;
    $('ebar').style.width=energy+'%';
    const p=Math.min(100,santa/25000*100);
    $('wbar').style.width=p+'%';
    $('pct').textContent=Math.floor(p)+'%';
    $('refs').textContent='Referrals '+refs+' / 10';
  }
  paint();

  function toast(m){ const t=$('toast'); t.textContent=m; clearTimeout(t._h); t._h=setTimeout(()=>{t.textContent=''},2600); }

  setInterval(()=>{ if(energy<100 && Date.now()-lastRegen>=12000){ energy++; lastRegen=Date.now(); set('energy',energy); paint(); } },1000);

  function start(){
    if(energy<1){ toast('Out of energy. Watch an ad for +10.'); return; }
    energy--; lastRegen=Date.now(); set('energy',energy);
    reset(); state='play'; $('gover').style.display='none'; paint();
  }

  function flap(){ if(state==='play') bird.vy=FLAP; else if(state==='menu') start(); }

  cvs.addEventListener('pointerdown', e=>{ e.preventDefault(); flap(); });
  window.addEventListener('keydown', e=>{ if(e.code==='Space'){ e.preventDefault(); flap(); } });
  $('again').onclick=start;

  function end(){
    state='over';
    santa+=runCoins; set('pts',santa);
    if(score>best){ best=score; set('best',best); }
    $('gosc').textContent=(runCoins>0?'+'+runCoins+' SC':'No coins')+' · '+score+' pipes cleared';
    $('gover').style.display='block';
    paint();
  }

  function hit(b,p){
    const cx=Math.max(p.x,Math.min(b.x,p.x+p.w));
    const cy=Math.max(0,Math.min(b.y,p.y+p.h));
    const dx=b.x-cx, dy=b.y-cy;
    return dx*dx+dy*dy < b.r*b.r;
  }

  function update(){
    tick++;
    for(const s of snow){ s.y+=s.s; s.x-=.22; if(s.y>H){s.y=-4;s.x=Math.random()*W} }

    if(state==='play'){
      bird.vy+=G; bird.y+=bird.vy;
      bird.rot=Math.max(-.5,Math.min(1.2,bird.vy/12));
      if(tick%92===0){
        const gap=142, gy=64+Math.random()*(H-GROUND-64-gap);
        pipes.push({x:W+20,y:gy,w:52,h:gap,passed:false});
        if(Math.random()<.72) gifts.push({x:W+46,y:gy+gap/2,got:false});
      }
      for(const p of pipes) p.x-=SPD;
      for(const g of gifts) g.x-=SPD;
      pipes=pipes.filter(p=>p.x>-60); gifts=gifts.filter(g=>g.x>-30);
      for(const g of gifts) if(!g.got && Math.abs(g.x-bird.x)<16 && Math.abs(g.y-bird.y)<16){ g.got=true; runCoins+=5; }
      if(tick%26===0) runCoins++;
      for(const p of pipes){
        if(hit(bird,p) || bird.y+bird.r>GROUND || bird.y-bird.r<0){ end(); break; }
        if(!p.passed && p.x+p.w<bird.x){ p.passed=true; score++; }
      }
    } else if(state==='menu'){
      bird.y=H/2+Math.sin(tick/34)*7;
      bird.rot=Math.sin(tick/34)*.18;
    }
  }

  function drawSanta(x,y,r){
    ctx.save(); ctx.translate(x,y); ctx.rotate(r);
    ctx.fillStyle='#c81e2b'; ctx.beginPath(); ctx.arc(0,0,13,0,7); ctx.fill();
    ctx.fillStyle='#f6f7fb'; ctx.beginPath(); ctx.arc(0,7,8,0,7); ctx.fill();
    ctx.fillStyle='#111a2e'; ctx.beginPath(); ctx.arc(-4,-3,1.9,0,7); ctx.arc(4,-3,1.9,0,7); ctx.fill();
    ctx.fillStyle='#c81e2b'; ctx.beginPath(); ctx.moveTo(-9,-9); ctx.lineTo(0,-24); ctx.lineTo(9,-9); ctx.closePath(); ctx.fill();
    ctx.fillStyle='#f6f7fb'; ctx.beginPath(); ctx.arc(0,-24,3.4,0,7); ctx.fill();
    ctx.fillRect(-9.5,-11,19,3.4);
    ctx.restore();
  }

  function draw(){
    const sky=ctx.createLinearGradient(0,0,0,H);
    sky.addColorStop(0,'#0d1a33'); sky.addColorStop(.55,'#1c3355'); sky.addColorStop(1,'#2d4a6b');
    ctx.fillStyle=sky; ctx.fillRect(0,0,W,H);
    ctx.fillStyle='rgba(255,255,255,.55)';
    for(const s of snow){ ctx.beginPath(); ctx.arc(s.x,s.y,s.r,0,7); ctx.fill(); }
    for(const p of pipes){
      ctx.fillStyle='#e8eef7'; ctx.fillRect(p.x,0,p.w,p.y); ctx.fillRect(p.x,p.y+p.h,p.w,GROUND-(p.y+p.h));
      ctx.fillStyle='#c81e2b';
      for(let i=0;i<p.y;i+=22) ctx.fillRect(p.x,i,p.w,11);
      for(let i=p.y+p.h;i<GROUND;i+=22) ctx.fillRect(p.x,i,p.w,11);
    }
    for(const g of gifts){
      if(g.got) continue;
      ctx.fillStyle='#f2b632'; ctx.fillRect(g.x-8,g.y-8,16,16);
      ctx.fillStyle='#c81e2b'; ctx.fillRect(g.x-1.6,g.y-8,3.2,16); ctx.fillRect(g.x-8,g.y-1.6,16,3.2);
    }
    ctx.fillStyle='#eef4fb'; ctx.fillRect(0,GROUND,W,H-GROUND);
    ctx.fillStyle='#c3d3e6'; ctx.fillRect(0,GROUND,W,4);
    drawSanta(bird.x,bird.y,bird.rot);
    ctx.fillStyle='#eaf1fa'; ctx.font='800 15px ui-sans-serif,sans-serif'; ctx.textAlign='left';
    ctx.fillText('RUN '+runCoins+' SC',12,26);
    if(state==='menu'){
      ctx.textAlign='center'; ctx.fillStyle='#eaf1fa'; ctx.font='800 22px ui-sans-serif,sans-serif';
      ctx.fillText('TAP TO FLAP',W/2,H/2-46);
      ctx.font='500 12px ui-sans-serif,sans-serif'; ctx.fillStyle='rgba(234,241,250,.72)';
      ctx.fillText('Collect gifts. Dodge canes.',W/2,H/2-24);
      ctx.font='500 11px ui-sans-serif,sans-serif'; ctx.fillStyle='rgba(234,241,250,.5)';
      ctx.fillText('Best run: '+best,W/2,H/2+44);
    }
  }

  (function loop(){ update(); draw(); requestAnimationFrame(loop); })();

  /* task rows */
  const tw=$('tasks');
  TASKS.forEach(([id,label,pts,link])=>{
    const row=document.createElement('div'); row.className='task';
    row.innerHTML='<div><div class="l">'+label+'</div><div class="p">+'+pts+' SC</div></div>';
    const b=document.createElement('button');
    b.textContent = claimed[id] ? 'Done' : 'Go';
    if(claimed[id]) b.classList.add('done');
    b.onclick=()=>{
      if(claimed[id]) return;
      window.open(link,'_blank');            /* open the page first */
      b.textContent='Claim';
      setTimeout(()=>{                        /* then allow the claim */
        b.onclick=()=>{
          if(claimed[id]) return;
          claimed[id]=1; set('claimed',claimed);
          santa+=pts; set('pts',santa); paint();
          if(id==='ref'){ refs++; set('refs',refs); paint(); }
          b.textContent='Done'; b.classList.add('done');
          toast('+'+pts+' Santa Coins');
        };
      },2000);
    };
    row.appendChild(b); tw.appendChild(row);
  });

  /* ad + reward */
  const modal=$('modal'), mbtn=$('mbtn'), mbig=$('mbig');
  $('adbtn').onclick=()=>{
    /* If your ad network gives a function, call it here instead of the timer. */
    modal.style.display='flex'; mbtn.disabled=true; mbtn.textContent='Claim reward';
    let n=5; mbig.textContent=n;
    const h=setInterval(()=>{
      n--; mbig.textContent=n>0?n:0;
      if(n<=0){
        clearInterval(h); mbig.textContent='✓'; mbtn.disabled=false;
        mbtn.classList.remove('btn-ghost'); mbtn.classList.add('btn-red');
        mbtn.onclick=()=>{
          santa+=50; energy=Math.min(100,energy+10); set('pts',santa); set('energy',energy);
          modal.style.display='none'; paint(); toast('+50 SC and +10 energy');
        };
      }
    },1000);
  };

  /* wallet */
  $('connect').onclick=async()=>{
    if(!window.ethereum) return toast('Open this inside MetaMask');
    try{
      const [addr]=await window.ethereum.request({method:'eth_requestAccounts'});
      $('connect').textContent=addr.slice(0,6)+'...'+addr.slice(-4);
      /* LATER: send addr to Supabase here */
    }catch(e){ toast('Connection cancelled'); }
  };

  $('wbtn').onclick=()=>{
    if(santa<25000) return toast('Need '+(25000-santa).toLocaleString()+' more SC.');
    if(refs<10) return toast('Need '+(10-refs)+' more verified referrals.');
    toast('Eligible — withdrawals open at TGE.');
  };

  /* countdown */
  (function(){
    const target=new Date('2027-03-31T23:59:59Z').getTime(), el=$('cd');
    const t=()=>{ const d=target-Date.now();
      if(d<=0){ el.textContent='Season closed'; return; }
      el.textContent=Math.floor(d/864e5)+'d '+Math.floor(d%864e5/36e5)+'h '+Math.floor(d%36e5/6e4)+'m';
      setTimeout(t,30000); };
    t();
  })();
})();
</script>
</body>
</html>
