# Engelsholm: Æstetisk Programmerings kursus: session 2

## Agenda
- Introduktion af translate(), rotate() && push(), pop()
- Fælles læsning af throbber kode
- Modificering af kode

## Immaterial transformation

[Translate](https://p5js.org/reference/#/p5/translate)

translate(__ , __);

flytter et object til dets eget punkt

```
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(0);
  fill(255);
  
  rect(50, 50, 60, 50);
  
  translate(100, 100);
   rect(50, 50, 60, 50);

}
```

[rotate](https://p5js.org/reference/#/p5/rotate)

rotation(__ , __);

angiv vinkel og akse, om hvilken rotationen skal ske.

- rotate() er afhængig af translate(). hvad er rotationens "point of origin" dets centrum? det giver translate.

- angiv vinkel enhed til computeren. default(RADIANS) men vi kan få det i DEGREES.

```
//let angle = 1;

function setup() {
  createCanvas(400, 400);
  angleMode(DEGREES);
}

function draw() {
  background(0);
  fill(255);
  
  rotate(0); // <-------- roter rect 
  //rotate(angle);
  
  rect(width/2, height/2, 50, 50);
  
  //angle = angle + 1;

}
```

### Push() & Pop()
[push()](https://p5js.org/reference/#/p5/push) & [pop()](https://p5js.org/reference/#/p5/pop)

push() == save transformations

pop() == restore transformations

```
let angle = 1;

function setup() {
  createCanvas(400, 400);
  angleMode(DEGREES);
  rectMode(CENTER);
}

function draw() {
  background(0);
  
  translate(50, 50);
  rotate(angle);
  fill(255, 100, 50);
  rect(0, 0, 100, 50);
  
  translate(300, 300);
  fill(50, 100, 255);
  rect(0, 0, 100, 50);

  
  angle = angle + 2;

}
```

en mulig løsning der virker i dette tilfælde er

```
rotate(-angle);
translate(-50, -50);
```
men det kan ikke skaleres og være svært at holde styr på så snart kompleksiteten i programmet intensiveres.

```
  push();
    translate(50, 50);
    rotate(angle);
    fill(255, 100, 50);
    rect(0, 0, 100, 50);
  pop();
```

## Throbber kode
![](https://i.gifer.com/origin/6f/6fa3434a7414e1c7de5ae4d97c06012e_w200.gif)

```
function setup(){
  createCanvas(400, 400);
  background(0);
  //frameRate(15);
}

function draw() {
  
  //fill(10, 80);
  //rect(0,0, width, height);
  
  translate(width/2, height/2);
  var cir = 360/8*(frameCount%8);
  rotate(radians(cir));
  noStroke();
  fill(255,255,0);
  ellipse(0, 35, 22,22);  
}
```

- tilføjelse af push() pop(), for at isolere throbbers transformation.
- lav en funktion til throbber

```
function setup(){
  createCanvas(400, 400);
  background(0);
  frameRate(15); //prøv at ændre dette parameter
}

function draw() {
  
  fill(10, 80); //afprøv andre aplha værdier
  rect(0,0, width, height);
  drawThrobber(8); //prøv at ændre tallet
}

function drawThrobber(num) {
  push();
  translate(width/2, height/2);
  var cir = 360/num*(frameCount%num);
  rotate(radians(cir));
  noStroke();
  fill(255,255,0);
  ellipse(0, 35, 22,22); //modificer parametre
  pop();
}
```


- modtag kode -----> [fjern, tilføj, modificer] ---> send kode return();


## Sources
- https://www.youtube.com/watch?v=o9sgjuh-CBM&ab_channel=TheCodingTrain
