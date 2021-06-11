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

This library allows you to get the coordinates of the different vertixes in your hand structure, thus getting the tip and bottom position from the index finger could give you the information about where it is pointing.

```javascript
// fingers array, index finger array, tip y and bottom y positions
const fingers = data.handpose.annotations
const indexFinger = fingers.indexFinger
const tipY = indexFinger[3]
const bottomY = indexFinger[0]

// if tip position higher than bottom then go North!
if (tipY > bottomY) {
  if (lat < 90) {
    console.log('North!')
    lat = lat + 2
    console.log(lat)
    map.flyTo({center: [lng, lat]})
  }
}

// if tip position lower than bottom then go South!
if (tipY < bottomY) {
  if (lat > -90) {
    console.log('South!')
    lat = lat - 2
    console.log(lat)
    map.flyTo({center: [lng, lat]})
  } 
}
``` 

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

The app calculates the length of the diagonal from the two coordinates of the bounding box of the user hand:

```javascript
const getLength = (bbox) => {
  let [x, y] = bbox.topLeft
  let [x0, y0] = bbox.bottomRight
  // from http://jsfromhell.com/math/line-length
  return Math.sqrt((x -= x0) * x + (y -= y0) * y);
};
```

Based on this calculation and setting a breaking point value to differenciate when the hand is a fist or it is open, the app zoom in or out respectively:

```javascript
const zoomBasedOnLength = (length) => {
  console.log(length)
  // 500 is an arbitrary value
  // if length less than 600, hand position as a fist, zoom in
  if (length < 600) {
    console.log('Zoom in!')
    if (zoom < 18) zoom += 1
  }
  // if length more or equal to 600, hand position open, zoom out
  else {
    console.log('Zoom out!')
    if (zoom > 1) zoom -= 1
  } 
  
  console.log(zoom)
  
  map.flyTo({center: [lng, lat], zoom: zoom})
};
``` 

```javascript
// get bbox from hand
let bbox = data.handpose.boundingBox
// get length from top left corner to bottom right corner
length = getLength(bbox)
// zoom in or out based on hand position
zoomBasedOnLength(length)
```

![zoom-handsfree](https://github.com/ramiroaznar/blog/blob/master/assets/imgs/2021-06-11-zoom.gif?raw=true)
