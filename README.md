let song_name= document.querySelector(".song_name");
let song_img= document.querySelector(".song_img");
let prevBtn = document.querySelector("#prev");
let playBtn = document.querySelector("#play");
let nextBtn = document.querySelector("#next");
let progressBar = document.querySelector(".progressBar");
let song_start = document.querySelector(".song_start");
let song_end = document.querySelector(".song_end");
const songs = [
    {
        name: "SHAPE OF YOU ",
        singer: "Ed Sheeran",
        path: "./Source/song1.mp3",
        songImgPath: "./Source/song1.jpeg",
    },
    {
        name: "Let Me Love You ",
        singer: "Ed Sheeran",
        path: "./Source/song2.mp3",
        songImgPath: "./Source/song2.jpeg",
    },
    {
        name: "Photograph",
        singer: "Ed Sheeran",
        path: "./Source/song3.mp3",
        songImgPath: "./Source/song3.jpeg",
    },
];
let path_id=1;
let audio = new Audio(`./Source/song${path_id}.mp3`);
playBtn.addEventListener("click", function () {
    audio.paused ? audio.play() : audio.pause();
    if (playBtn.classList.contains("fa-play")) {
        playBtn.classList.remove("fa-play");
        playBtn.classList.add("fa-pause");
    } else {
        playBtn.classList.remove("fa-pause");
        playBtn.classList.add("fa-play");
    }
});
audio.addEventListener("timeupdate", () => {
    const progress = audio.currentTime * 100 / audio.duration;
    progressBar.value = progress;
    song_start.innerText=audio.currentTime.toFixed(2);
    song_end.innerText=audio.duration.toFixed(2);
});
progressBar.addEventListener("change", () => {
    const updatedtime = progressBar.value * audio.duration / 100;
    audio.currentTime = updatedtime;
    song_start.innerText=audio.currentTime.toFixed(2);
    song_end.innerText=audio.duration.toFixed(2);
})
prevBtn.addEventListener("click",()=>
{
    path_id=3;
    audio.src=`./Source/song${path_id}.mp3`;
    song_name.innerText="Photograph ";
    song_img.src=`./Source/song${path_id}.jpeg`;
    audio.play();
    playBtn.classList.remove('fa-play');
    playBtn.classList.add('fa-pause')
    audio.currentTime = 0;

});
nextBtn.addEventListener('click',()=>
{
    path_id=2;
    audio.src=`./Source/song${path_id}.mp3`;
    song_name.innerText="Let Me Love You ";
    song_img.src=`./Source/song${path_id}.jpeg`;
    audio.play();
    playBtn.classList.remove('fa-play');
    playBtn.classList.add('fa-pause')
    audio.currentTime = 0;

});
