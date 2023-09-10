NextJS is component-based like Lego.

## Setup

1. To create NextJS App, use `npx create-next-app@latest`. Choose **No** on **Typescript, ESLint, and import alias** choice.
2. Inside `src/app`, there are multiple files. Delete `page.js` and `global.css`. Notes: `layout.js` and `page.js` is naming convention on NextJS, don't use another name!.
3. `layout.js` used to layouting the page and `page.js` used to fill the content on the layout.
4. Inside `layout.js` , there are `RootLayout` and `Layout`. `RootLayout` is like `index.html` which define the layout of the root. Remove `import "./global.css"`.

## Routing

NextJS use file-based routing.
1. Inside `src/app`, create a folder called `about` and create a file called `page.js` inside it.
2. Inside `page.js`, type the code :
```
export default function Page(){ //page must use export default and the first letter of function name should uppercase
  return <div>Hei ini adalah page about!</div>;
}
```
3. Open it using `npm run dev` and set to `/about`.

## Component

1. Create `components` folder inside `src`.
2. Inside it, create `CardName.jsx`. Components should use `.jsx` filename. 
3. Create a function
```
export const CardName = () => {
  return <div className = "p-8 rounded-xl bg-sky-300">Name : </div>;
}
```
4. Inside `src/app/about/page.js`, import the component.
```
import {CardName} from "@/components/CardName";

export default function Page(){
  return (
    <div>
      <p>Hei ini adalah page about!</div>;
      <CardName />
    </div>
  );
}
```

## Props

Props is a shorthand of properties.
1. Inside `CardName.jsx` 
```
export const CardName = ({name}) => { //destructuring
  return <div className = "p-8 rounded-xl bg-sky-300">Name : {name} </div>;
}
```
2. Inside `page.js`, we can use `<CardName name="Adam" />`.

## Children

Children same with Props and used in Components with children inside it.

```
//CardName.jsx
export const CardName = ({children}) => { 
return <div className = "p-8 rounded-xl bg-sky-300">{children}</div>;
}

```
//page.js
...
return (
  <div>
    <CardName>
      <div>test</div>
      <div>test</div>
    </CardName>
    <CardName>Ana</CardName>
)
...

```

## Conditional Rendering




## Keypoint from presentation
1. Page use name function and Component use arrow function
2. NextJS will automatically convert `js` file inside `src/app` into `jsx`.
3. Use `className` instead of `class`.
4. `return` can only used for one component which wrapped using a div.
5. Set the folder on tailwind config to ` ./src/**/*.{js,ts,jsx,tsx,mdx}`.
6. Create a file on `/src/styles/globals.css`, and insert the tailwind base config.
7. Import `globals.css` to `layout.js` using `import "@/styles/globals.css"`.
