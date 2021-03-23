---
title: Typing-Game
date: 2021-03-23 11:36:43
tags: Web Development
---

# How to create a typing game using event

## Things to be cared of

### Three blocks in HTML
- Quote Block
    - It has id='quote'
    - You can add more quote into the quot list
    - Element in Quote Block needs to be separate by <span> 
- Message Block
    - The information of time after you finishing the game
- Input Block
    - Used to type and compare with the element in quote block

### How to indicate error and highlight
When you compare with input and quote, mark quote.childNode[cur] with className = highlight. You need to remove highlight when you finish typing a word. If the input is not equal with quote just add className=error

Answers:

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Document</title>
</head>
<body>
    <h1>Welcome to type game</h1>
    <p>Click start to begin the game</p>
    <p id="quote"></p>
    <p id="message"></p>
    <div>
        <input type="text" aria-label="current world" id="typed-value" />
        <button type="button" id="start">start</button>
    </div>
    <script src="script.js"></script>
</body>
</html>
```

```javascript
// inside script.js
// all of our quotes
const quotes = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
];

// keep track of the words, (and quote)
let words = [];
let wordIndex = 0;

// keep track of start time
let startTime = Date.now();

//quote element
const quoteElement = document.getElementById('quote');
//message element, after wining and indicate the time used
const messageElement = document.getElementById('message');
//track typed elements
const typedElement = document.getElementById('typed-value')

// first indicate the quote text after click the start button
document.getElementById('start').addEventListener('click', () => {
    // get a numer of random quote
    const randomNum = Math.floor(Math.random() * quotes.length);
    // get the quote
    const getQuote = quotes[randomNum];
    
    // put the quotes into the words array
    words = getQuote.split(' ')
    wordIndex = 0;

    // append to quoteElement
    // !!!!! there is a white space between ${word} and </span>
    const spanList = words.map(function(word) { return `<span>${word} </span>`})
    quoteElement.innerHTML = spanList.join('')
    
    //highlight the first element
    quoteElement.childNodes[0].className = 'highlight'
    messageElement.innerText = '';

    // initiate the typedElement
    typedElement.value = ''
    typedElement.focus();

    //initiate time
    startTime = new Date().getTime();
})


// add event listener to input value
// keep track of quoteElement and typed Element
typedElement.addEventListener('input', () => {
    //get first word in the quote
    const word = words[wordIndex]
    // get typed value
    const typedValue = typedElement.value

    // game over
    // length == wordsIndex, typed == word
    if (typedValue === word && wordIndex === words.length - 1) {
        const finishedTime = new Date().getTime() - startTime;
        const message = `Congratulations, you've finished in ${finishedTime / 1000} seconds`
        messageElement.innerText = message;
    } else if(typedValue.endsWith(' ') && typedValue.trim() === word) {
        // if the current word type correctly
        //1. clear the highlight
        //2. set the next word highlight
        //3. clear the typevalue
        typedElement.value = ''
        wordIndex = wordIndex + 1;
        for (const wordElement of quoteElement.childNodes) {
            wordElement.className = ''
        }
        // highlight new word
        quoteElement.childNodes[wordIndex].className = 'highlight'
    } else if (word.startsWith(typedValue)) {
        // not finished yet, check the current word
        typedElement.className = ''
    } else {
        typedElement.className = 'error'
    }
})

```

```css
.highlight {
    background-color: yellow;
}

.error {
    background-color: lightcoral;
    border: red;
}

body {
    font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif
}


```