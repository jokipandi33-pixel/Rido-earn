# Rido-earn
Website kuis islami Rido EARN

<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>RIDO EARN - Kuis Islami</title>
<style>
body{font-family:Arial;background:#edf5ef;margin:0;color:#173c2c}
header{background:#075b40;color:white;text-align:center;padding:25px}
main{max-width:550px;margin:20px auto;padding:12px}
.card{background:white;padding:20px;border-radius:15px;margin-bottom:16px;box-shadow:0 3px 12px #0001}
h1{margin:0}
button{padding:14px;border:0;border-radius:9px;cursor:pointer;font-size:16px}
.answer{display:block;width:100%;text-align:left;background:#e9f3ec;margin:8px 0;color:#173c2c}
.answer:disabled{opacity:1}
.next{background:#08794e;color:white;width:100%;margin-top:10px}
#result{font-weight:bold}
.ad{border:2px dashed #aaa;padding:20px;text-align:center;color:#777}
</style>
</head>
<body>
<header>
<h1>🌙 RIDO EARN</h1>
<p>Belajar Islam, Bermain Kuis</p>
</header>
<main>
<div class="card">
<h2>Assalamu'alaikum!</h2>
<p>Selamat datang di Kuis Islami RIDO EARN.</p>
<p>Jawab 10 pertanyaan untuk mengumpulkan poin belajar.</p>
</div>
<div class="card">
<b>⭐ Skor: <span id="score">0</span></b>
<p id="progress">Soal 1 dari 10</p>
</div>
<div class="card">
<h3 id="question"></h3>
<div id="answers"></div>
<p id="result"></p>
<button class="next" id="next" disabled onclick="nextQuestion()">Soal berikutnya</button>
</div>
<div class="card">
<h3>📢 Ruang Iklan</h3>
<div class="ad">Tempat iklan RIDO EARN<br>Iklan belum diaktifkan</div>
</div>
</main>
<script>
const data=[
["Siapakah nabi terakhir?",["Musa","Muhammad","Isa","Ibrahim"],1],
["Berapa jumlah rukun Islam?",["4","5","6","7"],1],
["Kitab suci umat Islam?",["Taurat","Injil","Al-Qur'an","Zabur"],2],
["Berapa rakaat salat Subuh?",["2","3","4","5"],0],
["Bulan wajib berpuasa?",["Syawal","Ramadan","Rajab","Muharram"],1],
["Ke arah mana umat Islam menghadap saat salat?",["Ka'bah","Gunung Uhud","Masjid Nabawi","Laut"],0],
["Malaikat pembawa wahyu?",["Mikail","Israfil","Jibril","Izrail"],2],
["Surah pertama dalam Al-Qur'an?",["Al-Baqarah","Al-Fatihah","An-Nas","Al-Ikhlas"],1],
["Berapa jumlah rukun iman?",["5","6","7","8"],1],
["Berapa salat wajib sehari semalam?",["3","4","5","6"],2]
];
let current=0,score=0,answered=false;
function show(){
answered=false;
document.getElementById("progress").textContent="Soal "+(current+1)+" dari 10";
document.getElementById("question").textContent=data[current][0];
document.getElementById("result").textContent="";
document.getElementById("next").disabled=true;
document.getElementById("next").textContent="Soal berikutnya";
let area=document.getElementById("answers");
area.innerHTML="";
data[current][1].forEach((answer,i)=>{
let b=document.createElement("button");
b.className="answer";
b.textContent=answer;
b.onclick=()=>check(i,b);
area.appendChild(b);
});
}
function check(i,b){
if(answered)return;
answered=true;
let correct=data[current][2];
document.querySelectorAll(".answer").forEach((x,j)=>{
x.disabled=true;
if(j===correct)x.style.background="#bce9c8";
});
if(i===correct){
score+=10;
document.getElementById("result").textContent="✅ Benar! +10 poin belajar.";
}else{
b.style.background="#ffd6d6";
document.getElementById("result").textContent="Belum tepat. Jawaban benar: "+data[current][1][correct];
}
document.getElementById("score").textContent=score;
document.getElementById("next").disabled=false;
if(current===9)document.getElementById("next").textContent="Lihat hasil";
}
function nextQuestion(){
if(!answered)return;
current++;
if(current<10){show();return;}
document.querySelector("main").innerHTML=
'<div class="card"><h2>🎉 Kuis selesai!</h2><h1>Skor: '+score+'/100</h1><p>Terima kasih sudah belajar bersama RIDO EARN.</p><button class="next" onclick="location.reload()">Ulangi kuis</button></div>';
}
show();
</script>
</body>
</html>
