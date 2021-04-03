---
title: Pub Sub Pattern
date: 2021-04-03 16:38:58
tags:
---
# Publish-Subscribe pattern

## Why do we use Pub-Sub pattern?
1. Modular: When we wants to add new features or change features, we just need to change the code we need.
2. Separate: We don't have to know other parts of the code, easy for us to make change

### Concepts
- message: It is usually a text string(Piece of data that clarifies what the message is about). E.g. KEY_EVENT_DOWN
- publisher: Send commands to subscribers
- subscriber: Receive commands, run the command.


### How to create a Pub-Sub pattern
```javascript
class EventEmitter {
    constructor() {
        this.listeners = {}
    }

    /*
    This function register the function according to its eventName.
    When the message is received, let the listener to handle its payload.
    Publisher
    -> on(EventName, Callback)
    */
    on(message, listener) {
        if (!this.listeners[message]) {
            //this is official, create a new Array to store its callback function
            this.listeners[message] = [];
            //how I think
            // this.listeners[message] = [listener]
        }
        this.listneres[message].push(listener);
    }

    /*
    Triggers the function, send event out
    Subscriber
    */
    emit(message, payload = null) {
        if (this.listeners[message]) {
            // l is function call -> receving message from publisher and execute it
            this.listeners[message].forEach(l => l(message, payload))
        }
    }
}
```

### How to use Pub-Sub pattern
```javascript
const Messages = {
    // message is text string
    HERO_MOVE_UP: 'HERO_MOVE_UP'
};

// Create a eventEmitter
const ee = new EventEmitter();
// Create a new Hero
const hero = new Hero();
// Publish the message
ee.on(Messages.HERO_MOVE_UP, () => {
    hero.move(0, 5);
});

// Subscribe the message
window.addEventListener('keyup', (evt) => {
    if (evt.key === 'ArrowUp') {
        ee.emit(Messages.HERO_MOVE_UP);
    }
})
```