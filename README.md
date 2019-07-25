# snake-game

## DESCRIPTION
  Building a snake game using html, css and java script is considered as a step by step process.
  I.e., first of all, we draw canvas, an html element where our snake should be drawn. Here our snake body is drawn as rectangles inside the canvas. The drawing of rectangles, movements of snake, food for snake are done using java script. We use css to make our game more colourful and enhancing.

## STEP 1. Draw a canvas.
  Canvas is an html element which can be used draw graphics via scripting.Here script used is javascript. The tag used is       <canvas></canvas>. We have to specify height and width of canvas inside the canvas tag. The tag must be included inside the   body of html page.
  
  <canvas  width =”995” height= “495 “ id= “myCanvas”></canvas>
  The out will be :
  
  ![box](https://user-images.githubusercontent.com/52073455/61852263-ab332180-aed6-11e9-8b49-231226c24688.png)
  
  To access the canvas in our java script, we  use document.getElementById() method in javascript.
  var canvas =  document.getElementById(“myCanvas”);
  var ctx = canvas.getContext(‘2d’);
  here the ‘myCanvas’ is the id that is given for the canvas, getContext(‘2d’) will cover the properties and methods which     can be used to draw text,lines,boxes,circles on the canvas.

  As I have already said in the introduction, the snake’s body is drawn as rectangles . Now we should try to draw the         rectangles inside the canvas. The left top edge of the canvas is the origin ie,(0,0) where x = 0 and y = 0 ,x and y are     coordinates. This is the concept which is used in case of the movement of the snake body. The x and y coordinates are       stored inside an array.

  For drawing a rectangle we have fillRect() method,
  ```
  ctx.fillRect(snake1[0].x,snake1[0].y, 15,15);

  ctx.fillRect(snake1[1].x,snake1[1].y,15,15);

  ctx.fillRect(snake1[2].x,snake[2].y,15,15);

  ctx.fillRect(snake1[3].x,snake[3].y,15,15);
  
  ```

  snake1 is the array used for storing x,y coordinates.

  ![box1](https://user-images.githubusercontent.com/52073455/61852433-1bda3e00-aed7-11e9-8644-a2391e4b1e2f.png)

  This will your initial output.
## STEP2. Key press controlling.
   The snake moves according to the key pressed. To identify which key is pressed we uses console.log().The                    addEventListener in javascript listens to which key is pressed this helps us in our snake movements as our snake moves      respect to the corresponding keypress.
  ```
  window.addEventListener(‘keydown’, (e) => {
	switch(‘${e.keycode}’){
		case ‘38’:
			console.log(“up arrow is pressed”);
		break;
		case ‘40’:
			console.log(“down arrow is pressed”);
		break;
		case ‘39’:
			console.log(“right arrow is pressed”);
		break;
		case ‘40’:
			console.log(“left arrow is pressed”);
		break;
	}
  ```
  
## STEP3. The Snake movement.
  The movement of the snake happens in a grid. Let’s see that with the help of a diagram.
  This will be the current position of the snake.

  ![box2](https://user-images.githubusercontent.com/52073455/61852744-d2d6b980-aed7-11e9-917e-708a5e5e8ee0.png)

  When the Up arrow is pressed.
  A new rectangle will be created in the cell above the current cell. And the last rectangle should be deleted. I.e,
  
  ![box3](https://user-images.githubusercontent.com/52073455/61852796-f26de200-aed7-11e9-8331-32066a247889.png)

  Now it’s clear that a new x and y coordinates will be stored in the head of the array and the tail of the array will be     replaced with the array element before the last element of the array. This is how the adding of head and deletion of tail   happens in snake movement.
  
  When the Right arrowkey is pressed.
  
  ![box4](https://user-images.githubusercontent.com/52073455/61853133-c2730e80-aed8-11e9-869b-ec6690c6f4dd.png)


  When the Down arrowkey is pressed.
  
  ![box5](https://user-images.githubusercontent.com/52073455/61853219-fc441500-aed8-11e9-82c8-79c3d36a3e2c.png)
  
  When the Left arrowkey pressed.
  
  ![box6](https://user-images.githubusercontent.com/52073455/61853258-1a117a00-aed9-11e9-9aa3-4c5497574ea1.png)
  
  Now we face with the real problem
 
  Let’s deal with the case of upward movement, when the up arrow is pressed it calls the setInterval method which in turn     calls the method up for a specified interval of time. This method will be continued until the clearInterval is called. In   this case, when the up arrow key is pressed it will trigger method up by setInterval in each 100 milliseconds.  

  Inside the up method it clears the last rectangle and add a new rectangle by decreasing the y coordinate to a certain unit   and x remains the same. The array elements between the last and first elements of the array is swapped to one position up.

  
  ```
  <script>
    case:’38’:
	    interval = setInterval(up,100);
    break;
  function up()
  {
  	ctx.clearRect(snake1[snake1.length-1].x,snake1[snake1.length-1].y,unit,unit);
  	snake1[0] = {x: snake1[0].x , y: snake1[0].y - 20 };
  	for(var i=snake1.length;i>0;i--){
         snake1[i] = snake1[i-1];
     }
  	ctx.fillStyle = "red";
    ctx.fillRect(snake1[0].x,snake1[0].y,unit,unit);
  	for(var i=1;i<=snake1.length-1;i++){
          ctx.fillStyle = "yellow";
          ctx.fillRect(snake1[i].x,snake1[i].y,unit,unit); 
     }
  }
  </script>
  ```
  
  similarly in other movements:
  
	1.Down => y coordinate is incremented and x will be constant.
	2.Right=> x coordinate is incremented and y will be constant.
	3.Left=> y coordinate is decremented and x will be constant.
  
## STEP4. Food Consuming.
  In food consuming, a food is generated randomly inside the canvas and outside the body of the snake.
  While eating a food the snake length increases ie a new rectangle will be added at the tail. How can we say that the food   is eaten by the snake? The answer to your doubt is to check whether the head of the snake hits the food ie, the (x,y)       coordinates of head of the snake hits on or equal to  the (x,y) coordinates of the food. If this happens, it is clear that   the food is consumed by the snake and the snake length increases by 1.
  
  ```
  function food_generating(){
                for(i=0;i<snake1.length-1;i++){
                    if(snake1[i].x ==x1 && snake1[i].y ==y1){
                        x1= Math.floor(Math.random()*40)+1;
                        x1=x1*20+20;
                        y1= Math.floor(Math.random()*20)+1;
                        y1=y1 *20+20;
                    }
                }
                ctx.fillStyle="green";
                ctx.fillRect(x1,y1,unit,unit);  
            }
  ```  
  
  ## STEP5. Snake Collisions.
   The collision happens in 2 situations:
    (i) When the snake hits on its own body.
    (ii) When the snake hits on the boundary of the canvas.
    
   If  any of these collisions happen the snake game ends.
   
   ```
   i. Snake body collisions.
	for(var i=1;i<snake1.length;i++){
                        if(snake1[i].x==snake1[0].x && snake1[i].y==snake1[0].y){
                            alert("Game end");
                           
                        window.location.reload();
                        }
                    }
  ```
  This checks whether the first element of the array is already present in the array. If so, the head has been thrashed on     the body of the snake and the game ends here.
  
  ```
  ii. Snake boundary collisions.
 	  If the snake moves up and hits the canvas boundary, the snake should die and the game ends here.
    
    (*) In case of up movement:
	      if(snake1[0].y == 0){
             alert("Game end");
             window.location.reload();
             }
    
   
   
   
    (*) In case of down movement:
	      if(snake1[0].y == 480){
              alert("Game end");
              window.location.reload();
     
     }
     
    
    
    
    (*)  In case of right movement:
         if(snake1[0].x == 980){
              alert("Game end");
              window.location.reload();
            
     }
     
   
    
    (*)  In case of left movement:
         if(snake1[0].x == 0){
             alert("Game end");
             window.location.reload();   
     }  
     
     
    ```         
    

    



  
  
  
