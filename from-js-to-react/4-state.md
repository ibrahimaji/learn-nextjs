# State

Code below is how React works for event handling.

```
function HomePage() {
  const names = ['Ada Lovelace', 'Grace Hopper', 'Margaret Hamilton'];
  function handleClick(){
    console.log("increment like count");
  }

  return (
    <div>
      <Header title="Develop. Preview. Ship. 🚀" />
      <ul>
        {names.map((name) => (
          <li key={name}>{name}</li>
        ))}
      </ul>

      <button onClick={handleClick}>Like</button> //listening to event and event handling
    </div>
  );
}
```
React has a set of functions called Hooks. Hooks allow you to add additional logic such as state to your components. You can think of state as any information in your UI that changes over time, usually triggered by user interaction.
To store and increment the number of times a user has clicked the like button, we can use **use state**. This is what the React hook to manage state is called, `useState()`.
```
function HomePage(){
  const [likes, setLikes] = React.useState(0);
}
```
1. `useState()` returns an array, so to access and use that array we can use **array destructuring**.
2. The first item in array is the state **value**, we can name it anything.
3. The second item in array is a function to **update** the value. The best practice is use **set** followed by the name of the state variable.
4. **0** is initial values of **likes**.

We can use the state value inside component and to update the state, we can define a function.

```
function HomePage() {
  // ...
  const [likes, setLikes] = React.useState(0);

  function handleClick() {
    setLikes(likes + 1);
  }

  return (
    <div>
      {/* ... */}
      <button onClick={handleClick}>Likes ({likes})</button>
    </div>
  );
}
```
