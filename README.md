<!DOCTYPE html>
<html>
<head>
<title>Granny 1 Mini Escape</title>
<style>
body{
  margin:0;
  background:#000;
  color:#fff;
  font-family:Arial;
  text-align:center;
}
#game{
  width:400px;
  height:400px;
  margin:20px auto;
  border:3px solid white;
  position:relative;
  background:#111;
}
.player,.granny,.key,.door{
  width:40px;
  height:40px;
  position:absolute;
}
.player{background:#0f0;}
.granny{background:#900;}
.key{background:#ff0;}
.door{background:#0ff;}
#msg{font-size:18px;}
</style>
</head>

<body>
<h1>👵 GRANNY 1 – MINI ESCAPE</h1>
<p>Use Arrow Keys | Find key | Escape | Avoid Granny</p>

<div id="game">
  <div class="player" id="p"></div>
  <div class="granny" id="g"></div>
  <div class="key" id="k"></div>
  <div class="door" id="d"></div>
</div>

<p id="msg">You woke up in Granny's house…</p>

<script>
let px=0, py=0;
let gx=360, gy=360;
let kx=200, ky=200;
let dx=360, dy=0;
let hasKey=false;
let over=false;

function draw(){
  p.style.left=px+"px";
  p.style.top=py+"px";
  g.style.left=gx+"px";
  g.style.top=gy+"px";
  k.style.left=kx+"px";
  k.style.top=ky+"px";
  d.style.left=dx+"px";
  d.style.top=dy+"px";
}

document.addEventListener("keydown",e=>{
  if(over) return;

  if(e.key=="ArrowUp") py-=20;
  if(e.key=="ArrowDown") py+=20;
  if(e.key=="ArrowLeft") px-=20;
  if(e.key=="ArrowRight") px+=20;

  // limit walls
  px=Math.max(0,Math.min(360,px));
  py=Math.max(0,Math.min(360,py));

  // granny follows
  gx += Math.sign(px-gx)*20;
  gy += Math.sign(py-gy)*20;

  if(px==kx && py==ky && !hasKey){
    hasKey=true;
    msg.innerHTML="🗝️ You found the key!";
    k.style.display="none";
  }

  if(px==gx && py==gy){
    msg.innerHTML="👵 GRANNY CAUGHT YOU! GAME OVER!";
    over=true;
  }

  if(hasKey && px==dx && py==dy){
    msg.innerHTML="🚪 YOU ESCAPED! YOU SURVIVED!";
    over=true;
  }

  draw();
});

draw();
</script>
</body>
</html>
