// Bouncing.pde

ArrayList<Ball> balls; // store multiple Ball objects

void setup() {
  size(800, 500);
  balls = new ArrayList<Ball>();
  // start with one default ball
  balls.add(new Ball());
}

void draw() {
  background(30);
  
  // update and display all balls
  for (Ball b : balls) {
    b.update();
    b.display();
  }
}

// Add a new ball on mouse click
void mousePressed() {
  balls.add(new Ball(mouseX, mouseY));
}

class Ball {
  float x, y;   // position
  float vx, vy; // velocity
  float r;      // radius
  color c;      // color

  // Default constructor → center of screen
  Ball() {
    x = width/2;
    y = height/2;
    r = 30;
    vx = random(2, 5) * (random(1) > 0.5 ? 1 : -1);
    vy = random(2, 5) * (random(1) > 0.5 ? 1 : -1);
    c = color(random(255), random(255), random(255));
  }

  // Constructor with location (spawn at mouse)
  Ball(float startX, float startY) {
    x = startX;
    y = startY;
    r = 30;
    vx = random(2, 5) * (random(1) > 0.5 ? 1 : -1);
    vy = random(2, 5) * (random(1) > 0.5 ? 1 : -1);
    c = color(random(255), random(255), random(255));
  }

  // Update position and bounce off walls
  void update() {
    x += vx;
    y += vy;

    if (x - r < 0 || x + r > width) {
      vx *= -1;
    }
    if (y - r < 0 || y + r > height) {
      vy *= -1;
    }
  }

  // Draw the ball
  void display() {
    fill(c);
    noStroke();
    ellipse(x, y, r*2, r*2);
  }
}
