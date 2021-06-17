# Exercises 07

## Overview

### Aim

- Use ReactJS Hooks for their intended purpose.
- Develop knowledge of fetch/async/await.
- Express your basic understanding of UI/UX.

## Exercise 1 - Promises & Async/Await

In the `exercise1` folder run `yarn` and then `yarn start`.

This file currently uses promises (`promise.then().catch`) to handle the asynchronous fetch and json decoding. Refactor this code to only use `async`/`await` syntax.

After the conversion the component should have identical functionality.

## Exercise 2 - `Promise.all`

In this exercise, we will be looking at `Promise.all`.
`Promise.all` allows you to aggregate/analyse the results of multiple asynchronous calls at once.
You can give it an array of promises and once resolved, it will return an array of results to you.
For more information, see the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all).
The file `PromiseAll.js` contains a function called `getCompanyRepos`. It fetches a given company's public repositories from GitHub.
If the company does not exist or has no information available, it will throw an error.
We will be using NPM + Node.js for this exercise. When you go into the exercise folder, run `npm install`.
To run the exercise, execute `node PromiseAll.js`.

### Question 1

Currently, the `question1` function gets the repo names of "microsoft", "google" and "canva" and prints them out as soon each promise resolves.
Using `Promise.all` and `.then`, modify `question1()` so that the repo names are printed out all at once.
HINT: you can store an unresolved Promise in a variable like this: `const microsoftRepos = getCompanyRepos("microsoft");`

### Question 2

Repeat question 1, but use `async` and `await` instead.

### Question 3

See what happens when you give `Promise.all` a `Promise` that will reject.
Do this by getting the repo names of "microsoft" as well as "some_fake_company".
Does `Promise.all` resolve or reject?
Are we able to see the repo names of "microsoft"?

### Question 4

If you don't need the results of promise that was rejected, you can use `Promise.allSettled` instead of `Promise.all`.
Instead of an array of resolved results, `Promise.allSettled` returns an array of fulfilled or rejected items.
Each item will have one of the two formats:

1. `{ status: "fulfilled", value: ... }`
2. `{ status: "rejected", reason: ... }`

Use `Promise.allSettled` to print the repo names of "microsoft", "google", "canva" and "some_fake_company".
If you encounter a `status === "rejected"` item, log the reason for it rejecting.

## Exercise 3 - React App

In the `exercise3` folder run `yarn` and then `yarn start`.

Build a simple ReactJS app that does the following:

- Has an input form field where a user can enter a list of comma separated Github user names (e.g. `UNSWComputing`, `Microsoft`, `Google`). Examples of one of these can be found [here](https://api.github.com/users/Microsoft).
- After 500 miliseconds from the last time this user input fires an `onChange` event, the list of comma separated user names is split, and for each one a `fetch` is made to collect data at the URL "https://api.github.com/users/[USERNAMEGOESHERE]". You can leverage the stub code provided in `exercise1` to get a good head start here.
- Once ALL of the fetches complete (and not before), you shall display a series of cards underneath on the page. Each card should be a separate ReactJS component that is imported into your `App.js`. Each component simply needs to consist of:
  - A 50px by 50px image that is the `avatar_url` property returned by the fetch
  - The `name` of the organisation (derived from the `name` property of the fetch), where clicking on this name links (in a new tab) to the `url` (derived from the `url` property of the fetch).

Note: You can implement the multiple fetches one of two ways:

- With a loop and async/await
- Using promises (preferable), where you can execute many promises at once using [Promise.all](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

In this exercise you are expected to use: `fetch`, `React.useEffect`, `React.useState`, ReactJS Functional Components.

## [Challenge] Exercise 4 - Class component conversion

In the `exercise4` folder run `yarn` and then `yarn start`.

This ReactJS app currently uses functional components. Convert this functional component into a ReactJS **Class Component**. After the conversion the component should have identical functionality.

## [Challenge] Exercise 5 - React App Authentication with JWTs

In this exercise, we will be using a JSON Web Token (JWT) to access a private route on a backend API.
JWTs are the industry standard for authenticating users.
In a nutshell, the frontend client sends a user's username and password to the backend, the backend encrypts some information (usually the user's email & other details) and sends it back to the client.
The encrypted user details form a JWT, and the client can send this back to the backend to access private routes.
For more information on JWTs, [checkout this source](https://jwt.io/introduction/).

For the purposes of this exercise, the backend does not check passwords, but obviously this should be done in practice.
Also, the frontend is not styled, as the main goal is to familarise yourself with using JWTs.

To start the backend, `cd` into `exercise5/backend` and run `npm install`, then `node app.js`.
To start the frontend, `cd` into `exercise5/frontend` and run `yarn`, then `yarn start`.

### Question 1

Inside `frontend/src/App.js` there is a simple login form. If you enter `comp6080_student` as the username with any password, you will be able to see a JWT printed out in the console log (`data.token` in `App.js` line 23).

Once the JWT has been received, store it in `localStorage` and redirect to a new page (i.e. render a different component to the login form).

### Question 2

On this new page, attempt to fetch `localhost:5000/api/secret-message` from the backend.
Note that this response will give you an error message!
Use the details of this error message, as well as the token stored in `localStorage` to get a successful response.

_Hint: use 'JWT <TOKEN>' for the 'authorization' header value. For more information on the format of this header, [visit MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization)._

A successful response will look something like this:

```
{
  message: <SECRET-MESSAGE>,
  authData: {
    <USER DETAILS>
  },
}
```

### Question 3

Once you are able to receive the secret message, display it on the new page, as well as the username of the logged in user.
You can find the username from the response in `authData.user.username`.
