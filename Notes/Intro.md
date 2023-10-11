# **React**

#### The World's Most Popular Front-end Library!

---

## What is it?

- React is a library that helps us build user interfaces from components
- We can assemble smaller components to build large applications

### Components

- Components combine HTML and logic into a single reusable function
- `function Header() {
return <h1>I'm a header component!</h1>
}`
- Functions that "know" how to render themselves into HTML

### JSX

- JSX is a syntax extension for JavaScript
- It allows us to write markup that looks like HTML directly insie of our HTML!
- It's not "legal" JS on it's own, so it must be transpiled

### JSX Rules

- You must explicitely close self-closing elements like <br/>
- Components can only return a single element

### Looping in JSX

- It's comon to use _array.map()_ to output loops in JSX:
  `
export default function Friend() {
  render() {
  const {name, hobbies} = this.props;
      return (
        <div>
          <h1>{name}</h1>
          <ul>
            <li>Singing</li>
            <li>Dancing</li>
          </ul>
        </div>
      )
    }
  }`

---

### _How to Create a React App on our Local environment with Vite_

1. Run: `npm create vite@latest`
2. Once ran, create the project and choose what framework we will use from the prompt
3. Run: `npm install`
4. Run: `npm run dev`
   - This opens the development server
   - Open the Url given to view the development server

---

## **Props**

- Props are like argument we can provide to our components
- We use props to make configurable components
- Immutable (CANNOT change)

### Non-String Props

- We use {} to use non-string props
- Example: `<Die numSides={20} />`, This is for numbers.
- Example: `<ListPicker values={["a", "b", "c"]} />`, This is for arrays and objects

### Ternary Expressions

- These are very useful and common in the world of react.
- They are in-line logic that will run like normal JavaScript
- Example: `{num1 === num2 ? <h3>They are the same!</h3> : null}, If num1=num2, return the h3, if not return null`

---

## **State**

- Data specific to an instance of a component. (CAN change)

#### _What goes in State?_

- Data fetched from an API
- Form information
- A variable that "decides" whether something is shown or hidden
- Ask yourself: "Will this ever change?"
  - If so, It should go in state somewhere!

### Using State

We create state using the _useState_ hook
Example: `const [count, setCount] = useState(0);`

- This returns an array containing two elements:
  - The piece of state itself
  - A function to change the piece of state
- You must import first
  - `import { useState } from "react"`
- You must call useState INSIDE a component
- You can also have multiple instances of State in a component

### Common Array Updating Patterns

- These are for immutable arrays where we would want to make a new copy, not change the state of the original

`const shoppingCart = [
    {id: 1, product: "HDMI cable", price: 4},
    {id: 2, product: "Easy Bake Oven", price: 28},
    {id: 3, product: "Peach Pie", price: 5.5},
];`

- Adding to an array
  `
[...shoppingCart, {id: 4, product: "Coffee", price: 6}];`

- Removing an element
  `
shoppingCart.filter((item) => item.id !== 2)`

- Updating all elements in an array
  `shoppingCart.map((item) => {
    return {
        ...item,
        product: item.product.toLowerCase(),
    };
});`

- Modifying a particular element in an array
  `shoppingCart.map((item) => {
if (item.id === 3) {
    return {...item, price: 10.99};
} else {
    return item;
}
});`

---

### _Componenent Design_ (Do this section again sometime)

---

## _React Forms_

- HTML form elements work differently than other DOM elements in React.
  - Form elements naturally keep some internal state

### Controlled Components

`<form>
Full Name:
<input name="fullname" />
<button>Add!</button>

</form>`

- It's convenient to have a JS function that
  - Handles the submission of the form _and_
  - has access to the data the user entered.
- The technique to get this is _controlled components_

### Accessibility: Labeling Inputs

Good accessibility practice puts _<label>_ elements in forms:

`<form>
<label htmlFor="fullname-input">Full Name:</label>
<input id="fullname-input" name="fullname" />
<button>Add!</button>

</form>`

### Handling Multiple Inputs

To handle multiple controlled inputs:

- Instead of making a seperate _onChange_ handler for every single input,we can make one generic function for multiple inputs
- Add HTML _name_ attribute to each JSX input element
- Then the handler function can determine the key in state to update based on _event.target.name_

`const [formData, setFormData] = useState({
firstName = "",
lastName = ""
});

function handleChange(event) {
const fieldName = event.target.name;
const value = event.target.value;

setFormData(currentData => {
currentData[fieldName] = value;
return {...currentData};
});
}`

Using this method, keys in state must match input _name_ attributes

### useEffect()

- To use an effect, register it with _useEffect(fn)_:

  - Common to inline these:
    `import React, { useEffect } from 'react';

  function MyComponent() {
  useEffect(function myEffect() {
  // ...Do something
  });
  // ...Rest of component
  }`

  - My effect always runs _after_ first render
  - By default, my effect runs _after_ all re-renders

#### 2nd argument to useEffect

- useEffect(myCallbackFn);
  - Runs _myCallbackFn_ effect after _every_ render
- useEffect(myCallbackFn, [productId, userId])
  - Runs _myCallbackFn_ effect only if _productId_ or _userId_ const changed
- useEffect(myCallbackFn, [ ])
  - Runs _myCallbackFn_ effect only the first time (on _mount_)
