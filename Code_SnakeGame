//universal variables able to be used whenever throughout the code.
var snakeCells = [];
var letters = ["a","b","c","d","e","f","g","h","i","j"];
var directions = ["left","right","up","down"];
var direction = "";
var foodLocation = [];
var foodList = ["🍇","🍉","🍍","🍎","🍓","🍆","🍑","🍒","🥔","🥒"];
var prevFood = "";
var newFood = "";
var colorOptions = ["red","orange","yellow","green","blue","purple","pink"];
var color = "";
var spd = 500;
var score = 0;
var gameover = false;

//when the user presses the play button, the snake game begins by
//clearing the title from the titles from the screen, selecting a random color for the snake,
//randomly setting a location for the snake and the food, and starting the snake's movement.
onEvent("playButton", "click", function( ) {
  clearBoard();
  stopTimedLoop();
  hideElement("title1");
  hideElement("title2");
  gameover = false;
  direction = directions[randomNumber(0, directions.length-1)];
  color = colorOptions[randomNumber(0,colorOptions.length-1)];
  snakeCells[snakeCells.length] = randomNumber(2,9);
  snakeCells[snakeCells.length] = randomNumber(2,9);
  movement(randomNumber(2,9),randomNumber(2,9));
  randomFood();
  snakeSpeed();
});

//when the user presses the left button, the snake moves left and
//the variable "direction" is redefined as "left."
onEvent("leftButton", "click", function( ) {
  horizontalMove(-1);
  direction = "left";
});

//when the user presses the right button, the snake moves right and
//the variable "direction" is redefined as "right."
onEvent("rightButton", "click", function( ) {
  horizontalMove(1);
  direction = "right";
});

//when the user presses the up button, the snake moves up and
//the variable "direction" is redefined as "up."
onEvent("upButton", "click", function( ) {
  verticalMove(-1);
  direction = "up";
});

//when the user presses the down button, the snake moves down and
//the variable "direction" is redefined as "down."
onEvent("downButton", "click", function( ) {
  verticalMove(1);
  direction = "down";
});

//when the user presses the different arrow keys, the snake moves in the
//corresponding direction and "direction" is redefined as the corresponding direction.
onEvent("screen1", "keydown", function(event) {
  if (event.key == "Up"){
    verticalMove(-1);
    direction = "up";
  }else if ((event.key == "Down")){
    verticalMove(1);
    direction = "down";
  }else if ((event.key == "Left")){
    horizontalMove(-1); 
    direction = "left";
  }else if ((event.key == "Right")){
    horizontalMove(1);
    direction = "right";
  }
});

//purpose: creates a new location for the snake head and clears the old snake head location of text.
//how it works: creates the variable newNumber which applies the numberChange to the oldNumber
//and then runs the function movement using the same letterIndex and the newNumber
//if the newNumber passes the condition to not end the game.
//numberChange {number} - the change to be applied to the varaible oldNumber.
function horizontalMove(numberChange) {
  if (!gameover) {
    var oldNumber = snakeCells[snakeCells.length-1];
    var newNumber = oldNumber+numberChange;
    var letterIndex = snakeCells[(snakeCells.length-2)];
    if (newNumber<1||newNumber>10) {
      gameOver();
    } else {
      setProperty(letters[letterIndex]+ oldNumber, "text", "");
      movement(letterIndex,newNumber);
    }
  }
}

//purpose: creates a new location for the snake head and clears the old snake head location of text.
//how it works: creates the variable newLetterText which applies the letterChange to the oldLetterIndex
//and then runs the function movement with the newLetterIndex and number
//in the newLetterIndex passes the condition to not end the game.
//letterChange {number} - the change to be applied to the variable oldLetterIndex.
function verticalMove(letterChange) {
  if (!gameover) {
    var oldLetterIndex = snakeCells[snakeCells.length-2];
    var newLetterIndex = oldLetterIndex+letterChange;
    var number = snakeCells[snakeCells.length-1];
    if (newLetterIndex<0||newLetterIndex>9) {
      gameOver();
    } else {
      setProperty(letters[oldLetterIndex]+number, "text", "");
      movement(newLetterIndex,number);
    }
  }
}

//purpose: make snake appear to move
//how it works: sets location for head of snake, ends the game if the snake "runs into itself," 
//sets properties of cells to make body of snake, checks if the snake "ate" the food, and if so,
//makes snake's body one cell longer by defining previous last cell and keeps it colored one extra turn,
//lastly, adds locations to snakeCells list.
//letterIndex {number} - new vertical location of snake.
//number {number} - new horizontal location of snake.
function movement(letterIndex,number) {
  var newHead = letters[letterIndex]+number;
  if (getProperty(newHead,"background-color")==color) {
    gameOver();
  }
  setProperty(newHead, "background-color", color);
  setProperty(newHead, "text", "👀");
  if (!ateFood()) {
    var tailLetter = letters[snakeCells[0]];
    var tailNumber = snakeCells[1];
    var tailLocation = tailLetter+tailNumber;
    setProperty(tailLocation, "background-color", "rgba(242, 242, 242, 0)");
    removeItem(snakeCells, 0);
    removeItem(snakeCells, 0);
  }
  snakeCells[snakeCells.length] = letterIndex;
  snakeCells[snakeCells.length] = number;
}

//purpose: determines if the snake ate the food or not in order to increase the score.
//how it works: if the snake head and food are at the same location, ate is set to "true" and 
//the score is increased by one.
function ateFood() {
  var ate = false;
  var sameLetter = snakeCells[snakeCells.length-2]==foodLocation[0];
  var sameNumber = snakeCells[snakeCells.length-1]==foodLocation[1];
  if (sameLetter&&sameNumber) {
    ate = true;
    randomFood2(prevFood);
    score = score+1;
    setProperty("textScoreOutput", "text", score);
  }
  return ate;
}

//purpose: sets the speed and make the snake move.
//how it works: based on level setting, speed is set to three different options;
//uses a timed loop to run through the function every .5 seconds;
//depending on how direction is defined, the different move functions are ran.
function snakeSpeed() {
  if (getText("modeDropdown")=="Easy") {
    spd = 500;
  } else if (getText("modeDropdown")=="Medium") {
    spd = 350;
  } else if (getText("modeDropdown")=="Hard") {
    spd = 100;
  }
  timedLoop(spd, function() {
    if (direction=="left") {
      horizontalMove(-1);
    } else if (direction=="right") {
      horizontalMove(1);
    } else if (direction=="up") {
      verticalMove(-1);
    } else {
      verticalMove(1);
    }
  });
}

//purpose: end the game.
//how it works: ends the timed look from the snakeSpeed function and shows title2 which announces "GAME OVER"
//gameover is set to true which causes the move functions to not run, ending the game.
function gameOver() {
  stopTimedLoop();
  showElement("title2");
  gameover = true;
}

//purpose: clear the cells so all the boxes are white and no food remains.
//how it works: if snakeCells list has more than 0 items,
//snakeCells list is traversed and cell is defined as each snakeCells set of items
//then the defined cell's background is set to white.
//if foodLocation list has more than 0 items,
//then cell is defined as the items in foodLocation and set to blank text.
function clearBoard() {
  var cell = "";
  if (snakeCells.length>0) {
    for (var i = 0; i < snakeCells.length; i=i+2) {
      cell = letters[snakeCells[i]]+snakeCells[i+1];
      setProperty(cell, "background-color", "white");
    }
    //last item in list is snake's head
    setProperty(cell, "text", "");
  }
  if (foodLocation.length>0) {
    cell = letters[foodLocation[0]]+foodLocation[1];
    var food = "";
    setProperty(cell, "text", food);
  }
  snakeCells = [];
  score = 0;
  setProperty("textScoreOutput", "text", score);
}

//purpose: randomly place a randomly selected food for the start of the game.
//how it works: randomly selects a food from the food list and 
//randomly selects a location for the randomly selected food to go in
//then sets that cell's text as the food,
//prevFood is defined as firstFood.
function randomFood() {
  var firstFood;
  var random = randomNumber(0,foodList.length-1);
  foodLocation[0] = randomNumber(0,letters.length-1);
  foodLocation[1] = randomNumber(1,10);
  firstFood = foodList[random];
  setProperty(letters[foodLocation[0]]+foodLocation[1], "text", firstFood);
  prevFood = firstFood;
}

//purpose: randomly places the food text in a different cell.
//how it works: foodLocation index 0 and 1 are randomly set,
//and then the cell's text is filled with the newFood defined in determineFood function,
//then prevFood is set as newFood.
//previousFood {string} - current food text on screen, used in determineFood function.
function randomFood2(previousFood) {
  foodLocation[0] = randomNumber(0,letters.length-1);
  foodLocation[1] = randomNumber(1,10);
  prevFood = "";
  setProperty(letters[foodLocation[0]]+foodLocation[1], "text", determineFood(previousFood));
  prevFood = newFood;
}

//function: randomize which food is shown next, the same food cannot be shown twice in a row.
//how it works: foodList is traversed using a for loop,
//if previousFood matches the first item in the list, the first item is removed from the list, 
//newFood is randomly determined, the removed item is added back, then newFood is returned.
//if previousFood is not the first item in the list, it is set as newFood and newFood is returned.
//previous food {string} - current food text on the screen, 
//input value is compared to values in a list using boolean expressions.
function determineFood(previousFood) {
  var selectFood = "";
  for (var i = 0; i < foodList.length; i++) {
    if (previousFood==foodList[i]) {
      selectFood = foodList[i];
      removeItem(foodList, i);
      var random = randomNumber(0,foodList.length-1);
      newFood = foodList[random];
      appendItem(foodList, selectFood);
      return newFood;
    } else if ((previousFood!=foodList[i])) {
      newFood = foodList[i];
      return newFood;
    }
  }
}
