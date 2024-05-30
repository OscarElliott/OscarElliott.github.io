---
layout: page
permalink: /shmizzyP/
title: Happy 21st <3
description: ewewewewewew
nav: false
nav_order: 5
---

<style>
    body {
        text-align: center;
        font-family: 'Comic Sans MS', 'Comic Sans', cursive;
        color: #ff69b4;
    }
    h1 {
        font-size: 3em;
        margin-top: 50px;
        cursor: pointer;
        padding-bottom: 20px;
    }
    h2 {
        font-size: 2em;
        margin-top: 20px;
    }
    img {
        border: 5px solid #ff69b4;
        border-radius: 20px;
        box-shadow: 0 0 20px pink;
        max-width: 100%;
        height: auto;
        cursor: pointer;
    }
    .hidden {
        display: none;
    }
    .sparkle {
        font-size: 1.5em;
        color: #ffd700;
        animation: sparkle 1s infinite;
    }
    @keyframes sparkle {
        0% { opacity: 1; }
        50% { opacity: 0.5; }
        100% { opacity: 1; }
    }
</style>


<img src="https://oscarelliott.github.io/assets/img/Evilcat.jpeg" class="hidden" alt="Surprise Image">

<h1 onclick="handleClick()" >I love you <span class="sparkle">❤️</span></h1>

<img id="hiddenImage" onclick="playAudio()" src="https://oscarelliott.github.io/assets/img/cat.png" width="100%" height="400px">

<h2>Happy Birthday!</h2>

<audio id="audio" src="https://oscarelliott.github.io/assets/audio/ewewewewe.mp3"></audio>

<script>
    let imageSize = 2;

    function handleClick() {
        showAndResizeImage();
    }

    function showAndResizeImage() {
        const img = document.getElementById('hiddenImage');
        img.style.display = 'block';
        imageSize += 10;
        img.style.cssText = 'width: ' + imageSize + '% !important;';
    }

    function playAudio() {
        var audio = document.getElementById('audio');
        audio.play();
    }
</script>