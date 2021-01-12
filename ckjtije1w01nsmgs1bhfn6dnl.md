## Manage global states with Context API and useContext

Have you ever heard this?

> "When we change the way we communicate, we'll change society."

> Clay Shriky

We all know that human communication 🗣 is vital to our society. The process of sharing thoughts, ideas, feelings, or stories has been and still is, a key point for all the great things humans have achieved. 

You may be wondering, why is this guy talking about communication? 🤔 Isn't this post supposed to be about React? 🤔 🤔 Of course, it is. The take away ⭐ here is that all I said above applies to React, **humans being our components**, **society the actual React application**, and the **thoughts or ideas data**.

Hi! I'm Ernesto, and in this post, I will give you an introduction to the `Context API` and the `useContext` hook, so you can **manage your global state easily**. 😉

![meme.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610424043935/KlVn_SOmH.png)



---
# Table of content
1. [Data flow](#data-flow)
2. [Contex API](#context-api)
  1. [Create a context](#create-a-context)
  2. [Provide context](#provide-context)
  3. [Consume context with useContext hook](#consume-context-with-usecontext-hook)
3. [Example](#example)
4. [Conclusions](#conclusions)
---



# Data flow
Consider this tree of React components:

![components-tree.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1610422495068/6VKJKPSBs.jpeg)

We know that component communication (data flow) is vital for our React applications. But how can we make data flow through our components? One way to do it is by passing the data via props from a parent component to a child.

![props.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1610422562042/jPQisEgRM.jpeg)

However, that way comes with one problem. What if we want to pass data to a component that is many levels below? 🤔

![props-problem.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1610422728547/cPP8UrY-Y.jpeg)

Passing data to all the intermediary components to the one which needs the data at the bottom, even when these intermediary levels do not need it, can be a tedious process. 😖

Now is when the Context API comes in to save us. 🤓 We can make a component a source (provider) of data and pass it directly to any level. That takes away the need to send the data to intermediary levels. 🥳

![context-api.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1610422859922/2nqxpCFLg.jpeg)



# Context API
According to the [documentation](https://reactjs.org/docs/context.html), the Context API provides a way to **send data through the component tree without having to pass props down manually at every level**. In simpler words, it allows us to **pass data to a component directly**. 🔼🔽

> React recommends using Context when we have **data or states that are global or used in many different components**.


### Create a context

To use the Context API, we have to create a context first. **A context is like a source** 🗄️ **where the provider gets the data from** and passes it to the components. We create a context with the `createContext` method.

```jsx
/*  MyContext.js  */

// Import createContext method from React
import {createContext} from 'react'

// Create and export context with a default value
export const MyContext = createContext(defaultValue)

```

> The `defaultValue` argument is optional, and a component uses it only when it does not have a matching Provider above it in the tree.


### Provide context
After we create our context, we have to provide it to the component tree. We do that by wrapping the component that will use the context's data with a context provider. 📤 **A Provider is a component that the context we created gives us**.

```jsx
/*  MainApp.jsx  */

//Import the context created
import { MyContext } from 'your-path/MyContext.js'
// Import MyComponent
import MyComponent from 'your-path/MyComponent.jsx'

//Main Component
const MainApp = () => {
	return (
		// Wrap MyComponent with MyContext.Provider and give it a value
		<MyContext.Provider value={contextValue}>
			<MyComponent />
		</MyContext.Provider>
	)
}
```

`contextValue` is the data that will flow through `MyComponent` and its children (components it renders).

> Note the difference between `defaultValue` and `contextValue`. The second is the principal value of the context; whereas the first is the one we use if there is no provider.


### Consume context with useContext hook
`useContext` hook allows us to access the **current value of a context**. 📩 This value is determined by the value prop of the nearest `<MyContext.Provider>`.

```jsx
/*  MyComponent.jsx  */

// Import useContext
import { useContext } from 'react'
// Import the context created
import { MyContext } from 'your-path/MyContext.js'

// MyComponent
const MyComponent = () => {
	// useContext hook returns the current value of the context
	const contextValue = useContext(MyContext)

	//...
}
```

Remember that the argument that `useContext` takes is the actual context created.

> This hook works only with functional components. If you want to consume a context with a class component, you will need a [Consumer](https://reactjs.org/docs/context.html#contextconsumer).

Enough with the theory, let´s make an example. 😃



# Example
We have a `Global` component that renders a `Parent`. This component renders a `Child` component, and it renders a `GrandChild`.

> Global → Parent → Child → GrandChild

![example.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610423347308/Cqtyhrtr6.png)

The Global component has a state that will be `true` or `false`, depending on the state of the bulb (on or off). We want the `GrandChild` component to be the one that manages the bulb state. That means that we need to pass this state to the `GrandChild` component, and we do not want to pass it through props.

*You can check the full example in [my CodePen](https://codepen.io/netoTests/pen/xxEaOXq).* ✒️

> Remember that I created this basic example only for teaching means. It may not be the best use case for using Context.

```jsx
//Grand Child Component
const GrandChild = () => {
  return (
    <div className="grand-child p-3 m-3">
      <h1>Grandchild</h1>
      <p className="mb-2">You can turn on the bulb by clicking the button</p>
      {/* Button to turn on/off the bulb */}
      <button className="btn btn-success d-flex justify-content-center btn-block">
        Turn on
      </button>
    </div>
  );
};

//Child Component
const Child = React.memo(() => {
  return (
    <div className="child p-3 m-3">
      <h1>Child</h1>
      {/* Renders GrandChildComponent */}
      <GrandChild />
    </div>
  );
});

//Parent Component
const ParentComponent = React.memo(() => {
  return (
    <div className="parent p-3 m-3">
      <h1>Parent</h1>
      {/* Renders ChildComponent */}
      <Child />
    </div>
  );
});
```

```jsx
// Global Component
const App = () => {
  // Bulb state (on - off)
  const [state, setState] = React.useState(false)
  return (
    <>
      <div className="container p-3 m-3">
        <h1>Global App</h1>
        <div className="bulb-container">
          <p className="bulb-title">This is a bulb 😅:</p>
	      {/* Bulb */}
          <div className={`${state ? 'bulb bulb-on' : 'bulb'}`}>
            <p>{state ? 'ON' : 'OFF'}</p>
          </div>
        </div>
	    {/* Renders ParentComponent */}
        <Parent />
      </div>
    </>
  );
};
```

Let's create a context.

```jsx
// Import createContext
import {createContext} from 'react';

// BulbContext with a default value
const BulbContext = createContext({
	value: 'This is the default value'
});
```

> We'll see how to use the default value later.

Once we created the context, we have to use the `Provider` to wrap the component that will use our context.

```jsx
const App = () => {
  // Bulb state (on - off)
  const [bulbState, setState] = React.useState(false)
  return (
    // Provider with a value
    <BulbContext.Provider value={{bulbState, setState}}>
      <div className="container p-3 m-3">
        <h1>Global App</h1>
        <div className="bulb-container">
          <p className="bulb-title">This is a bulb 😅:</p>
          <div className={`${bulbState ? 'bulb bulb-on' : 'bulb'}`}>
            <p>{bulbState ? 'ON' : 'OFF'}</p>
          </div>
        </div>
		{/* Renders ParentComponent */}
        <Parent />
      </div>
    </BulbContext.Provider>
  );
};
```

The value we pass is an object that contains the `bulbState` and the `setState` method that we use to change it.

Now, we have to use that context in our `GrandChild` component.

```jsx
// Import useContext hook
import {useContext} from 'react';

const GrandChild = () => {
  // useContext hook
  const { bulbState, setState } = useContext(BulbContext)
  return (
    <div className="grand-child p-3 m-3">
      <h1>Grandchild</h1>
      <p className="mb-2">You can turn on the bulb by clicking the button</p>
		{/* setState method to change the bulbState */}
      <button className="btn btn-success d-flex justify-content-center btn-block" onClick={() => setState(!bulbState)}>
		{/* bulbState */}
        {bulbState ? 'Turn off' : 'Turn on'}
      </button>
    </div>
  );
};
```

We get the `bulbState` and the `setState` method from the `useContext` hook. Then we use the method on the `onClick` event of the button.

Now, our application working. The button toggles the bulb state, and the one that controls it is the `GrandChild` component. 😎😎

![https://i.makeagif.com/media/1-11-2021/6UnFMJ.gif](https://i.makeagif.com/media/1-11-2021/6UnFMJ.gif)

Great! Now, what about the default value? As I said before, we use it when a component uses a context, and it does not have a `Provider`.

Let's create a component inside `App` but outside the context provider.

```jsx
const NoProvider = () => {
	// Use the context without a value. We use the default value
  const { value } = React.useContext(BulbContext)
  return (
    <div className="container no-provider mt-3">
      <h1>Component with no provider</h1>
      <p>This component uses the default value of the context</p>
			{/* Print the default value */}
      <p className="mt-3"><span>{value}</span></p>
    </div>
  )
}

const App = () => {
    // code...
    <>
    <BulbContext.Provider value={{value: state, setState}}>
			{/* code... */}
    </BulbContext.Provider>
		{/* Component outside the Provider */}
    <NoProvider />
    </>
  );
};
```
With the `useContext` hook, we get the default value because there is no `Provider` for this component.

![no-provider.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610423902288/hTq2R7CII.png)

And that's it, pretty easy, right? Now, we know how to use `Context API` and `useContext` hook. 🎉🥳

> Tip: If you have read [my post about React.memo](https://ernestoangulo.hashnode.dev/boost-your-react-apps-with-reactmemo-usecallback-and-usememo) 😅, you'll notice that we can use it to avoid an unnecessary rendering. 😉😉



# Conclusions
- `Context API` helps us to pass data through components directly. 🔼🔽
- Use the `Context API` when you have a global state 🌎 or when many components will use the same state.
- When creating a context, use the default value for a component that does not have a `Provider`. 📤
- `useContext` makes it easier to read a context value 📨, but it only works for functional components.
- If you want to read a context value with a class component, you will have to use a [Consumer](https://reactjs.org/docs/context.html#contextconsumer). 📥

Thanks for reading! 📖 If this post helped you, please give it a reaction. And If you have any contribution, comment, doubt, or recommendation, write it down in the comments section. It helps me a lot to improve my content. 😃

See you in the next post. 👋


---
# Resources
* [https://reactjs.org/docs/hooks-reference.html#usecontext](https://reactjs.org/docs/hooks-reference.html#usecontext)
* [https://reactjs.org/docs/context.html](https://reactjs.org/docs/context.html)