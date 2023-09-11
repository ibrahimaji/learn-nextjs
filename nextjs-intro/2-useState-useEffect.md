# Server vs Client Component, useState, useEffect

## Server vs Client Component

1. NextJS always has Server Component and Client Component.
2. Server Component will rendered in Server and delivered to user as a rendered document (HTML page).
3. In Client Component, the code will downloaded to browser and rendered directly inside browser.

## Hooks

Hooks is a built-in function that help to do certain action.

### useState

`useState` is a hook for set and derive component state.

```
import { useState } from "react"

const Component = () => {
  const [state, setState] = useState("Initial Value");
  
  return <div></div>
}
```
![useState](https://media.graphassets.com/QvKtGhSzSXe8a0851syB)

Component will be re-rendered when props or state changed.

1. Create new NextJS Project.
2. The default folder structure is
- public
- src
  - app
    - favicon.ico
    - layout.js
    - page.js
  - components
    - Card.jsx
  - styles
    - globals.css
3. Anything inside `app` folder will used as Server Component. Out of `app` folder will be Server or Client Component.
4. Create `Card.jsx` inside `components`.

```
export const Card = () => {
  return <div>Card</div>
}
```

5. Import into `page.js`

```
import { Card } from "@components/Card";

export default function Page(){
  return <div>Hey!</div>;
}
```

6. Create `Hooks` inside `Card.jsx`.

```
"use client"
export const Card = () => {
  const [state,useState] = useState(0);

  const addToState = () => {
    setState(state+1);
  }
  return (
    <div>
      <div>Number = {state}</div>
      <button onClick={addToState}>Add 1</button>
    </div>
}
```

As `Card.jsx` is inside `app` folder, it uses Service Component so we should change it to `"use client"`. The code above will add 1 everytime we click the button.

7. Now we create event listener so when we type, it will displayed automatically.

```
//Card.jsx

"use client"

import { useState } from "react";

export const Card = () => {
    const [state, setState] = useState(0);
    const [name, setName] = useState("");

    const changeName = (e) => {
        setName(e.target.value);
    };

    return (
        <div>
            <div>Name: {name}</div>
            <input onChange={changeName} className="border-2 p-2" />
        </div>
    );
}
```

```
//pages.js

import { Card } from "@/components/Card"

export default function Page(){
  return (
    <div>
      <Card />
      <Card />
      <Card />
    </div>
  )
}
```

There is no logic inside return.

## Create Login Component

1. Create `src/components/Auth/`. Inside `Auth` create 3 folders `components, libs, template`.
2. Inside components create `Login.jsx`

```

export const Login = () => {
    return (
        <div>
            <h2>Login</h2>
            <p>Login to your account</p>
            <div>
                <input placeholder="email@something.com" type="email" />
                <input placeholder="password" type="password" />
            </div>
        </div>
    )
}
```
3. Create `src/app/login/page.js`

```
import { Login } from "@/components/Auth/components/Login"

export default function Page(){
  return (
    <div>
      <Login />
    </div>
  )
}
```

4. Style the `input` in `globals.css`

```
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base{
    h2{
        @apply text-xl font-medium;
    }
    input{
        @apply border-2 p-2 rounded-lg w-full focus:outline-none focus:border-indigo-500
    }
}
```

5. Create new component `src/app/components/Auth/template/AuthTemplate.jsx`.

```
export const AuthTemplate = ({children}) => {
    return <main className="h-screen flex justify-center items-center">{children}</main>
}
```

6. Create new folder `src/app/login/layout.js` 

```
import { AuthTemplate } from "@/components/Auth/template/AuthTemplate";

export default function Layout({children}){
    return <AuthTemplate>{children}</AuthTemplate>
}
```
Any files inside same folder with `layout.js` will be `children`.

7. Add div to `AuthTemplate.jsx`

```
export const AuthTemplate = ({ children }) => {
  return (
    <main className="h-screen flex justify-center items-center">
      <div className="w-[320px">{children}</div>
    </main>
  );
};

```
## Keypoint from presentation

1. Folder structure using `Domain Design Driven (DDD)` which each folder have specific utility. 
