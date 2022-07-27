# Wavemaker

- Go to https://editor.p5js.org
- Sign up or log in to enable saving 

## Code

```js
let time = 0;

function setup() {
  createCanvas(600, 600);
  noStroke();
  fill(40, 200, 40);
}

function draw() {
  background(10, 10);

  for (let x = 0; x <= width; x = x + 30) {
    for (let y = 0; y <= height; y = y + 30) {
      
      const xAngle = map(mouseX, 0, width, -4 * PI, 4 * PI, true);
      const yAngle = map(mouseY, 0, height, -4 * PI, 4 * PI, true);
      
      const angle = xAngle * (x / width) + yAngle * (y / height);

      const circleX = x + 20 * cos(2 * PI * time + angle);
      const circleY = y + 20 * sin(2 * PI * time + angle);

      circle(circleX, circleY, 10);
    }
  }
  time += 0.01;
}
```

## Challenges

- Can you change the colours?
- Can you change the speed?
- Can you make the trails on the circle longer or shorter?
