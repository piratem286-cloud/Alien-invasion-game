# alien invasion
<!DOCTYPE html><html lang="en"><head><meta charset="utf-8"><meta name="viewport"
content="width=device-width,initial-scale=1,viewport-fit=cover"><title>Alien
Invasion</title>
<style>
:root{--bg:#0c0e0b;--fg:#e9eee4;--ac:#d9b44a;--ov:rgba(10,12,9,.92);box-
sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-
bottom:env(safe-area-inset-bottom,0px)}
*{-webkit-user-select:none;user-select:none;-webkit-touch-callout:none}
html,body{margin:0;height:100%;background:var(--bg);color:var(--fg);font:15px/1.4
Georgia,serif}
body{display:flex;align-items:center;justify-content:center}
#w{position:relative;width:100%;max-width:960px}
canvas{display:block;image-rendering:pixelated;width:100%;aspect-ratio:8/5;touch-
action:none;background:#000}
#o{position:absolute;inset:0;display:flex;flex-direction:column;align-
items:center;justify-content:center;gap:8px;text-align:center;background:var(--
ov);padding:10px;overflow:auto}
h1,h2,p{margin:0}h1{font-size:30px;letter-spacing:.04em}p{max-width:520px}.s{font-
size:12px;opacity:.7}
button{font:inherit;font-weight:700;background:var(--
ac);color:#17140a;border:0;border-radius:4px;padding:9px
18px;margin:2px}button.g{background:#2b2f27;color:var(--fg)}
</style></head><body><div id="w"><canvas id="c"></canvas><div id="o"></div></div>
<script>
const
C=document.getElementById('c'),X0=C.getContext('2d'),O=document.getElementById('o'
),W=800,H=500,WW=1600,WH=1200,G=document.createElement('canvas'),GX=G.getContext('
2d'),PS=.4;C.width=W;C.height=H;G.width=W*PS;G.height=H*PS;let X=X0;
const DN=['Easy','Medium','Hard'],BN=['First Contact','Flying Bastards','Tonga
Oasis','Virginia Encounter','Alien Fungus','The Immortal','Cross the Sea','The
Kuns','Return of the Alien Fungus','The Tank','The Slop Tank','The Mutated
Moose','The Tank Battle','The Immortal Returns','The God of the New World','New
York Settlement','Death Corridor','Mission 18','Mission 19','Mission 20','Mission
21','Mission 22','Mission 23','Last Preparing','Last Stand'];
const IN=['Fight beside your squad inside the Tremors base. The aliens have to
break through the wooden walls. No matter how well you fight, they all die. When
RUN appears, leave through the door on the east side and run to the east end of
the map before the missile hits. The screen goes black and the next mission
starts.','Alkema Desert. Shoot the mounts first, then the riders. Plasma does not
always hit, so keep moving.','Tonga Oasis. Something is gathered around that
pile.','Wake up in an abandoned military base with 25 HP. Grab sticky bombs, throw
them at HTYU, then hit EXPLODE before time runs out.','Dodge every telegraphed
attack and take the fungus down.','A mysterious creature appears. Find out what
happens when you shoot it.','Aliens are chasing you across the water. Swim, dodge,
and reach the island.','You wake up in West Virginia. The Kuns attack.','Destroy
the towers before the head surfaces, then hurt it while it is above ground. Dodge
everything.','Flying Bastards with purple magic attack. Then finish building the
tank.','Find every missing tank part and the explosion chambers scattered through
the ruins, then bring them to the gray chassis.','Appalachian Mountains. You need
gas for the tank. Two mutated moose guard the area.','Fight with the Slop Tank. If
the tank is destroyed, you die.','The Immortal returns.','Keep walking.','You hear
a voice in your ear. Destroy everything in the settlement.','Escape the Alien
Fungus through the mountain corridor for 2 minutes. Dodge the
hazards.','Skipped.','Skipped.','Skipped.','Skipped.','Skipped.','Skipped.','The
Immortal appears.','No tank. No gun. Only the Blood Knife.'];
const PAL=[['#bfa46a','#a88f58','#2d2a2a'],['#c4a86c','#a88f58','#26231f'],
['#7d8a66','#6f7c5a','#56603f'],['#6f6a72','#5e5a62','#4a4650'],
['#3b2f45','#4a3a58','#2a2033'],['#6a6f5c','#5c6150','#44483c'],
['#2a5f8f','#2f6b9e','#245076'],['#7d8a66','#6f7c5a','#56603f'],
['#3a2a20','#2e2018','#1d140e'],['#8a8573','#78746a','#5a564c'],
['#7a7a74','#6a6a64','#4a4a46'],['#5f7a4a','#4f6a3c','#3a5030'],
['#8a8573','#78746a','#5a564c'],['#6a5f7a','#5a506a','#443c52'],
['#3b2f45','#4a3a58','#2a2033'],['#4a2a5a','#5a346c','#341a44'],
['#7a7a7a','#686868','#4e4e4e'],['#6a665a','#5a564a','#403c32'],
['#222','#222','#222'],['#222','#222','#222'],['#222','#222','#222'],
['#222','#222','#222'],['#222','#222','#222'],['#222','#222','#222'],
['#201828','#2a2034','#14101c'],['#2a0a14','#3a1020','#180610']];
const rnd=(a,b)=>a+Math.random()*(b-a),cl=(v,a,b)=>Math.max(a,Math.min(b,v)),dist=
(a,b)=>Math.hypot(a.x-b.x,a.y-b.y);
let D=0,M=0,s=null,mode='menu',js=null,last=0,cam={x:0,y:0};let PR=
[0,0,0];try{const
sv=JSON.parse(localStorage.getItem('aiPR'));if(Array.isArray(sv)&&sv.length==3)PR=
sv}catch(e){}const K={},ms={x:400,y:250,down:0};
const nm=m=>D==2&&m==3?'Fungus-Controlled HTYU':D==2&&m==4?'The
Minion':D==0&&m==16?'The Final Boss':BN[m];function nxt(m){return m==16&&D>0?
23:m+1}
const ov=h=>{O.innerHTML=h;O.style.display='flex'};
function menu(){mode='menu';ov(`<h1>ALIEN INVASION</h1><p>You are a soldier of The
Tremors. Missions 1–10 of 25.</p><div>${DN.map((n,i)=>`<button
onclick="D=${i};brief(0)">${n}</button>`).join('')}</div><p class=s>WASD move ·
mouse aim and fire · 1 / 2 swap gold rifle mode<br>Touch: drag left side to move,
tap or hold right side to fire. Landscape works best.</p>`)}
function brief(m){if(m>PR[D])m=PR[D];M=m;mode='brief';ov(`<h2>Mission ${m+1}:
${nm(m)}</h2><p>${D==0&&m==16?'The final boss: the Alien Fungus with its giants,
Flying Bastards, flying giants and purple magic.':IN[m]}</p><div><button
onclick="go()">Start mission</button><button class=g
onclick="menu()">Menu</button></div><p class=s>${DN[D]} · replay
${Array.from({length:PR[D]+1},
(_,i)=>i).filter(i=>D==0||i<17||i>22).map(i=>`<button class=g
onclick="brief(${i})">${i+1}</button>`).join('')}</p>`)}
function go(){O.style.display='none';mode='play';init(M);last=performance.now()}
function end(win,t){if(s.over)return;s.over=1;if(win){PR[D]=Math.min(D==0?
16:24,Math.max(PR[D],nxt(M)));try{localStorage.setItem('aiPR',JSON.stringify(PR))}
catch(e){}}setTimeout(()=>{mode='end';ov(`<h2>${win?'Mission complete':'Mission
failed'}</h2><p>${t}</p><div>${win?(M<(D==0?16:24)?`<button
onclick="brief(${nxt(M)})">Next mission</button>`:'<p>The story ends here. Thanks
for playing the whole campaign.</p>'):`<button onclick="go()">Retry</button>`}
<button class=g onclick="menu()">Menu</button></div>`)},win?1400:900)}
const msg=(t,n)=>{s.msg=t;s.mt=n};
function E(o){const
e=Object.assign({x:0,y:0,r:16,hp:60,mhp:0,sp:100,col:'#4a4',dmg:10,cd:0,k:'m',rg:0
,tt:rnd(0,2),st:1},o);s.en.push(e);return e}
function Z(x,y,r,t,dmg,col,kill){s.z.push({x,y,r,t,t0:t,dmg,col,kill})}
function B(x,y,tx,ty,sp,dmg,col,own,r){const a=Math.atan2(ty-y,tx-
x);s.b.push({x,y,vx:Math.cos(a)*sp,vy:Math.sin(a)*sp,dmg,col,own,r:r||5,l:2.5})}
function hurt(n){const p=s.p;p.hp-
=n;s.sh=.25;if(!p.rgT)p.reg=0;if(p.hp<=0)end(0,'You died.')}
function hit(e,n){e.fl=.1;e.idle=0;if(e.mhp>0){e.mhp-=n;if(e.mhp<=0)
{e.mhp=0;e.sp*=.6;s.corp.push({x:e.x,y:e.y,a:rnd(0,6)});s.fx.push({x:e.x,y:e.y,r:3
0,t:.4,t0:.4,c:'#9cf'})}}else e.hp-=n}
function init(m){const d=D;s={t:0,p:
{x:800,y:600,hp:100,cap:0,ammo:0,cd:0,wep:'plasma',pd:20,pc:'#4af',bomb:0,mode:1,r
eg:0},en:[],b:[],z:[],fx:[],pk:
[],msg:'',mt:0,beam:null,grab:null,stuck:0,ready:0,over:0,sh:0,gold:0,run:0,sp:1,c
orp:[]};const p=s.p;
if(m==0){p.x=320;p.y=600;p.wep='rifle';p.ammo=[50,50,20][d];s.mates=[];for(let
i=0;i<6;i++)s.mates.push({x:285+(i%3)*45,y:565+
(i/3|0)*70,a:0,cd:rnd(0,.4),wep:'rifle'});s.mis=[];s.mt2=0;s.walls=[];for(let
i=0;i<4;i++)s.walls.push({x:210+i*55,y:490,w:55,h:14,hp:12},
{x:210+i*55,y:696,w:55,h:14,hp:12},{x:210,y:490+i*55,w:14,h:55,hp:12},
{x:416,y:490+i*55,w:14,h:55,hp:12});s.walls[7].door=1;msg('Your squad is with you.
Hold the shelter.',4)}
if(m==1){p.y=900;p.pc=['#4af','#fd3','#4af'][d];for(let i=0;i<[10,10,5][d];i++)
{const
a=rnd(0,6.28);E({x:cl(800+Math.cos(a)*520,30,1570),y:cl(500+Math.sin(a)*380,30,117
0),k:'r',hp:[60,105,300][d],mhp:[150,200,0][d],sp:80,col:['#3af','#fc3','#d22']
[d],st:Math.random()<.5?1:-1,dmg:[50,30,50][d]})}msg('Shoot the mounts first.',4)}
if(m==2){p.y=950;for(let i=0;i<5;i++){const
a=i*1.256;E({x:800+Math.cos(a)*45,y:600+Math.sin(a)*45,r:14,hp:[100,100,200]
[d],dmg:[5,50,20][d],sp:[100,115,100][d],idle:1,col:['#c96','#a22','#8a5']
[d]})}msg(['What the fuck are y’all doing?','What the fuck are those
things?','What the fuck are those things?'][d],4)}
if(m==3){p.hp=25;p.cap=[70,60,60][d];s.need=[10,25,40][d];s.tm=[120,120,300]
[d];s.boss=E({x:800,y:300,r:65,hp:[500,500,1000][d],sp:[45,90,80]
[d],col:'#fc0',k:'boss',tt:2});for(let
i=0;i<5;i++)s.pk.push({x:rnd(80,1520),y:rnd(450,1150)});msg('Pick up a sticky
bomb, then throw it at HTYU.',4)}
if(m==4){const h=[1000,1000,2000]
[d];s.boss=E({x:800,y:300,r:95,hp:h,sp:35,col:'#b6f',k:'fung',tt:2,bt:5,gt:9});s.b
oss.mx=h;if(d<2){p.pd=50;p.pc='#4f4'}msg(d<2?'Workstation upgrade: green plasma,
50 damage.':'You’re fighting one of my minions. Good luck. I don’t even think you
can beat this.',5)}if(m>=5&&m<10)init2(m,d,p);if(m>=10)init3(m,d,p)}
function fire(){const p=s.p,tx=ms.x+cam.x,ty=ms.y+cam.y,ag=Math.atan2(ty-p.y,tx-
p.x);p.rc=.08;if(!p.bomb&&p.wep!='knife'&&
(p.wep!='gold'||p.mode==2))s.fx.push({x:p.x+Math.cos(ag)*34,y:p.y+Math.sin(ag)*34,
r:16,t:.07,t0:.07,c:'#ffe27a'});
if(p.bomb){p.bomb=0;B(p.x,p.y,tx,ty,520,0,'#f44','bomb',8);p.cd=.3}
else if(p.wep=='tank'){const pb=p.mode==2&&p.pb,sp=pb?90:p.ex?
70:0;s.b.push({x:p.x,y:p.y,vx:Math.cos(ag)*650,vy:Math.sin(ag)*650,dmg:pb?
200:p.ex?90:60,col:pb?'#e8c8ff':'#ffb04a',own:'p',r:pb?14:8,l:2,sp});p.cd=pb?
2:.55}
else if(p.wep=='knife'){for(const e of s.en){const b2=Math.atan2(e.y-p.y,e.x-
p.x);let df=Math.abs(b2-ag);if(df>3.14)df=6.28-df;if(dist(e,p)
<e.r+125&&df<1)hit(e,500)}s.fx.push({x:p.x+Math.cos(ag)*55,y:p.y+Math.sin(ag)*55,r
:65,t:.2,t0:.2,c:'#c00'});p.cd=.35}
else if(p.wep=='rifle'){if(p.ammo<=0){msg('Out of ammo!',1);p.cd=.5;return}p.ammo-
-;B(p.x,p.y,tx,ty,750,10,'#ff8','p');p.cd=.13}
else if(p.wep=='plasma'){B(p.x,p.y,tx,ty,700,p.pd,p.pc,'p',6);p.cd=.15}
else if(p.mode==1){const a=Math.atan2(ty-p.y,tx-p.x);for(const e of s.en){const
b=Math.atan2(e.y-p.y,e.x-p.x);let df=Math.abs(b-a);if(df>3.14)df=6.28-
df;if(dist(e,p)
<e.r+130&&df<.9)hit(e,100)}s.fx.push({x:p.x+Math.cos(a)*60,y:p.y+Math.sin(a)*60,r:
70,t:.2,t0:.2,c:'#fd0'});s.stab={a:a,t:.2};p.cd=.3}
else{B(p.x,p.y,tx,ty,800,85,'#fd0','p',8);p.cd=.3}}
function ai(e,dt){const p=s.p,a=Math.atan2(p.y-e.y,p.x-e.x),d=dist(e,p);e.cd-
=dt;e.tt-=dt;
if(e.k=='r'){const dir=d>320?1:d<220?-1:0;e.x+=
(Math.cos(a)*dir+Math.cos(a+1.57)*.5*e.st)*e.sp*dt;e.y+=
(Math.sin(a)*dir+Math.sin(a+1.57)*.5*e.st)*e.sp*dt;e.x=cl(e.x,10,WW-
10);e.y=cl(e.y,10,WH-10);if(e.tt<=0){e.tt=(M==9?2.8:[2.2,2,1.8]
[D])+rnd(0,1);B(e.x,e.y,p.x,p.y,260,e.dmg,M==9?'#c6f':'#f55','e',6);e.atk=.3}retur
n}
if(e.idle){if(s.t>2.5)e.idle=0;else return}
let sp=e.sp;if(D>=1&&M==2){if(e.dash>0)e.dash-=dt,sp*=3.5;else if(e.tt<=0)
{e.dash=.45;e.tt=3}}
if(d>e.r+10){e.x+=Math.cos(a)*sp*dt;e.y+=Math.sin(a)*sp*dt}
if(d<e.r+14+e.rg&&e.cd<=0){hurt(e.dash>0?25:e.dmg);e.cd=.7;e.atk=.35}if(s.walls)
{const w=wallPush(e,e.r);if(w&&e.cd<=0){w.hp-
=e.wd||1;w.hf=.15;e.cd=.7;e.atk=.35;if(w.hp<=0)wallBreak(w)}}}
function upd(dt){const p=s.p,d=D,m=M;s.t+=dt;p.cd-=dt;s.sh-=dt;s.mt-=dt;s.flash-
=dt;if(s.stab)s.stab.t-=dt;p.rc-=dt;
let mx=(K.d||K.arrowright?1:0)-(K.a||K.arrowleft?1:0),my=(K.s||K.arrowdown?1:0)-
(K.w||K.arrowup?1:0);
if(js){mx=(js.x-js.ox)/40;my=(js.y-js.oy)/40}if(s.lock>0){s.lock-
=dt;mx=0;my=0}const
l=Math.hypot(mx,my);p.mv=l>.1;if(l>.1)p.ba=Math.atan2(my,mx);if(l>1){mx/=l;my/=l}
if(!s.grab){p.x=cl(p.x+mx*(p.spd||230)*dt,15,WW-15);p.y=cl(p.y+my*
(p.spd||230)*dt,15,WH-15);if(s.walls)wallPush(p,13,1)}
cam.x=cl(p.x-W/2,0,WW-W);cam.y=cl(p.y-H/2,0,WH-H);
if(K['1'])p.mode=1;if(K['2'])p.mode=2;
if(ms.down&&p.cd<=0&&!s.grab&&!s.ready&&!(s.lock>0)&&!s.noFire)fire();
if(p.cap&&p.hp<p.cap){p.reg+=dt;if(p.reg>=(p.rgT||15)){p.hp=Math.min(p.cap,p.hp+
(p.rgA||5));p.reg=0}}
if(m==0){for(const q of s.mis){const dx=q.tx-q.x,dy=q.ty-
q.y,dd=Math.hypot(dx,dy);if(dd<30)
{q.dead=1;s.fx.push({x:q.tx,y:q.ty,r:75,t:.6,t0:.6,c:'#fa3'});s.sh=Math.max(s.sh,.
25);for(const w of s.walls)if(w.hp>0&&Math.hypot(w.x+w.w/2-q.tx,w.y+w.h/2-q.ty)
<90){w.hp-
=5;if(w.hp<=0)wallBreak(w)}}else{q.x+=dx/dd*700*dt;q.y+=dy/dd*700*dt}}s.mis=s.mis.
filter(q=>!q.dead);for(const w of s.walls)if(w.hf>0)w.hf-=dt;s.sp-
=dt;if(s.sp<=0&&s.en.length<12){s.sp=[2.4,2,1.1][d];const a=rnd(0,6.28);const o=
[{hp:Math.ceil(rnd(4,10))*10,sp:150,r:18,col:'#3c3',dmg:100,rg:42,wd:1},
{hp:160,sp:140,r:20,col:'#cc3',dmg:70,rg:30,wd:6},
{hp:180,sp:245,r:18,col:'#d22',dmg:60,wd:12,rg:30}]
[d];E(Object.assign({x:cl(p.x+Math.cos(a)*520,20,1580),y:cl(p.y+Math.sin(a)*520,20
,1180)},o))}
for(const q of s.mates){q.cd-=dt;q.rc-=dt;let n=null,nd=380;for(const e of s.en)
{const dd=dist(q,e);if(dd<nd){nd=dd;n=e}}if(n){q.a=Math.atan2(n.y-q.y,n.x-
q.x);if(q.cd<=0)
{q.cd=.45;q.rc=.08;B(q.x,q.y,n.x,n.y,700,8,'#ff8','p');s.fx.push({x:q.x+Math.cos(q
.a)*32,y:q.y+Math.sin(q.a)*32,r:12,t:.06,t0:.06,c:'#ffe27a'})}if(nd<n.r+34+n.rg)
{q.dead=1;s.fx.push({x:q.x,y:q.y,r:34,t:.5,t0:.5,c:'#a00'})}}}
if(s.run){s.kt-=dt;if(s.kt<=0){const q=s.mates.find(z=>!z.dead);if(q)
{q.dead=1;s.fx.push({x:q.x,y:q.y,r:40,t:.6,t0:.6,c:'#a00'})}s.kt=1}}
s.mates=s.mates.filter(q=>!q.dead);
if(!s.run&&s.t>[18,15,3][d]){s.run=1;s.fuse=[14,12,10][d];s.kt=.8}
if(s.run&&!s.over&&(p.x>=WW-30||(D==2&&(p.x<=30||p.y<=30||p.y>=WH-30))))
{s.over=1;s.black=1;mode='end';PR[D]=Math.max(PR[D],1);try{localStorage.setItem('a
iPR',JSON.stringify(PR))}catch(e){}setTimeout(()=>brief(1),700)}if(s.run){s.fuse-
=dt;msg('RUN',.5);s.mt2-=dt;if(s.mt2<=0&&s.fuse>1){s.mt2=.45;const
an=rnd(0,6.28),tx=320+rnd(-140,140),ty=600+rnd(-140,140);s.mis.push({x:tx+Math.cos
(an)*1000,y:ty+Math.sin(an)*1000,tx,ty,ang:an+3.14})}if(s.fuse<=0&&!s.over)
{s.fx.push({x:320,y:600,r:700,t:1.5,t0:1.5,c:'#fa3'});s.destroyed=1;s.walls=
[];s.mates=[];s.flash=1;s.sh=1.2;if(Math.hypot(p.x-320,p.y-600)>1e9){end(1,'Your
whole squad is gone and the base is destroyed. You are the only survivor. You find
a blue plasma weapon in the wreckage.')}else{s.sh=1;end(0,'The missiles destroyed
the camp.')}}}}
if(m==3){const b=s.boss;if(b.hp>0){const a=Math.atan2(p.y-b.y,p.x-
b.x),dd=dist(b,p);if(dd>90)
{b.x+=Math.cos(a)*b.sp*dt;b.y+=Math.sin(a)*b.sp*dt}b.tt-=dt;if(b.tt<=0){b.tt=d==2?
1.4:1.6;b.atk=.5;const r=Math.random(),x2=d==2?2:1;
if(dd<140){const v=[[20,'Claw!'],[30,'Bite!'],[10,'Punch!']]
[r*3|0];hurt(v[0]*x2);msg(v[1],.6)}
else if(d==0&&r<.25){Z(p.x,p.y,70,1.3,0,'#a3f',1);msg('Purple fire! Move!',1)}
else if(r<.6)B(b.x,b.y,p.x,p.y,300,[10,50,100][d],'#f73','e',7);else
B(b.x,b.y,p.x,p.y,300,[50,90,180][d],'#38f','e',8)}}
s.tm-=dt;for(let i=0;i<s.pk.length;i++){const
k=s.pk[i];if(!p.bomb&&Math.hypot(k.x-p.x,k.y-p.y)<26){p.bomb=1;s.pk[i]=
{x:rnd(80,1520),y:rnd(450,1150)}}}
if(!s.ready&&s.stuck>=s.need&&(d>0||b.hp<=300)){s.ready=1;msg('Press
EXPLODE!',9)}else if(s.stuck>=s.need&&d==0&&b.hp>300&&!s.ready)msg('Shoot HTYU
down to 300 HP too.',.5);
if(s.tm<=0)end(0,'Time ran out.')}
if(m==4){const b=s.boss;if(b.hp>0){const a=Math.atan2(p.y-b.y,p.x-
b.x),dd=dist(b,p);if(dd>160){b.x+=Math.cos(a)*b.sp*dt;b.y+=Math.sin(a)*b.sp*dt}
if(!s.gold&&b.hp<=b.mx/2){s.gold=1;p.wep='gold';msg('Weapon upgrade: Gold Robot
Rifle. 1 = stabbers, 2 = golden energy.',6)}
if(s.grab){s.grab.t-=dt;if(s.grab.c>=30){s.grab=null;hurt(5);p.x=cl(p.x-
Math.cos(a)*-200,15,WW-15);p.y=cl(p.y-Math.sin(a)*-200,15,WH-15)}else
if(s.grab.t<=0)end(0,'The fungus absorbed you.')}
else{b.tt-=dt;if(b.tt<=0){b.tt=[2,1.8,1.6][d];b.atk=.6;const
r=Math.random();if(r<.5)Z(p.x+rnd(-40,40),p.y+rnd(-40,40),70,[3,3,1][d],[50,50,75]
[d],'#9ff');else if(r<.75)Z(b.x,b.y,230,.9,[30,30,40][d],'#fa4');else if(d>=1)
{if(Math.random()<.5)Z(p.x,p.y,40,.9,70,'#f44');else s.reach={a:Math.atan2(p.y-
b.y,p.x-b.x),t:.9}}else Z(p.x,p.y,70,[3,3,1][d],[50,50,75][d],'#9ff')}
if(d>=1){b.bt-=dt;if(!s.beam&&b.bt<=0){s.beam={a:a,t:2.5};b.bt=7}if(s.reach){const
q=s.reach;q.t-=dt;if(q.t<=0&&!q.hit){q.hit=1;q.s=.3;b.atk=.6;const px=p.x-
b.x,py=p.y-b.y,al=px*Math.cos(q.a)+py*Math.sin(q.a),pe=Math.abs(-
px*Math.sin(q.a)+py*Math.cos(q.a));if(al>0&&al<520&&pe<34)hurt(d==2?
60:40)}if(q.hit){q.s-=dt;if(q.s<=0)s.reach=null}}}
if(d==0){b.gt-=dt;if(b.gt<=0&&dd<400){s.grab={c:0,t:8};b.gt=15;msg('Grabbed! Click
fast!',3)}}}
if(s.beam){const q=s.beam;q.t-=dt;let da=Math.atan2(p.y-b.y,p.x-b.x)-
q.a;while(da>3.14)da-
=6.28;while(da<-3.14)da+=6.28;if(q.t>1.8)q.a+=cl(da,-1,1)*dt*.9;const px=p.x-
b.x,py=p.y-b.y;if(px*Math.cos(q.a)+py*Math.sin(q.a)>0&&Math.abs(-
px*Math.sin(q.a)+py*Math.cos(q.a))<22&&!q.h)
{q.h=1;hurt(20)}if(q.t<=0)s.beam=null}}}
if(m>=5)upd2(dt,m,d,p);if(m>=10)upd3(dt,m,d,p);for(const e of
s.en)if(e.k!='boss'&&e.k!='fung'&&e.k!='x')ai(e,dt);
for(const b of s.b){b.x+=b.vx*dt;b.y+=b.vy*dt;b.l-=dt;if(b.own=='e')
{if(Math.hypot(b.x-p.x,b.y-p.y)<b.r+13){hurt(b.dmg);b.l=0}}
else if(b.own=='bomb'){const o=s.boss;if(o&&o.hp>0&&Math.hypot(b.x-o.x,b.y-o.y)
<o.r+10){s.stuck++;b.l=0;s.fx.push({x:b.x,y:b.y,r:25,t:.4,t0:.4,c:'#f44'})}}
else for(const e of s.en)if(Math.hypot(b.x-e.x,b.y-e.y)<e.r+b.r)
{hit(e,b.dmg);b.l=0;if(b.sp){for(const o of s.en)if(o!=e&&Math.hypot(o.x-b.x,o.y-
b.y)
<b.sp)hit(o,b.dmg*.6);s.fx.push({x:b.x,y:b.y,r:b.sp*.8,t:.35,t0:.35,c:'#fb4'})}bre
ak}}
s.b=s.b.filter(b=>b.l>0&&b.x>-50&&b.x<WW+50&&b.y>-50&&b.y<WH+50);
for(const z of s.z){z.t-=dt;if(z.t<=0)
{s.fx.push({x:z.x,y:z.y,r:z.r,t:.35,t0:.35,c:z.col});if(Math.hypot(p.x-z.x,p.y-
z.y)<z.r+8){if(z.kill)end(0,'The purple fire got you.');else hurt(z.dmg)}}}
s.z=s.z.filter(z=>z.t>0);
s.en=s.en.filter(e=>{if(e.fl>0)e.fl-=dt;if(e.atk>0)e.atk-=dt;if(e.hp>0)return
1;s.fx.push({x:e.x,y:e.y,r:e.r*2,t:.5,t0:.5,c:e.k=='fung'?'#b6f':'#8cf'});s.corp.p
ush({x:e.x,y:e.y,bl:1,col:M==0?'#000a':M==1?'#2a4fc0aa':'#8a0f0f99'});return 0});
if(s.boss&&s.boss.hp<=0&&!s.over){if(m==3)end(1,'HTYU is down. You walk out of the
ruined base.');if(m==4)end(1,'The creature explodes. You find a workstation: the
Gold Robot Rifle is yours.');if(m==8)end(1,'The giant plant dies and the ground
goes still.')}
if((m==1||m==2)&&!s.en.length&&!s.over)end(1,m==1?'The sky is clear. Onward to
Tonga Oasis.':'The five attackers are dead.');
for(const f of s.fx)f.t-=dt;s.fx=s.fx.filter(f=>f.t>0)}
function eye(x,y,a,r)
{X.fillStyle='#fff';X.beginPath();X.arc(x,y,r,0,7);X.fill();X.fillStyle='#000';X.b
eginPath();X.arc(x+Math.cos(a)*r*.4,y+Math.sin(a)*r*.4,r*.5,0,7);X.fill()}
const SC={};const shd=(c,a)=>{const k=c+a;if(SC[k])return SC[k];let
h=c.slice(1);if(h.length==3)h=h.replace(/./g,'$&$&');if(h.length!=6)return
SC[k]=c;const n=parseInt(h,16),f=v=>Math.max(0,Math.min(255,v+a));return
SC[k]='#'+((1<<24)+(f(n>>16)<<16)+(f((n>>8)&255)
<<8)+f(n&255)).toString(16).slice(1)};
const R=(x,y,w,h,c)=>{X.fillStyle=c;X.fillRect(x,y,w,h);if(w>7&&h>7&&
(c.length==4||c.length==7))
{X.fillStyle=shd(c,40);X.fillRect(x,y,w,2);X.fillStyle=shd(c,-45);X.fillRect(x,y+h
-2,w,2)}};
function wallPush(o,r,pl){let hit=null;for(const w of s.walls){if(w.hp<=0||
(pl&&w.door))continue;const cx=cl(o.x,w.x,w.x+w.w),cy=cl(o.y,w.y,w.y+w.h),dx=o.x-
cx,dy=o.y-cy,d=Math.hypot(dx,dy);if(d<r){if(d>0){o.x+=dx/d*(r-d);o.y+=dy/d*(r-
d)}else o.x+=r;hit=w}}return hit}
function wallBreak(w)
{s.fx.push({x:w.x+w.w/2,y:w.y+w.h/2,r:40,t:.5,t0:.5,c:'#a77a43'});s.sh=.2}
function soldier(p,a)
{X.save();X.translate(p.x,p.y);R(-9,-7,24,20,'#0004');X.rotate(a);const st=p.mv?
Math.sin(s.t*14)*4:0,rc=p.rc>0?-3:0,pl=p==s.p;R(-4+st,-13,8,5,'#222');R(-4-
st,8,8,5,'#222');R(-9,-7,6,14,'#2a3318');R(-5,-10,11,20,pl?
(s.sh>0?'#e66':'#3d6a9a'):'#4a5a2a');R(-2,-8,6,16,pl?'#2f5278':'#5d6e3a');R(-4,-5,
10,10,pl?'#1f2a38':'#2f3a1f');R(3,-3,4,6,'#d2a679');R(0,-9,5,4,'#d2a679');R(2+rc,-
8,p.wep=='knife'?
16:26,4,p.wep=='knife'?'#b00':p.wep=='gold'?'#fd0':p.wep=='rifle'?'#222':p.pc);R(8
+rc,-5,6,4,'#333');R(24+rc,-9,6,6,'#555');X.restore()}
const SEA=(d,pt)=>({pt,k:'x',ty:'sea',r:20,hp:250,mx:250,sp:(pt==1?190:150)*(d==2?
1.6:1),col:['#5a4a6a','#6a8a3a','#8a1818'][d],dmg:d==2?999:d==1?60:pt==1?
25:30,cd:0});
function tw(n){for(let i=0;i<n;i++){const
h=s.holes[(Math.random()*s.holes.length)|0],hp=D==2?
500:50;E({k:'x',ty:'tower',x:h.x,y:h.y,r:22,hp,mx:hp,sp:0,col:'#2f5a2a',tt:rnd(1,3
)})}}
const HT=
(x,y)=>E({k:'x',ty:'htyu',x,y,r:60,hp:600,mx:600,sp:70,col:'#b8a',tt:2.5,dmg:30});
function init2(m,d,p){p.wep='gold';p.mode=2;s.warn=[];s.bm=[];if(m>=7)
{p.mh=150;p.hp=150;p.cap=150;p.rgT=10;p.rgA=10}
if(m==5)
{p.x=500;p.y=750;s.cr=E({x:900,y:450,r:34,hp:1e6,mx:1e6,sp:0,col:d==2?'#6f6':'#b6f
',k:'x',ty:'imm',nb:1});s.cr.x0=900;s.cr.y0=450;s.cr.lbl=d?'HP 0 DMG
0':'';msg(d?'A mysterious creature floats ahead.':'Ha, let’s see what you
had.',4)}
if(m==6)
{p.x=70;p.y=600;p.spd=200;s.st=1;s.noFire=1;s.tmr=120;s.sp2=1;s.emerged=0;msg('ALI
ENS ARE CHASING YOU',4)}
if(m==7){p.x=300;p.y=900;for(let i=0;i<[4,4,7]
[d];i++)E({k:'x',ty:'kun',x:rnd(700,1500),y:rnd(100,500),r:22,hp:[200,250,260]
[d],mx:[200,250,260][d],sp:[90,90,150][d],col:'#fc4',tt:rnd(1,3),st:Math.random()
<.5?1:-1,dmg:[25,25,100][d]});msg('You wake up in West Virginia. The Kuns
attack!',4)}
if(m==8){p.mh=150;p.hp=150;p.x=800;p.y=1000;s.holes=[];for(let
i=0;i<20;i++)s.holes.push({x:rnd(100,1500),y:rnd(100,1100)});const h=d==2?
3500:2500;s.boss=E({x:800,y:600,r:95,hp:h,mx:h,sp:60,col:'#2d6a2d',k:'x',ty:'plant
',nb:1,tt:2,sa:0,spin:0,scd:0,hc:0});s.en=[];s.ph=0;s.bs=0;s.rt=2;tw(3);if(d==2)
{HT(200,200);HT(1400,200)}msg('Destroy the towers.',4)}
if(m==9){p.x=800;p.y=1000;s.st=1;for(let i=0;i<6;i++){const
a=i*1.05;E({k:'r',x:800+Math.cos(a)*600,y:500+Math.sin(a)*400,hp:100,mx:100,sp:80,
col:'#a5f',st:i%2?1:-1,dmg:50})}msg('Flying Bastards! Purple magic!',4)}}
function upd2(dt,m,d,p){const c=s.cr;s.pf-=dt;
if(s.fin>0){s.fin-=dt;if(s.fin<=0)end(1,s.fm)}
for(const q of s.bm){if(q.src.hp<=0||(q.src.ty=='plant'&&s.bs!=1))
{q.t=0;continue}if(!q.fix){q.x=q.src.x;q.y=q.src.y}const ta=Math.atan2(p.y-
q.y,p.x-q.x);if(q.tr&&q.w>0){let da=ta-q.a;while(da>3.14)da-
=6.28;while(da<-3.14)da+=6.28;q.a+=cl(da,-q.tr*dt,q.tr*dt)}if(q.w>0)q.w-
=dt;else{q.t-=dt;const px=p.x-q.x,py=p.y-
q.y;if(px*Math.cos(q.a)+py*Math.sin(q.a)>0&&Math.abs(-
px*Math.sin(q.a)+py*Math.cos(q.a))<q.wd&&!q.h)
{q.h=1;hurt(q.dps*.6)}}}s.bm=s.bm.filter(q=>q.t>0);
for(const w of s.warn){w.t-=dt;if(w.t<=0&&!w.d)
{w.d=1;if(m==6)E(Object.assign(SEA(d,s.st),
{x:w.x,y:w.y}))}}s.warn=s.warn.filter(w=>w.t>0);
for(const e of s.en){const a=Math.atan2(p.y-e.y,p.x-e.x),dd=dist(e,p);
if(e.ty=='sea'&&e.pt==1){if(!e.j1){e.j0={x:e.x,y:e.y};e.j1=
{x:p.x,y:p.y};e.jp=0;e.jw=.35}if(e.jw>0){e.jw-=dt;e.jy=(1-
e.jw/.35)*12}else{e.jp+=dt/[.9,.9,.65][d];const g=Math.min(1,e.jp);e.x=e.j0.x+
(e.j1.x-e.j0.x)*g;e.y=e.j0.y+(e.j1.y-
e.j0.y)*g;e.jy=Math.sin(g*3.14)*70;e.atk=.2;if(g>.4&&!e.hit&&dd<e.r+20)
{hurt(e.dmg);e.hit=1}if(g>=1){e.x=e.y=-9999;e.hp=0}}}
else if(e.ty=='sea'){e.cd-=dt;if(dd>e.r+14)
{e.x+=Math.cos(a)*e.sp*dt;e.y+=Math.sin(a)*e.sp*dt}else if(e.cd<=0)
{hurt(e.dmg);e.cd=.8;e.atk=.35}}
else if(e.ty=='kun'){const dr=dd>340?1:dd<240?-1:0;e.x=cl(e.x+
(Math.cos(a)*dr+Math.cos(a+1.57)*.6*e.st)*e.sp*dt,20,WW-20);e.y=cl(e.y+
(Math.sin(a)*dr+Math.sin(a+1.57)*.6*e.st)*e.sp*dt,20,WH-20);e.tt-=dt;if(e.tt<=0)
{e.tt=d==2?2.2:4;e.atk=.35;if(d==2)B(e.x,e.y,p.x,p.y,330,100,'#c6f','e',8);else
s.bm.push({src:e,x:e.x,y:e.y,fix:1,a,t:1.6,w:.8,dps:25,wd:20,col:'#c6f',tr:0})}}
else if(e.ty=='tower'){e.tt-=dt;if(e.tt<=0&&dd<900){e.atk=.3;if(d==0)
{e.tt=1.8;B(e.x,e.y,p.x,p.y,380,12,'#333','e',7)}else if(d==1)
{e.tt=3;Z(p.x,p.y,55,1.8,40,'#9ff')}else{e.tt=3.2;if(Math.random()
<.5)s.bm.push({src:e,a,t:.8,w:.6,dps:75,wd:18,col:'#222',tr:0});else
Z(p.x,p.y,50,.9,50,'#f44')}}}
else if(e.ty=='htyu'){e.cd-=dt;e.tt-=dt;if(dd>e.r+16)
{e.x+=Math.cos(a)*e.sp*dt;e.y+=Math.sin(a)*e.sp*dt}else if(e.cd<=0)
{hurt(e.dmg);e.cd=.9;e.atk=.5}if(e.tt<=0)
{e.tt=2.6;e.atk=.4;B(e.x,e.y,p.x,p.y,300,20,'#c6f','e',7)}}}
if(m==5&&c&&c.hp>0){const dm=c.mx-c.hp;if(d==0)
{c.y=c.y0+Math.sin(s.t*2)*8;if(dm>=425&&!s.fin){s.fin=2.2;s.fm='The creature
vanishes.';msg('Well, good luck to you.',3);s.pf=1;c.hp=-1}}else{c.tt=(c.tt||0)-
dt;if(!c.gx||c.tt<=0)
{c.tt=.5;c.gx=c.x0+rnd(-250,250);c.gy=c.y0+rnd(-180,180)}c.x+=(c.gx-
c.x)*2.5*dt;c.y+=(c.gy-c.y)*2.5*dt;if(dm>0&&!s.cs)
{s.cs=1;s.lock=2.2;s.pf=1;msg('What the fuck? How the fuck are you
immortal?',3)}if(s.lock>0)p.y-=250*dt;else if(s.cs==1){s.cs=2;p.x=c.x-
90;p.y=c.y}if(dm>=500)c.lbl='??';if((dm>=500||s.t>120)&&!s.fin)
{s.fin=2.2;s.fm=d==2?'“You are not ready for what is to come.”':'The creature
vanishes in a purple flash.';msg(d==2?'You are not ready for what is to
come.':'Well, good luck for you.',3);s.pf=1;c.hp=-1}}}
if(m==6){if(s.st==1){s.tmr-=dt;s.hud='Swim! '+Math.ceil(s.tmr)+'s';s.sp2-
=dt;if(s.sp2<=0){s.sp2=[1.6,1.4,1.1]
[d];s.warn.push({x:cl(p.x+rnd(100,320),0,1560),y:cl(p.y+rnd(-260,260),20,1180),t:1
.1})}if(p.x>=1330){s.st=2;s.noFire=0;p.spd=230;s.en=[];s.warn=[];s.sp2=1;msg('The
island. No way off. Fight!',4)}if(s.tmr<=0)end(0,'You ran out of
time.')}else{const dx=p.x-1450,dy=p.y-600,dd=Math.hypot(dx,dy);if(dd>170)
{p.x=1450+dx/dd*170;p.y=600+dy/dd*170}s.sp2-
=dt;if(s.emerged<100&&s.en.length+s.warn.length<14&&s.sp2<=0){s.sp2=.4;const
an=rnd(0,6.28);s.warn.push({x:1450+Math.cos(an)*260,y:600+Math.sin(an)*260,t:.8});
s.emerged++}s.hud='Creatures left '+(100-
s.emerged+s.en.length+s.warn.length);if(s.emerged>=100&&!s.en.length&&!s.warn.leng
th)end(1,'You collapse and sleep on the rock. The tide carries you all the way to
West Virginia.')}}
if(m==7&&!s.en.length)end(1,'The Kuns fall. Something rumbles in the ground
ahead.');
if(m==8){const b=s.boss,a=Math.atan2(p.y-b.y,p.x-b.x),dd=dist(b,p);
if(s.tent){const q=s.tent,ta=Math.atan2(p.y-q.y,p.x-q.x);q.t-
=dt;q.x+=Math.cos(ta)*200*dt;q.y+=Math.sin(ta)*200*dt;if(dist(q,p)<26)end(0,'The
tentacle absorbed you.');if(q.t<=0)s.tent=null}
if(d==2){s.rt-=dt;if(s.rt<=0){s.rt=3;Z(p.x,p.y,36,.8,25,'#8a5')}}
if(s.must)
{b.x+=Math.cos(a)*900*dt;b.y+=Math.sin(a)*900*dt;if(dd<b.r+10)hurt(9999)}
else if(s.bs==0){if(!s.en.some(e=>e.ty=='tower')){s.bs=1;s.bt=[10,20,50]
[s.ph];b.x=800;b.y=600;s.en.push(b);b.atk=.6;msg('The head surfaces! Hit it
now!',3)}}
else{s.bt-=dt;s.hud='Head: '+Math.ceil(s.bt)+'s';b.scd-=dt;b.hc-=dt;if(b.spin>0)
{b.spin-
=dt;b.sa+=dt*30;b.x+=Math.cos(a)*260*dt;b.y+=Math.sin(a)*260*dt;if(Math.random()
<.5)s.fx.push({x:b.x+rnd(-100,100),y:b.y+rnd(-100,100),r:18,t:.35,t0:.35,c:'#6b4a2
a'});if(dd<b.r+60&&b.hc<=0){hurt(39);b.hc=.18}}
else{if(dd>120){b.x+=Math.cos(a)*b.sp*dt;b.y+=Math.sin(a)*b.sp*dt}b.tt-
=dt;if(b.tt<=0){b.tt=2;b.atk=.5;const r=Math.random();
if(r<.3){for(let
i=0;i<40;i++)Z(rnd(60,1540),rnd(60,1140),44,1.6,30,'#f44');for(let
i=0;i<5;i++)Z(p.x+rnd(-130,130),p.y+rnd(-130,130),44,1.6,30,'#f44');msg('BRACHER!'
,1)}
else if(r<.55){if(d==1)for(const o
of[-.45,0,.45])s.bm.push({src:b,a:a+o,t:1.8,w:.6,dps:50,wd:22,col:'#4af',tr:0});el
se s.bm.push({src:b,a,t:1.8,w:.6,dps:50,wd:22,col:'#4af',tr:.7})}
else if(r<.62&&!s.tent)s.tent={x:b.x,y:b.y,t:3};
else if(r<.8&&b.scd<=0){b.spin=3;b.scd=d==1?10:2;msg('Spinning!',1)}
else if(d==1&&r<.9){if(dd<200)hurt(30);else for(let
i=-2;i<3;i++)B(b.x,b.y,p.x+i*60,p.y,320,14,'#9ff','e',7)}
else Z(p.x,p.y,60,1.2,30,'#f44')}}
if(s.bt<=0){if(s.ph==2){s.must=1;msg('YOU MUST
DIE',6)}else{s.en=s.en.filter(x=>x!=b);s.bm=s.bm.filter(q=>q.src!=b);s.ph++;s.bs=0
;s.hud='';tw([3,5,10][s.ph]);msg('Destroy '+[3,5,10][s.ph]+' towers.',3)}}}}
if(m==9){if(s.st==1&&!s.en.length){s.st=2;s.ch={x:800,y:600,n:0};s.parts=
[{x:rnd(150,500),y:rnd(150,450)},{x:rnd(1100,1500),y:rnd(150,450)},
{x:rnd(400,1200),y:rnd(850,1100)}];p.car=0;msg('A gray, half-built vehicle. Find
its missing parts.',5)}
if(s.st==2){for(const q of s.parts)if(!q.t&&Math.hypot(q.x-p.x,q.y-p.y)<28)
{q.t=1;p.car++}if(p.car>0&&dist(s.ch,p)<60){s.ch.n+=p.car;p.car=0}s.hud='Tank
parts '+s.ch.n+'/3'+(p.car?' (carrying '+p.car+')':'');if(s.ch.n>=3)end(1,'The
tank is finished. The engine roars.')}}}
function gdraw(){if(M>=10)gdraw3();if(M==6)
{R(0,0,110,WH,'#c4a86c');R(1290,470,320,260,'#6b6a66');R(1310,490,280,220,'#7a7974
')}
if(M==8)for(const h of s.holes){R(h.x-16,h.y-11,32,22,'#1a120a');R(h.x-11,h.y-
7,22,14,'#000')}
if((M==9||M==10)&&s.ch){const c=s.ch;R(c.x-54,c.y-36,108,12,'#2c2c2c');R(c.x-
54,c.y+24,108,12,'#2c2c2c');R(c.x-48,c.y-26,96,52,'#7a7d80');if(c.n>=1)R(c.x-
34,c.y-20,68,40,'#8f9396');if(c.n>=2)R(c.x-16,c.y-
16,32,32,'#5d6266');if(c.n>=3)R(c.x,c.y-4,64,8,'#444');for(const q of
s.parts)if(!q.t){R(q.x-14,q.y-14,28,28,q.c?'#b55':'#9a9d7a');R(q.x-6,q.y-
6,12,12,'#555')}}}
function fdraw(){if(M>=10)fdraw3();for(const q of s.bm)
{X.save();X.translate(q.x,q.y);X.rotate(q.a);if(q.w>0)
{X.globalAlpha=.4;X.fillStyle='#f44';X.fillRect(0,-2,900,4)}else{X.fillStyle=q.col
;X.fillRect(0,-q.wd,900,q.wd*2);X.fillStyle='#fff9';X.fillRect(0,-
q.wd/3,900,q.wd*.66)}X.restore()}
if(s.tent){const b=s.boss,q=s.tent;for(let i=0;i<=12;i++){const f=i/12;R(b.x+(q.x-
b.x)*f-7,b.y+(q.y-b.y)*f-7+Math.sin(i+s.t*8)*5,14,14,i==12?'#c6f':'#2d6a2d')}}}
function spr2(e,a){const
t=s.t,f=e.fl>0,c=f?'#fff':e.col,w=Math.sin(t*12+e.x)*4,ty=e.ty;
if(ty=='moose')
{R(-18,-14+w*.2,40,28,c);R(20,-8,18,16,c);R(30,-22,4,14,'#d8d0b0');R(30,8,4,14,'#d
8d0b0');R(-14,-18,6,6,'#6f6');R(-6,10,8,6,'#6f6');R(30,-4,4,4,'#6f6');for(let
k=0;k<2;k++){R(-12+k*22,-18-
w*.4,6,8,'#3a2412');R(-12+k*22,12+w*.4,6,8,'#3a2412')}return}
if(ty=='human'){R(-5,-6,10,12,c);R(-3,-3,6,6,'#d2a679');return}
if(ty=='animal'){R(-9,-5,18,10,c);R(8,-3,6,6,c);R(-9,-7+w*.3,3,3,c);R(-9,5-
w*.3,3,3,c);return}
if(ty=='beast')
{R(-26,-22,52,44,c);R(-18,-34,36,14,c);R(20,-10,16,20,c);R(28,-6,4,4,'#f00');R(-34
,-26,10,14,c);R(-34,12,10,14,c);return}
if(ty=='kuto')
{R(-70,-50,140,100,'#8a6d1a');R(-60,-45,120,90,c);R(-90,-34,24,70,c);R(66,-34,24,7
0,c);R(50,-18,30,36,'#e8c050');R(66,-8,8,8,'#f0f');R(-50,50,30,26,'#6a5214');R(20,
50,30,26,'#6a5214');R(-30,-50,60,14,'#e8c050');return}
if(ty=='fgiant'){spr2(Object.assign({},e,{ty:'kun'}),a);return}
if(ty=='chain'){X.scale(.75,.75);spr(Object.assign({},e,
{ty:0,k:'boss'}),a);R(-20,-30,22,16,'#666');R(6,-26,18,14,'#777');return}
if(ty=='avatar'||ty=='real'){X.rotate(-a);X.scale(ty=='real'?1.5:1.1,ty=='real'?
1.5:1.1);spr(Object.assign({},e,{ty:0,k:'fung'}),a);return}
if(ty=='htyu'){spr(Object.assign({},e,{ty:0,k:'boss'}),a);return}
if(ty=='imm'&&e.half)
{R(-26,-26,52,26,'#b6f4');R(-12,-12,24,12,f?'#fff':'#e8ddff');for(let
k=0;k<5;k++)R(-10+k*5,0,4,3+
((t*4+k*1.7)%3)*3,'#e8ddff88');R(14,-6,8,8,'#c4f');for(let k=0;k<2;k++)R(-8-
k*5,-18-k*6-w,5,14+k*3,'#fff9');return}
if(ty=='imm'){R(-26,-26,52,52,D==2?'#6f64':'#b6f4');for(let k=0;k<4;k++){R(-8-
k*5,-18-k*6-w,5,14+k*3,'#fff9');R(-8-
k*5,4+k*6+w,5,14+k*3,'#fff9')}R(-12,-12,24,24,f?'#fff':D==2?'#cfc':'#e8ddff');R(14
,-4,9,9,D==2?'#4f4':'#c4f');R(16,-2,5,5,'#fff');if(D==2)for(let i=0;i<16;i++)
{const g=i*.39,r2=100-Math.abs(Math.sin(t*2+i))*22;X.save();X.rotate(-
a);R(Math.cos(g)*r2-4,Math.sin(g)*r2-4,9,9,'#3a8a2a');R(Math.cos(g)*
(r2+14)-3,Math.sin(g)*(r2+14)-3,6,6,'#2d6a2d');X.restore()}return}
if(ty=='sea'){if(D==0){R(-8,-22-
w,5,14,'#6a5a7a');R(-8,8+w,5,14,'#6a5a7a');R(-14,-9,28,18,c);R(12,-20+w*.3,16,5,'#
ddd');R(12,15-w*.3,16,5,'#ddd');R(10,-6,12,12,c);for(let
k=0;k<3;k++)R(18,-5+k*4,4,2,'#fff');R(14,-4,3,3,'#f00')}else if(D==1)
{R(-14,-16,12,5,'#cba');R(-14,11,12,5,'#cba');R(-12,-12,24,24,c);R(-6,-6,8,8,'#6f4
');for(let
k=0;k<4;k++)R(Math.cos(k*1.57+.8)*14,Math.sin(k*1.57+.8)*14,10,4,c);R(12,-3,6,6,'#
fff')}else{R(-14,-12+w*.3,28,24-
w*.3,c);R(-8,-6,10,10,'#1a0a0a');R(2,2,8,8,'#2a0a0a');R(-12,6,6,6,'#2a0a0a');R(8,-
8,5,5,'#fb0')}return}
if(ty=='kun'){R(-16,-16,32,32,'#ffd24a44');for(let k=0;k<3;k++){R(-6-k*5,-12-k*6-
w,5,12+k*3,'#ffe27a');R(-6-
k*5,6+k*6+w,5,12+k*3,'#ffe27a')}R(-9,-9,18,18,f?'#fff':'#ffd24a');R(6,-3,5,6,'#a0f
');return}
if(ty=='tower')
{R(-12,-12,24,24,f?'#fff':'#2f5a2a');R(-6,-18,12,8,'#3f7a35');R(-6,10,12,8,'#3f7a3
5');R(-5,-5,10,10,'#fff');R(1,-2,5,5,'#000');return}
if(ty=='plant'){X.rotate(-a+(e.sa||0));for(let i=0;i<7;i++){const
g=i*.9+Math.sin(t+i)*.2;R(Math.cos(g)*72-11,Math.sin(g)*72-
11,22,22,i%2?'#c9f':'#8be')}for(let i=0;i<8;i++){const g=i*.785;R(Math.cos(g)*58-
14,Math.sin(g)*58-
14,28,28,i%2?'#1d4d1d':'#3f9a35')}R(-50,-50,100,100,f?'#fff':'#2d6a2d');for(let
i=0;i<5;i++){const g=i*1.26;R(Math.cos(g)*22-7,Math.sin(g)*22-
7,14,14,'#fff');R(Math.cos(g)*22-3,Math.sin(g)*22-3,6,6,'#d00')}for(let
i=0;i<10;i++){let px=Math.cos(i*.63)*50,py=Math.sin(i*.63)*50;for(let j=0;j<4;j++)
{px+=Math.cos(i*.63+Math.sin(t*3+i+j)*.4)*12;py+=Math.sin(i*.63+Math.sin(t*3+i+j)*
.4)*12;R(px-4,py-4,8,8,'#3f8a35')}}}}
const LN=(x,y)=>E({x,y,hp:60,mx:60,sp:150,r:18,col:'#3c3',dmg:30,rg:42});
const FL=(x,y)=>E({k:'r',x,y,hp:60,mx:60,mhp:150,sp:80,col:'#3af',dmg:35});
const BH=
(x,y,hp,nm)=>E({k:'x',ty:'bigh',x,y,r:60,hp,mx:hp,sp:70,col:'#fc0',tt:rnd(1,2.5),n
m});
const KU=
(x,y)=>E({k:'x',ty:'kuto',x,y,r:110,hp:2000,mx:2000,sp:45,col:'#c9a02a',tt:2,nb:1,
nm:'Giant Kuto'});
const FG=
(x,y)=>E({k:'x',ty:'fgiant',x,y,r:30,hp:200,mx:200,sp:80,col:'#4c4',tt:rnd(1,3)});
const MO=
(x,y)=>E({k:'x',ty:'moose',x,y,r:34,hp:500,mx:500,sp:260,col:'#5a3a22',dmg:15,ms:'
c',mt:rnd(4,7)});
const KN=
(x,y)=>E({k:'x',ty:'kun',x,y,r:22,hp:250,mx:250,sp:100,col:'#fc4',tt:rnd(1,3),dmg:
25});
function init3(m,d,p){s.warn=[];s.bm=
[];p.x=800;p.y=1000;p.wep='gold';p.mode=2;p.mh=150;p.hp=150;p.cap=150;p.rgT=10;p.r
gA=10;s.stg=0;s.n3=0;s.sp3=0;
if(m>=12&&m<=16){const hp=m>=14?2000:1000;Object.assign(p,
{tank:1,wep:'tank',mode:1,spd:185,mh:hp,hp:hp,cap:hp,rgT:25,rgA:100,ex:1,pb:m>=14?
1:0})}
if(m==10){s.parts=[];s.ch={x:800,y:600,n:0};for(let
i=0;i<8;i++)s.parts.push({x:rnd(100,1500),y:rnd(100,1100),c:i>4});msg('Find the
tank parts and the explosion chambers.',5)}
if(m==11){s.trees=[];for(let
i=0;i<30;i++)s.trees.push({x:rnd(80,1520),y:rnd(120,1100)});MO(300,200);MO(1300,20
0);msg('Two mutated moose. Find gas for the tank.',4)}
if(m==12)msg(d==0?'50 Green Longnecks attack!':d==1?'Bosses incoming!':'Chained
creatures ahead!',4);
if(m==13)s.cr=E({x:900,y:450,r:34,hp:1e6,mx:1e6,sp:0,col:'#b6f',k:'x',ty:'imm',hal
f:1,nb:1});
if(m==14){p.y=1120;msg('Keep walking.',3)}
if(m==15){s.bld=[];for(let i=0;i<14;i++)s.bld.push({x:100+
(i%5)*290+rnd(-20,20),y:100+((i/5)|0)*380+rnd(-20,20),w:90,h:90,hp:300});for(let
i=0;i<30;i++)E({k:'x',ty:'human',x:rnd(60,1540),y:rnd(60,1140),r:8,hp:20,mx:20,sp:
90,col:['#c44','#48c','#4a4','#cc4'][i%4],gun:i%3==0,wx:rnd(0,6)});for(let
i=0;i<10;i++)E({k:'x',ty:'animal',x:rnd(60,1540),y:rnd(60,1140),r:10,hp:40,mx:40,s
p:70,col:'#7a5a3a',wx:rnd(0,6)});for(let
i=0;i<3;i++)E({k:'x',ty:'beast',x:rnd(200,1400),y:rnd(100,500),r:34,hp:400,mx:400,
sp:70,col:'#6a6a80',dmg:40,cd:0});msg('“Kill everything.”',5)}
if(m==16){if(d==0)
{s.boss=E({x:800,y:250,r:100,hp:7000,mx:7000,sp:35,k:'x',ty:'avatar',nb:1,tt:2,nm:
'The Alien Fungus'});for(let
i=0;i<3;i++)E({k:'x',ty:'beast',x:300+i*500,y:150,r:40,hp:600,mx:600,sp:60,col:'#7
a6a8a',dmg:80,cd:0});msg('The final
boss!',4)}else{p.x=400;p.y=600;s.fz=-120;s.tmr=120;msg('RUN through the
corridor!',4)}}
if(m==23)s.cr=E({x:900,y:450,r:34,hp:1e6,mx:1e6,sp:0,col:'#b6f',k:'x',ty:'imm',nb:
1});
if(m==24){Object.assign(p,
{wep:'knife',mh:500,hp:500,cap:0,rgT:0,rgA:0,spd:230});s.boss=E({x:800,y:300,r:120
,hp:d==2?10000:9500,mx:d==2?10000:9500,sp:50,k:'x',ty:'real',nb:1,tt:2,nm:'The
REAL Alien Fungus'});msg('Only the Blood Knife. 500 damage per hit.',5)}}
function upd3(dt,m,d,p){
for(const e of s.en){const a=Math.atan2(p.y-e.y,p.x-e.x),dd=dist(e,p);e.cd-
=dt;e.tt-=dt;
if(e.ty=='moose'){if(e.ms=='c'){if(dd>e.r+16)
{e.x+=Math.cos(a)*e.sp*dt;e.y+=Math.sin(a)*e.sp*dt}else if(e.cd<=0)
{hurt(15);e.cd=.7;e.atk=.35}e.mt-=dt;if(e.mt<=0){let bt=null,bd=500;for(const q of
s.trees||[]){const dq=dist(e,q);if(dq<bd){bd=dq;bt=q}}if(bt)
{e.tg=bt;e.ms='t';e.mt=1.6;e.ar=0}else e.mt=3}}
else if(e.ms=='t'){const tg=e.tg,dq=dist(e,tg);if(dq>12){e.x+=(tg.x-
e.x)/dq*520*dt;e.y+=(tg.y-e.y)/dq*520*dt}else e.ar=1;if(e.ar){e.jy=36;e.mt-
=dt;if(e.mt<=0){e.ms='l';e.j0={x:e.x,y:e.y};e.j1={x:p.x,y:p.y};e.jp=0;e.hit=0}}}
else{e.jp+=dt/.6;const g=Math.min(1,e.jp);e.x=e.j0.x+(e.j1.x-e.j0.x)*g;e.y=e.j0.y+
(e.j1.y-e.j0.y)*g;e.jy=36*(1-g)+Math.sin(g*3.14)*50;if(g>.5&&!e.hit&&dd<e.r+24)
{hurt(15);e.hit=1}if(g>=1){e.ms='c';e.mt=rnd(5,8);e.jy=0}}}
else if(e.ty=='bigh'){if(e.an&&e.an.hp<=0)e.an=null;if(e.an)
{e.x=e.an.x+e.ox;e.y=e.an.y+e.oy}else if(dd>e.r+30)
{e.x+=Math.cos(a)*e.sp*dt;e.y+=Math.sin(a)*e.sp*dt}else if(e.cd<=0)
{hurt(60);e.cd=1;e.atk=.5}if(e.tt<=0){e.tt=2;e.atk=.5;const bl=Math.random()
<.5;B(e.x,e.y,p.x,p.y,300,bl?80:40,bl?'#38f':'#f73','e',8)}}
else if(e.ty=='kuto'){if(dd>e.r+40)
{e.x+=Math.cos(a)*e.sp*dt;e.y+=Math.sin(a)*e.sp*dt}else if(e.cd<=0)
{hurt(100);e.cd=1.6;e.atk=.6}if(e.tt<=0){e.tt=2.2;e.atk=.5;const bl=Math.random()
<.5;B(e.x,e.y,p.x,p.y,300,bl?100:60,bl?'#38f':'#f93','e',9)}}
else if(e.ty=='chain'){if(dd>e.r+30)
{e.x+=Math.cos(a)*e.sp*dt;e.y+=Math.sin(a)*e.sp*dt;const ad=Math.hypot(e.x-
e.ax,e.y-e.ay);if(ad>300){e.x=e.ax+(e.x-e.ax)/ad*300;e.y=e.ay+(e.y-
e.ay)/ad*300}}else if(e.cd<=0){hurt(e.dmg);e.cd=1.3;e.atk=.5}}
else if(e.ty=='fgiant'){const dr=dd>380?1:dd<260?-1:0;e.x=cl(e.x+
(Math.cos(a)*dr+Math.cos(a+1.57)*.5)*e.sp*dt,20,WW-20);e.y=cl(e.y+
(Math.sin(a)*dr+Math.sin(a+1.57)*.5)*e.sp*dt,20,WH-20);if(e.tt<=0)
{e.tt=3;s.bm.push({src:e,x:e.x,y:e.y,fix:1,a,t:1.2,w:.8,dps:30,wd:18,col:'#4f4',tr
:0})}}
else if(e.ty=='human'||e.ty=='animal'){if(dd<350){e.x-=Math.cos(a)*e.sp*dt;e.y-
=Math.sin(a)*e.sp*dt}else{e.wx+=rnd(-1,1)*dt*3;e.x+=Math.cos(e.wx)*e.sp*.4*dt;e.y+
=Math.sin(e.wx)*e.sp*.4*dt}e.x=cl(e.x,20,WW-20);e.y=cl(e.y,20,WH-
20);if(e.gun&&e.tt<=0&&dd<500){e.tt=2;B(e.x,e.y,p.x,p.y,320,4,'#ff8','e',4)}}
else if(e.ty=='beast'){if(dd>e.r+28)
{e.x+=Math.cos(a)*e.sp*dt;e.y+=Math.sin(a)*e.sp*dt}else if(e.cd<=0)
{hurt(e.dmg);e.cd=.9;e.atk=.4}}}
if(m==10){for(const q of s.parts)if(!q.t&&Math.hypot(q.x-p.x,q.y-p.y)<28){q.t=1;
(p.cl=p.cl||[]).push(q.c)}if(p.cl&&p.cl.length&&dist(s.ch,p)<60){for(const f of
p.cl){s.ch.n++;if(f)s.ch.cc=(s.ch.cc||0)+1}p.cl=[]}const
cc=s.ch.cc||0;s.hud='Parts '+(s.ch.n-cc)+'/5 Chambers
'+cc+'/3';if(s.ch.n>=8)end(1,'Your first Slop Tank is built. It is gray, and now
it can explode.')}
if(m==11&&!s.en.some(e=>e.ty=='moose'))end(1,'Their blood is pure gas. In a
cutscene you fill the gas container and pour it into the tank. It is fueled.');
if(m==12){const L=s.stg;if(L==0){if(d==0){s.sp3-
=dt;if(s.n3<50&&s.en.length<10&&s.sp3<=0){s.sp3=.7;s.n3++;const
an=rnd(0,6.28);LN(cl(p.x+Math.cos(an)*600,20,1580),cl(p.y+Math.sin(an)*600,20,1180
))}if(s.n3>=50&&!s.en.length){s.stg=1;s.boss=BH(800,200,1600,'HTYU');msg('A giant
monster from Virginia!',4)}}
else{if(!s.n3){s.n3=1;if(d==1){for(let
i=0;i<3;i++)BH(300+i*500,200,500,'Boss')}else{for(let i=0;i<6;i++){const
ax=200+i*250,ay=300+
(i%2)*200;E({k:'x',ty:'chain',x:ax,y:ay,r:36,hp:700,mx:700,sp:75,col:'#6a4a32',dmg
:100,cd:0,ax,ay})}}msg(d==1?'Three bosses attack!':'Chained creatures carrying
rocks!',4)}
else if(!s.en.length){s.stg=1;const k=KU(800,200);s.boss=k;for(let i=0;i<(d==1?
1:2);i++){const h=BH(k.x,k.y,500,'HTYU');h.an=k;h.ox=(i?1:-1)*130;h.oy=50}msg('The
Giant Kuto!',4)}}}
else{if(d==0&&s.boss.hp<=1000&&!s.fl){s.fl=1;for(let
i=0;i<4;i++)FL(rnd(100,1500),100);msg('Flying Bastards
arrive!',3)}if(d==2&&s.boss.ty=='kuto'&&s.boss.hp<=500&&!s.fg){s.fg=1;for(let
i=0;i<3;i++)FG(rnd(200,1400),100);msg('Flying giants!',3)}if(!s.en.length)
{if(d==0&&!s.gk){s.gk=1;s.boss=KU(800,200);msg('The Giant Kuto!',4)}else
end(1,'Every enemy is down and your tank is still rolling.')}}}
if(m==13){const c=s.cr,t=s.t;c.y=450+Math.sin(t*2)*8;if(t>1&&!s.a1)
{s.a1=1;msg('“The fungus is the God of the New World.”',4)}if(t>5&&!s.a2)
{s.a2=1;s.pf=1;s.lock=2.5;s.sh=1;p.hp=60;msg('...',2)}if(t>9&&!s.a3)
{s.a3=1;s.pf=1;p.mh=2000;p.hp=2000;p.cap=2000;p.pb=1;msg('Tank upgraded: 2,000 HP
and Purple Blast (2 or right-click).',5)}if(t>14&&!s.fin){s.fin=1.5;s.fm='The
Immortal vanishes again. Your tank is stronger.';c.hp=-1;s.pf=1}}
if(m==14){if(p.y<700&&!s.a1){s.a1=1;s.t0=s.t;s.lock=7;msg('The REAL Alien Fungus.
You cannot even see all of it.',3)}if(s.a1){const u=s.t-s.t0;if(u>3&&!s.a2)
{s.a2=1;msg('“I’ll give you your tank. I feel that confident. Have your puny
object.”',4)}if(u>7&&!s.fin){s.pf=1;s.fin=1.5;s.fm='The Alien Fungus sends you and
your tank flying all the way to New York.'}}}
if(m==15){for(const b of s.b)if(b.own=='p'&&b.l>0)for(const bl of
s.bld)if(bl.hp>0&&b.x>bl.x&&b.x<bl.x+bl.w&&b.y>bl.y&&b.y<bl.y+bl.h){bl.hp-=b.dmg*
(b.sp?
1.5:1);b.l=0;s.fx.push({x:b.x,y:b.y,r:40,t:.35,t0:.35,c:'#fb4'});if(bl.hp<=0)s.fx.
push({x:bl.x+45,y:bl.y+45,r:70,t:.6,t0:.6,c:'#fa3'})}const
left=s.en.length+s.bld.filter(b=>b.hp>0).length;s.hud='Left to destroy:
'+left;if(!left)end(1,'Everything in the settlement is destroyed.')}
if(m==16&&d>0){s.tmr-=dt;s.hud='Survive
'+Math.max(0,Math.ceil(s.tmr))+'s';p.y=cl(p.y,330,870);if(s.tmr>0){s.fz+=(p.mv?
160:235)*dt;if(p.x-s.fz<150)end(0,'The Alien Fungus caught you.');s.sp3-
=dt;if(s.sp3<=0)
{s.sp3=.9;Z(p.x+rnd(100,450),rnd(340,860),60,1.3,200,'#f44');Z(p.x+rnd(-50,250),p.
y+rnd(-120,120),55,1.3,200,'#f44')}}
if(p.x>1400){const dx=1100;p.x-=dx;s.fz-=dx;for(const z of s.z)z.x-=dx;for(const b
of s.b)b.x-=dx}
if(s.tmr<=0&&!s.fin)
{E({k:'x',ty:'imm',x:p.x+330,y:p.y,r:34,hp:1e6,mx:1e6,sp:0,col:'#b6f',nb:1});s.fin
=4;s.fm='The Immortal sends you straight to Mission 24.';msg('“I am going to send
you to Mission 24.”',4);s.pf=1}}
if(m==16&&d==0){const b=s.boss;if(b.hp<=0){if(!s.over)end(1,'The final boss falls.
The Alien Fungus is defeated. This is the Easy Mode ending.')}else{const
a=Math.atan2(p.y-b.y,p.x-b.x),dd=dist(b,p);if(dd>380)
{b.x+=Math.cos(a)*b.sp*dt;b.y+=Math.sin(a)*b.sp*dt}b.tt-=dt;if(b.tt<=0)
{b.tt=1.6;b.atk=.5;const r=Math.random();if(r<.25){for(let
i=0;i<6;i++)Z(p.x+rnd(-200,200),p.y+rnd(-200,200),60,1.6,100,'#9ff')}else
if(r<.5)B(b.x,b.y,p.x,p.y,340,90,'#c6f','e',9);else if(r<.7){for(let
i=-1;i<2;i++)B(b.x,b.y,p.x+i*90,p.y,380,60,'#fd0','e',7)}else
if(r<.85)s.bm.push({src:b,x:b.x,y:b.y,fix:1,a,t:1.5,w:.8,dps:60,wd:22,col:'#c6f',t
r:0});else{FL(b.x+rnd(-200,200),b.y+100);FL(b.x+rnd(-200,200),b.y+100)}}s.sp3-
=dt;if(s.sp3<=0){s.sp3=14;for(let
i=0;i<4;i++)FL(rnd(100,1500),80)}if(b.hp<=3500&&!s.fg){s.fg=1;for(let
i=0;i<3;i++)FG(rnd(200,1400),100);msg('Flying giants!',3)}}}
if(m==23){const c=s.cr;c.y=450+Math.sin(s.t*2)*8;if(s.t>1&&!s.a1)
{s.a1=1;msg('“Your death is awaiting.”',4)}if(s.t>6&&!s.fin){s.fin=1.5;s.fm='The
Immortal disappears. The final mission is next.';c.hp=-1;s.pf=1}}
if(m==24){const b=s.boss;if(b.hp<=0){if(!s.over)end(1,'THE REAL ALIEN FUNGUS IS
DEAD. The Blood Knife made of pure hatred did it. The full ending of the
game.')}else{const a=Math.atan2(p.y-b.y,p.x-b.x),dd=dist(b,p),X2=d==2?
10:5;if(dd>260){b.x+=Math.cos(a)*b.sp*dt;b.y+=Math.sin(a)*b.sp*dt}b.tt-
=dt;if(b.tt<=0){b.tt=1.4;b.atk=.5;const r=Math.random();
if(r<.2)Z(p.x,p.y,70,1.5,50*X2,'#9ff');else
if(r<.35)s.bm.push({src:b,a,t:2,w:.7,dps:20*X2,wd:24,col:'#4f4',tr:.5});else
if(r<.5)Z(p.x,p.y,40,.9,70*X2,'#f44');else
if(r<.62)s.bm.push({src:b,x:b.x,y:b.y,fix:1,a,t:.4,w:.9,dps:40*X2,wd:34,col:'#c9f'
,tr:0});else if(r<.74){for(let
i=0;i<30;i++)Z(rnd(60,1540),rnd(60,1140),44,1.6,30*X2,'#f44')}else
if(r<.86)B(b.x,b.y,p.x,p.y,330,50*X2,'#c6f','e',9);else
Z(p.x,p.y,36,.8,25*X2,'#8a5')}
s.sp3-=dt;if(s.sp3<=0&&s.en.length<10){s.sp3=5;const an=rnd(0,6.28);[LN,FL,MO,KN]
[(Math.random()*4)|0]
(cl(p.x+Math.cos(an)*650,30,1570),cl(p.y+Math.sin(an)*650,30,1170))}}}}
function gdraw3(){const t=s.t;
if(M==11)for(const q of s.trees){R(q.x-5,q.y,10,16,'#4a2f18');R(q.x-22,q.y-
30,44,34,'#2f6a2f');R(q.x-14,q.y-40,28,14,'#3f8a3f')}
if(M==14){R(0,0,WW,420,'#3a1f52');for(let i=0;i<14;i++)R((i*131)%1500,
(i*97)%360,160,90,i%2?'#4f2a6a':'#5f3480');for(let i=0;i<500;i++){const x=
(i*73)%WW,y=(i*131)%410;R(x,y,7,7,'#fff');R(x+2+((i+
(t*2|0))%2),y+2,3,3,'#d00')}R(0,420,WW,12,'#6a3a8a');for(let i=0;i<20;i++)
{R(i*80+10,440,60,50,'#555');R(i*80+14,444,52,42,'#2a2a2a');R(i*80+24,458,10,10,'#
a86');R(i*80+42,462,10,8,'#8a8')}for(let i=0;i<30;i++)R((i*97+t*
(40+i%3*20))%WW,500+(i%5)*14,12,10,i%2?'#d33':'#3d3')}
if(M==15)for(const b of s.bld){if(b.hp>0){R(b.x,b.y,b.w,b.h,'#6a6a70');for(let
i=0;i<3;i++)for(let
j=0;j<3;j++)R(b.x+10+i*26,b.y+10+j*26,14,14,'#d8d080');R(b.x,b.y,b.w,8,'#4a4a50')}
else{R(b.x,b.y+b.h-20,b.w,20,'#33302c');R(b.x+10,b.y+b.h-34,30,16,'#44403a')}}
if(M==16&&D>0)
{R(0,0,WW,300,'#3a3a36');R(0,900,WW,300,'#3a3a36');R(0,290,WW,12,'#222');R(0,900,W
W,12,'#222');R(s.fz-420,0,440,WH,'#3a1f52');for(let i=0;i<60;i++){const y=
(i*97)%WH;R(s.fz-60-(i%5)*70,y,8,8,'#fff');R(s.fz-58-(i%5)*70,y+2,3,3,'#d00')}}}
function fdraw3(){for(const e of s.en){if(e.ty=='chain')for(let i=0;i<=8;i++)
{const f=i/8;R(e.ax+(e.x-e.ax)*f-3,e.ay+(e.y-e.ay)*f-3,6,6,'#aaa')}if(e.an)for(let
i=0;i<=6;i++){const f=i/6;R(e.x+(e.an.x-e.x)*f-3,e.y+(e.an.y-e.y)*f-
3,6,6,'#b8a')}}}
function tankDraw(p,a)
{X.save();X.translate(p.x,p.y);R(-24,-18,50,40,'#0004');X.rotate(p.ba||0);R(-26,-2
0,52,9,'#2c2c2c');R(-26,11,52,9,'#2c2c2c');for(let i=0;i<6;i++)
{R(-24+i*9,-20,3,9,'#555');R(-24+i*9,11,3,9,'#555')}R(-22,-12,44,24,s.sh>0?'#c88':
'#8a8d90');X.rotate(a-
(p.ba||0));R(-10,-10,22,20,'#6e7276');R(8,-4,32,8,'#4a4d50');R(38,-5,6,10,p.ex?'#c
33':'#333');if(p.pb)R(-6,-6,8,8,'#d9f');X.restore()}
function soldierOld(p,a)
{X.save();X.translate(p.x,p.y);R(-8,-6,22,18,'#0004');X.rotate(a);R(-5,-10,10,20,p
==s.p?
(s.sh>0?'#e66':'#3d6a9a'):'#4a5a2a');R(-4,-5,9,10,'#2f3a1f');R(3,-3,3,6,'#d2a679')
;R(0,-8,5,4,'#d2a679');R(2,-7,28,4,p.wep=='gold'?'#fd0':p.wep=='rifle'?'#222':p.pc
);R(24,-8,6,6,'#555');X.restore()}
function spr(e,a){const
t=s.t,w=Math.sin(t*9+e.x*.05)*3,f=e.fl>0,c=f?'#fff':e.col,r=e.r,at=e.atk>0?
e.atk/.35:0;
if(e.ty){spr2(e,a);return}if(e.k=='fung'){const n=D>0?40:14,ex=1+(e.atk>0?
e.atk*1.2:0);for(let i=0;i<n;i++){let
ang=i*6.283/n,px=Math.cos(ang)*r*.55,py=Math.sin(ang)*r*.55;for(let j=0;j<6;j++)
{ang+=Math.sin(t*2+i*1.7+j*.6)*.3;px+=Math.cos(ang)*14*ex;py+=Math.sin(ang)*14*ex;
R(px-5,py-5,10-j,10-j,j==5?'#fe8':j%2?'#c9f':'#8be')}}for(let i=0;i<12;i++){const
q=i*.9;R(Math.cos(q)*r*.5-16,Math.sin(q)*r*.5-
16,34,34,f?'#fff':i%2?'#a6e':'#7ad')}R(-45,-45,90,90,f?'#fff':'#9a6fe0');for(let
i=0;i<7;i++){const x2=Math.cos(i*.9+1)*r*.5,y2=Math.sin(i*.9+1)*r*.5;R(x2-7,y2-
7,14,14,'#fff');R(x2-3+Math.cos(a)*3,y2-3+Math.sin(a)*3,6,6,'#000')}return}
if(e.k=='boss'){const hl=e.atk>0?Math.sin(e.atk/.5*3.14)*18:0,mo=e.atk>0?
7:0,lw=Math.sin(t*6)*6;for(const[y,x,k]of[[-42,-35,1],[-42,15,-1],[32,-35,-1],
[32,15,1]])R(x+lw*k,y,18,12,'#222');R(-52,-30,92,60,c);for(let
i=0;i<4;i++)R(-46+i*23,-30,9,60,'#111');for(let
i=0;i<6;i++)R(-40+i*14,-34,6,6,'#b90');R(38,-9,40+hl*.5,18,c);R(76+hl,-15,32,30,c)
;R(80+hl,-12,6,6,'#f00');R(80+hl,6,6,6,'#f00');R(100+hl,-8-
mo,14,6,'#a22');R(100+hl,2+mo,14,6,'#a22');if(mo)
{R(114+hl,-6,12,12,'#f93');R(122+hl,-3,10,6,'#ff7')}return}
if(e.k=='r'){const wf=Math.sin(t*(e.atk>0?
22:14)+e.x*.1)*6,mt=e.mhp>0,rc=f?'#fff':'#7a5230';
if(D==2){for(let k=0;k<3;k++){R(-12+k*7,-14-k*5-
wf,5,12+k*3,'#8a1414');R(-12+k*7,2+k*5+wf,5,12+k*3,'#8a1414')}R(-12,-7,26,14,c);R(
10,-5,6,4,'#000');R(10,1,6,4,'#000');R(-16,-3,5,6,'#611');if(e.atk>0)R(16,-3,10,6,
'#f55');return}
if(mt){const mc=D==1?'#a8841a':'#3a7a3a';for(let k=0;k<5;k++){const L=10+(4-
k)*4;R(-20+k*7,-9-L-
wf,5,L,'#2f6a2f');R(-20+k*7,9+wf,5,L,'#2f6a2f')}R(-26,-9,42,18,mc);for(let
k=0;k<4;k++)R(-20+k*9,-12,3,4,'#8f8');R(14,-4,22,8,mc);R(34,-7,16,14,mc);R(44,-4,3
,3,'#000');for(let k=0;k<2;k++){R(-10,-9-5-
wf*.7,4,7,'#5a3a1c');R(-10,9+wf*.7,4,7,'#5a3a1c')}}else{for(let k=0;k<3;k++)
{R(-8+k*5,-16-k*3-wf*1.4,4,8+k*3,'#5a3a1c');R(-8+k*5,8+wf*1.4,4,8+k*3,'#5a3a1c')}}
const bx=mt?-4:0;R(bx-
6,-5,12,10,rc);R(bx+4,-3,8,6,f?'#fff':'#8a6038');R(bx+9,-2,2,2,'#f22');R(bx+6,3,10
,3,'#555');if(e.atk>0)R(bx+16,3,8,4,'#fd5');return}
if(M==2){const L=D==2?22:12,sw=e.atk>0?
Math.sin(e.atk/.35*6.28)*9:Math.sin(t*8+e.x)*2,ar=e.dash>0?
5:0;R(-8+w,-7,5,4,'#432');R(-8-
w,3,5,4,'#432');R(-5,-9,10,18,c);R(-3,-4,8,8,'#d2a679');R(5,-9+sw,L+ar,3,'#d2a679'
);R(5,6-
sw,L+ar,3,'#d2a679');R(-3,-7,4,4,'#a00');R(2,3,3,3,'#a00');R(5+L+ar,-10+sw,4,3,'#d
dd');R(5+L+ar,7-sw,4,3,'#ddd');if(e.atk>0)R(8,-2,5,4,'#a00');return}
if(D==0){for(let i=0;i<4;i++){R(-14+i*9,-14+w*(i%2?
1:-1)*.3,4,6,'#1c5a1c');R(-14+i*9,8-w*(i%2?
1:-1)*.3,4,6,'#1c5a1c')}R(-18,-9,30,18,c);for(let
i=0;i<4;i++)R(-14+i*7,-11,3,4,'#8f8');const sw=at?
(at-.5)*2.6:Math.sin(t*2+e.x)*.1;let cx=10,cy=0;for(let i=0;i<5;i++){const an=sw*
(i+1)/5;cx+=Math.cos(an)*10;cy+=Math.sin(an)*10;R(cx,cy-3,12,6,c)}R(cx+2,cy-
6,16,12,c);R(cx+12,cy-3,4,3,'#000');R(cx+14,cy+3,8,3,'#222');if(at)for(let
i=0;i<6;i++)R(cx*.4+i*9-4,(i-3)*7,5,5,'#fff6');return}
if(D==1){const
ex=1+at*1.2;R(-16,-16,32,32,c);R(-8,-8,16,16,'#9c3');R(-12,6,8,8,'#7a3');for(let
i=0;i<4;i++){const ang=i*1.57+.78+Math.sin(t*4+i)*.4;for(let
j=0;j<5;j++)R(Math.cos(ang)*(16+j*8*ex)-3,Math.sin(ang)*
(16+j*8*ex)-3,6,6,j==4?'#fe5':c)}for(let i=0;i<4;i++){R(-10+(i%2)*14,-10+
(i>>1)*14,6,6,'#fff');R(-8+(i%2)*14,-8+(i>>1)*14,3,3,'#000')}return}
R(-18,-14,34,28,c);R(-6,-18,8,8,'#6f4');R(6,8,8,8,'#6f4');R(-14,6,8,8,'#6f4');R(-2
,-12,6,6,'#6f4');for(let i=0;i<8;i++)R(-16+i*4,14+((i%2)?w:-w)*.4+(at?
4:0),3,6,'#611');R(6,-8,6,6,'#fff');if(at)R(16,-6,10,12,'#300')}
function sprOld(e,a){const
w=Math.sin(s.t*9+e.x*.05)*3,c=e.fl>0?'#fff':e.col,r=e.r;
if(e.k=='fung'){const n=D==1?40:D==0?14:24;for(let i=0;i<n;i++){let
ang=i*6.283/n,px=Math.cos(ang)*r*.55,py=Math.sin(ang)*r*.55;for(let j=0;j<6;j++)
{ang+=Math.sin(s.t*2+i*1.7+j*.6)*.3;px+=Math.cos(ang)*14;py+=Math.sin(ang)*14;R(px
-5,py-5,10-j,10-j,j==5?'#fe8':j%2?'#c9f':'#8be')}}for(let i=0;i<12;i++){const
q=i*.9;R(Math.cos(q)*r*.5-16,Math.sin(q)*r*.5-
16,34,34,e.fl>0?'#fff':i%2?'#a6e':'#7ad')}R(-45,-45,90,90,e.fl>0?'#fff':'#9a6fe0')
;for(let i=0;i<7;i++){const
ex=Math.cos(i*.9+1)*r*.5,ey=Math.sin(i*.9+1)*r*.5;R(ex-7,ey-7,14,14,'#fff');R(ex-
3+Math.cos(a)*3,ey-3+Math.sin(a)*3,6,6,'#000')}return}
if(e.k=='boss'){for(const[y,x]of[[-42,-35],[-42,15],[32,-35],
[32,15]])R(x,y,18,12,'#222');R(-52,-30,92,60,c);for(let
i=0;i<4;i++)R(-46+i*23,-30,9,60,'#111');R(38,-9,40,18,c);R(76,-15,32,30,c);R(80,-9
,6,6,'#f00');R(98,-6,14,12,'#a22');return}
if(e.k=='r'){if(e.mhp>0)
{R(-24,-10,46,20,'#3a7a3a');R(20,-4,18,8,'#3a7a3a');R(36,-7,10,14,'#3a7a3a')}const
f=Math.sin(s.t*14+e.x)*6;R(-8,-24-
f,10,18,'#fff7');R(-8,6+f,10,18,'#fff7');if(D==2){R(-18,-20-
f,8,14,'#fff5');R(-18,6+f,8,14,'#fff5')}R(-10,-7,22,14,c);R(6,-5,5,4,'#000');R(6,1
,5,4,'#000');R(-4,-4,8,8,'#fc8');return}
if(M==2){const L=D==2?
22:12;R(-5,-9,10,18,c);R(-3,-4,8,8,'#d2a679');R(5,-9,L,3,'#d2a679');R(5,6,L,3,'#d2
a679');R(-3,-7,4,4,'#a00');R(2,3,3,3,'#a00');if(D==1)
{R(5+L,-10,4,3,'#ddd');R(5+L,7,4,3,'#ddd')}return}
if(D==0){for(let i=0;i<4;i++){R(-14+i*9,-14+w*(i%2?
1:-1)*.3,4,6,'#1c5a1c');R(-14+i*9,8-w*(i%2?
1:-1)*.3,4,6,'#1c5a1c')}R(-18,-9,30,18,c);for(let
i=0;i<4;i++)R(-14+i*7,-11,3,4,'#8f8');for(let i=0;i<5;i++)R(10+i*10,-3-
Math.sin(s.t*3+i)*3,12,6,c);R(60,-6,16,12,c);R(70,-3,4,3,'#000')}
else if(D==1){R(-16,-16,32,32,c);R(-8,-8,16,16,'#9c3');for(let i=0;i<4;i++){const
ang=i*1.57+.78+Math.sin(s.t*4+i)*.4;for(let j=0;j<5;j++)R(Math.cos(ang)*
(16+j*8)-3,Math.sin(ang)*(16+j*8)-3,6,6,c)}for(let i=0;i<4;i++)R(-10+(i%2)*14,-10+
(i>>1)*14,5,5,'#000')}
else{R(-18,-14,34,28,c);R(-6,-18,8,8,'#6f4');R(6,8,8,8,'#6f4');R(-14,6,8,8,'#6f4')
;for(let i=0;i<6;i++)R(-14+i*5,14+(i%2)*w*.3,3,5,'#611');R(6,-8,6,6,'#fff')}}
function drawE(e){const p=s.p,a=Math.atan2(p.y-e.y,p.x-
e.x),fl=e.k=='r',ln=e.atk>0&&!fl?
Math.sin(e.atk*9)*7:0;X.save();X.translate(e.x,e.y);if(fl)R(4,20,44,28,'#0003');el
se R(-e.r+4,-e.r+5,e.r*2,e.r*1.7,'#0004');X.translate(0,-
(e.jy||0));if(e.k!='fung')X.rotate(a);if(ln)X.translate(ln,0);if(fl)X.translate(0,
Math.sin(s.t*3+e.x)*2);spr(e,a);X.restore();if(e.lbl)txt(e.lbl,e.x,e.y-e.r-
30,'center',30);if(e.k=='boss'||e.k=='fung'||e.nb)return;X.fillStyle='#300';X.fill
Rect(e.x-15,e.y-e.r-12,30,5);X.fillStyle='#e33';X.fillRect(e.x-15,e.y-e.r-
12,30*cl(e.hp/(e.mx||(e.k=='r'?[60,105,300][D]:100)),0,1),5)}
function drawEold(e){const p=s.p,a=Math.atan2(p.y-e.y,p.x-e.x);
if(e.k=='fung'){X.globalAlpha=.8;for(let i=0;i<9;i++){const
q=i*.7+s.t*.5;X.fillStyle=i%2?'#c9f':'#8cf';X.beginPath();X.arc(e.x+Math.cos(q)*e.
r*.65,e.y+Math.sin(q*1.3)*e.r*.65,e.r*.42,0,7);X.fill()}X.globalAlpha=1;for(let
i=0;i<7;i++)eye(e.x+Math.cos(i*.9+1)*e.r*.55,e.y+Math.sin(i*.9+1)*e.r*.55,a,8);ret
urn}
X.fillStyle=e.fl>0?'#fff':e.col;X.beginPath();X.arc(e.x,e.y,e.r,0,7);X.fill();
if(e.k=='boss'){X.strokeStyle='#000';X.lineWidth=9;for(let i=1;i<4;i++)
{X.beginPath();X.arc(e.x,e.y,e.r*i/4,0,7);X.stroke()}X.fillStyle='#fc0';X.beginPat
h();X.arc(e.x+Math.cos(a)*e.r,e.y+Math.sin(a)*e.r,e.r*.4,0,7);X.fill();eye(e.x+Mat
h.cos(a)*e.r,e.y+Math.sin(a)*e.r,a,8);return}
if(e.mhp>0)
{X.strokeStyle='#9cf';X.lineWidth=4;X.beginPath();X.arc(e.x,e.y,e.r+5,0,7);X.strok
e()}
if(e.k=='r'){X.fillStyle='#fff6';X.fillRect(e.x-e.r*2,e.y-4,e.r*4,8)}
if(e.rg)
{X.strokeStyle=e.col;X.lineWidth=7;X.beginPath();X.moveTo(e.x,e.y);X.lineTo(e.x+Ma
th.cos(a)*(e.r+e.rg),e.y+Math.sin(a)*(e.r+e.rg));X.stroke()}
eye(e.x+Math.cos(a)*e.r*.4-
4,e.y+Math.sin(a)*e.r*.4,a,4);eye(e.x+Math.cos(a)*e.r*.4+4,e.y+Math.sin(a)*e.r*.4,
a,4);
X.fillStyle='#300';X.fillRect(e.x-15,e.y-e.r-
10,30,4);X.fillStyle='#e33';X.fillRect(e.x-15,e.y-e.r-10,30*cl(e.hp/(e.k=='r'?
[60,105,300][D]:100),0,1),4)}
function txt(t,x,y,al,sz){X.font='bold '+(sz||20)+'px
Georgia';X.textAlign=al||'left';X.fillStyle='#000';X.fillText(t,x+1,y+1);X.fillSty
le='#fff';X.fillText(t,x,y)}
function draw(){const
p=s.p,pl=PAL[M];X=GX;X.setTransform(PS,0,0,PS,0,0);X.imageSmoothingEnabled=false;X
.save();X.translate(-cam.x+(s.sh>0?rnd(-6,6):0),-cam.y+(s.sh>0?rnd(-6,6):0));
const i0=Math.floor(cam.x/40),j0=Math.floor(cam.y/40);for(let
i=i0;i<i0+22;i++)for(let j=j0;j<j0+14;j++){const h=
((i*73856093)^(j*19349663))>>>0;X.fillStyle=pl[h%100<14?2:h%100<40?
1:0];X.fillRect(i*40,j*40,40,40);for(let q=0;q<5;q++){const hh=(h>>
(q*3))&255;X.fillStyle=pl[(hh&3)?2:1];X.fillRect(i*40+(hh%36),j*40+((hh>>2)%36),3+
(hh&3),3)}if(h%61==0)
{X.fillStyle='#4a4a4a';X.fillRect(i*40+4,j*40+6,32,26);X.fillStyle='#777';X.fillRe
ct(i*40+4,j*40+6,32,7);X.fillStyle='#222';X.fillRect(i*40+10,j*40+18,8,8)}if(M<2&&
h%47==0)
{X.fillStyle='#eee';X.fillRect(i*40+8,j*40+10,14,3);X.fillRect(i*40+12,j*40+7,3,9)
}if(M<2&&h%5==0)
{X.fillStyle='#0002';X.fillRect(i*40+3,j*40+15,30,2);X.fillRect(i*40+8,j*40+19,22,
2)}}
X.strokeStyle='#0003';X.lineWidth=1;X.strokeRect(0,0,WW,WH);if(M<2)for(const[x,y,w
,h]of[[120,140,200,120],[1180,260,240,160],[640,780,260,140],[1300,900,200,200],
[260,900,180,150],[900,100,160,120]])
{R(x,y,w,h,'#4b4b48');R(x,y,w,12,'#8a8a82');R(x,y,12,h*.7,'#8a8a82');R(x+w-
12,y+h*.35,12,h*.65,'#6e6e68');R(x+30,y+40,w*.3,h*.25,'#2e2e2c');R(x+w*.5,y+h*.5,2
2,16,'#777')}
if(M==0){if(s.destroyed){X.fillStyle='#241b14';X.fillRect(200,480,240,240);for(let
i=0;i<14;i++){X.fillStyle=i%3?'#4a3320':'#111';X.fillRect(205+(i*37)%220,485+
(i*53)%210,18+(i%4)*6,10+(i%3)*5)}X.fillStyle='#f73';X.fillRect(300+
(Math.sin(s.t*9)>0?4:0),590,10,8)}else{for(let i=0;i<11;i++)
{X.fillStyle=i%2?'#7a5530':'#6b4a2a';X.fillRect(210,490+i*20,220,20)}for(const w
of s.walls)
{if(w.hp<=0)continue;X.fillStyle=w.hf>0?'#fff':w.door?'#a8763a':'#5b3b1c';X.fillRe
ct(w.x,w.y,w.w,w.h);X.fillStyle='#0004';const L=Math.max(w.w,w.h);for(let
k=0;k<L;k+=10)w.w>w.h?
X.fillRect(w.x+k,w.y,2,w.h):X.fillRect(w.x,w.y+k,w.w,2);X.fillStyle='#7a5228';w.w>
w.h?X.fillRect(w.x,w.y,w.w,3):X.fillRect(w.x,w.y,3,w.h);if(w.hp<9)
{X.fillStyle='#000';w.w>w.h?X.fillRect(w.x+w.w*.3,w.y+2,3,w.h-
4):X.fillRect(w.x+2,w.y+w.h*.3,w.w-4,3)}if(w.hp<5){X.fillStyle='#000';w.w>w.h?
X.fillRect(w.x+w.w*.6,w.y+1,3,w.h-2):X.fillRect(w.x+1,w.y+w.h*.6,w.w-
2,3)}if(w.door){X.fillStyle='#fd0';X.fillRect(w.x+4,w.y+w.h/2-3,6,6)}}}}
if(M==2)
{X.fillStyle='#6a0d0d';X.fillRect(766,585,70,30);X.fillRect(782,568,40,64);X.fillS
tyle='#8a1010';X.fillRect(790,592,16,12)}
for(const k of s.pk){R(k.x-9,k.y-9,18,18,'#111');R(k.x-4,k.y-4,8,8,'#f33');R(k.x-
9,k.y-9,18,4,'#444')}
for(const w of s.warn||[])
{X.fillStyle='#f334';X.beginPath();X.arc(w.x,w.y,34,0,7);X.fill();X.strokeStyle='#
f33';X.lineWidth=5;X.stroke()}
for(const z of s.z){const f=1-
z.t/z.t0;X.fillStyle=z.col;X.globalAlpha=.15+.35*f;X.beginPath();X.arc(z.x,z.y,z.r
,0,7);X.fill();X.globalAlpha=1;X.strokeStyle=z.col;X.lineWidth=3;X.stroke()}
if(s.reach){const
q=s.reach,b=s.boss;X.save();X.translate(b.x,b.y);X.rotate(q.a);if(!q.hit)
{X.fillStyle='#f446';X.fillRect(0,-30,520,60);X.fillStyle='#f44';X.fillRect(0,-1,5
20,2)}else{for(let
i=0;i<16;i++)R(i*32,-8+Math.sin(i+s.t*20)*5,34,16,i%2?'#c9f':'#8be');R(512,-16,24,
32,'#fe8')}X.restore()}
if(s.beam){const
b=s.boss;X.strokeStyle='#4f4';X.lineWidth=14;X.beginPath();X.moveTo(b.x,b.y);X.lin
eTo(b.x+Math.cos(s.beam.a)*900,b.y+Math.sin(s.beam.a)*900);X.stroke()}
for(const q of s.corp){if(q.bl){R(q.x-14,q.y-9,28,18,q.col);R(q.x-
6,q.y+8,10,6,q.col);continue}R(q.x-30,q.y-
20,60,40,'#1b3a8a55');X.save();X.translate(q.x,q.y);X.rotate(q.a);R(-24,-9,40,18,'
#3a7a3a');R(14,-4,18,8,'#3a7a3a');R(-18,-12,3,4,'#8f8');R(-22,-24,6,14,'#2f6a2f');
X.restore()}
if(M>=5)gdraw();for(const e of s.en)drawE(e);if(M>=5)fdraw();
for(const b of s.b){X.fillStyle=b.col;X.fillRect(b.x-b.r,b.y-
b.r,b.r*2,b.r*2);X.globalAlpha=.4;X.fillRect(b.x-b.vx*.03-b.r*.7,b.y-b.vy*.03-
b.r*.7,b.r*1.4,b.r*1.4);X.globalAlpha=1}
for(const q of s.mates||[])soldier(q,q.a||0);const aa=Math.atan2(ms.y+cam.y-
p.y,ms.x+cam.x-p.x);p.tank?tankDraw(p,aa):soldier(p,aa);if(s.stab&&s.stab.t>0)
{const q=s.stab,L=40+110*(1-
q.t/.2);X.save();X.translate(p.x,p.y);X.rotate(q.a);for(const y of[-12,0,12])
{R(12,y-2,L,4,'#fd0');R(12+L,y-4,8,8,'#fff')}X.restore()}for(const q of s.mis||[])
{X.save();X.translate(q.x,q.y);X.rotate(q.ang);for(let i=1;i<9;i++)R(-10-i*14,-3+
(i%2),10,5,i<4?'#ffb04a':'#8886');R(-12,-4,24,8,'#c8c8c8');R(10,-4,8,8,'#d33');X.r
estore()};
if(p.bomb){X.fillStyle='#f33';X.fillRect(p.x-5,p.y-28,10,10)}
for(const f of s.fx){const q=f.t/f.t0;X.globalAlpha=q*.8;X.fillStyle=f.c;{const
rr=f.r*(1.3-q*.5);for(let i=0;i<12;i++){const an=i*.9+f.x,d=rr*(.25+
(i%4)*.22),z=Math.max(4,rr*.28);X.fillRect(f.x+Math.cos(an)*d-
z/2,f.y+Math.sin(an)*d-
z/2,z,z)}}}X.globalAlpha=1;X.restore();X=X0;X.imageSmoothingEnabled=false;X.drawIm
age(G,0,0,W,H);
if(M==0&&s.run&&!s.destroyed){X.fillStyle='rgba(255,0,0,'+
(.1+.08*Math.sin(s.t*8))+')';X.fillRect(0,0,W,H)}if(s.pf>0)
{X.fillStyle='rgba(190,90,255,'+Math.min(1,s.pf)+')';X.fillRect(0,0,W,H)}if(s.flas
h>0){X.fillStyle='rgba(255,240,200,'+Math.min(1,s.flash)+')';X.fillRect(0,0,W,H)}
// HUD
X.fillStyle='#0008';X.fillRect(10,10,190,16);X.fillStyle='#d33';X.fillRect(10,10,1
90*cl(p.hp/(p.mh||100),0,1),16);txt('HP '+Math.ceil(p.hp),14,40,'left',16);
const wn=p.wep=='tank'?'Tank '+(p.mode==2&&p.pb?'Purple
Blast':'cannon'):p.wep=='knife'?'Blood Knife':p.wep=='rifle'?'Assault rifle
'+p.ammo:p.wep=='plasma'?'Plasma '+p.pd+' dmg':'Gold rifle: '+
(p.mode==1?'stabbers':'energy');txt(wn,14,62,'left',16);
if(M==3)txt('Bombs '+s.stuck+'/'+s.need+' Time '+Math.max(0,Math.ceil(s.tm)),W-
14,30,'right');
if(M==0)txt('Squad '+s.mates.length,W-14,56,'right',16);if(M==0&&s.run)txt('Base
explodes in '+Math.max(0,Math.ceil(s.fuse)),W-
14,30,'right');if(M==0&&s.run)txt(D==2?'Reach any map edge':'Run east:
'+Math.max(0,Math.round(WW-30-p.x))+' left',W-14,80,'right',16);
if(M==1||M==2)txt('Enemies '+s.en.length,W-14,30,'right');if(s.hud)txt(s.hud,W-
14,30,'right');
if(s.boss&&s.boss.hp>0){const b=s.boss,mx=b.mx||[500,500,1000]
[D];X.fillStyle='#0008';X.fillRect(200,H-
26,400,14);X.fillStyle='#e8a';X.fillRect(200,H-
26,400*cl(b.hp/mx,0,1),14);txt(s.boss.nm||(M==3?'HTYU':M==8?'Alien
Fungus':D==2&&M==4?'Minion':'Alien Fungus'),W/2,H-32,'center',14)}
if(s.mt>0)txt(s.msg,W/2,M==0&&s.run?120:90,'center',s.msg=='RUN'||s.msg=='YOU MUST
DIE'?64:22);
if(s.grab)txt('CLICK! '+s.grab.c+'/30
'+Math.ceil(s.grab.t)+'s',W/2,250,'center',34);
if(s.ready)
{X.fillStyle='#d22';X.fillRect(250,200,300,100);txt('EXPLODE',W/2,265,'center',44)
}
if(p.wep=='gold'||p.pb){X.fillStyle='#fd04';X.fillRect(W-
70,50,60,34);txt('swap',W-40,74,'center',14)}
if(js)
{X.strokeStyle='#fff6';X.lineWidth=3;X.beginPath();X.arc(js.ox,js.oy,40,0,7);X.str
oke();X.beginPath();X.arc(js.x,js.y,16,0,7);X.stroke()}}
function loop(t){const dt=Math.min(.05,(t-
last)/1000||0);last=t;if(s&&mode=='play'){upd(dt)}if(s&&
(mode=='play'||mode=='end'))draw();if(s&&s.black&&mode=='end')
{X0.fillStyle='#000';X0.fillRect(0,0,W,H)}requestAnimationFrame(loop)}
addEventListener('keydown',e=>{K[e.key.toLowerCase()]=1;if(' ArrowUp ArrowDown
ArrowLeft ArrowRight'.includes(e.key))e.preventDefault()});
addEventListener('keyup',e=>K[e.key.toLowerCase()]=0);
const cp=e=>{const r=C.getBoundingClientRect();return{x:(e.clientX-
r.left)*W/r.width,y:(e.clientY-r.top)*H/r.height}};
C.addEventListener('contextmenu',e=>{e.preventDefault();if(s)s.p.mode=3-
s.p.mode});
C.addEventListener('pointerdown',e=>{if(!s||mode!='play')return;const q=cp(e);
if(e.pointerType=='touch'&&q.x<W/2){js=
{id:e.pointerId,ox:q.x,oy:q.y,x:q.x,y:q.y};return}
if(s.ready&&q.x>250&&q.x<550&&q.y>200&&q.y<300){end(1,'The base erupts with HTYU
inside. You walk out through the fire.');return}
if((s.p.wep=='gold'||s.p.pb)&&q.x>W-70&&q.y>50&&q.y<84){s.p.mode=3-
s.p.mode;return}
if(s.grab)s.grab.c++;ms.x=q.x;ms.y=q.y;ms.down=e.pointerId||1;ms.id=e.pointerId;C.
setPointerCapture(e.pointerId)});
C.addEventListener('pointermove',e=>{const q=cp(e);if(js&&js.id==e.pointerId)
{js.x=q.x;js.y=q.y}else if(e.pointerType!='touch'||ms.down){ms.x=q.x;ms.y=q.y}});
const up=e=>{if(js&&js.id==e.pointerId)js=null;else
if(ms.id==e.pointerId)ms.down=0};
C.addEventListener('pointerup',up);C.addEventListener('pointercancel',up);
['copy','cut','paste','contextmenu','selectstart','dragstart'].forEach(v=>addEvent
Listener(v,e=>e.preventDefault()));menu();requestAnimationFrame(loop);
</script></body></html>
