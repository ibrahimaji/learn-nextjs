# Props

Props used to pass pieces of information as properties to React components.

## Using Props

```
function Header({title}) { //props is an object, so it can use object destructuring
  console.log(title); // "React"
  return <h1>title</h1>; // the output will be just title as it rendering a plain text instead of DOM
}

function HomePage() {
  return (
    <div>
      {/* Nesting the Header component */}
      <Header title="React"/> // passing a custom title props
    </div>
  );
}

ReactDOM.render(<HomePage/>, app);
```
## Using Variables in JSX

Use curly braces `return <h1>{title}</h1>;` to add any **JavaScript expression**.

Example:
1. An **object property**
```
function Header(props) {
  return <h1>{props.title}</h1>;
}
```
2. A *template literal*
```
function Header({ title }) {
  return <h1>{`Cool ${title}`}</h1>;
}
```
3. The **returned value of a function**
```
function createTitle(title) {
  if (title) {
    return title;
  } else {
    return 'Default title';
  }
}

function Header({ title }) {
  return <h1>{createTitle(title)}</h1>;
}
```
4. **Ternary Operators**
```
function Header({ title }) {
  return <h1>{title ? title : 'Default Title'}</h1>;
}
```
## Iterating through lists

Use **array.map**

```
function HomePage() {
  const names = ['Ada Lovelace', 'Grace Hopper', 'Margaret Hamilton'];

  return (
    <div>
      <Header title="Develop. Preview. Ship. 🚀" />
      <ul>
        {names.map((name) => (
          <li>{name}</li>
        ))}
      </ul>
    </div>
  );
}
```
When running the code, it will run the error as React needs something to uniquely identify items in array so it knows which elements to update in the DOM, such as **item ID**.

```
function HomePage() {
  const names = ['Ada Lovelace', 'Grace Hopper', 'Margaret Hamilton'];

  return (
    <div>
      <Header title="Develop. Preview. Ship. 🚀" />
      <ul>
        {names.map((name) => (
          <li key={name}>{name}</li>
        ))}
      </ul>
    </div>
  );
}
```
