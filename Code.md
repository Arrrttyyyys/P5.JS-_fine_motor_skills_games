# P5.JS-_fine_motor_skills_games
Sketch,js
//Screen control
let screenMode = 0;

//buttons
let b1;
let b2;
let b3;
let back;

//Loads all files that will be used in the code
function preload() {
  rocket = loadImage('rocket.png');
  soundFormats('mp3');
  fail = loadSound('fail.mp3');
  success = loadSound('success.mp3')
}

//Creates buttons and creates background that is not constantly being drawn
function setup() {
  createCanvas(800, 700);
  background('black');
  b1 = createButton("Start")
  b2 = createButton("Quit")
  b3 = createButton("Exercise 3")
  back = createButton("< Back")
  drawStars()
}

function draw() {
//Statement that calls other methods to be constantly drawn as other screens
  if(screenMode == 0) {
    screen1()
  }
  else if(screenMode == 1) {
    screen2()
  }
  else if(screenMode == 2) {
    Exer1();
  }
  else if(screenMode == 3) {
    Exer2();
  }
  else if(screenMode == 4) {
    Exer3();
  }
}

//Sets up menu with a start and a quit button to initiate UI
function screen1() {
  fill('white');
  textSize(45);
  text('Space Game', width/3, height/3)
  
  b1.html("Start")
  b1.position(width/2.4, height/2.15)
  b1.size(150, 50)
  b1.style("font-size", "25px")
  b1.mousePressed(updateScreen)
  
  b2.html("Quit")
  b2.position(width/2.4, height/1.7)
  b2.size(150, 50)
  b2.style("font-size", "25px")
  b2.mousePressed(quitBut)
}

//Creates exercise selection screen that allows user to navigate to each screen
function screen2() {
  fill('white');
  textSize(45);
  text('Select Exercise', width/3.2, height/3)
  
  b1.html("Exercise 1")
  b1.mousePressed(updateToExercise1)
  
  b2.html("Exercise 2")
  b2.mousePressed(updateToExercise2)
  
  b3.position(width/2.4, height/1.4)
  b3.size(150, 50)
  b3.style("font-size", "25px")
  b3.mousePressed(updateToExercise3)
  
  back.position(0, 0)
  back.size(150, 50)
  back.style("font-size", "25px")
  back.html("< Back")
  back.mouseClicked(backBut)
}

//Sets screen to exercise selection screen
function updateScreen() {
  screenMode = 1;
  background('black')
  drawStars()
  back.show()
  b3.show()
}

//Long back button that essentially resets every value every time the back button is selected
function backBut() {
  stroke(0.0001)
  screenMode = 0;
  background('black')
  drawStars()
  back.hide()
  b3.hide()
  b1.show()
  b2.show()
  screenSetup = 0
  screenSetup2 = 0
  ex2ScreenMode = 0
  ex3ScreenMode = 0
  setScreen = 0
  sScreen = 0
  ssScreen = 0
  ex2Score = 0
  timer2 = 3
  ex2screenSetup2 = 0
  score = 0;
  backColor = "black"
  lives = 3
  ex2screenSetup2 = 0
  setScreenLose = 0;
  ex1ScreenMode = 0
}

function quitBut() {
  remove()
}


function drawStars() {
  let i = 0
  while(i < height) {
    i++
    fill('white')
    circle(random(width), i, 2.5)
  }
}

//Ensures default values are correct and transfers screen to Exercise1.js
function updateToExercise1() {
  screenMode = 2
  setScreen = 0
  live = 3

}

//Ensures default values are correct and transfers screen to Exercise2.js
function updateToExercise2() {
  screenMode = 3
  setupScreen = 0
}

//Ensures default values are correct and transfers screen to Exercise3.js
function updateToExercise3() {
  screenMode = 4
  instruct = 0
  screenSetup = 0
  ex3ScreenMode = 0
}
Exercise1.js: 
//Sets up default values to ensure exercise 1 is the same every time it is launched.
let setScreen = 0;
let setScreenLose = 0;
let ex1ScreenMode = 0;
let d = 70;
let p1 = d;
let p2 = p1 + d;
let p3 = p2 + d;
let p4 = p3 + d;
let circleY = 350;
let ellipseY = 350;
let YVel = 2;
let direction = 0;
let projectileX = 400;
let projectileY = 100;
let projectileStatus = 0;
let invaderX = 0;
let live = 3;
let scores = 0;

//Called in the draw function, repeated constantly
function Exer1() {
  b1.hide();
  b2.hide();
  b3.hide();
  
  //Instruction screen is run one time and not being constantly drawn, code below is to make sure that the background is drawn once. If not, drawStars() would repetitely be called and stars would bounce all over the screen
  if (ex1ScreenMode == 0) {
    if (setScreen == 0) {
      background("black");
      drawStars();
      invaderX = width / 2 - 25;
      setScreen++;
    }
    //Instructions
    fill("white");
    textSize(45);
    text("Instructions", width / 3 + 20, height / 3);
    textSize(25);
    text(
      "The goal of this exercise is to develop timing skills and hand-eye",
      30,
      height / 2.5
    );
    text(
      "coordination. A UFO will bounce back and forth at the top of the",
      30,
      height / 2.5 + 40
    );
    text(
      "screen, and when the user presses the SPACE key, a projectile will",
      30,
      height / 2.5 + 80
    );
    text(
      "shoot. The goal is to hit the enemy at the bottom of the screen as",
      30,
      height / 2.5 + 120
    );
    text(
      "many times as you can. If you miss 3 times, you lose. Good Luck!",
      30,
      height / 2.5 + 160
    );
    b1.html("Begin");
    b1.show();
    b1.position(width / 2.4, height / 1.4);
    b1.mousePressed(updateScreenModeEX1);
  } else if (ex1ScreenMode == 1) {
    if (live == 0) {
      updateScreenModeEX1();
    }
    //Sets up UFO and how it moves across screen
    stroke(255);
    background(48, 20, 45);
    drawLive();
    stroke(153);
    line(700, 100, 100, 100);
    line(100, 70, 100, 130);
    line(700, 70, 700, 130);

    fill(0);
    circle(circleY, 50, 50);

    fill(0);
    ellipse(ellipseY, 60, 90, 20);

    circleY = circleY + YVel;
    ellipseY = ellipseY + YVel;

    if (circleY > 670) {
      YVel = YVel * -1;
    }
    if (ellipseY < 130) {
      YVel = YVel * -1;
    }
    //Sets up non-moving items on screen
    fill("white");
    textSize(25);
    text("Lives: ", 5, 75);
    text("Score: ", width / 2 - 40, height - 50);
    text(scores, width / 2 + 40, height - 48);
    line(100, 500, 700, 500);
    line(100, 470, 100, 530);
    line(700, 470, 700, 530);
    if (projectileStatus == 1) {
      projectileX = circleY;
      drawProjectile();
    }
    drawInvader();
  } else if (ex1ScreenMode == 2) {
    stroke(0.0001)
    if(setScreenLose == 0) {
       background("black")
       drawStars()
       setScreenLose++
       }
    textSize(80);
    fill("white");
    text("Game Over!", width / 2 - 220, height / 2);
    textSize(25);
    text("Score Received: ", width / 2 - 120, height / 2 + 30);
    text(scores, width / 2 + 80, height / 2 + 30);
    back.position(430, height / 2 + 50);
    back.html("Quit");
    b1.show();
    b1.position(230, height / 2 + 50);
    b1.html("Try Again");
    b1.mousePressed(resetGame1);
  }
}
    //Draws the square that the user targets with UFO
function drawInvader() {
  fill("black");
  square(invaderX, 475, 50);
}

//Shoots a projectile at target each time space button is pressed.
function keyPressed() {
  if (key == " ") {
    projectileStatus = 1;
    if (YVel > 0) {
      direction = 2;
    } else {
      direction = -2;
    }
    YVel = 0;
  }
}

//Draws lives that decrease each time user makes a mistake
function drawLive() {
  fill("white");
  if (live == 1 || live == 2 || live == 3) {
    rocket.resize(25, 50)
    image(rocket, 25, 100)
  }
  if (live == 2 || live == 3) {
    image(rocket, 25, 160)
  }
  if (live == 3) {
    image(rocket, 25, 220)
  }
  fill("white");
}

//Draws circle that fires from UFO's position and hits target
function drawProjectile() {
  if (setScreen == 1) {
    fill("red");
    circle(projectileX, projectileY, 25);
    if (projectileY != 500) {
      projectileY += 5;
    } else {
      projectileY = 100;
      YVel = direction;
      projectileStatus = 0;
    }

    if (
      projectileX <= invaderX + 50 &&
      projectileX >= invaderX &&
      projectileY == 500
    ) {
      invaderX = random(150, 650);
      scores += 10;
      success.play()
    } else if (
      (projectileX >= invaderX + 50 || projectileX <= invaderX) &&
      projectileY == 500
    ) {
      live--;
      fail.play()
    }
  }
}

//Updates screen from instruction, to game, to game over screen.
function updateScreenModeEX1() {
  ex1ScreenMode++;
}

//Resets game from game over screen and makes sure all values are default.
function resetGame1() {
  ex1ScreenMode = 1;
  d = 70;
  p1 = d;
  p2 = p1 + d;
  p3 = p2 + d;
  p4 = p3 + d;
  circleY = 350;
  ellipseY = 350;
  setScreenLose = 0;
  YVel = 1;
  direction = 0;
  projectileX = 400;
  projectileY = 100;
  projectileStatus = 0;
  live = 3;
  scores = 0;
  back.position(0, 0);
  back.html("< Back");
}
![image](https://github.com/Arrrttyyyys/P5.JS-_fine_motor_skills_games/assets/125960838/a577548b-47fb-43b7-b510-7bccb25d72bf)
