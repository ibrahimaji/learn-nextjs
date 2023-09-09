# Components


UI can be broken down into smaller building blocks called components.
![UI Components](https://nextjs.org/static/images/learn/foundations/components.png)

## Creating Components

```
<script type="text/jsx">

  const app = document.getElementById("app")

  function Header() {
     return (<h1>Develop. Preview. Ship. 🚀</h1>)
   }


   ReactDOM.render(<Header />, app)
</script>
```
1. A component is a function that returns UI elements. Inside return, you can write JSX.
2. React Components should be capitalized.
3. To use React Components, use angle brackets `<Header />`.

## Nesting Components

```
function Header() {
  return <h1>Develop. Preview. Ship. 🚀</h1>;
}

function HomePage() {
  return (
    <div>
      {/* Nesting the Header component */}
      <Header />
    </div>
  );
}

ReactDOM.render(<HomePage/>, app);
```
![Component Trees](https://nextjs.org/static/images/learn/foundations/component-tree.png)
