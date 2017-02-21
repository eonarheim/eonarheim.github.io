Title: Conway’s Game of Life in JavaScript
Published: 10/18/2013
Tags:
- JavaScript
- Canvas
RedirectFrom: blog/conways-game-of-life-in-javascript/index.html
disqus_identifier: https://erikonarheim.com/blog/conways-game-of-life-in-javascript/
---

After stumbling onto a code kata [video](http://vimeo.com/18350401) about Conway’s “Game of Life” I wanted to learn more about it.

TL;DR – Here is the code on [github](https://github.com/eonarheim/GameOfLife), and here is a running [example](http://erikonarheim.com/GameOfLife/), click to seed the board and any key to start the simulation.

Once I got to googling I noticed a neat little easter egg in the sides of the page:

![](images/google-easter-egg.png)

Bam! I was inspired to implement the simulation for myself.

The “Game of Life” is a simulation of cellular automatons that demonstrates that complex patterns can emerge from simple rules. Evolution of the simulation is determined by the initial state of the simulation and progresses forward.

The rules that drive the simulation are as follows:

> Any live cell with fewer than two live neighbors dies, as if caused by under-population.
> Any live cell with two or three live neighbors lives on to the next generation.
> Any live cell with more than three live neighbors dies, as if by overcrowding.
> Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
> From [Wikipedia](http://en.wikipedia.org/wiki/Conway's_Game_of_Life)


There is a compact notation that is used to describe these rules to the simulation, fore example “B3/S23”. The way to read this is a cell is spontaneously born if it has exactly 3 neighboring cells, “stays lives on if it has 2 or 3 living neighboring cells. In all other cases, the cell dies. There are many people who tweak the rules to bring about interesting variations in the standard game.

So how would you do this in JavaScript?

The first thing to accomplish is to represent a “Cell”.

```javascript
var Cell = function(x,y, _cells){
        var me = this;

        me.isAlive = false;
        me.x = x;
        me.y = y;
        me.distance = function(cell){
                return Math.abs(cell.x - me.x) + Math.abs(cell.y - me.y);
        };

        me.neighbors = null;        

        me.countNeighbors = function(){
                return me.neighbors.filter(function(cell){
                        return cell.isAlive;
                }).length;
        };

        return me;
};
```

Cells have an pair of coordinates, an “isAlive” flag, and they also know about their neighbors. Having a reference to their neighbors makes it very simple to interrogate cells and find out whether or not they will survive to the next generation of the simulation.

Once we have the cells figured out, we need some way to arrange and keep track of them. I did this by creating a simple grid structure.

```JavaScript
var Grid = function(width, height){
        var me = this;
        var _cells = new Array(width*height);

        var _living = [];

        // instantiate cells
        for(var i = 0; i < width; i++){
                for(var j = 0; j < height; j++){
                        (function(){
                                _cells[i+j*width] = new Cell(i, j, _cells);
                        })();// Self executing function necessary to capture i and j values
                             // For-loops in JavaScript DO NOT create scope which is a bummer                       
                }
        }
        // Continued below...
```

Here I’m applying a trick to pack a 2D grid into a 1D array. You may also notice the self executing function inside the for-loop, this is to create scope and capture the values of i and j.

Next, we need to assign neighbor references to all the cell, in this example I’m really brute forcing this. There is definitely a more elegant way to do this, but for the purposes of the example I feel this is okay.

```javascript
       // assign neighbors
        _cells.forEach(function(cell){
                cell.neighbors = _cells.filter(function(cell2){
                        var dx = Math.abs(cell2.x - cell.x);
                        var dy = Math.abs(cell2.y - cell.y);
                        return (dx === 1 && dy === 1 ) || (dx === 1 && dy === 0) || (dx === 0 && dy === 1);
                });
        });

       // Continued below..
```

The next piece is the implementation of the rules of the simulation. First the cells that die are calculated then the cells that live on and reproduce. This step is made easier by the ability to ask cells about their neighbors directly, no need for complicated array math with “.countNeighbors()”.

```javascript
        me.updateLiving = function(){

                var deadOvercrowded = _cells.filter(function(cell){
                        return cell.isAlive && (cell.countNeighbors() > 3);
                });

                var deadUnderpop = _cells.filter(function(cell){
                        return cell.isAlive && (cell.countNeighbors() < 2);
                })

                var reproduction = _cells.filter(function(cell){
                        return !cell.isAlive && cell.countNeighbors() === 3;
                });

                var livesOn = _cells.filter(function(cell){
                        return cell.isAlive && (cell.countNeighbors() === 2 || cell.countNeighbors() === 3);
                });

                deadOvercrowded.concat(deadUnderpop).forEach(function(cell){
                        cell.isAlive = false;
                });

                reproduction.forEach(function(cell){
                        cell.isAlive = true;
                });
                livesOn.forEach(function(cell){
                        cell.isAlive = true;
                });

        };

        //Helpers
        me.filter = function(fcn){
                return _cells.filter(fcn);
        };

        me.getCell = function(x,y){
                return _cells[x+y*width];
        };

        return me;
};
```

Now with the simulation “engine” and data structures out of the way, we can work on the drawing aspect. With the HTML5 canvas we can accomplish some pretty cool stuff. Here is the basic boiler plate we need before we can get started.

```
var App = function(targetElementId, squaresX, squaresY){
        var me = this;
        // Grab the canvas and drawing context
        me.canvas = document.getElementById(targetElementId);
        me.ctx = me.canvas.getContext("2d");

        // Grab the start button
        me.button = document.getElementById("start");

        // Initialize page styles
        var body = document.getElementsByTagName('body')[0];
        body.style.margin = '0px';
        body.style.overflow = "hidden";

        // Set height and width to window inner height to make the app 'fullscreen'
        var viewWidth = me.canvas.width = window.innerWidth;
        var viewHeight = me.canvas.height = window.innerHeight;

        squaresX = squaresX || 20;
        squaresY = squaresY || 20;

        // Calculate the height and width of each cell
        var _squareWidth = me.canvas.width/squaresX;
        var _squareHeight = _squareWidth;

        // Initialize our Grid data structure from above
        var grid = new Grid(squaresX, squaresY);

        // Continued below

```

The user is going to want to setup the initial state of the simulation to they can play around, so we are going to setup event handlers for starting and stopping the simulation as well as handlers for clicking. To start and stop we will response with any keypress to make things simple, and mouse click and drag with lay down intial state.

```javascript
        // Handle Click events
        var _mouseDown = false;
        var handleClick = function(event){
                var x = event.pageX - me.canvas.offsetLeft;
                var y = event.pageY - me.canvas.offsetTop;

                var i = Math.floor(x/_squareWidth);
                var j = Math.floor(y/_squareHeight);

                grid.getCell(i, j).isAlive = true;
                return;
        };

        var _startSim = false;

        window.onkeydown = function(ev){
                _startSim = !_startSim;
        };

        window.onresize = function(ev){
                viewWidth = me.canvas.width = window.innerWidth;//viewWidth || 600;
                  viewHeight = me.canvas.height = window.innerHeight;//viewHeight || 600;
        };

        me.canvas.addEventListener('mousedown', function(event){
                _mouseDown = true;
                handleClick(event);
                me.canvas.addEventListener('mousemove', handleClick);
        });

        me.canvas.addEventListener('mouseup', function(event){
                _mouseDown = false;
                me.canvas.removeEventListener('mousemove', handleClick);
        });
        // Continued below...
```

Now for the fun part, drawing and updating

```javascript
        // Here is our start responsible for kicking off our mainloop 
        me.start = function(){
                setInterval(function(){
                        me.update();
                        me.draw();
                }, 60); // Mainloop set to refresh every ~60 milliseconds

        };

        // Update is responsible for updating all state in the app
        me.update = function(){
                if(_startSim){
                        grid.updateLiving();        
                }
        };

        // Draw is responsible for drawing the entire app
        me.draw = function(){
                // Erase previous draw by filling the entire canvas with white
                me.ctx.fillStyle = 'white';
                me.ctx.fillRect(0,0,me.canvas.width,me.canvas.height);

                // Draw living squares first
                grid.filter(function(cell){
                        return cell.isAlive;
                }).forEach(function(cell){
                        me.ctx.fillStyle = 'black';
                        me.ctx.fillRect(cell.x * _squareWidth, cell.y * _squareHeight, _squareWidth, _squareHeight);
                });

                // Draw grid

                // First draw vertical lines
                me.ctx.fillStyle = 'gray';
                for(var x = 0; x <= viewWidth; x+=_squareWidth){
                        me.ctx.beginPath();
                        me.ctx.moveTo(x, 0);
                        me.ctx.lineTo(x, viewHeight);
                        me.ctx.stroke();
                };

                // Second draw horizontal lines
                for(var y = 0; y <= viewHeight; y+= _squareHeight){
                        me.ctx.beginPath();
                        me.ctx.moveTo(0, y);
                        me.ctx.lineTo(viewWidth, y);
                        me.ctx.stroke();        
                };
        };

        return me;
};
```

To kick off the whole thing, all you need to do is the following

```javascript
var app = new App("game", 100, 50);
app.start();
```

Check out the code on github, and here is a running example on the web.

Happy games!

Cheers,
Erik