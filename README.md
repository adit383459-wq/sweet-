<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Surat Cinta SUPER PLUS</title>
<style>
body {
    margin:0; padding:0;
    font-family:'Segoe UI',sans-serif;
    height:100vh;
    display:flex; justify-content:center; align-items:center;
    background: linear-gradient(45deg,#ff69b4,#9b59b6,#87cefa,#6a5acd,#ff1493);
    background-size:500% 500%;
    animation:gradientBG 30s ease infinite;
    overflow:hidden;
    transition: background 1s ease;
}
@keyframes gradientBG{0%{background-position:0% 50%;}50%{background-position:100% 50%;}100%{background-position:0% 50%;}}

.card{width:90%;max-width:420px;perspective:1000px;}
.envelope{width:100%;transform-style:preserve-3d;transition:transform 1s ease;cursor:pointer;}
.envelope.open{transform:rotateX(-180deg);}
.front,.back{background:#ffe6f0;border-radius:25px;padding:25px;text-align:center;box-shadow:0 0 50px rgba(255,105,180,0.5);position:absolute;width:100%;backface-visibility:hidden;}
.back{transform:rotateX(180deg);display:flex;flex-direction:column;align-items:center;}
.info{font-size:14px;margin-bottom:15px;line-height:1.6em;}
input{width:100%;padding:14px;border-radius:12px;border:1px solid #ff85c1;margin-bottom:12px;font-size:16px;}
button{width:100%;padding:14px;border-radius:12px;border:none;background:#ff69b4;color:white;font-size:16px;margin-top:6px;cursor:pointer;transition:0.3s;}
button:hover{background:#ff85c1;}
.surat{margin-top:15px;font-size:14px;line-height:1.6em;}
.heart,.particle{position:absolute;border-radius:50%;opacity:0.9;pointer-events:none;}
.heart{width:20px;height:20px;background:red;transform:rotate(45deg);box-shadow:0 0 15px rgba(255,0,100,0.8);animation:floatHeart 3s linear infinite;}
@keyframes floatHeart{0%{transform:translateY(0) rotate(45deg);opacity:1;}100%{transform:translateY(-300px) rotate(45deg);opacity:0;}}
.particle{width:4px;height:4px;background:white;animation:floatParticle linear infinite;}
@keyframes floatParticle{0%{transform:translateY(0) scale(0.5);}50%{transform:translateY(-250px) scale(1);}100%{transform:translateY(0) scale(0.5);}}
.browser-link{display:inline-block;margin-top:10px;font-size:16px;color:white;background:#9b59b6;padding:12px 20px;border-radius:20px;cursor:pointer;box-shadow:0 0 15px rgba(155,89,182,0.7);transition:0.3s;text-decoration:none;}
.browser-link:hover{background:#ff69b4;box-shadow:0 0 25px rgba(255,105,180,0.8);}
.theme-btns{display:flex;justify-content:center;margin-top:10px;gap:8px;}
.theme-btn{padding:8px 12px;border:none;border-radius:12px;color:white;cursor:pointer;transition:0.3s;}
.theme-btn:hover{opacity:0.8;}
@media screen and (max-width:420px){.card{width:95%;}input,button{font-size:15px;padding:12px;}.info{font-size:13px;}.browser-link{font-size:14px;padding:10px 15px;}}
</style>
</head>
<body>

<div class="card">
  <div class="envelope" id="envelope">
    <div class="front">
      <h2>💌 Amplop Cinta</h2>
      <p class="info">
        Untuk: <b id="nama">Lilis Karlina Awaliahh Tersayanggggggggg</b><br>
        Jadian sejak: <b id="tanggal">17 Agustus 2025</b><br>
        Lama jadian: <b id="lamaJadian">0 hari</b><br>
        <span id="countdown"></span>
      </p>
      <input type="password" id="password" placeholder="Masukkan password">
      <button onclick="bukaEnvelope()">Buka Amplop</button>
      <div class="browser-link" onclick="window.open('https://username.github.io/digital-love-letter/','_blank')">
        🔗 Buka link di browser
      </div>
      <div class="theme-btns">
        <button class="theme-btn" style="background:#ff69b4" onclick="gantiTema('#ff69b4','#9b59b6','#87cefa','#6a5acd','#ff1493')">Pink</button>
        <button class="theme-btn" style="background:#6a5acd" onclick="gantiTema('#6a5acd','#ff69b4','#ff1493','#9b59b6','#87cefa')">Biru</button>
        <button class="theme-btn" style="background:#000000" onclick="gantiTema('#000000','#434343','#666666','#888888','#111111')">Hitam</button>
      </div>
    </div>
    <div class="back">
      <div class="surat" id="surat"></div>
      <div style="margin-top:10px; width:100%;">
        <button onclick="gantiSurat()">💬 Ganti Pesan</button>
        <button onclick="playMusic()">🎶 Musik</button>
      </div>
    </div>
  </div>
</div>

<audio id="music" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" loop></audio>

<script>
const namaPacar="Lilis Karlina Awaliahh Tersayanggggggggg";
const tanggalJadian=new Date("2025-08-17");
const passwordBenar="17";
let surat=[
"🥰 Hai Cintaakuu 🥺🥺💖, setiap detik bersamamu membuat hatiku meleleh 😘💕🌸.",
"💖 Hai Cintaakuu 🥺🥺, aku bersyukur bisa mengenalmu, mendengar tawamu yang manis 🌸💞✨.",
"🌹 Hai Cintaakuu 🥺🥺, semoga kita selalu saling menguatkan 💕💖💫.",
`💝 Hai Cintaakuu 🥺🥺, aku bangga memilikimu, ${namaPacar}. Kenangan bersamamu tak ternilai ❤️💖🥰.`,
"💖 Hai Cintaakuu 🥺🥺, ingatlah aku selalu mencintaimu 😘💞✨💖. Terima kasih telah menjadi dirimu 💕🥰."
];
let index=0;

function hitungLamaJadian(){
  const sekarang=new Date();
  const diff=sekarang-tanggalJadian;
  const hari=Math.floor(diff/(1000*60*60*24));
  document.getElementById("lamaJadian").innerText=hari+" hari";
}
function hitungCountdown(){
  const sekarang=new Date();
  let nextAnniv=new Date(tanggalJadian);
  nextAnniv.setFullYear(sekarang.getFullYear());
  if(sekarang>nextAnniv) nextAnniv.setFullYear(sekarang.getFullYear()+1);
  const diff=nextAnniv-sekarang;
  const days=Math.floor(diff/(1000*60*60*24));
  document.getElementById("countdown").innerText=`Hari ulang tahun jadian berikutnya: ${days} hari`;
}
function bukaEnvelope(){
  const input=document.getElementById("password").value;
  if(input===passwordBenar){
    document.getElementById("envelope").classList.add("open");
    document.getElementById("surat").innerText=surat[index];
    hitungLamaJadian();
    hitungCountdown();
    playMusic();
    createParticles(200);
  } else { alert("Password salah 😅"); }
}
function gantiSurat(){
  index++; if(index>=surat.length) index=0;
  document.getElementById("surat").innerText=surat[index];
  createHeart(20);
}
function playMusic(){document.getElementById("music").play();}
function createHeart(count=1){
  for(let i=0;i<count;i++){
    const heart=document.createElement("div");
    heart.classList.add("heart");
    heart.style.left=Math.random()*90+"%";
    heart.style.top="80%";
    heart.style.width=heart.style.height=(Math.random()*15+15)+"px";
    document.body.appendChild(heart);
    setTimeout(()=>{heart.remove();},5000);
  }
}
function createParticles(count=50){
  for(let i=0;i<count;i++){
    const p=document.createElement("div");
    p.classList.add("particle");
    p.style.background=Math.random()>0.5?'white':'pink';
    p.style.top=Math.random()*100+'%';
    p.style.left=Math.random()*100+'%';
    p.style.width=p.style.height=(Math.random()*4+2)+'px';
    p.style.animationDuration=(Math.random()*15+10)+'s';
    document.body.appendChild(p);
    setInterval(()=>{p.style.top=(Math.random()*100)+'%'; p.style.left=(Math.random()*100)+'%';},12000);
  }
}
function gantiTema(...colors){
  document.body.style.background=`linear-gradient(45deg,${colors.join(',')})`;
}
</script>
</body>
</html>
