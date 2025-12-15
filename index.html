const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let state = "intro"; // intro | game | shop | controls | dead | win
let introT = 0;
const keys = {};
let shopMessage = "";

// ---------- PLAYER ----------
const player = {
  x: 450,
  y: 380,
  hp: 100,
  maxHp: 100,
  coins: 0,
  speed: 4,
  color: "#00eaff",
  hasArmor: false,
  dashTime: 0,
  weapon: 0,
  damageBonus: 0
};

const weapons = [
  { name: "SMG", dmg: 4, rate: 6 },
  { name: "AR", dmg: 8, rate: 12 },
  { name: "SHOTGUN", dmg: 5, rate: 30 }
];

let shootCooldown = 0;
let bullets = [];
let enemyBullets = [];

// ---------- BOSSES ----------
let bossIndex = 0;
const MAX_BOSSES = 50;

function createBoss(i) {
  return {
    x: 450,
    y: 130,
    hp: 300 + i * 120,
    maxHp: 300 + i * 120,
    damage: 10 + i * 4,
    fireRate: 0.02 + i * 0.002,
    size: 1.2 + i * 0.02
  };
}
let boss = createBoss(0);

// ---------- INPUT ----------
document.addEventListener("keydown", e => {
  keys[e.key] = true;
  if (e.key === "Shift" && player.dashTime <= 0) player.dashTime = 12;
});
document.addEventListener("keyup", e => keys[e.key] = false);

canvas.addEventListener("mousedown", e => {
  const r = canvas.getBoundingClientRect();
  const mx = e.clientX - r.left;
  const my = e.clientY - r.top;

  if (state === "intro") { state = "game"; return; }
  if (state === "dead" || state === "win") { resetGame(); return; }

  if (state === "game") {
    if (mx >= 20 && mx <= 140 && my >= 470 && my <= 505) {
      state = "shop"; shopMessage=""; return;
    }
    if (mx >= 160 && mx <= 300 && my >= 470 && my <= 505) {
      state = "controls"; return;
    }
    shoot();
  }

  if (state === "shop") {
    if (mx >= 20 && mx <= 120 && my >= 20 && my <= 50) { state="game"; return; }

    // ARMOR
    if (mx >= 300 && mx <= 600 && my >= 220 && my <= 270) {
      if (!player.hasArmor && player.coins >= 50) {
        player.coins -= 50;
        player.hasArmor = true;
        player.maxHp += 5;
        player.hp += 5;
        shopMessage = "ARMOR BOUGHT!";
      } else shopMessage = "NOT ENOUGH COINS";
    }

    // DAMAGE
    if (mx >= 300 && mx <= 600 && my >= 290 && my <= 340) {
      if (player.coins >= 40) {
        player.coins -= 40;
        player.damageBonus += 2;
        shopMessage = "+2 DAMAGE BOUGHT!";
      } else shopMessage = "NOT ENOUGH COINS";
    }
  }

  if (state === "controls") {
    if (mx >= 20 && mx <= 120 && my >= 20 && my <= 50) {
      state = "game";
    }
  }
});

// ---------- SHOOT ----------
function shoot() {
  if (shootCooldown > 0) return;
  const w = weapons[player.weapon];
  shootCooldown = w.rate;

  bullets.push({
    x: player.x,
    y: player.y,
    vy: -9,
    dmg: w.dmg + player.damageBonus
  });
}

// ---------- DRAW HELPERS ----------
function button(x,y,w,h,color,text,size=16){
  ctx.fillStyle=color;
  ctx.fillRect(x,y,w,h);
  ctx.fillStyle="#000";
  ctx.font=size+"px Arial";
  ctx.textAlign="center";
  ctx.textBaseline="middle";
  ctx.fillText(text,x+w/2,y+h/2);
}

function drawStickman(x,y,scale,color,armor=false){
  ctx.strokeStyle=color;
  ctx.lineWidth=3*scale;

  ctx.beginPath(); ctx.arc(x,y-20*scale,8*scale,0,Math.PI*2); ctx.stroke();
  ctx.beginPath(); ctx.moveTo(x,y-12*scale); ctx.lineTo(x,y+20*scale); ctx.stroke();
  ctx.beginPath(); ctx.moveTo(x-12*scale,y); ctx.lineTo(x+12*scale,y); ctx.stroke();
  ctx.beginPath(); ctx.moveTo(x,y+20*scale); ctx.lineTo(x-10*scale,y+40*scale); ctx.stroke();
  ctx.beginPath(); ctx.moveTo(x,y+20*scale); ctx.lineTo(x+10*scale,y+40*scale); ctx.stroke();

  if (armor) {
    ctx.strokeStyle="silver";
    ctx.lineWidth=5*scale;
    ctx.strokeRect(x-12*scale,y-4*scale,24*scale,28*scale);
  }
}

// ---------- INTRO ----------
function drawIntro(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  introT+=0.05;
  const wobble=Math.sin(introT)*10;

  ctx.fillStyle="white";
  ctx.font="48px Arial";
  ctx.textAlign="center";
  ctx.fillText("STICK ARENA",450,180);
  button(350+wobble,240,200,60,"#00eaff","CLICK TO CONTINUE",20);
}

// ---------- GAME ----------
function drawGame(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  let sp = player.dashTime>0 ? 10 : player.speed;
  if (keys.a) player.x -= sp;
  if (keys.d) player.x += sp;
  if (keys.w) player.y -= sp;
  if (keys.s) player.y += sp;
  if (player.dashTime>0) player.dashTime--;

  shootCooldown=Math.max(0,shootCooldown-1);

  bullets.forEach(b=>b.y+=b.vy);
  bullets=bullets.filter(b=>{
    if(Math.hypot(b.x-boss.x,b.y-boss.y)<35*boss.size){
      boss.hp-=b.dmg;
      player.coins+=1;
      return false;
    }
    return b.y>-20;
  });

  if(Math.random()<boss.fireRate){
    const dx=player.x-boss.x, dy=player.y-boss.y;
    const d=Math.hypot(dx,dy);
    enemyBullets.push({ x:boss.x,y:boss.y,vx:(dx/d)*3,vy:(dy/d)*3 });
  }

  enemyBullets.forEach(b=>{
    b.x+=b.vx; b.y+=b.vy;
    if(Math.hypot(b.x-player.x,b.y-player.y)<18){
      player.hp-=boss.damage;
      b.hit=true;
    }
  });
  enemyBullets=enemyBullets.filter(b=>!b.hit);

  if(player.hp<=0) state="dead";
  if(boss.hp<=0){
    bossIndex++;
    if(bossIndex>=MAX_BOSSES){ state="win"; return; }
    boss=createBoss(bossIndex);
    enemyBullets=[];
  }

  ctx.fillStyle="yellow";
  bullets.forEach(b=>ctx.fillRect(b.x-3,b.y-6,6,12));
  ctx.fillStyle="orange";
  enemyBullets.forEach(b=>ctx.fillRect(b.x-3,b.y-3,6,6));

  drawStickman(player.x,player.y,1,player.color,player.hasArmor);
  drawStickman(boss.x,boss.y,boss.size,"#ff4d4d",true);

  ctx.fillStyle="white";
  ctx.font="16px Arial";
  ctx.fillText(`Coins: ${player.coins}`,20,25);
  ctx.fillText(`Damage: ${player.damageBonus}`,20,45);
  ctx.fillText(`Boss ${bossIndex+1}/50`,20,80);

  ctx.fillStyle="red";
  ctx.fillRect(20,90,200*(boss.hp/boss.maxHp),12);
  ctx.fillStyle="lime";
  ctx.fillRect(20,110,200*(player.hp/player.maxHp),12);

  button(20,470,120,35,"#00ff7f","SHOP");
  button(160,470,140,35,"#00aaff","CONTROLS");
}

// ---------- SHOP ----------
function drawShop(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  button(20,20,100,30,"#ff4d4d","BACK");

  ctx.fillStyle="white";
  ctx.font="36px Arial";
  ctx.textAlign="center";
  ctx.fillText("SHOP",450,120);

  button(300,220,300,50,player.hasArmor?"#666":"#00eaff","ARMOR +5 HP (50)");
  button(300,290,300,50,"#ffaa00","+2 DAMAGE (40)");

  ctx.font="20px Arial";
  ctx.fillText(`Coins: ${player.coins}`,450,360);

  if (shopMessage) {
    ctx.fillStyle = shopMessage.includes("NOT") ? "red" : "lime";
    ctx.fillText(shopMessage,450,400);
  }
}

// ---------- CONTROLS ----------
function drawControls(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  button(20,20,100,30,"#ff4d4d","BACK");

  ctx.fillStyle="white";
  ctx.font="36px Arial";
  ctx.textAlign="center";
  ctx.fillText("CONTROLS",450,120);

  ctx.font="22px Arial";
  ctx.fillText("WASD - Move",450,200);
  ctx.fillText("Mouse Click - Shoot",450,240);
  ctx.fillText("SHIFT - Dash",450,280);
}

// ---------- END ----------
function drawEnd(text){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  button(300,220,300,80,"#fff",text,36);
  ctx.fillStyle="white";
  ctx.font="18px Arial";
  ctx.textAlign="center";
  ctx.fillText("CLICK ANYWHERE TO RESTART",450,330);
}

function resetGame(){
  player.x=450;
  player.y=380;
  player.hp=100;
  player.maxHp=100;
  player.coins=0;
  player.hasArmor=false;
  player.damageBonus=0;
  bossIndex=0;
  boss=createBoss(0);
  bullets=[]; enemyBullets=[];
  state="intro";
}

// ---------- LOOP ----------
function loop(){
  if(state==="intro") drawIntro();
  else if(state==="game") drawGame();
  else if(state==="shop") drawShop();
  else if(state==="controls") drawControls();
  else if(state==="dead") drawEnd("YOU DIED");
  else if(state==="win") drawEnd("YOU WIN");
  requestAnimationFrame(loop);
}
loop();
