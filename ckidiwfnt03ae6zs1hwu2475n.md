## Reducers in JavaScript explained

We all know that state management 🧠 in our applications is essential, and a core concept to understand it is the reducer 🧬. Every JavaScript framework, React, Vue, and Angular use reducers for state management. Therefore, **learning what a reducer is and what it can do is mandatory to understand state management well.**

Hi! I'm Ernesto, and in this post, I will talk about what reducers are so you don't have any problems if you want to start learning Redux or other state management library. 😉

---
# Table of content
1. [What is a reducer?](#what-is-a-reducer)
2. [Actions](#actions)
  1. [Type](#type)
  2. [Payload](#payload)
3. [What about the example](#what-about-the-example)
4. [Conclusions](#conclusions)
---



# What is a reducer?
Understanding what a reducer is won't be hard because, in simple words, **it is just a JS function**. This function **takes two parameters and returns a new state**. The two parameters the reducer takes are an initial state and an action that will modify this state.

```jsx
const myReducer = (initialState, action) => newState;
```

Easy right? However, the reducers are [Pure Functions](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976), so they have some rules:

- It should not have side effects; the reducer has to **compute everything by itself**.
- It should not require or interact with **another function**.
- It should take and **return a state.**
- It should **not mutate** the state directly.

> The idea is to have all the actions that modify the state in a single place.



# Actions
It is a simple JS object that allows us to **communicate** to the reducer **what specific action we want to perform** to modify the state. It has two properties; the type and the payload.

```jsx
action = {
	type: "ACCTION_TYPE",
	payload: {
		property1: value,
		property2: value,
	}
}
```

### Type 🏹

It is a string that **names the type** of action we want to perform. To make the type as understandable as possible, make it **uppercase.**

### Payload 📄

It is a **value that the action will take to modify the state**. It can be of any type; however, it is usually an object because the state will not be that simple, and by using an object, we can easily organize and manage it.

Great! Now, you are familiar with the core concepts. 😎



# What about the example? 🤷‍♂️
```jsx
const initialState = [{
  id: 1,
  name: 'Ernesto',
  email: 'ernestoangulo@ieee.org',
  age: 20,
}, {
  id: 2,
  name: 'Juan',
  email: 'juan@mail.com',
  age: 25,
}, {
  id: 3,
  name: 'Melissa',
  email: 'melissa@mail.com',
  age: 21,
}]
```

Here we have an initial state that is just an array that contains three users with different data. Let's create a reducer that allows us to create a new user.

```jsx
//Reducer
const formReducer = (initialState, action) => {
    //Check Type
    switch(action.type) {
      //Add user
      case "ADD_USER":
        return [...initialState, action.payload]
      //Unknown type or no type
      default:
        return initialState
    }
}
```

Notice that we use the **switch statement** to select the type of action we want to perform and that we put all the logic of the action inside the cases. Also, notice that we use the default case that will return the same state if we pass an unknown type.

> That allows us to have all the logic of our different actions in a single place.

As the **state should be immutable**, we use the **spread operator** to make a copy, so we don't mutate it directly.

Now, let's create our `addUser` function that will use our reducer to perform the "ADD_USER" action.

We create the object action with its respective type and payload. Then, we pass the initial state and the action to the reducer and print the results.

```jsx
//addUser function
const addUser = (newUser) => {
  //Create the action
  const action = {
    type: 'ADD_USER',
    payload: newUser
  }
  //Use the reducer
  const newState = formReducer(initialState, action)
  //Print the result
  console.log(newState)
}

//Run the addUser function
addUser({
  id: 4,
  name: 'Karina',
  email: 'karina@mail.com',
  age: 18
})
```
![results.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1607282425753/s99F-eiix.jpeg)

*You can check the example in [my CodePen](https://codepen.io/netoTests/pen/QWKNdMz).*✒



# Conclusions
- The reducer is **a simple JS function 🔥** that returns a new state. `const myReducer = (initialState, action) => newState;`
- Use the **switch statement 👈** to select and put the logic of the actions.
- Make the actions names 🅿 uppercase.
- You must not mutate the state 🧬 directly. Use the spread operator `(...)`.

Now you are ready to learn any state management library like Redux. Try adding new actions to the reducer we just made. It gets easier as you practice more. 😀 You'll notice that once you understand the core concepts, it will become much easier for you to learn anything you want. 😎

Thanks for reading! 📖 If this post helped you, please give it a reaction. And If you have any contribution, comment, doubt, or recommendation, write it down in the comments section. It helps me a lot to improve my content. 😃

See you in the next post. 👋