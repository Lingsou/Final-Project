# Final-Project
My final project is a solo player pong game. The goal for this game is to prevent the ball reach the bottom, also try to bounce it back to hit bricks in order to get points and win.

Summary
I draw 12 bricks on the top of the screen, a ball randomly bouncing within the canvas and a brick at the bottom og the canvas that player can control. Player need to use the bottom bricks to prevent ball hitting the bottom part of the canvas, otherwise the game will end. Player also need to control the bottom bricks to bounce the ball up to hit the upper bricks in order to get points. The upper bricks will disappear when ball hit on them. Once all the upper bricks disappear the player will win.


Component Parts
This project contain a bouncing ball, a contral brick at the bottom, 12 bricks in the upper part of the canvas for points, a score recorder on the top right corner.



Timeline


Week 0: Write Proposal
Week 1:Draw the set up of the canvas(12 bricks, ball and bottom bricks)
Week 2:Figure out how to use the brick to bounce the ball back and how to make upper bricks disappear after hit by the ball
Week 3:Add score recoder and end game text.
Week 4: Present!

Challenges
I have encounter trouble when I try to make the upper bricks disappear after hit by the ball. Finally I realize i only need to change their x or y coordinate to change their location instead of actually delete them.

Completed Work
Links: https://editor.p5js.org/lingsou@cca.edu/sketches/NZb68pE_y

var w = 800;
var h = 600;
//12个方块的x,y坐标
var b1x = w/9;
var b2x = ((w/9)*3);
var b3x = ((w/9)*5);
var b4x = ((w/9)*7);

var b1y = h/6;
var b2y = h/6;
var b3y = h/6;
var b4y = h/6;

var b1x2 = w/9;
var b2x2 = ((w/9)*3);
var b3x2 = ((w/9)*5);
var b4x2 = ((w/9)*7);

var b1y2 = (h/6)*2;
var b2y2 = (h/6)*2;
var b3y2 = (h/6)*2;
var b4y2 = (h/6)*2;

var b1x3 = w/9;
var b2x3 = ((w/9)*3);
var b3x3 = ((w/9)*5);
var b4x3 = ((w/9)*7);

var b1y3 = (h/6) + ((h/6)/2);
var b2y3 = (h/6) + ((h/6)/2);
var b3y3 = (h/6) + ((h/6)/2);
var b4y3 = (h/6) + ((h/6)/2);

var r = 20;
var x;
var y;    

var xs = 4;  
var ys = 4; 

var xd = 1;  
var yd = 1;  

var lives = 1;
var Score = 0;


var bw = (w/9);
var bh = (h/24);

function setup() 
{
  createCanvas(800, 600);

  noStroke();
  x = w/2;
  y = h/2;
}
//小球碰到墙壁会反弹
function wallBounce() {
  
  if (x > w-r || x < r ) {
    xd *= -1;
  }
 
  if (y > h-r || y < r ) {
    yd *= -1;
  }
}
//鼠标反弹位置
function paletteBounce() {

  if (y >= h-100 && y <= h-100 && x >= mouseX-(w/10) && x <= mouseX+(w/10)) {
    yd = random(-1,-0.75);
  }
}

function fail() {
//如果没有接到小球，那么就会弹出失败
  if (y >= 580 ) {
    x = w/2;
    y = h/2;
    lives--;
    Streak=0;
    yd=1;
  }
  if (lives <= 0) {
    fill(255);
    textSize(50);
    text("Lose", 305, 300);

    x=0;
    y=0;
    xs = 0;
    ys = 0;
    Streak = 0;
    
    if (mouseIsPressed) {
      x = w/2;
      y = h/2;
      xs = 4;
      ys = 4;
      lives = 1;
      Score = 0;
      yd = 1;
      xd = -1;

      b1x = w/9;
      b2x = ((w/9)*3);
      b3x = ((w/9)*5);
      b4x = ((w/9)*7);

      b1y = h/6;
      b2y = h/6;
      b3y = h/6;
      b4y = h/6;

      b1x2 = w/9;
      b2x2 = ((w/9)*3);
      b3x2 = ((w/9)*5);
      b4x2 = ((w/9)*7);

      b1y2 = (h/6)*2;
      b2y2 = (h/6)*2;
      b3y2 = (h/6)*2;
      b4y2 = (h/6)*2;
      
      b1x3 = w/9;
      b2x3 = ((w/9)*3);
      b3x3 = ((w/9)*5);
      b4x3 = ((w/9)*7);

      b1y3 = (h/6) + ((h/6)/2);
      b2y3 = (h/6) + ((h/6)/2);
      b3y3 = (h/6) + ((h/6)/2);
      b4y3 = (h/6) + ((h/6)/2);
    }
  }
}

//12个方块的代码
function blocks(bx,by,bw,bh) {
  fill(random(255),random(255),random(255));
  rect(bx, by, bw, bh);
}
function drawBlocks() {
  blocks(b1x, b1y, bw, bh);
  blocks(b2x, b2y, bw, bh);
  blocks(b3x, b3y, bw, bh);
  blocks(b4x, b4y, bw, bh);

  blocks(b1x2, b1y2, bw, bh);
  blocks(b2x2, b2y2, bw, bh);
  blocks(b3x2, b3y2, bw, bh);
  blocks(b4x2, b4y2, bw, bh);
  
  blocks(b1x3, b1y3, bw, bh);
  blocks(b2x3, b2y3, bw, bh);
  blocks(b3x3, b3y3, bw, bh);
  blocks(b4x3, b4y3, bw, bh);
}
//方块被碰撞之后就会消失

function blockBounce() {
  if ( x >= b1x && x <= b1x+bw && y <= b1y + bh  && y >= b1y) {
    yd *= -1;
    b1x = 1000;
    Score++;
  }
  if ( x >= b2x && x <= b2x+bw && y <= b2y + bh  && y >= b2y) {
    yd *= -1;
    b2x = 1000;
    Score++;
  }
  if ( x >= b3x && x <= b3x+bw && y <= b3y + bh  && y >= b3y) {
    yd *= -1;
    b3x = 1000;
    Score++;
  }
  if ( x >= b4x && x <= b4x+bw && y <= b4y + bh  && y >= b4y) {
    yd *= -1;
    b4x = 1000;
    Score++;
  }

  
  if ( x >= b1x2 && x <= b1x2+bw && y <= b1y2 + bh  && y >= b1y2) {
    yd *= -1;
    b1x2 = 1000;
    Score++;
  }
  if ( x >= b2x2 && x <= b2x2+bw && y <= b2y2 + bh  && y >= b2y2) {
    yd *= -1;
    b2x2 = 1000;
    Score++;
  }
  if ( x >= b3x2 && x <= b3x2+bw && y <= b3y2 + bh  && y >= b3y2) {
    yd *= -1;
    b3x2 = 1000;
    Score++;
  }
  if ( x >= b4x2 && x <= b4x2+bw && y <= b4y2 + bh  && y >= b4y2) {
    yd *= -1;
    b4x2 = 1000;
    Score++;
  }
  
    if ( x >= b1x3 && x <= b1x3+bw && y <= b1y3 + bh  && y >= b1y3) {
    yd *= -1;
    b1x3 = 1000;
    Score++;
  }
  if ( x >= b2x3 && x <= b2x3+bw && y <= b2y3 + bh  && y >= b2y3) {
    yd *= -1;
    b2x3 = 1000;
    Score++;
  }
  if ( x >= b3x3 && x <= b3x3+bw && y <= b3y3 + bh  && y >= b3y3) {
    yd *= -1;
    b3x3 = 1000;
    Score++;
  }
  if ( x >= b4x3 && x <= b4x3+bw && y <= b4y3 + bh  && y >= b4y3) {
    yd *= -1;
    b4x3 = 1000;
    Score++;
  }
}
///////////////////////////判断胜利的条件，每次击打中方块score变量就会增加1，当全部打中，也就是12的时候，就会提示胜利
function win() {
  if (Score == 12) {
    fill(255);
    textSize(50);
    text("Win", 305, 300);
    textSize(25);
    x = 0;
    y = 0;
    xs = 0;
    ys = 0;
    
    if (mouseIsPressed) {
      x = w/2;
      y = h/2;
      xs = 4;
      ys = 4;
      yd = 1;

      lives = 1;
      Score = 0;
      yd *= 1;
      xd *= -1;

      b1x = w/9;
      b2x = ((w/9)*3);
      b3x = ((w/9)*5);
      b4x = ((w/9)*7);

      b1y = h/6;
      b2y = h/6;
      b3y = h/6;
      b4y = h/6;

      b1x2 = w/9;
      b2x2 = ((w/9)*3);
      b3x2 = ((w/9)*5);
      b4x2 = ((w/9)*7);

      b1y2 = (h/6)*2;
      b2y2 = (h/6)*2;
      b3y2 = (h/6)*2;
      b4y2 = (h/6)*2;
      
      b1x3 = w/9;
      b2x3 = ((w/9)*3);
      b3x3 = ((w/9)*5);
      b4x3 = ((w/9)*7);

      b1y3 = (h/6) + ((h/6)/2);
      b2y3 = (h/6) + ((h/6)/2);
      b3y3 = (h/6) + ((h/6)/2);
      b4y3 = (h/6) + ((h/6)/2);
      
  
    }
  }
}

function draw() {
  background(0);
//小球运动变量
  x = x + ( xs * xd );
  y = y + ( ys * yd );
  textSize(50);
  fill(255);
//分数
  text(Score, 710,50);
//小球碰到墙壁反弹
  wallBounce();
//鼠标反弹小球
  paletteBounce();
//判断是否失败
  fail();
  
  fill(255);
  ellipse(x, y, r+random(10), r+random(10));
  fill(random(255),random(255),random(255));
  rect(mouseX-(w/10), h-100, w/10, h/25);
//画出方块
  drawBlocks();
//小球碰到方块反弹
  blockBounce();
  win();
   
  
}
