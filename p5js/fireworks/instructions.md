# Fireworks

- Go to https://editor.p5js.org
- Sign up or log in to enable saving 

## Code

```js
function randomColour() {
  return color(
    random(0, 255),
    random(0, 255),
    random(0, 255)
  );
}

class Particle {
  constructor(x, y) {
    this.position = createVector (x, y);
    
    const angle = random(0, 2 * PI);
    const magnitude = random(0.2, 5);
    this.velocity = p5.Vector.fromAngle(angle, magnitude);
    this.friction = createVector (0.99, 0.99);
    this.gravity = createVector (0, 0.1);
    this.colour = randomColour();
    this.size = random(1, 6);
  }
  
  draw() {
    strokeWeight(this.size);
    stroke(this.colour);
    point(this.position.x, this.position.y);
    
    this.position.add (this.velocity);
    this.velocity.mult (this.friction);
    this.velocity.add (this.gravity);

    this.colour.setAlpha(alpha(this.colour) * random(0.98, 1.0))
  }
  
  isVisible() {
    return this.position.x >= 0 && 
      this.position.x <= width && 
      this.position.y >= 0 &&
      this.position.y <= height &&
      alpha(this.colour) > 0;
  }
}

let particles = [];

function setup() {
  createCanvas(400, 400);
}

function createParticleExplosion(x, y, numberOfParticles) {
  for (var i = 0; i < numberOfParticles; ++i) {
    particles.push(new Particle(x, y));
  }
}

function mouseClicked() {
  createParticleExplosion(mouseX, mouseY, random(250, 750));
}

function drawParticles() {
  particles.forEach(function (particle) {
    particle.draw();
  });
}

function removeInvisibleParticles() {
  particles = particles.filter(function (particle) {
    return particle.isVisible();
  });
}

function draw() {
  background(0);
  
  if (random (100) < 3) {
    createParticleExplosion (random(0, width), 
                             random(0, height), 
                             random(100, 350));
  }
  
  drawParticles();
  removeInvisibleParticles();
}
```

## Challenges

- What happens if you remove the line `removeInvisibleParticles();`

- Can you increase the gravity?

- Can you change the number 