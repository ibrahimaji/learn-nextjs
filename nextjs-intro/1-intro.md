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

```
export const CardName = ({name, age, gender}) => {
    if(gender === "female"){
        return(
            <div className="p-8 rounded-xl bg-pink-300">
                <div>Name: {name}</div>
                <div>Age: {age}</div>
                <div>Gender: {gender}</div>
            </div>
        );
    }
    //default return
    return(
        <div className="p-8 rounded-xl bg-sky-300">
            <div>Name: {name}</div>
            <div>Age: {age}</div>
            <div>Gender: {gender}</div>
        </div>
    );
}
```
Conditional rendering is used to display different render for different value.


## Fetch API using NextJS

1. Delete `CardName.jsx` and `about` folder. Create `page.js` inside `src/app`
2. Inside `page.js` insert the codepage.

```
// Fetch Data in NextJS
async function getData(){
    const res = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await res.json();
    return data;
}

export default async function Page(){
    const data = await getData();
    console.log(data);
    return <div>Page</div>
}
```
3. We should create component to contain the data from API. Create `TaskCard.jsx` inside `components`.

```
export const TaskCard = ({title, completed}) => {
    return (
        <div className="p-4 border-2 rounded-xl">
            <div>{title}</div>
            <div>{completed}</div>
        </div>
    )
}
```
4. Import the component inside `page.js`

```
import { TaskCard } from "@/components/TaskCard";

async function getData(){
    const res = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await res.json();
    return data;
}

export default async function Page(){
    const data = await getData();
    console.log(data);
    return (
        <div>
            <TaskCard title="Notes" completed={true} /> //on boolean, use curly brackets
        </div>
    );
}
```

5. Refactor the component using ternary operator for conditional operator.

```
export const TaskCard = ({title, completed}) => {
    return (
        <div className="p-4 border-2 rounded-xl">
            <div>{title}</div>
            <div>{completed ? "It's Done" : "Don't proscatinate!"}</div>
        </div>
    )
}
```

6. Use `map` to iterate through the data from API. Refactor `page.js` return to

```
    return (
        <div>
            {data.map(({title,completed}) => {
                return <TaskCard title={title} completed={completed} />
            })}
        </div>
    );
```

7. Style and refactor the component.

```
export const TaskCard = ({title, completed}) => {
    return (
        <div className="p-4 border-2 rounded-xl">
            <div>{title}</div>
            <div className={ completed ? "text-xs font-medium bg-rose-300 w-fit p-2 rounded-full" : "text-xs font-medium bg-sky-300 w-fit p-2 rounded-full"}>{completed ? "It's Done" : "Don't proscatinate!"}</div>
        </div>
    )
}
```

## Dynamic Routing

1. Create a folder `src/app/task/[taskId]`
2. Inside `[taskId]` create `page.js`
```
export default function Page({ params }){
    const taskId = params.taskId;
    return <div>Ini dynamic route {taskId}</div>;
}
```
3. Use live server and use `localhost:3000/task/1`
4. Now, we can try to use `href` to target the `id` number.

```
import Link from "next/link";

export const TaskCard = ({href,title, completed}) => {
    return (
        <div className="p-4 border-2 rounded-xl">
            <Link href={href}><div>{title}</div></Link>
            <div className={ completed ? "text-xs font-medium bg-rose-300 w-fit p-2 rounded-full" : "text-xs font-medium bg-sky-300 w-fit p-2 rounded-full"}>{completed ? "It's Done" : "Don't proscatinate!"}</div>
        </div>
    )
}
```
5. On the `page.js`, add `id` to `map` function.

```
            {data.map(({id, title,completed}) => {
                return <TaskCard title={title} completed={completed} href={`/task/$id`} />
            })}
```

From the code above, you can click and route to specific task ID.

6. Now we try to fetch the data from API targetting the id.

```
async function getTaskData(id){
    const res = await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`);
    const data = await res.json();
    return data;
}

async function getUserData(userId){
    const res = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`);
    const data = await res.json();
    return data;
}

export default async function Page({ params }){
    const taskId = params.taskId;
    const taskData = await getTaskData(taskId);
    const userData = await getUserData(taskData.userId);
    console.log(taskData,userData);
    return <div>Ini dynamic route {taskId}</div>;
}
```

7. Refactor the return so it displayed task, status, user, email

```
    return (
    <div>
        <div>Task: {taskData.id}</div>
        <div>Status: {taskData.completed ? "Done" : "Get away from your bed"}</div>
        <div>User : {userData.name}</div>
        <div>Email : {userData.email} </div>
    </div>
    );
```

8. Fetch Digimon API

```
//src/app/page.js
import { TaskCard } from "@/components/TaskCard";

async function getData(){
    const res = await fetch("https://www.digi-api.com/api/v1/digimon");
    const data = await res.json();
    return data;
}

export default async function Page(){
    const {content} = await getData();
    return (
        <div>
            {content.map(({id, name , image}) => {
            return (
                <div>
                    <img src={image} width={200} />
                    <div>{name}</div>
                    </div>
            );
            })}
        </div>
    );
}
```

9. Dynamic Routing from Display Datas of Digimon API to the Detail of the Data. Create `src/app/digimon/[digimonId]/page.js`

```
async function getSingleDigimon(id){
    const res = await fetch(`https://www.digi-api.com/api/v1/digimon/${id}`);
    const data = await res.json();
    return data;
}

export default async function Page({params}) {
    const digimonId = params.digimonId;
    const digimonData = await getSingleDigimon(digimonId);
  return (
    <div>
        <div>{digimonData.name}</div>
        <div>{digimonData.level}</div>
        <div>{digimonData.attribute}</div>
    </div>
  )
}

```

10. After that, we can create a `Link` to the page.

```
import { TaskCard } from "@/components/TaskCard";
import Link from "next/link";

async function getData(){
    const res = await fetch("https://www.digi-api.com/api/v1/digimon");
    const data = await res.json();
    return data;
}

export default async function Page(){
    const {content} = await getData();
    return (
        <div>
            {content.map(({id, name, image})=>{
                return (
                    <Link href={`/digimon/${id}`}>
                        <div>
                            <img src={image} width={200} />
                            <div>{name}</div>
                        </div>
                    </Link>
                )
            })}
        </div>
    );
}
```

## Keypoint from presentation
1. Page use name function and Component use arrow function
2. NextJS will automatically convert `js` file inside `src/app` into `jsx`.
3. Use `className` instead of `class`.
4. `return` can only used for one component which wrapped using a div.
5. Set the folder on tailwind config to ` ./src/**/*.{js,ts,jsx,tsx,mdx}`.
6. Create a file on `/src/styles/globals.css`, and insert the tailwind base config.
7. Import `globals.css` to `layout.js` using `import "@/styles/globals.css"`.
8. Install React Snippet Extension, use `rfc` to automatically create React Function.
9. Square Bracket like `[taskId]` will be automatically used as 
