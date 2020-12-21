## Boost your React apps with React.memo, useCallback, and useMemo

One of the many reasons we love 💙 React is because it is really fast. React does tons of work under the hood to guarantee **everything renders efficiently**. Hence, in most cases, performance is not something we need to worry about. However, we can run into **some situations** where we find out that our components are **rendering more than they need to**, and as a consequence, slowing our apps down. 🐢🐢

Hi! I'm Ernesto, and in this post, I'll talk about how to use `React.memo`, `useCallback`, and `useMemo` to make our React applications run like the wind. ⚡⚡

![performance-meme.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606270889794/f5L90hClV.png)



---
# Table of content
1. [React.memo](#reactmemo)
2. [useCallback and useMemo](#usecallback-and-usememo)
  1. [useCallback](#usecallback)
  2. [useMemo](#usememo)
3. [Conclusions](#conclusions)
---



# React.memo 🧠
It is one of the coolest features that came with the release of React 16.6.0. ⚛️ As its name refers, `React.memo` allows us to make a **performance boost** only for **function components** by a **memoizing process**. It's similar to `PureComponent` used for class components.

> `React.memo` is a [High Order Component](https://reactjs.org/docs/higher-order-components.html) (HOC), which is a function that takes a component and returns a new component.

`React.memo` takes a function component and returns a [memorized](https://en.wikipedia.org/wiki/Memoization) (optimized) component.

Confused? 😐 Let's see an example. 😁 - *You can check the example in [my CodePen](https://codepen.io/netoTests/pen/wvWVBxZ). ✒*

```jsx
//Child Component
const ChildComponent = (props) => {
  //This message is printed when the component renders
  console.log("ChildComponent rendered")

  return (
    <div className="box">
      <h1>Child Component</h1>
      <h2>{props.name}</h2>
      <p>This component does not change, so it should not render</p>
    </div>
  )
}
```

```jsx
//Main Component
const MainComponent = () => {
  const [value, setValue] = React.useState(0)
  handleClick = () => {
    setValue(value => value + 1)
  };
  
  return (
    <div>
      <h1 className="title">React.memo example</h1>
      <div className="box">
        <div>{value}</div>
        <button onClick={handleClick}>+</button>
      </div>
      {/*Child component, its prop does not change*/}
      <ChildComponent name="Ernesto"/>
    </div>
  )
}
```

We have a `MainComponent` that renders a `ChildComponent` with the `name` prop. The `MainComponent` has a state, and if it changes, the component will re-render. 

It makes sense, right? 🤔 **If a component changes, it should re-render, but if it does not, it should not.**

However, when we click the + button and change the `MainComponent` state, the `ChildComponent` re-renders too. If you check the console, you'll see the *"ChildComponent rendered"* message.

![react-memo-problem.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606271560677/d3dHk6qv1.png)

That is an unnecessary re-render because the `ChildComponent` did not change at all; the only one that changed is the `MainComponent`.

How can we solve this problem? 🤨 Well, now is when `React.memo` comes to the rescue. The only thing we have to do is to wrap our `ChildComponent` inside the `React.memo()` function.

```jsx
//Child Component
//We use React.memo
const ChildComponent = React.memo((props) => {
  //This message is printed when the component renders
  console.log("ChildComponent rendered")

  return (
    <div className="box">
      <h1>Child Component</h1>
      <h2>{props.name}</h2>
      <p>This component does not change, so it should not render</p>
    </div>
  )
})
```

Now, if you see the console, the *"ChildComponent rendered"* message should appear only once, and when you click the + button and change the state, this message won't show because the `ChildComponent` did not re-render. 😎

![react-memo-solution.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606271694761/m47tohVqO.png)

`React.memo` compares the props passed to a component. If they are the same as last time, `React.memo` will use the previous rendered result and skip the re-rendering process.

> Remember that `React.memo` only looks for **props changes**. That means that if your function component has a state (with `useState` hook), it will still re-render when the state changes.



# useCallback 🏹 and useMemo 🔥
These two hooks can be kind of confusing. 😵 Both of them receive a function and an array of dependencies as parameters, and both will compute a new value only when one of the dependencies changes.

```js
//Returns a memoized function
const memoizedCallback = useCallback(() => {
  doSomething();
}, [dependencies]);
```

```js
//Returns a memoized value
const memoizedValue = useMemo(() => {
	return computeExpensiveValue()
}, [dependencies]);
```

The difference is that `useMemo` will return a **memoized value**, the result of the function passed, and `useCallback` will return the **memoized function** itself.

Let's see how and when to use them. 😉


### useCallback
It is especially useful when **passing callbacks to optimized child components**. Therefore, `useCallback` always works with `React.memo`.

We will take the previous example and change it a little bit. - *You can check the example in [my CodePen](https://codepen.io/netoTests/pen/OJXKVdN). ✒*

```jsx
//Child Component
const ChildComponent = React.memo((props) => {
  console.log("ChildComponent rendered")
  const [value, setValue] = React.useState(0)

  return (
    <div className="box">
      <h1>Child Component</h1>
      <h2>{props.name}</h2>
      <p>This component does not change, so it should not re-render</p>
      {/*Button that will change the state of its parent component*/}
      <button onClick={props.handle}>+</button>
    </div>
  )
})

```

```jsx
//Main Component
const App = () => {
  const [value, setValue] = React.useState(0)
  handleClick = () => {
    setValue(value => value + 1)
  };
  
  return (
    <div className="main-comp">
        <h1 className="title">Main Component</h1>
        <div className="box">
          <div>{value}</div>
        </div>
        {/*Pass the handleClick function through props*/}
        <ChildComponent name="Ernesto" handle={handleClick}/>
    </div>
  )
}
```

Now, the button that changes the state of the `MainComponent` is inside the `ChildComponent`; therefore, we have to pass the `handle` prop that contains the `handleClick` function from the `MainComponent`.

If you go to the console, you'll notice the *"ChildComponent rendered"* message shows again every time we click the button. We are using `React.memo`, but the component is still re-rendering. What is happening? 🥴

![useCallback - problem.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606272293456/Lk1fFB0oQ.png)

That happens because every time the `MainComponent` state changes, a NEW `handleClick` function is being created. That means that the `handle` prop of the `ChildComponent` is different every time we click the + button. That is the reason why `React.memo` is not working; the `handle` prop is changing.

We can fix the problem by using the `useCallback` hook to memoize the `handleClick` function.

```jsx
//Main Component
const App = () => {
  const [value, setValue] = React.useState(0)
  //useCallback hook
  const handleClick = useCallback(() => {
    setValue(value => value + 1)
  }, []);
  
  return (
    <div className="main-comp">
        <h1 className="title">Main Component</h1>
        <div className="box">
          <div>{value}</div>
        </div>
        {/*Pass the handleClick memoized function through props*/}
        <ChildComponent name="Ernesto" handle={handleClick}/>
    </div>
  )
}
```

Notice that the array of dependencies is empty; this means that the function will be created only once. Therefore, the `handle` prop of the `MainComponent` will always be the same. 😎

![useCallback - solution.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606272412704/Sd18X2JMV.png)


### useMemo
We use `useMemo` when we have to **compute an excessive value**, and we do not want to re-compute it again every time our component re-renders.

Let's go with an example. - *You can check the example in [my CodePen](https://codepen.io/netoTests/pen/QWEezwZ). ✒*

```jsx
//Function that computes an exessive value
const heavyProcess = (times) => {
  for (let i = 0; i < times; i++) {
    console.log('Go ...', i + 1);
  }
  return `Heavy process done (result: ${times})`;
};

//Main Component
const MainComponent = () => {
  const [value, setValue] = React.useState(0)
  handleClick = () => {
    setValue(value => value + 1)
  };
//The returned value is saved
const heavyProcessValue = heavyProcess(1000)
  
  return (
    <div className="main-comp">
        <h1 className="title">Main Component</h1>
        <div className="box">
          <div>{value}</div>
          {/*The returned value is printed*/}
          <p>{heavyProcessValue}</p>
          <button onClick={handleClick}>+</button>
        </div>
    </div>
  )
}
```

We are simulating a heavy process with the `heavyProcess` function that will print to the console the numbers from 1 to 1000 and return the last number printed (1000). Our `MainComponent` has a simple counter, and it prints the returned value of the `heavyProcess` function.

If you go to the console, you will notice that all numbers from 1 to 1000 are being printed every single time we click the + button. So, every time the components re-renders (due to a change in its state) the `heavyProcess` executes again.

![useMemo-problem.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606272864527/6yycCahS6.png)

This time, `useMemo` will save us. We will use it to memoize the computed value.

```jsx
//Main Component
const MainComponent = () => {
  const [value, setValue] = React.useState(0)
  handleClick = () => {
    setValue(value => value + 1)
  };
  //The returned memoized value is saved with useMemo
  const memoizedHeavyProcessValue = React.useMemo(() => {
    return heavyProcess(1000)
  }, [])
  
  return (
    <div className="main-comp">
        <h1 className="title">Main Component</h1>
        <div className="box">
          <div>{value}</div>
          {/*The memoized value is printed*/}
          <p>{memoizedHeavyProcessValue}</p>
          <button onClick={handleClick}>+</button>
        </div>
    </div>
  )
}
```

Now, instead of passing the value that the `heavyProcess` function returns, we pass the memoized value that the `useMemo` hook gives us; this value will be computed again only if one of the dependencies changes. In our case, the array is empty, which means the value will be computed only once. 😎

> Do not forget the `return` statement in the first parameter of the `useMemo` hook.

![useMemo-solution.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606273120608/r-3l4c00_.png)



# Conclusions
* Use `React.memo` to skip ⏭ **unnecessary renders** in your function components. If you want something similar to that for class components, use `PureComponent`.
* Use the `useCallback` hook when you want to **pass callbacks 🏹 to child components** through props.
* Use the `useMemo` hook when you want to memorize an **excessive value** 🔥 returned by a function, like an HTTP request that gets tons of data.

Remember that before you start optimizing your apps, you should **measure the cost first**.  ⚖ Otherwise, you will be optimizing things that may don't need to be optimized. 😉

Thanks for reading! 📖 If this post helped you, please give it a reaction. And If you have any contribution, comment, doubt, or recommendation, write it down in the comments section. It helps me a lot to improve my content. 😃

See you in the next post. 👋

---
# Resources
* [https://reactjs.org/docs/react-api.html#reactmemo](https://reactjs.org/docs/react-api.html#reactmemo)
* [https://reactjs.org/docs/hooks-reference.html#usecallback](https://reactjs.org/docs/hooks-reference.html#usecallback)
* [https://reactjs.org/docs/hooks-reference.html#usememo](https://reactjs.org/docs/hooks-reference.html#usememo)
---

*If you want to read the Spanish version of this post, you can find it [here](https://netosym.medium.com/optimiza-tus-aplicaciones-de-react-con-react-memo-usecallback-y-usememo-82ab57fe162c).*