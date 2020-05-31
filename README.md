# oyunsevgisi
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<style>
canvas {
    border:1px solid #d3d3d3;
    background-color: #f1f1f1;
}
.container-kontrol-alani{

border:  1px solid black;
background: rgb(216, 216, 116);
height: 300px;
width: 600px;
margin: 1em;
padding: 1em;
border-radius: 12px;
}

.ortakdiv{
height: 3em;
width: 4em;
border: 1px solid black;
margin: 2px;
padding: 2px;

}

.div-control{
display: flex;
float: top;
justify-content: space-between;
align-content: center;
}
.yon{
object-fit: scale-down;
}

.div-yon{
display: flex;
justify-content: center;
}

.button {
border: none;
color: white;
padding: 16px 32px;
text-align: center;
text-decoration: none;
display: inline-block;
font-size: 16px;
margin: 4px 2px;
transition-duration: 0.4s;
cursor: pointer;
margin: 0 41%;
}

.button1 {
background-color: white; 
color: black; 
border: 2px solid #4CAF50;
}

.yazi{
padding: 0;
margin: 0;
}
</style>
</head>
<body onload="startGame()">

    <div class="container-kontrol-alani">
        <p class="yazi"><b>Oyun kontrol kutusu</b>  <br>  
        Karakteri yönlendirmek için yön tuşlarını adım lara bırakın!</p><br>
        <div class="container-kontrol-kutusu">
            <div class="div-control"> <br> 1. adım <br>
                <div id="div1" class="ortakdiv" ondrop="drop(event)" ondragover="allowDrop(event)" contentEditable = true data-text="Enter name here"></div><br>
                2. adım <br>
                <div id="div2" class="ortakdiv" ondrop="drop(event)" ondragover="allowDrop(event)" contentEditable = true data-text="Enter name here"></div><br>
                3. adım <br>
                <div id="div3" class="ortakdiv" ondrop="drop(event)" ondragover="allowDrop(event)" contentEditable = true  data-text="Enter name here"></div><br>
                4. adım <br>
                <div id="div4" class="ortakdiv" ondrop="drop(event)" ondragover="allowDrop(event)" contentEditable = true data-text="Enter name here"></div><br>
         
            </div><br><br>
        </div>
        <div class="container-yon-img">
            <div class="div-yon">
                <img id="yukari" class="yon" src="up.png" draggable="true" ondragstart="drag(event)" width="55px" height="48px">
                <img id="sol" class="yon" src="left.png" draggable="true" ondragstart="drag(event)" width="55px" height="48px">
                <img id="sag" class="yon" src="right.png" draggable="true" ondragstart="drag(event)" width="55px" height="48px">
                <img id="asagi" class="yon" src="down.png" draggable="true" ondragstart="drag(event)" width="55px" height="48px"> 
            </div>
            <br><br><button class="button button1" onclick="icerial()">Basla</button>
        </div>

    </div>
<script>

var myObstacle;
var myObstacle2;
var myObstacle3;
var myObstacle4;
var myObstacle5;
var myObstacle6;
var myObstaclesagköse;
var myObstaclesagüst;
//var myObstaclesagüst2;
var myObstacleorta1;
var myObstacleorta2;
var myObstacleorta3;
var myGamePiece;
var mySound; //ses için tanımlanan değişken 
var myBackground;
var karakter;
var bitis2;
var mySound2;
var ahtapot1;
var ahtapotengel1;
var ahtapot2;
var ahtapotengel2;
var ahtapot3;
var ahtapotengel3;
var mySound3;


function allowDrop(ev) {
    ev.preventDefault();
  }
  
  function drag(ev) {
    ev.dataTransfer.setData("text", ev.target.id);
  }
  
  function drop(ev) {


    var data = ev.dataTransfer.getData("text");
    var nodeCopy = document.getElementById(data).cloneNode(true);
    // nodeCopy.id = "newId"; /* We cannot use the same ID */
    ev.target.appendChild(nodeCopy);
    // ev.target.appendChild(document.getElementById(data)); 
    ev.preventDefault();   
  }

  
function icerial(){
  let durum;
  for(var a=0;a<4;){
    durum=document.querySelector("#div"+(a+1)).lastChild.id;
    console.log(typeof durum);

    switch (durum){

      case "yukari":
      a++;
           move("up");
           updateGameArea();
           clearmove();
           
         console.log("yukarı gidiyor....");

      break;

      case "asagi":
      a++;
          move("down");
          updateGameArea();
           clearmove();
     
        console.log("aşağı gidiyor....");

      break;

      case "sag":
      a++;
            move("right");
            updateGameArea();
           clearmove();
          
        console.log("sağa gidiyor....");

      break;

      case "sol":
      a++;
          move("left");
          updateGameArea();
           clearmove();

           
        console.log("sola gidiyor....");

      break;
    }
    console.log(durum);
    console.log(a);


  }
  setTimeout(function(){ 
    let imagesRemove = document.querySelectorAll(".ortakdiv");
    imagesRemove.forEach(function(nodes){
        nodes.removeChild(nodes.firstElementChild);
    })
    console.log(imagesRemove);
},500);
}

function startGame() {
    myObstacle  = new component(778, 50, "green", 0, 585);   //altkenar
    myObstacle2  = new component(778, 50, "green", 0, -19); //üst kenar   
    myObstacle3  = new component(50, 780, "green", 585, 0);//sağ kenar
    myObstacle4  = new component(50, 780, "green", -17, 0);//sol kenar 
    myObstacle5=new component(64,68,"green",36,302);//sol alt 1 engel 
    myObstacle6=new component(66,85,"green",101,516);//sol alt 2. engel
    myObstaclesagköse=new component(85,85,"green",515,514);//dsğ alt engel 
    myObstaclesagüst=new component(70,76*2,"green",520,20);//sağ üst köşe 
    myObstacleorta1=new component(75,72*3,"green",300,27);//orta ikinci engel
    myObstacleorta2=new component(68,66*3,"green",242,180);//orta birinci engel 
    myObstacleorta3=new component(68,68,"green",375,308);//orta tek engel 3. 
    myGamePiece = new component(47.5, 47.5, "mario1.gif", 42, 42, "image");
    myBackground = new component(600, 600, "arkaplan11.jpeg", 0, 0, "image");
    mySound = new sound("bounce.mp3");  //ses 
    mySound2 = new sound("lullaby.mp3");
    mySound3 = new sound("swimstep.mp3");
    bitis2 = new component(50, 50, "green", 380,37);
    karakter = new component(60, 60, "bitis.jpeg", 380,37, "image");
    ahtapot1 = new component(47.5, 47.5, "1476785010793.gif", 40,515, "image");
    ahtapotengel1 = new component(45, 45, "green", 40,515 );
    ahtapot2 = new component(47.5, 47.5, "1476785010793.gif", 455,37, "image");
    ahtapotengel2 = new component(45, 45, "green", 455,37, );
    ahtapot3 = new component(47.5, 47.5, "1476785010793.gif", 250,390, "image");
    ahtapotengel3 = new component(40, 40, "green", 250,390 );
    myGameArea.start();
}

var myGameArea = {
    canvas : document.createElement("canvas"),
    start : function() {
        this.canvas.width = 600;
        this.canvas.height = 600;
        this.context = this.canvas.getContext("2d");
        document.body.insertBefore(this.canvas, document.body.childNodes[0]);
        this.frameNo = 0;
        this.interval = setInterval(updateGameArea, 200);
        },
    clear : function() {
        this.context.clearRect(0, 0, this.canvas.width, this.canvas.height);
    },
    stop : function() {
        clearInterval(this.interval);
    }
}

function component(width, height, color, x, y, type) {
    this.type = type;
    if (type == "image") {
        this.image = new Image();
        this.image.src = color;
    }
    this.width = width;
    this.height = height;
    this.speedX = 0;
    this.speedY = 0;    
    this.x = x;
    this.y = y;    
    this.update = function() {
        ctx = myGameArea.context;
        if (type == "image") {
            ctx.drawImage(this.image, 
                this.x, 
                this.y,
                this.width, this.height);
        } else {
            ctx.fillStyle = color;
            ctx.fillRect(this.x, this.y, this.width, this.height);
        }
    }
    this.crashWith = function(otherobj) {
        var myleft = this.x;
        var myright = this.x + (this.width);
        var mytop = this.y;
        var mybottom = this.y + (this.height);
        var otherleft = otherobj.x;
        var otherright = otherobj.x + (otherobj.width);
        var othertop = otherobj.y;
        var otherbottom = otherobj.y + (otherobj.height);
        var crash = true;
        if ((mybottom < othertop) || (mytop > otherbottom) || (myright < otherleft) || (myleft > otherright)) {
            crash = false;
        }
        return crash;
    } 
    this.newPos = function() {
        this.x += this.speedX;
        this.y += this.speedY;        
    }    
}

function updateGameArea() {
    if (myGamePiece.crashWith(myObstacle)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    } 
    if (myGamePiece.crashWith(myObstacle2)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(myObstacle3)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(myObstacle4)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(myObstacle5)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(myObstacle6)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(myObstaclesagköse)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(myObstaclesagüst)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(myObstacleorta1)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(myObstacleorta2)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(myObstacleorta3)) {
        myGameArea.stop();
        mySound.play();// engelde ses çalma
    }
    if (myGamePiece.crashWith(bitis2)) {
        myGameArea.stop();
        mySound2.play();// engelde ses çalma 
        alert("OYUNU BİTİRDİNİZ!!!");
       
      
    
    }
    if (myGamePiece.crashWith(ahtapotengel2)) {
        myGameArea.stop();
        mySound3.play();// engelde ses çalma 
        alert("AHTAPOTA YAKALANDINIZ !!!");
    }
    if (myGamePiece.crashWith(ahtapotengel1)) {
        myGameArea.stop();
        mySound3.play();// engelde ses çalma 
        alert("AHTAPOTA YAKALANDINIZ !!!");
    }
    if (myGamePiece.crashWith(ahtapotengel3)) {
        myGameArea.stop();
        mySound3.play();// engelde ses çalma 
        alert("AHTAPOTA YAKALANDINIZ !!!");
    }

    //if (myGamePiece.crashWith(myObstaclesagüst2)) {
     //   myGameArea.stop();
    //}
    else {
        myGameArea.clear();
        myBackground.newPos();
        myGamePiece.newPos();
        myObstacle.update();
        myObstacle2.update();
        myObstacle3.update();
        myObstacle4.update();
        myObstacle5.update();
        myObstacle6.update();
        myObstaclesagköse.update();
        myObstaclesagüst.update();
        myObstacleorta1.update();
        myObstacleorta2.update();
        myObstacleorta3.update();
        ahtapotengel2.update();
        ahtapotengel3.update();
        bitis2.update();
        ahtapotengel1.update();
       // myObstaclesagüst2.update();
        myBackground.update();  
        karakter.update();
        ahtapot1.update();
        ahtapot2.update();
        ahtapot3.update();
        myGamePiece.update();
    }     
    
}

function move(dir) {
    myGamePiece.image.src = "mario.gif";
    if (dir == "up") {myGamePiece.speedY = -68; }
    if (dir == "down") {myGamePiece.speedY = 68; }
    if (dir == "left") {myGamePiece.speedX = -68; }
    if (dir == "right") {myGamePiece.speedX = 68; }
}
function sound(src) { //sess 
    this.sound = document.createElement("audio");
    this.sound.src = src;
    this.sound.setAttribute("preload", "auto");
    this.sound.setAttribute("controls", "none");
    this.sound.style.display = "none";
    document.body.appendChild(this.sound);
    this.play = function(){
        this.sound.play();
    }
    this.stop = function(){
        this.sound.pause();
    }    
}

function clearmove() {
    myGamePiece.image.src = "mario1.gif";

    myGamePiece.speedX = 0; 
    myGamePiece.speedY = 0; 
}
</script>
<div style="text-align:center;width:480px;">
  <button onmousedown="move('up')" onmouseup="clearmove()" >UP</button><br><br>
  <button onmousedown="move('left')" onmouseup="clearmove()" >LEFT</button>
  <button onmousedown="move('right')" onmouseup="clearmove()" >RIGHT</button><br><br>
  <button onmousedown="move('down')" onmouseup="clearmove()" >DOWN</button>
</div>

<p>Update the background before updating other components to make sure the other components are dispalyed on top of the background.</p>
</body>
</html>
