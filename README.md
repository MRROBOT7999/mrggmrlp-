
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>Valentine ❤️</title>

<style>
body{
    margin:0;
    background: radial-gradient(circle at center, #1a0005, #000);
    overflow:hidden;
    font-family: Arial;
    color:white;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}

/* نص الأغنية */
#lyrics{
    font-size:40px;
    text-align:center;
    width:80%;
    min-height:60px;
    text-shadow:0 0 20px #ff004c;
    animation: glow 1.5s infinite alternate;
}

@keyframes glow{
    from{ text-shadow:0 0 10px #ff004c; }
    to{ text-shadow:0 0 30px #ff4d88; }
}

/* قلوب متحركة */
.heart{
    position:absolute;
    color:#ff4d88;
    font-size:20px;
    animation: float 5s linear infinite;
}

@keyframes float{
    0%{ transform:translateY(100vh); opacity:1; }
    100%{ transform:translateY(-10vh); opacity:0; }
}

/* نبض */
.beat{
    animation: beat 0.6s infinite;
}

@keyframes beat{
    0%,100%{ transform:scale(1); }
    50%{ transform:scale(1.1); }
}
</style>
</head>
<body>

<div id="lyrics"></div>

<audio id="song">
    <source src="Amr_Diab_Khalik_Maaya.mp3" type="audio/mpeg">
</audio>

<script>
const song = document.getElementById("song");
const lyricsDiv = document.getElementById("lyrics");

// ✍️ حط كلماتك هنا
const lyrics = [
    { time: 67, text: "عارف بتعمل فيه اي كلمه حبيبي" },
    { time: 71, text: "زي اول مره بي حس بـ امان " },
    { time: 75, text: "خليك معايه يا حبيبي  " },
    { time: 79, text: "مهما كان " }
];

// كتابة حرف حرف
function typeWriter(text){
    lyricsDiv.textContent = "";
    lyricsDiv.classList.add("beat");
    let i = 0;
    let speed = 50;

    function typing(){
        if(i < text.length){
            lyricsDiv.textContent += text.charAt(i);
            i++;
            setTimeout(typing, speed);
        }
    }
    typing();
}

// تحديث الكلمات حسب الوقت
song.addEventListener("timeupdate", ()=>{
    const current = Math.floor(song.currentTime);
    lyrics.forEach(line=>{
        if(current === line.time){
            typeWriter(line.text);
        }
    });
});

// يبدأ من 1:07
song.currentTime = 67;
song.play();

// توليد قلوب عشوائية
setInterval(()=>{
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "❤️";
    heart.style.left = Math.random()*100 + "vw";
    heart.style.fontSize = (15 + Math.random()*25) + "px";
    document.body.appendChild(heart);

    setTimeout(()=>{ heart.remove(); },5000);
},400);

</script>

</body>
</html>
