---
title: 👋 Handsfree
date: 2021-06-11
layout: post
---

Last week I experimented with [Handsfree](https://handsfree.js.org/), a JS library to allow users to track body, face and hand movement. I tried to apply it to a webmapping application. [In the following example](https://t.co/6i4zz7KPge?amp=1), you can pan North or South depending on where your index finger is pointing up ☝️ or down 👇.

<div class="glitch-embed-wrap" style="height: 420px; width: 100%;">
  <iframe
    src="https://glitch.com/embed/#!/embed/handsfree-webmapping?path=index.html&previewSize=100"
    title="handsfree-zoom-webmapping on Glitch"
    allow="geolocation; microphone; camera; midi; vr; encrypted-media"
    style="height: 100%; width: 100%; border: 0;">
  </iframe>
</div>

![north-handsfree](https://github.com/ramiroaznar/blog/blob/master/assets/imgs/2021-06-11-north.gif?raw=true)

![south-handsfree](https://github.com/ramiroaznar/blog/blob/master/assets/imgs/2021-06-11-south.gif?raw=true)

In this second example, you can zoom in or out based on the bounding box of your hand. If it is a fist ✊, it will zoom in. If your hand is open ✋, it will zoom out.

<div class="glitch-embed-wrap" style="height: 420px; width: 100%;">
  <iframe
    src="https://glitch.com/embed/#!/embed/handsfree-webmapping?path=index.html&previewSize=100"
    title="handsfree-zoom-webmapping on Glitch"
    allow="geolocation; microphone; camera; midi; vr; encrypted-media"
    style="height: 100%; width: 100%; border: 0;">
  </iframe>
</div>

![zoom-handsfree](https://github.com/ramiroaznar/blog/blob/master/assets/imgs/2021-06-11-zoom.gif?raw=true)
