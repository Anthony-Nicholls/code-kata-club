# Rainfall

- Go to https://editor.p5js.org
- Sign up or log in to enable saving 

## Code

```js
class RainDrop {  
  constructor() {
    this.position = createVector(random(-width, width * 2), 0);
    this.velocity = createVector(0, random(7, 12));
    this.thickness = random(0.01, 1.2);
    this.wind = createVector(0, 0);
  }
  
  setWind(wind) {
    this.wind = createVector (wind, 0);
  }
  
  draw() {
    const start = this.position.copy();
    this.position.add (this.velocity);
    this.position.add (this.wind);
    strokeWeight(this.thickness);
    line(start.x, start.y, this.position.x, this.position.y);
  }
  
  isFalling() {
    return this.position.y < height;
  }
}

var rainDrops = [];
var rainColour;

function setup() {
  createCanvas(400, 400);
  backgroundColour = color('black');
  rainColour = color('deepskyblue');
}

function createRainDrops (numberOfRainDrops) {
  for (var i = 0; i < numberOfRainDrops; ++i) {
    rainDrops.push(new RainDrop());
  }
}

function clearDroppedRain() {
  rainDrops = rainDrops.filter (function (rainDrop) {
    return rainDrop.isFalling();
  });
}

function applyWindToRainDrops(wind) {
  rainDrops.forEach(function (rainDrop) {
    rainDrop.setWind (wind);
  });
}

function drawRainDrops() {
  rainDrops.forEach(function (rainDrop) {
    rainDrop.draw();
  });
}

function draw() {
  background(backgroundColour);
  stroke(rainColour);
  
  const numberOfNewRainDrops = map(mouseY, 0, height, 5, 30, true);
  const wind = map(mouseX, 0, width, -5, 5, true);
  
  createRainDrops(numberOfNewRainDrops);
  applyWindToRainDrops(wind);
  drawRainDrops();
  clearDroppedRain();
}
```

## Challenges