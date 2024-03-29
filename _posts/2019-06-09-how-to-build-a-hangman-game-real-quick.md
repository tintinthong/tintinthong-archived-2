---
title: "How to Build a Hangman Game Real Quick"
tags: javascript software
---


<p>
  <!-- <a href="MY WEBSITE LINK" target="_blank"> -->
    <img src="/img/hangman_pics/hangman.png" style='width:60%; display:block; margin-left:auto;margin-right:auto' border="0" alt="Null">
  <!-- </a> -->
</p>



It seems to me that one of the first few things that you'll be told to do as a new javascript programmer is to build a game. At Hacker Collective, we attempted to build a hangman game in the fastest time possible; it took me about 4 hours to build this game. 

Note: This article is most suitable for someone who knows Javascript fundamentals. 

## Introduction

A lot of my ideas were extracted from a [codepen][1]. The elements of a basic hangman game is straightforward. Have a:

1. Keyboard of buttons to access input
2. Canvas to draw the hangman
3. Placeholder to include the guessed letters
4. Hint 

Initially, I truly wanted to copy the pen and add features on top of it, however, my frustration of the naming conventions used and my hidden OCD of needing to build everything from scratch compelled me to do otherwise. The principles were the same: to build a hangman game with a vanilla codebase. I gave myself some leeway to not focus on coding practices, rather just completing the game. 

## Building the UI

Firstly, let us begin by crafting the html file. I knew for a fact that I would have to dynamically add elements to the DOM, e.g. there are different number of blanks. Hence, my html file will not have all it's element in place until later on when I write `main.js`, the main javascript file. Within html, I source a `main.js` and `style.css`.

```html
<!-- index.html -->
<!DOCTYPE html>

<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title></title>
    <meta name="description" content="">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    
    <div id="introHeader" class="container">
        <h1>Hangman</h1>
        <p>An urban dictionary take</p>
    </div>
    
    <div class="container">
        <div id="blanksFrame">
            <!-- where to put the word -->
        </div>
        <div id="lives"></div>
    </div>
    
    <canvas id="drawing">
        
    </canvas>
    
    <div class="container">
        <div id="hint"></div> 
        <div id="keyboard">
            <!-- Showing buttons here -->
        </div> 
    </div>
    
    <script src="main.js"></script>
    
</body>
</html>
```

Additionally, we load the `style.css` files. We do several things with the style. 

1. We make the `#blank` and `#letter` which is a `<li></li>` tag to be inline; the `#blank` is the empty spaces for the answer and the `#letter` is container of the buttons to input guessed letter.
2. `#introHeader` is the container of a `<h1></h1>` and `<p></p>`; I made them inline (on the same row).
3. Change the color of button to yellow upon `.hover`. 
4. I changed the fonts for `#introHeader` and `#hint`.

```css
/* style.css */
#letter{
    display:inline-block;
}

#blank{
    display:inline-block;
    padding:2px;
    
}


#buttonLetter:hover { 
    background-color: yellow;
}

#introHeader h1,
#introHeader p {
    display: inline;
    vertical-align: top;
    font-family: 'Open Sans', sans-serif;
}

#hint {
    font-family: 'Open Sans', sans-serif;
}

```

Chances are you see something as below. Wait a minute. Where is `#blank`? Where is `#buttonLetter`?
The reason for that is that the tags don't exist yet. We need to impute html tags from our javascript, but we haven't written that code yet.

<p>
  <!-- <a href="MY WEBSITE LINK" target="_blank"> -->
    <img src="/img/hangman_pics/ui.png" style='width:60%; display:block; margin-left:auto;margin-right:auto' border="0" alt="Null">
  <!-- </a> -->
</p>



## Build the Logic

Here is the most important file, `main.js`. It is where we create the javscript -- the logic of the game. We have a play function that takes in `result_word` and `result_definition` (a word and it's corresponding definition).

```javascript
//main.js

let play = function(result_word, result_definition){

  //main body of code is inside here
}
```

To build the logic, we need to instantiate a few objects. 

1. `player`: A player object ( mainly to store how many lives left)
2. `game`: A game object to keep list of 26 alphabets, `word` object used and `correctList` which keeps track of winning condition.
3. `drawing`: Canvas object for drawing on.



```javascript 

//main.js

//main body of code is inside here

    //this is the main code

    //INITIALISE OBJECTS
    
    let player = {
        lives: 10,
    }
    
    let game = {
        alphabets: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h',
        'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's',
        't', 'u', 'v', 'w', 'x', 'y', 'z'],
        word: {
            name:result_word.toLowerCase(),
            definition:result_definition,
            get wordLetters(){
                return stringToList(this.name)
            }
            
            
        }
    }
    
    // keep track of true and false guessed
    game.correctList=[]
    for (var i=0; i<game.word.name.length; i++) {
        game.correctList.push( false);
    }
    //decided not to use a getter
    
    
    //set up drawing
    let drawing = document.getElementById("drawing");
    let context = drawing.getContext('2d');
    context.strokeStyle = "blue";
    context.lineWidth = 1;
    context.beginPath();


// include helper functions

// include main methods

// run all main methods


```


There are also several helper functions: 

1. `stringToList()`: Transpose string to list. For example, `"food panda" --> ["f","o","o","d"," ","p","a","n","d","a"]`.
2. `drawLine()`: Simplifies code for drawing. It references a coordinate system `(x1,y1) --> (x2,y2)` beginning from the top-left of the canvas.


```javascript 
//main.js
// include helper functions

 //HELPER FUNCTIONS
    
    //method to change a string into list (accounting for spaces)
    let stringToList= function(str){
        
        let list= str.split("")
        return list
    }
    
    //draw function
    let drawLine = function($pathFromx, $pathFromy, $pathTox, $pathToy) {
        
        context.moveTo($pathFromx, $pathFromy);
        context.lineTo($pathTox, $pathToy);
        context.stroke(); 
    }


```



Under this code we continue to contain a list of main methods:

1. `checkLetter()`: After input, check whether guessed letter is correct.
2. `showButtons()`: Expose all buttons for input. 
3. `showBlanks()`: Expose all blanks of given word in game object.
4. `showLives()`: Expose number of lives of player object.
5. `draw()`: Draw additional stickman limb if guesss is wrong or lives is deducted. 

Remember in the ui section, I said that certain html tags will be included with javascript. That is exactly what `showButtons()`, `showBlanks()` and `showLives()` is for. The only difference is that `showButtons()` and `showBlanks()` is called once, whereas, `showLives()` is called several times to update lives in the ui.

There are a few important things to note about the functionality, particularly `showBlanks()`. Although `showBlanks()` is meant to `showBlanks()`, the random words we are producing occasionally has spaces, numbers, and special characters. Therefore, we resolve for this by exposing these characters, wherease, only alphabets are treated as blanks. 

```javascript 
//main.js
// include main methods

//MAIN METHODS


    //check whether guessed letter is correct and enter into blanks
    let checkLetter= function(letter){
        
        
        if(game.word.wordLetters.includes(letter)){
            //if correct
            
            console.log(`Correct! ${letter} is inside ${game.word.name}`)
            
            //collect indexes in list
            let indexList=[]
            game.word.wordLetters.filter(
                function(currentValue,index){
                    if(currentValue==letter){
                        indexList.push(index)
                    }
                }
                )
                
                let blanks = document.getElementById('blanks');
                indexList.forEach(function(index){
                    game.correctList[index]=true; 
                    blanks.childNodes[index].innerHTML= letter;
                })
                
                if(game.correctList.every(function(currentValue){
                    return currentValue==true;
                })){
                    alert("You Win!")
                }
                
                
            }else{
                // if wrong
                
                console.log(`Wrong! ${letter} is not in ${game.word.name}`);
                player.lives--
                console.log(`You have ${player.lives} lives left`)
                showLives();
                draw();
                
                if(player.lives==0){
                    alert("Game Over!")
                }
            }
            
        }
        
        // create buttons
        let showButtons = function () {
            let keyboard = document.getElementById('keyboard');
            let letters = document.createElement('ul');
            letters.id = 'letters';
            keyboard.appendChild(letters);
            for (let i = 0; i < game.alphabets.length; i++) {
                let letter = document.createElement('li');
                letter.id= 'letter'
                let buttonLetter= document.createElement('button')
                buttonLetter.setAttribute('id','buttonLetter');
                buttonLetter.innerHTML = game.alphabets[i];
                buttonLetter.addEventListener('click',function(id){
                    console.log(`you just clicked ${this.innerHTML}`)
                    checkLetter(this.innerHTML)
                    this.parentNode.removeChild(this);
                })
                letters.appendChild(letter);
                letter.appendChild(buttonLetter);
            }
        }
        
        // display all blanks 
        // expose spaces and special characters
        let showBlanks = function(){
            let blanksFrame = document.getElementById('blanksFrame');
            let blanks = document.createElement('ul');
            blanks.setAttribute('id','blanks')
            blanksFrame.appendChild(blanks);
            for (let i=0; i<game.word.wordLetters.length; i++) {
                let blank = document.createElement('li');
                blank.setAttribute('id','blank')
                
                // if not alphabet then put special character
                if(!game.alphabets.includes(game.word.wordLetters[i])){
                    
                    if(game.word.wordLetters[i]==" "){
                        blank.innerHTML = "&nbsp&nbsp&nbsp";
                    }else{
                        blank.innerHTML = game.word.wordLetters[i];
                        
                    }
                    // make filled blank with space or special character correct
                    game.correctList[i]=true;
                    
                }else{
                    blank.innerHTML = "__";
                }
                
                
            
                blanks.appendChild(blank);
            }
        
            
            
        }
        
        //show hint (do not need to click button)
        let showHint= function(){
            let hint= document.getElementById('hint');
            hint.innerHTML = game.word.definition;
        }
        
        // show lives based on player object
        let showLives= function(){
            let lives= document.getElementById('lives');
            
            lives.innerHTML= `You have ${player.lives} lives left`;
        }
        
        // add limb to player based on player.lives
        let draw =function(){
            
            switch(player.lives){
                case 9:
                
                drawLine(5, 130, 30, 130)
                
                break;
                
                case 8:
                drawLine(10, 20, 10, 130)
                
                
                break;
                
                case 7:
                drawLine(10, 20, 50, 20) 
                break; 
                
                case 6:
                drawLine(50,20,50,30)
                break; 
                
                case 5:
                
                //drawing head
                context.beginPath();
                context.arc(50, 40, 10, 0, Math.PI*2, true);
                context.stroke();
                break;
                
                case 4:
                
                drawLine(50,50,50,90)
                
                break;
                
                case 3:
                drawLine(50,90,30,110)
                break; 
                
                case 2:
                drawLine(50,90,70,110)
                break;
                
                case 1:
                drawLine(50,60,30,80)
                break;
                
                case 0:
                
                drawLine(50,60,70,80)
                break;
                
            }
            
            
        }
        
```


Last but not least, we need to run all the methods within the function. Note, we haven't called the `play()` function yet, so these methods are not being run. 

```javascript
   // main .js
   // run all main methods

        //RUN MAIN METHODS
        showButtons();
        showBlanks();
        showHint();
        showLives();

```

## Running Things 

Somewhere in the main script, run the following function.

```javascript

//main.js

play("hakuna matata","It means no worries for the rest of your days")

```


<p>
  <!-- <a href="MY WEBSITE LINK" target="_blank"> -->
    <img src="/img/hangman_pics/hakuna_matata.png" style='width:100%; display:block; margin-left:auto;margin-right:auto' border="0" alt="Null">
  <!-- </a> -->
</p>

We can then go ahead and run our index.html. You can do this by going to your folders and clicking on the file. Notice, that we only managed to include "hakuna matata" and it's corresponding definition manually. In the next section, we discuss how to get a random word from a dictionary. 

## An Urban Twist

Upon looking for an npm module to produce a word, I was looking for some modules which would fetch me words and definitions(as the hint). Initially, I used an npm-module called  `random-words` and `word-definition`. It would have been a two-part process: 1) generate random word 2) lookup definition of word using wiktionary api. Since `word-definition` had it's most recent version 3 years ago, I anticipated some problems and I actually did encounter them; fetching resources from wiktionary would always return me errors.

I realised, "Why am I doing this in two parts? There has to be an npm module which fetches both a random word and defintion together". There was! It is called `urban-dictionary` npm module. For those of you who have not used "urban-dictionary", it is a dictionary of slang words and phrases that arise from current and non-current culture -- this would make playing hangman great again.

From the hangman games I had played online, I realised that most of it was boring. The words were simple; often times only one word and it's question scope limited (since they do not use a whole dictionary). The `urban-dictionary` module, however, uses Urban Dictionary's API and fetches pretty interesting content.

Try these hangman questions out for yourself.

<p>
  <!-- <a href="MY WEBSITE LINK" target="_blank"> -->
    <img src="/img/hangman_pics/urban_example2.png" style='width:40%; display:block; margin-left:auto;margin-right:auto' border="0" alt="Null">
  <!-- </a> -->
</p>

> When a guy is [driving] into the [lane], gets fouled, and still manages to [score].


<p>
  <!-- <a href="MY WEBSITE LINK" target="_blank"> -->
    <img src="/img/hangman_pics/urban_example4.png" style='width:60%; display:block; margin-left:auto;margin-right:auto' border="0" alt="Null">
  <!-- </a> -->
</p>

> An alcoholic beverage, specifically any type of beer. It doesn't matter which, coz down here in Oz, [no one gives] [a hoot], so long as you [get pissed]!


## Putting Everything Together

Firstly, include `main.js`, `index.html` and `style.css` into a directory named "whateveryouwant". Before we add modules,we need to initialise our npm directory,

```bash
npm init
```

We have to install `urban-dictionary` modules using

```bash
npm install urban-dictionary
```

The great thing about [`urban-dictionary` module][3] is that there is a way to randomise the dictionary word and definition that is returned. There is one caveat: The word and definition is returned as a promise. Unlike anything we have coded here, we have not used any promises. No big deal. The idea of a promise is that we can only extract the data when we have received it, i.e. `then()` response will run after the promise is fulfilled. Therefore, we need only include `play()` function inside of `then()`.

```javascript 
//main.js -- put this at top of your main.js file

var ud= require('urban-dictionary');

//promise object returned by ud directory
ud.random().then((result) => {

    // console.log(result.word);
    play(result.word,result.definition)
    
    
}).catch((error) => {
    console.error(error.message)
})

```

There is an additional thing that we are missing. We can't use `require()` without having a bundler concatenate all dependency modules in one file. For that we can use an npm module called "Browserify".

```bash
npm install browserify
```

Additionally, you have to add the "build" key to "scripts" to your package json. This is to execute the bash command that bundles `main.js` to `bundle.js` with dependent node modules. Edit accordingly; my package.json looks like this.


```json
{
  "name": "hangman",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "browserify main.js -o bundle.js"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/tintinthong/hangman.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/tintinthong/hangman/issues"
  },
  "homepage": "https://github.com/tintinthong/hangman#readme",
  "dependencies": {
    "browserify": "^16.2.3",
    "urban-dictionary": "^2.2.1"
  }
}

```

We need to update our `index.html`. We just need to replace `main.js` and `bundle.js` within the script tags.


```javascript 

//  <script src="main.js"></script>
 <script src="bundle.js"></script>

```


## Result

To run the script. 

``` javascript
npm run-script build
```
Click on index.html. Below is the result you should obtain. Everytime you refresh a page, there will be a new hint and a new word. Now, you can enjoy obtaining random hangman words from urban-dictionary.

<p>
  <!-- <a href="MY WEBSITE LINK" target="_blank"> -->
    <img src="/img/hangman_pics/urban_examplefinal.png" style='width:100%; display:block; margin-left:auto;margin-right:auto' border="0" alt="Null">
  <!-- </a> -->
</p>


## What is missing? 

1. One of the main problems of the `urban-dictionary` api is that occasionally, it will expose the answer in the definitions. These are some of the repurcussions of having a community-developed dictionary. Therefore, if you are smart, you can find the answers in the definition. 
2. A greater separation of logic and ui. it is well-known that a developer should not maintain a close couping between the ui and logic. As I am developing on client side, it may not matter as much. But future revisions of the code to be hosted on a server will benefit from this sort of thinking. 
3. There is a lot of need to beautify this app further. It is not centered and the buttons are too small. I would also prefer if the buttons did not dissappear and shift; instead I would prefer clicked buttons to no longer be clickable and be "darkened" out.
4.  There are subtleties to the continuation of the game. Two-fold: 1) although an `alert()` is invoked stating that a person has lost, one can still continue the game and go ahead and win it. 2) it will be helpful if the answer was given after a person has lost.


## Contribute

Let's not pretend that this is a perfectly built app. However, I believe that it has the potential to become a really interesting variation of hangman that many people can enjoy playing. If you have any interesting ideas of suggestions, please contribute here [https://github.com/tintinthong/hangman][2]. 

[1]: https://codepen.io/cathydutton/pen/ldazc

[2]: https://github.com/tintinthong/hangman

[3]: https://www.npmjs.com/package/urban-dictionary