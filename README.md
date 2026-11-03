# an-tinh
AN TỊNH – The Silent Sanctuary | A peaceful 3D online world.
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<meta name="theme-color" content="#101c29">
<title>AN TỊNH — The Silent Sanctuary</title>
<style>
:root{--gold:#e8d6a2;--cream:#f5efdf;--glass:rgba(13,25,36,.68);--line:rgba(238,222,177,.24)}
*{box-sizing:border-box}html,body{margin:0;width:100%;height:100%;overflow:hidden;background:#0b1723;color:var(--cream);font-family:Georgia,"Times New Roman",serif}
#scene{position:fixed;inset:0}canvas{display:block}
.vignette{position:fixed;inset:0;pointer-events:none;background:linear-gradient(180deg,rgba(5,12,20,.48),transparent 30%,transparent 65%,rgba(5,12,20,.45));}
header{position:fixed;top:0;left:0;right:0;padding:22px 26px;display:flex;justify-content:space-between;align-items:flex-start;pointer-events:none}
.brand{pointer-events:auto}.brand .name{font-size:clamp(22px,4vw,32px);letter-spacing:.28em;color:#f3e4bd}.brand .sub{font:10px Arial,sans-serif;letter-spacing:.25em;color:#c6c1b3;margin-top:6px}
.top-actions{display:flex;gap:9px;pointer-events:auto}
button{border:1px solid var(--line);background:var(--glass);color:var(--cream);border-radius:999px;padding:10px 15px;font:12px Arial,sans-serif;letter-spacing:.04em;backdrop-filter:blur(12px);cursor:pointer}
button:active{transform:scale(.97)}button.primary{background:rgba(211,177,111,.2);border-color:rgba(232,214,162,.55)}
.hint{position:fixed;left:50%;top:105px;transform:translateX(-50%);text-align:center;font:11px Arial,sans-serif;letter-spacing:.12em;color:rgba(245,239,223,.78);white-space:nowrap;text-shadow:0 2px 10px #000}
.panel{position:fixed;left:22px;bottom:22px;width:min(310px,calc(100vw - 44px));padding:17px 18px;background:var(--glass);border:1px solid var(--line);border-radius:18px;backdrop-filter:blur(15px)}
.panel h2{font-size:17px;font-weight:normal;letter-spacing:.12em;color:var(--gold);margin:0 0 8px}
.panel p{font:12px/1.6 Arial,sans-serif;color:#d8d4ca;margin:0}
.status{display:flex;gap:14px;margin-top:12px;font:10px Arial,sans-serif;color:#c8b98f;letter-spacing:.08em}
.controls{position:fixed;right:22px;bottom:22px;display:grid;grid-template-columns:48px 48px 48px;grid-template-rows:48px 48px;gap:6px;touch-action:none}
.controls button{padding:0;border-radius:15px;font-size:18px;background:rgba(13,25,36,.58)}
.controls .up{grid-column:2}.controls .left{grid-column:1;grid-row:2}.controls .down{grid-column:2;grid-row:2}.controls .right{grid-column:3;grid-row:2}
.modal{position:fixed;inset:0;background:rgba(3,9,15,.72);display:none;align-items:center;justify-content:center;padding:22px;backdrop-filter:blur(8px)}
.modal.show{display:flex}.modal-card{width:min(430px,100%);padding:25px;border:1px solid var(--line);border-radius:22px;background:linear-gradient(145deg,#1a2a37,#101b27)}
.modal h2{font-weight:normal;color:var(--gold);letter-spacing:.12em;margin:0 0 12px}.modal p{font:13px/1.7 Arial,sans-serif;color:#dedbd2}
.modal .close{margin-top:12px}
.toast{position:fixed;left:50%;bottom:115px;transform:translate(-50%,15px);opacity:0;transition:.3s;background:rgba(15,28,39,.9);border:1px solid var(--line);padding:11px 17px;border-radius:30px;font:12px Arial,sans-serif;pointer-events:none;white-space:nowrap}
.toast.show{opacity:1;transform:translate(-50%,0)}
@media(max-width:600px){header{padding:16px}.top-actions{gap:6px}.top-actions button{padding:9px 11px;font-size:10px}.hint{top:88px;font-size:9px}.panel{left:12px;bottom:12px;width:calc(100vw - 24px);padding:13px 15px}.panel h2{font-size:15px}.panel p{font-size:11px}.status{margin-top:8px}.controls{right:12px;bottom:105px;grid-template-columns:43px 43px 43px;grid-template-rows:43px 43px}.controls button{border-radius:13px}.toast{bottom:205px}}
</style>
</head>
<body>
<div id="scene"></div><div class="vignette"></div>
<header>
 <div class="brand"><div class="name">AN TỊNH</div><div class="sub">THE SILENT SANCTUARY</div></div>
 <div class="top-actions">
  <button id="cycle" class="primary">☾ Đêm</button>
  <button id="bell">♧ Chuông</button>
  <button id="about">Giới thiệu</button>
 </div>
</header>
<div class="hint">DÙNG PHÍM WASD / MŨI TÊN HOẶC CỤM NÚT ĐỂ KHÁM PHÁ</div>
<div class="panel">
 <h2 id="place">CÕI THANH SƠN</h2>
 <p id="message">Giữa núi non tĩnh lặng, hãy bước chậm lại và để lòng mình nghỉ ngơi.</p>
 <div class="status"><span id="clock">TRỜI ĐÊM</span><span>•</span><span>KHÔNG GIAN AN YÊN</span></div>
</div>
<div class="controls" aria-label="Điều khiển di chuyển">
 <button class="up" data-move="up">↑</button><button class="left" data-move="left">←</button><button class="down" data-move="down">↓</button><button class="right" data-move="right">→</button>
</div>
<div class="modal" id="modal"><div class="modal-card"><h2>AN TỊNH</h2><p>Một góc nhỏ để dừng chân giữa nhịp sống vội vàng. Phiên bản khởi đầu này là không gian 3D thử nghiệm: bạn có thể dạo bước quanh sân chùa, đổi ánh sáng ngày/đêm và ngân chuông.</p><p>Bản phát triển tiếp theo có thể bổ sung tạo nhân vật, hồ sen tương tác, thiền định, lưu tiến trình và thế giới nhiều người.</p><button class="close primary" id="close">Trở lại khu vườn</button></div></div>
<div class="toast" id="toast">Tiếng chuông ngân vang giữa núi rừng…</div>
<script type="module">
import * as THREE from 'https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js';
const mount=document.querySelector('#scene');
const scene=new THREE.Scene();scene.background=new THREE.Color(0x101d2d);scene.fog=new THREE.FogExp2(0x101d2d,.018);
const camera=new THREE.PerspectiveCamera(58,innerWidth/innerHeight,.1,250);camera.position.set(0,7,14);
const renderer=new THREE.WebGLRenderer({antialias:true});renderer.setPixelRatio(Math.min(devicePixelRatio,1.8));renderer.setSize(innerWidth,innerHeight);renderer.shadowMap.enabled=true;renderer.shadowMap.type=THREE.PCFSoftShadowMap;renderer.toneMapping=THREE.ACESFilmicToneMapping;renderer.toneMappingExposure=1.15;mount.appendChild(renderer.domElement);
const hemi=new THREE.HemisphereLight(0xb8d5ec,0x25352c,1.25);scene.add(hemi);
const moonLight=new THREE.DirectionalLight(0xc5d7ff,2.1);moonLight.position.set(-8,14,7);moonLight.castShadow=true;moonLight.shadow.mapSize.set(1024,1024);scene.add(moonLight);
const warm=new THREE.PointLight(0xffbd70,25,25);warm.position.set(0,4,0);scene.add(warm);
const mat=(color,roughness=.85)=>new THREE.MeshStandardMaterial({color,roughness});
const ground=new THREE.Mesh(new THREE.PlaneGeometry(150,150),mat(0x243c39));ground.rotation.x=-Math.PI/2;ground.position.y=-.12;ground.receiveShadow=true;scene.add(ground);
function box(w,h,d,m,x,y,z){const o=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),m);o.position.set(x,y,z);o.castShadow=true;o.receiveShadow=true;scene.add(o);return o}
function cone(r,h,m,x,y,z,seg=8){const o=new THREE.Mesh(new THREE.ConeGeometry(r,h,seg),m);o.position.set(x,y,z);o.castShadow=true;scene.add(o);return o}
function cylinder(rt,rb,h,m,x,y,z,seg=10){const o=new THREE.Mesh(new THREE.CylinderGeometry(rt,rb,h,seg),m);o.position.set(x,y,z);o.castShadow=true;scene.add(o);return o}
const stone=mat(0x8c887a),wood=mat(0x4b3026),roof=mat(0x263c48),gold=mat(0xc9a96e),leaf=mat(0x365b47),darkLeaf=mat(0x28483d);
// Temple platform and steps
box(9,.5,7,stone,0,.25,-5);box(7,.25,5,wood,0,.62,-5);
for(let i=0;i<4;i++)box(3.2+i*.65,.16,.7,stone,0,.08+i*.16,-1.1-i*.62);
box(5,.16,3,wood,0,1.0,-5);
for(const x of [-2.1,2.1])for(const z of [-6.1,-3.9])cylinder(.13,.16,2.4,wood,x,2.15,z,8);
box(5.8,.22,3.7,wood,0,3.35,-5);
const roofMesh=new THREE.Mesh(new THREE.ConeGeometry(4.3,1.7,4),roof);roofMesh.rotation.y=Math.PI/4;roofMesh.scale.set(1,.55,.72);roofMesh.position.set(0,4.25,-5);roofMesh.castShadow=true;scene.add(roofMesh);
const roofTop= new THREE.Mesh(new THREE.ConeGeometry(2.8,1.05,4),mat(0x405a62));roofTop.rotation.y=Math.PI/4;roofTop.scale.set(1,.5,.7);roofTop.position.set(0,4.8,-5);scene.add(roofTop);
box(1.3,1.7,.15,mat(0x241c1a),0,1.95,-3.43);
for(let x=-2.4;x<=2.4;x+=.8)box(.08,1.05,.1,gold,x,2.0,-3.32);
// Lotus pond
const water=new THREE.Mesh(new THREE.CircleGeometry(4.1,64),new THREE.MeshStandardMaterial({color:0x244f59,metalness:.35,roughness:.22,transparent:true,opacity:.92}));water.rotation.x=-Math.PI/2;water.position.set(5,.02,3);scene.add(water);
const ring=new THREE.Mesh(new THREE.RingGeometry(4.05,4.22,64),gold);ring.rotation.x=-Math.PI/2;ring.position.set(5,.04,3);scene.add(ring);
const lotusMat=new THREE.MeshStandardMaterial({color:0xe7b7bd,side:THREE.DoubleSide,roughness:.55});
for(let i=0;i<13;i++){const a=i*2.4,r=1.1+(i%4)*.65,x=5+Math.cos(a)*r,z=3+Math.sin(a)*r;const pad=new THREE.Mesh(new THREE.CircleGeometry(.36,7),mat(0x477b61));pad.rotation.x=-Math.PI/2;pad.position.set(x,.07,z);scene.add(pad);if(i%2===0){const flower=new THREE.Mesh(new THREE.SphereGeometry(.19,10,8),lotusMat);flower.scale.set(1,.35,1);flower.position.set(x,.2,z);scene.add(flower)}}
// Trees, mountain silhouettes
function tree(x,z,s=1){cylinder(.16*s,.25*s,1.5*s,wood,x,.75*s,z,7);for(let j=0;j<3;j++){const crown=new THREE.Mesh(new THREE.IcosahedronGeometry((1.0-j*.16)*s,1),j===1?darkLeaf:leaf);crown.position.set(x,(1.65+j*.55)*s,z);crown.castShadow=true;scene.add(crown)}}
for(const [x,z,s] of [[-8,-5,1.5],[-7,2,1.2],[9,-7,1.6],[10,1,1.3],[-5,8,1.1],[1,10,1.3],[12,8,1.1],[-12,-1,1.4]])tree(x,z,s);
const mountainMat=mat(0x293d4b);
for(let i=0;i<9;i++){const m=new THREE.Mesh(new THREE.ConeGeometry(5+Math.random()*4,10+Math.random()*9,5),mountainMat);m.position.set(-28+i*7,3,-22-Math.random()*9);m.rotation.y=i*.7;scene.add(m)}
// Lanterns
const lanterns=[];
for(const [x,z] of [[-4,-1],[4,-1],[-5,4],[9,4],[0,5]]){cylinder(.06,.06,1.5,wood,x,1.4,z,7);const l=new THREE.Mesh(new THREE.SphereGeometry(.24,12,10),new THREE.MeshStandardMaterial({color:0xffc878,emissive:0xffa43c,emissiveIntensity:1.4}));l.position.set(x,2.25,z);scene.add(l);const pl=new THREE.PointLight(0xffb55c,3,5);pl.position.copy(l.position);scene.add(pl);lanterns.push(pl)}
// Moon and stars
const moon=new THREE.Mesh(new THREE.SphereGeometry(1.15,32,24),new THREE.MeshBasicMaterial({color:0xf0e5c5}));moon.position.set(-9,13,-25);scene.add(moon);
const starGeo=new THREE.BufferGeometry(),pts=[];for(let i=0;i<450;i++)pts.push((Math.random()-.5)*100,Math.random()*35+4,-25-Math.random()*50);starGeo.setAttribute('position',new THREE.Float32BufferAttribute(pts,3));scene.add(new THREE.Points(starGeo,new THREE.PointsMaterial({color:0xf4e8c9,size:.12,transparent:true,opacity:.85})));
// Avatar - simple robed traveler
const avatar=new THREE.Group();scene.add(avatar);avatar.position.set(0,0,4);
const robe=new THREE.Mesh(new THREE.CapsuleGeometry(.42,.85,4,8),mat(0xd6c9a9));robe.position.y=1;robe.castShadow=true;avatar.add(robe);
const head=new THREE.Mesh(new THREE.SphereGeometry(.29,16,12),mat(0xd9ad8d));head.position.y=1.9;head.castShadow=true;avatar.add(head);
const hood=new THREE.Mesh(new THREE.SphereGeometry(.31,16,12,0,Math.PI*2,0,Math.PI/2),mat(0x51483d));hood.position.y=2.03;avatar.add(hood);
const sash=new THREE.Mesh(new THREE.TorusGeometry(.38,.055,8,24),gold);sash.rotation.x=Math.PI/2;sash.position.y=.95;avatar.add(sash);
const keys={};let day=false;let moving=false;const speed=5;
function move(dir,on){keys[dir]=on}
addEventListener('keydown',e=>{const k=e.key.toLowerCase();if(['w','a','s','d','arrowup','arrowdown','arrowleft','arrowright'].includes(k)){keys[k]=true;e.preventDefault()}});
addEventListener('keyup',e=>keys[e.key.toLowerCase()]=false);
document.querySelectorAll('[data-move]').forEach(b=>{const d=b.dataset.move;const start=e=>{e.preventDefault();move(d,true)},end=e=>{e.preventDefault();move(d,false)};b.addEventListener('pointerdown',start);b.addEventListener('pointerup',end);b.addEventListener('pointerleave',end);b.addEventListener('pointercancel',end)});
document.querySelector('#cycle').onclick=()=>{day=!day;scene.background.set(day?0xb6c8d1:0x101d2d);scene.fog.color.set(day?0xb6c8d1:0x101d2d);hemi.intensity=day?2.0:1.25;moonLight.intensity=day?1.0:2.1;moon.visible=!day;warm.intensity=day?5:25;lanterns.forEach(l=>l.intensity=day?.4:3);document.querySelector('#cycle').textContent=day?'☀ Ngày':'☾ Đêm';document.querySelector('#clock').textContent=day?'TRỜI BAN NGÀY':'TRỜI ĐÊM'};
function ringBell(){try{const ctx=new (window.AudioContext||window.webkitAudioContext)();const now=ctx.currentTime;[220,330,440,554].forEach((f,i)=>{const o=ctx.createOscillator(),g=ctx.createGain();o.type='sine';o.frequency.value=f;o.connect(g);g.connect(ctx.destination);g.gain.setValueAtTime(.0001,now);g.gain.exponentialRampToValueAtTime(.12/(i+1),now+.03);g.gain.exponentialRampToValueAtTime(.0001,now+3.5+i*.35);o.start(now);o.stop(now+4)});}catch(e){}const t=document.querySelector('#toast');t.classList.add('show');setTimeout(()=>t.classList.remove('show'),2400)}
document.querySelector('#bell').onclick=ringBell;document.querySelector('#about').onclick=()=>document.querySelector('#modal').classList.add('show');document.querySelector('#close').onclick=()=>document.querySelector('#modal').classList.remove('show');
const clock=new THREE.Clock();
function animate(){requestAnimationFrame(animate);const dt=Math.min(clock.getDelta(),.04);let dx=0,dz=0;if(keys.w||keys.arrowup||keys.up)dz-=1;if(keys.s||keys.arrowdown||keys.down)dz+=1;if(keys.a||keys.arrowleft||keys.left)dx-=1;if(keys.d||keys.arrowright||keys.right)dx+=1;moving=dx!==0||dz!==0;if(moving){const len=Math.hypot(dx,dz);avatar.position.x+=dx/len*speed*dt;avatar.position.z+=dz/len*speed*dt;avatar.position.x=THREE.MathUtils.clamp(avatar.position.x,-11,11);avatar.position.z=THREE.MathUtils.clamp(avatar.position.z,-3,11);avatar.rotation.y=Math.atan2(dx,dz);robe.position.y=1+Math.sin(performance.now()*.012)*.035}else robe.position.y=1;
camera.position.x=THREE.MathUtils.lerp(camera.position.x,avatar.position.x,dt*2);camera.position.z=THREE.MathUtils.lerp(camera.position.z,avatar.position.z+10,dt*2);camera.lookAt(avatar.position.x,1.1,avatar.position.z-2);
water.material.opacity=.88+Math.sin(performance.now()*.001)*.05;renderer.render(scene,camera)}
animate();addEventListener('resize',()=>{camera.aspect=innerWidth/innerHeight;camera.updateProjectionMatrix();renderer.setSize(innerWidth,innerHeight)});
</script>
</body></html>
