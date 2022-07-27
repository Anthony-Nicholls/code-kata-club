# Recursion Tree

- Go to https://editor.p5js.org
- Sign up or log in to enable saving 

## Code

```js
function branch(length, thickness) {
  push();
  if (length > 3) {
    stroke(color('black'));
    strokeWeight(thickness);
    line(0, 0, 0, -length);
    translate(0, -length);
    
    rotate(random (15, 35));
    branch(length * random (0.6, 0.75), 
           thickness * random (0.6, 0.9));
    
    rotate(random (-30, -70));
    branch(length * random (0.6, 0.75), 
           thickness * random (0.6, 0.9));
    
  } else {
    noStroke();
    var leafColour = color('white');
    leafColour.setAlpha (random(0, 200));
    fill(leafColour)
    circle(0, 0, random(3, 15));
  }
  pop();
}

function setup() {
  createCanvas(400, 400);
  angleMode(DEGREES);
  noLoop();
}

function draw() {
  background(240);
  translate(width / 2, height);
  branch(random(50, 120), random(2, 4));
}
```

## Challenges

