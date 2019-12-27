---
layout: post
title:  "CSS demonstrations"
date:   2016-03-02
categories: ['web development']
tags: ['css']
---

<div class="css-demo-carousel-container">
  <div class="css-demo-carousel">
    <div>1</div>
  	<div>2</div>
  	<div>3</div>
  	<div>4</div>
    <div>5</div>
  	<div>6</div>
  </div>
</div>

```html
<div class="css-demo-carousel-container">
  <div class="css-demo-carousel">
    <div>1</div>
  	<div>2</div>
  	<div>3</div>
  	<div>4</div>
    <div>5</div>
  	<div>6</div>
  </div>
</div>
```

```css
.css-demo-carousel-container { perspective: 1000px; transform: translateX(100px);}
.css-demo-carousel { position: relative; transform-style: preserve-3d; width: 100px; height: 60px; animation: play 10s infinite linear;}
.css-demo-carousel div { position: absolute; width: 100%; height: 100%; text-align: center; line-height: 60px; color: white;}
.css-demo-carousel div:nth-child(1) { background: rgba(255,0,0,.5); transform: rotateY(0deg) translateZ(110px);}
.css-demo-carousel div:nth-child(2) { background: rgba(128,128,0,.5); transform: rotateY(60deg) translateZ(110px);}
.css-demo-carousel div:nth-child(3) { background: rgba(255,165,0,.5); transform: rotateY(120deg) translateZ(110px);}
.css-demo-carousel div:nth-child(4) { background: rgba(255,255,0,.5); transform: rotateY(180deg) translateZ(110px);}
.css-demo-carousel div:nth-child(5) { background: rgba(255,128,0,.5); transform: rotateY(240deg) translateZ(110px);}
.css-demo-carousel div:nth-child(6) { background: rgba(128,255,0,.5); transform: rotateY(300deg) translateZ(110px);}
@keyframes play {
  from { transform: rotateY(360deg);}
  to { transform: rotateY(0);}
}
```

<div class="css-demo-cube-container">
  <div class="css-demo-cube">
    <div>1</div>
  	<div>2</div>
  	<div>3</div>
  	<div>4</div>
  </div>
</div>

```html
<div class="css-demo-cube-container">
  <div class="css-demo-cube">
    <div>1</div>
  	<div>2</div>
  	<div>3</div>
  	<div>4</div>
  </div>
</div>
```

```css
.css-demo-cube-container { perspective: 1000px; transform: translateX(15px);}
.css-demo-cube { position: relative; transform-style: preserve-3d; width: 60px; height: 60px; animation: play 4s infinite linear;}
.css-demo-cube div { position: absolute; width: 100%; height: 100%; text-align: center; line-height: 60px; color: white; backface-visibility: hidden;}
.css-demo-cube div:nth-child(1) { background: rgba(255,0,0,1); transform: rotateY(0deg) translateZ(30px);}
.css-demo-cube div:nth-child(2) { background: rgba(128,128,0,1); transform: rotateY(90deg) translateZ(30px); }
.css-demo-cube div:nth-child(3) { background: rgba(255,165,0,1); transform: rotateY(180deg) translateZ(30px);}
.css-demo-cube div:nth-child(4) { background: rgba(255,255,0,1); transform: rotateY(-90deg) translateZ(30px);}
@keyframes play {
  from { transform: rotateY(360deg);}
  to { transform: rotateY(0);}
}
```

<div class="css-demo-loading"></div>

```html
<div class="css-demo-loading"></div>
```

```css
.css-demo-loading { position: relative; width: 40px; height: 40px; border-radius: 50%; border: solid 2px transparent; border-top-color: red; animation: rotate 1s linear infinite;}
.css-demo-loading::before { content: ''; position: absolute; left: 4px; right: 4px; top: 4px; bottom: 4px; border-radius: 50%; border: solid 2px transparent; border-top-color: blue; animation: rotate 1.5s linear infinite;}
.css-demo-loading::after { content: ''; position: absolute; left: 8px; right: 8px; top: 8px; bottom: 8px; border-radius: 50%; border: solid 2px transparent; border-top-color: green; animation: rotate 2s linear infinite;}
@keyframes rotate {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
```

<div class="css-demo-5"></div>

```html
<div class="css-demo-5"></div>
```

```css
.css-demo-5 { width: 60px; height: 40px; background: #3f2f44; animation: 1.5s polygon infinite; clip-path: polygon(45% 45%, 55% 45%, 55% 55%, 45% 55%);}
@keyframes polygon {
  12% { clip-path: polygon(25% 25%, 55% 45%, 55% 55%, 45% 55%);}
  24% { clip-path: polygon(0 0, 55% 45%, 55% 55%, 45% 55%);}
  36% { clip-path: polygon(0 0, 75% 25%, 55% 55%, 45% 55%);}
  48% { clip-path: polygon(0 0, 100% 0, 55% 55%, 45% 55%);}
  60% { clip-path: polygon(0 0, 100% 0, 75% 75%, 45% 55%);}
  72% { clip-path: polygon(0 0, 100% 0, 100% 100%, 45% 55%);}
  84% { clip-path: polygon(0 0, 100% 0, 100% 100%, 25% 55%);}
  100% { clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);}
}
```

<div class="css-demo-4"><i class="icon home"></i></div>

```html
<div class="css-demo-4"><i class="icon home"></i></div>
```

```css
.css-demo-4 { position: relative; width: 40px; height: 40px; box-shadow: 0 0 1px #666; border-radius: 50%; font-size: 1.5em; line-height: 40px; text-align: center; color: #666; transition: .5s cubic-bezier(.3,0,0,1.3);}
.css-demo-4:before { content: ''; position: absolute; left: 0; right: 0; top: 0; bottom: 0; border-radius: 50%; background: #39c492; opacity: 0; transform: scale(0,0); transition: .5s cubic-bezier(.3,0,0,1.3);}
.css-demo-4:hover { color: #fff; box-shadow: 0 0 1px #39c492;}
.css-demo-4:hover:before { opacity: 1; transform: scale(1,1);}
.css-demo-4 i { position: relative; }
```

<div class="css-demo-3"></div>

```html
<div class="css-demo-3"></div>
```

```css
.css-demo-3 { width: 32px; height: 32px; border: 2px solid #444; border-radius: 50%; animation: pulsecircle .7s linear infinite;}
@keyframes pulsecircle {
  0% {
    transform: scale(.1);
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  100% {
    transform: scale(1.2);
    opacity: 0;
  }
}
```

<div class="css-demo-2">Hover me</div>

```html
<div class="css-demo-2">Hover me</div>
```

```css
.css-demo-2 { position: relative; display: inline-block; cursor: pointer;}
.css-demo-2:before { content: ''; position: absolute; left: 0; bottom: 0; width: 100%; height: 1px; background: #444; transition: transform .2s; backface-visibility: hidden; transform: scaleX(0);}
.css-demo-2:hover:before { transform: scaleX(1);}
```

<div class="css-demo-1"><span></span><span></span><span></span></div>

```html
<div class="css-demo-1"><span></span><span></span><span></span></div>
```

```css
.css-demo-1 { position: relative; width: 25px; height: 35px; cursor: pointer;}
.css-demo-1 span { position: absolute; left: 0; top: 7px; width: 100%; height: 2px; background: #444; transition: all .2s; transform-origin: right center;}
.css-demo-1 span:nth-child(2) { top: 16px;}
.css-demo-1 span:last-child { top: 25px;}
.css-demo-1:hover span:first-child { transform: rotate(-45deg);}
.css-demo-1:hover span:nth-child(2) { height: 0;}
.css-demo-1:hover span:last-child { transform: rotate(45deg);}
```
