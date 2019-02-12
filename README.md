<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<link type="text/css" rel="stylesheet" href="home_page.css" />
	<title>Che's Web I Web Site</title>
</head>
<body>

	<h1>Che’s Web I Home Page</h1>
	<figure class="right"><span title="A totally awesome Archen."><a href="https://bulbapedia.bulbagarden.net/wiki/Archen_(Pok%C3%A9mon)"><img src="awesome.png" alt="An awesome Pokemon."></a></span><figcaption>An awesome Archen.</figcaption></figure>
		
	<h2>Links to my Web I projects</h2>
	<ul>
	<li><a href="pages/favorites.html">My favorites</a></li>
	<li><a href="homework/recipe2.html">Recipe 2</a></li>
	</ul>
	<p>Final projects-</p>
	<ul>
	<li>project1</li>
	<li>project2</li>
	<li>project3</li>
	</ul>
	
	<h2>About Me</h2>
	
	<p>This will be a paragraph about me. I don't know exactly WHEN it will be a paragraph about me, but... <del>oh wait crap</del></p>
	
	<p>This is a paragraph about me. I was born in utah, but my family moved to new york at age 2 and never looked back.
	I'm a fan of Pokemon (especially the TCG), I enjoy writing and programming in my free time, and I plan on changing to the Computing Security major next simester.</p>
	
	<p>I took this course because I figured that, whatever my final career path ended up being, there was good chance I would have to deal with HTML in some way, shape, or form. So far I'm expecting to be a security expert, but there's still a chance something might change my mind.</p>
	
	<figure class="right"><iframe allowfullscreen="" height="270" src="https://www.youtube.com/embed/GGosfrleOfE" width="480"></iframe></figure>
		
	<h2>Some of my Favorite Web Sites:</h2>
	<ol>
	<li><a href="http://xkcd.com">xkcd</a></li>
	<li><a href="https://youtu.be/kSU0w7KwRIw">Youtube</a></li>
	<li><a href="https://thetrove.net/">The Trove</a></li>
	</ol>
	<br>
	<br>
	<br>
	<p>Okay fine you can have an actual picture but it's dumb</p>
	<img src="dumb.jpg" alt="It's me I guess" />
	<br>
	<br>
	<br>
	
	
	<div class="center">
	<h1 class="center">Conway's Game of Life</h1>
	</div>
	<br>
	<br>
	
	<canvas id="theCanvas" width="599" height="599" style="border:1px solid #0000FF;"></canvas>
	<br>
	<button id="Button" onclick="button()">Run</button>
	<button onclick="scramble()">Scramble</button>
	<button onclick="clearg()">Clear</button>
	<br>
	<br>
	<button onclick="rulesrandom()">random rules</button>
	<br>
	<button onclick="t(0)">0</button>
	<button onclick="t(1)">1</button>
	<button onclick="t(2)">2</button>
	<button onclick="t(3)">3</button>
	<button onclick="t(4)">4</button>
	<button onclick="t(5)">5</button>
	<button onclick="t(6)">6</button>
	<button onclick="t(7)">7</button>
	<button onclick="t(8)">8</button>
	<br>
	<button onclick="b(0)">0</button>
	<button onclick="b(1)">1</button>
	<button onclick="b(2)">2</button>
	<button onclick="b(3)">3</button>
	<button onclick="b(4)">4</button>
	<button onclick="b(5)">5</button>
	<button onclick="b(6)">6</button>
	<button onclick="b(7)">7</button>
	<button onclick="b(8)">8</button>
	<br>
	<p class="center" id="rules">0,0,1,1,0,0,0,0,0</p>
	<p class="center" id="rulesn">0,0,0,1,0,0,0,0,0</p>
	<a class="center">Speed: </a><input class="center" id="spd" type="number" value=100>
	<br>
	<a>Size: </a><input class="center" id="sizet" type="number" value=100>
	<br>
	<button onclick="sizeupd()">Update size</button>
	
	<script>
var rulesa = new Array(0,0,1,1,0,0,0,0,0);
var rulesb = new Array(0,0,0,1,0,0,0,0,0);
var grid = new Array();
var gridb = new Array();
var loop;
var toggle = true;
var size = 100;
var x = Math.floor(size/2);
var y = Math.floor(size/2);
var clearg = function(){
	for (i=0; i<size*size; i++) {
		grid[i] = 0;
		gridb[i] = 0;
	}
	draw();
}
	
var sizeupd = function() {
	clearg();
	size = parseInt(document.getElementById("sizet").value);
	x = Math.floor(size/2);
	y = Math.floor(size/2);
	grid=new Array();
	gridb=new Array();
	clearg();
}
	
var down = function() {
	drawcell(x,y);
	y++;
	if (y > size) {
		y = 0;
	}
	drawcur();
}
	
var up = function() {
	drawcell(x,y);
	y--;
	if (y < 0) {
		y = size;
	}
	drawcur();
}
	
var right = function() {
	drawcell(x,y);
	x++;
	if (x > size) {
		x = 0;
	}
drawcur();
}
	
var left = function() {drawcell(x,y);
	x--;
	if (x < 0) {
		x = size;
	}
	drawcur();
}
	
var drawsquare = function(a,b,gg) {
	var ps = Math.floor(600/size);
	ctx.fillStyle = gg;
	if (ps<5) {
		ctx.fillRect(a*ps,b*ps,ps,ps);
	} else {
		ctx.fillRect(a*ps,b*ps,ps-1,ps-1);
	}
}
	
var drawcur = function() {
	if (getCell(x,y) == 1) {
		drawsquare(x,y,"#00FF00");
	} else {
		drawsquare(x,y,"#0000FF");
	}
}
	
var togglecell = function() {
	if (grid[x+y*size] == 1) {
		grid[x+size*y] = 0;
	} else {
		grid[x+size*y] = 1;
	}
	drawcell(x,y);
	drawcur();
}
	
var Step = function() {
	for (i=0; i<size; i++) {
		for (j=0; j<size; j++) {
			var count = 0;
			for (k=-1; k<2; k++) {
				for (l=-1; l<2; l++) {
					count = count + getCell(i+k,j+l);
				}
			}
			if (getCell(i,j) == 1) {
				if (rulesa[count - 1] == 1) {
					gridb[(i+j*size)] = 1;
				} else {
				gridb[(i+j*size)] = 0;
				}
				} else {if (rulesb[count] == 1) {
					gridb[(i+j*size)] = 1;
				} else {
					gridb[(i+j*size)] = 0;
				}
			}
		}
	}
	for (i=0; i<size*size; i++) {
		grid[i] = gridb[i];
	}
	draw();
}
	
var scramble = function() {
	for (i=0; i<size*size; i++) {
		grid[i] = Math.floor(Math.random()*2);
	}
	draw();
}

var getCell = function(x,y) {
	var lx = x;
	var ly = y;
	if (x>size-1) {lx = 0;}
	if (x<0) {lx = size-1;}
	if (y>size-1) {ly = 0;}
	if (y<0) {ly = size-1;}
	return grid[lx+size*ly];
}

var draw = function() {
	ctx.fillStyle = "#000000";
	ctx.fillRect(0,0,600,600);
	for (i=0; i<size; i++) {
		for (j=0; j<size; j++) {
			drawcell(i,j);
		}
	}
}

var drawcell = function(i,j) {
	if (getCell(i,j) == 1) {
		drawsquare(i,j,"#FFFF00");
	} else {
		drawsquare(i,j,"#222222")
	}
}

var t = function(a) {
	if (rulesa[a] == 0) {
		rulesa[a] = 1;
	} else {
		rulesa[a] = 0;
	}
	updtable();
}

var b = function(a) {
	if (rulesb[a] == 0) {
		rulesb[a] = 1;
	} else {
		rulesb[a] = 0;
	}
	updtable();
}

var rulesrandom = function() {
	for (i=0; i<9; i++) {
		rulesa[i] = Math.floor(Math.random()*2);
		rulesb[i] = Math.floor(Math.random()*2);
	}
	updtable();
}

var updtable = function() {
	document.getElementById("rules").innerHTML=rulesa;
	document.getElementById("rulesn").innerHTML=rulesb;
}

var button = function() {
	if (toggle == true) {
		loop = setInterval(Step, parseInt(document.getElementById("spd").value));
		toggle = false;
		document.getElementById("Button").innerHTML="Pause";
	} else {
		clearInterval(loop);
		toggle = true;
		document.getElementById("Button").innerHTML="Run";
	}
}

var cs = document.getElementById("theCanvas");
var ctx = cs.getContext("2d");
clearg();
</script>
	

	
</body>
</html>
