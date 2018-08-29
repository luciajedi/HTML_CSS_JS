# HTML, CSS, JS - Jedi Course
## Canvas Exercises

### Snake Tutorial

We will go through different phases so we will be able to see the process, and also prevent major bugs.

Do each part consecutively and check if everything works fine at the end of it. You can optionally do a commit (git) after every part, so if anything goes wrong at least you have a "checkpoint".

The name of the variables and functions can be your own, I use mine just as an example.

#### Part 1: Two rectangles

1. Create an HTML file with a canvas (fix the width and height). Also add some CSS:
   - center the canvas with flex
   - put a border so you can see the limits

1. Now we start the JS. Create some variables:
   - an object (x, y) for the snake position
   - an object (x, y) for the fruit position
   - the size (in pixels) of the fruit
   - the size of the snake (the head) 
   - the size of the canvas
   - a variable that saves the context (basic in all canvas)

   **I used the same size for the fruit and the snake.**


1. Let's create a function, initialize(), that will:
   * find the canvas (getElementById) and save it in the variable created
   * assign the context
   * call updateFruit(), that will:
      1. calculate for the x a random number between 0 and the maximum size of the canvas
      1. calculate the y as well
      1. call the draw function (it is described below!), with "red" in the color parameter
      
         (be aware that if the x or y position is canvas_max_size, **you will not see the rectangle**)
      
         (also it would be better if you calculate the random number with increment of snake_size like (random of 1 to max_canvas/snake_size + 1) x snake_size)
      
   * call updateSnake() that will just call draw() with "black" in the color parameter


1. And let's also create the draw(...) function. It will have some parameters: 
   - x
   - y
   - size
   - color

   And it will use the context to draw a rectangle with all this info (use `rec(x,y,size,size)` to draw the rectangle).

1. Finally, create the window.onload and an anonymus function that will call initialize().

1. **YOU SHOULD SEE**, in the website:
   - the centered canvas with borders
   - two rectangles, one black in 0,0 and another red in a random position

#### Part 2: The moving snake

1. For this part we will need more variables:
   - how many parts has the snake (it will start with 1 and every time it picks a fruit, it will add one more)
   - a variable to save the setInterval so we can clearInterval
   - an array, or 4 variables to save which direction will have the snake (set an initial direction!)

1. Then, we need to get the input keys. If we use up, down, left and right arrows, remember to assign in the window.onload function a keydown or keyup event (`window.onkeydown = function(new_event)`), and to check which key is pressed (`new_event.keyCode`). It will be:
   - 37 for left
   - 38 for up
   - 39 for right
   - 40 for down
   
   When a new direction is assigned, the array containing which direction are we going should have only one direction assigned, all others should be cleared.

1. We need an update() function that will:
   1. clear the screen
   1. check if the fruit and the snake are in the same position, so it can call updateFruit() and add 1 to the varable that count how many snake parts we have
   1. if not, it will call the drawFruit() function, that will draw the fruit in the same position (because the screen is clear now)
   1. also it will call the updateSnake() function

1. To the updateSnake() function we will add:
   - a variable to save the current position
   - a variable to calculate the new position using the variable direction, and the amount of px the snake will move (snake size for example)
   - if there is more than one square for the snake (not only the head, we need to update the positions of each square, using a for)
   - if there is a new square (like we just eat a fruit and the snake needs to grow, we will use array.push({x:old_position_x, y:old_position_y}))
   - if not, we just draw the snake in the new position and update the only position we have

1. In the initialize() function, we need to add:
   - a setInterval of the function update() so we can see the snake updated

1. **YOU SHOULD SEE**, in the website:
   - that the "snake" rectangle moves in a specific, predefined direction 
   - if we press up, down, left and right INSIDE THE WEBPAGE (I was pressing it inside the inspector and didn't work), the square should change its movement and never go diagonally
   - if we "eat" the fruit, it will dissapear and appear in another place, and the snake should be one square longer and this square should follow the first one

#### Part 3: Game Over

1. To program the losing conditions we need, in update():
   - check if the snake goes outside the canvas (ALTERNATIVE: program that if it goes outside the canvas, it appears on the other side!)
   - check if the snake head is in the same x and y than one of its parts/other squares (use a for or a while)

   If something is true, it should be game over (I have a boolean gameover, but you can make a function if you please), and if not the snake should be updated normally.

1. If it is game over and we want to end it like this:
   - in update: must clear the interval (clearInterval(name_of_interval))

1. If we want something more cool, we can add a button "Play" in the HTML that is disabled while gameover is false, and enabled when it is true (`document.getElementById("btn").disable = true`)
So if we want to play again, we should:
   - In update: clear interval
   - In initialize: reset all variables to the initial values (snake position, fruit position, snake squares, initial direction) and clear the canvas
   - In window.onload: add the event of the button and it will set gameover to true and call initialize

#### Part 4: Surprise!

Make it your own! Change rect for images or put a background, make whatever you want so it's unique :)
