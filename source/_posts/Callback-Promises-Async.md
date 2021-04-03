---
title: Callback, Promises, Async Await
date: 2021-04-03 18:17:44
tags:
---
# Why we use callback and how

In this example, because getPosts Timeout is only 1 sec, but 
createPost Timeout is 2 sec. So the Page will not wait for the new post
to be generated
```javascript
const posts = [
    {title: 'post 1', body: 'This is post 1'},
    {title: 'post 2', body: 'This is post 2'}
]

function getPosts() {
    setTimeout(() => {
        // create the output string
        let output = '';
        // store post into output
        posts.forEach((post, index) => {
            output += `<li>${post.title}</li>`;
        });
        // print in the page
        document.body.innerHTML = output;
    }, 1000);
    
};

function createPost(post) {
    setTimeout(() => {
        posts.push(post);
        
    }, 2000);
}

getPosts();

createPost({title: 'post 3', body: 'This is post 3'})
```

How do we make it work
- We put getPosts() into createPost
- After all post are being generated, we print the post
- Generate a callback function into createPost
```javascript
// Change timeout to be half to make it appears quicker
const posts = [
    {title: 'post 1', body: 'This is post 1'},
    {title: 'post 2', body: 'This is post 2'}
]

function getPosts() {
    setTimeout(() => {
        // create the output string
        let output = '';
        // store post into output
        posts.forEach((post, index) => {
            output += `<li>${post.title}</li>`;
        });
        // print in the page
        document.body.innerHTML = output;
    }, 500);
    
};

function createPost(post, callback) {
    setTimeout(() => {
        posts.push(post);
        callback()
    }, 1000);
}

// Without () after getPosts!! we pass a function not a function call
createPost({title: 'post 3', body: 'This is post 3'}, getPosts)
```

# How do we use Promise

```javascript
const posts = [
    {title: 'post 1', body: 'This is post 1'},
    {title: 'post 2', body: 'This is post 2'}
]

function getPosts() {
    setTimeout(() => {
        // create the output string
        let output = '';
        // store post into output
        posts.forEach((post, index) => {
            output += `<li>${post.title}</li>`;
        });
        // print in the page
        document.body.innerHTML = output;
    }, 500);
    
};

function createPost(post) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            posts.push(post);

            // put inside timeout
            const err = false;

            if (!err) {
                resolve();
            } else {
                 reject('Something went wrong')
            }
        }, 1000);
    })
}

// normal
// createPost({title: 'post 3', body: 'This is post 3'}).then(getPosts);

// error = true
// createPost({title: 'post 3', body: 'This is post 3'}).then(getPosts).catch(err => console.log('Error!'))

// how to use promise.all
const p1 = Promise.resolve(1);
const p2 = 20;
const p3 = new Promise((resolve, reject) => {
    setTimeout(resolve,500, 'Hello')
});

const p4 = fetch('https://jsonplaceholder.typicode.com/comments').then(res => res.json())

Promise.all([p1,p2,p3,p4]).then(vals => console.log(vals));
```
# What is Async and Await
A more elegant way to handle Promise
```javascript
async function init() {
    await createPost({title: 'post 3', body: 'This is post 3'});
    getPosts();
}

init();
```

```javascript
async function fetchComments() {
    const res = await fetch('https://jsonplaceholder.typicode.com/comments');
    const data = await res.json();

    console.log(data)
}

fetchComments();
```