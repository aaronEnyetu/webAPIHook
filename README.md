# Alchemy React Base Template

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

Use this template for all your "from scratch" deliverables. To start, simply run

- `npm install`
- `npm start`

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

## The Golden Rule:

🦸 🦸‍♂️ `Stop starting and start finishing.` 🏁

If you work on more than one feature at a time, you are guaranteed to multiply your bugs and your anxiety.

## Making a plan in React

1. Make a drawing of your app. Simple "wireframes"
1. Component Tree
   1. Look at the drawing and break it down into Components. Label these Components explicitly (i.e., DogList, etc)
   1. Draw a hierarchy (or tree) of components, describing which components are parents and which are children
   1. Looking at the drawing, make a list of your app's features. What should a user "be able to do" with this app?
   1. Now look at your component tree: which components "go with" which features? Draw lines and make these connections explicitly.
1. State
   1. Look back at the drawing and your list of features and imagine using the app. What _state_ do you need to track?
   1. For each piece of state, ask: "When does it change?" If the answer is, "never", then it is not state.
   1. Similarly, find all the 'events' (user clicks, form submit, on load etc) in your app. Ask one by one, "What state changes?" for each of these events. (This should feel like the the inverse of the previous step.)
   1. Think about how to validate each of your state changes. How will I know if state changed in response to this event? (Hint: react dev tools or console.log usually helps here.)
1. Data flow
   1. Look at your hierarchy and ask: which components need access to which state? Another way to ask this is: for each component, what does this component need to "do its job?". This list becomes the "props" of the component.
   1. If a child needs state from a parent, you will need to pass props. What will you name these props?
   1. Notice especially if two siblings need the same state: if so, you need a callback (i.e., debit card).
1. Pick one feature from your list and build it out. Start with its parentmost component, and work down the component chain. Do not build another feature until this one is finished (and you can prove that it is finished by validating state change).

## Additional considerations

- Is any of your state redundant? For example, if you're tracking `wins`, `losses`, and `total`, you can probably get rid of `losses` state, and calculate it as `total - wins`.
- Where should each piece of state live? How are you going to get data from where it lives to where it needs to be?

## Step 1

---

create a local REST API using JSON server, which you will use as a test data source. Later, you’ll build an application to display a grocery list and to add items to the list. JSON server will be your local API and will give you a live URL to make GET and POST requests. With a local API, you have the opportunity to prototype and test components while you or another team develops live APIs.

By the end of this step, you’ll be able to create local mock APIs that you can connect to with your React applications.

On many agile teams, front-end and API teams work on a problem in parallel. In order to develop a front-end application while a remote API is still in development, you can create a local version that you can use while waiting for a complete remote API.

There are many ways to make a mock local API. You can create a simple server using Node or another language, but the quickest way is to use the JSON server Node package. This project creates a local REST API from a JSON file.

## To begin, install json-server:

`npm install --save-dev json-server`
json-server creates an API based on a JavaScript object. The keys are the URL paths and the values are returned as a response. You store the JavaScript object locally and commit it to your source control.

## Open a file called db.json in the root of your application. This will be the JSON that stores the information you request from the API:

`nano db.json`
Add an object with the key of list and an array of values with an id and a key of item. This will list the item for the grocery list. The key list will eventually give you a URL with an endpoint of /list:
`{ "list": [ { "id": 1, "item": "bread" }, { "id": 2, "item": "grapes" } ] }`
In this snippet, you have hard-coded bread and grapes as a starting point for your grocery list.

Save and close the file. To run the API server, you will use json-server from the command line with an argument point to the API configuration file. Add it as a script in your package.json.

## Open package.json:

`nano package.json`

## Then add a script to run the API. In addition, add a delay property. This will throttle the response, creating a delay between your API request and the API response. This will give you some insights into how the application will behave when waiting for a server response. Add a delay of 1500 milliseconds. Finally, run the API on port 3333 using the -p option so it won’t conflict with the create-react-app run script:

{
"name": "do-14-api",
"version": "0.1.0",
"private": true,
"dependencies": {
"@testing-library/jest-dom": "^4.2.4",
"@testing-library/react": "^9.3.2",
"@testing-library/user-event": "^7.1.2",
"react": "^16.13.1",
"react-dom": "^16.13.1",
"react-scripts": "3.4.3"
},
"scripts": {
`"api": "json-server db.json -p 3333 --delay 1500",`
"start": "react-scripts start",
"build": "react-scripts build",
"test": "react-scripts test",
"eject": "react-scripts eject"
},
"eslintConfig": {
"extends": "react-app"
},
"browserslist": {
"production": [
">0.2%",
"not dead",
"not op_mini all"
],
"development": [
"last 1 chrome version",
"last 1 firefox version",
"last 1 safari version"
]
},
"devDependencies": {
"json-server": "^0.16.1"
}
}

## Save and close the file. In a new terminal or tab, start the API server with the following command:

`npm run api`
Output

> json-server db.json -p 3333

\{^\_^}/ hi!

Loading db.json
Done

Resources
http://localhost:3333/list

Home
http://localhost:3333

Type s + enter at any time to create a snapshot of the database

## Open http://localhost:3333/list and you’ll find the live API:

## When you open an endpoint in your browser, you are using the GET method. But json-server is not limited to the GET method. You can perform many other REST methods as well. For example, you can POST new items. In a new terminal window or tab, use curl to POST a new item with a type of application/json:

`curl -d '{"item":"rice"}' -H 'Content-Type: application/json' -X POST http://localhost:3333/list`

## Note that you must stringify the content before you send it. After running the curl command, you’ll receive a success message:

Output
{
"item": "rice",
"id": 3
}

## If you refresh the browser, the new item will appear:

In this step, you created a local API. You learned how to create a static file with default values and how to fetch or update those values using RESTful actions such as GET and POST. In the next step, you’ll create services to fetch data from the API and to display in your application.

## Step 2 — Fetching Data from an API with useEffect

In this step, you’ll fetch a list of groceries using the useEffect Hook. You’ll create a service to consume APIs in separate directories and call that service in your React components. After you call the service, you’ll save the data with the useState Hook and display the results in your component.

By the end of this step, you’ll be able to call web APIs using the Fetch method and the useEffect Hook. You’ll also be able to save and display the results.

Now that you have a working API, you need a service to fetch the data and components to display the information. Start by creating a service. You can fetch data directly inside any React component, but your projects will be easier to browse and update if you keep your data retrieval functions separate from your display components. This will allow you to reuse methods across components, mock in tests, and update URLs when endpoints change.

## Create a directory called services inside the src directory:

`mkdir src/services`

## Then open a file called list.js in your text editor:

`nano src/services/list.js`

You’ll use this file for any actions on the /list endpoint. Add a function to retrieve the data using the fetch function:

api-tutorial/src/services/list

export function getList() {
return fetch('http://localhost:3333/list')
.then(data => data.json())
}

The only goal of this function is to access the data and to convert the response into JSON using the data.json() method. GET is the default action, so you don’t need any other parameters.

In addition to fetch, there are other popular libraries such as Axios that can give you an intuitive interface and will allow you to add default headers or perform other actions on the service. But fetch will work for most requests.

## Save and close the file. Next, open App.css and add some minimal styling:

nano src/components/App/App.css

## Add a class of wrapper with a small amount of padding by replacing the CSS with the following:

api-tutorial/src/components/App/App.css

.wrapper {
padding: 15px;
}

## Save and close the file. Now you need to add in code to retrieve the data and display it in your application.

## Open App.js:

nano src/components/App/App.js

In functional components, you use the useEffect Hook to fetch data when the component loads or some information changes. For more information on the useEffect Hook, check out How To Handle Async Data Loading, Lazy Loading, and Code Splitting with React. You’ll also need to save the results with the useState Hook.

## Import useEffect and useState, then create a variable called list and a setter called setList to hold the data you fetch from the service using the useState Hook:

api-tutorial/src/components/App/App.js

import React, { useEffect, useState } from 'react';
import './App.css';

function App() {
const [list, setList] = useState([]);
return(
<>
</>
)
}

export default App;

Next, import the service, then call the service inside your useEffect Hook. Update the list with setList if the component is mounted. To understand why you should check if the component is mounted before setting the data, see Step 2 — Preventing Errors on Unmounted Components in How To Handle Async Data Loading, Lazy Loading, and Code Splitting with React.

Currently you are only running the effect once when the page loads, so the dependency array will be empty. In the next step, you’ll trigger the effect based on different page actions to ensure that you always have the most up-to-date information.

## Add the following highlighted code:

api-tutorial/src/components/App/App.js

import React, { useEffect, useState } from 'react';
import './App.css';
import { getList } from '../../services/list';

function App() {
const [list, setList] = useState([]);

useEffect(() => {
let mounted = true;
getList()
.then(items => {
if(mounted) {
setList(items)
}
})
return () => mounted = false;
}, [])

return(
<>
</>
)
}

export default App;

## Finally, loop over the items with .map and display them in a list:

api-tutorial/src/components/App/App

import React, { useEffect, useState } from 'react';
import './App.css';
import { getList } from '../../services/list';

function App() {
const [list, setList] = useState([]);

useEffect(() => {
let mounted = true;
getList()
.then(items => {
if(mounted) {
setList(items)
}
})
return () => mounted = false;
}, [])

return(

<div className="wrapper">
<h1>My Grocery List</h1>
<ul>
{list.map(item => <li key={item.item}>{item.item}</li>)}
</ul>

   </div>
  )
}

export default App;

## Save and close the file. When you do, the browser will refresh and you’ll find a list of items:

In this step, you set up a service to retrieve data from an API. You learned how to call the service using the useEffect Hook and how to set the data on the page. You also displayed the data inside your JSX.

In the next step, you’ll submit data to the API using POST and use the response to alert your users that an actions was successful.

## Step 3 — Sending Data to an API

In this step, you’ll send data back to an API using the Fetch API and the POST method. You’ll create a component that will use a web form to send the data with the onSubmit event handler and will display a success message when the action is complete.

By the end of this step, you’ll be able to send information to an API and you’ll be able to alert the user when the request resolves.

## Sending Data to a Service

You have an application that will display a list of grocery items, but it’s not a very useful grocery app unless you can save content as well. You need to create a service that will POST a new item to the API.

Open up src/services/list.js:
`nano src/services/list.js`

Inside the file, add a function that will take an item as an argument and will send the data using the POST method to the API. As before, you can use the Fetch API. This time, you’ll need more information. Add an object of options as the second argument. Include the method—POST—along with headers to set the Content-Type to application/json. Finally, send the new object in the body. Be sure to convert the object to a string using JSON.stringify.

When you receive a response, convert the value to JSON:

export function getList() {
return fetch('http://localhost:3333/list')
.then(data => data.json())
}

export function setItem(item) {
return fetch('http://localhost:3333/list', {
method: 'POST',
headers: {
'Content-Type': 'application/json'
},
body: JSON.stringify({ item })
})
.then(data => data.json())
}

## Save and close the file.

Note: In production applications, you’ll need to add error handling and checking. For example, if you misspelled the endpoint, you’d still receive a 404 response and the data.json() method would return an empty object. To solve the issue, instead of converting the response to JSON, you could check the data.ok property. If it is falsy, you could throw an error and then use the .catch method in your component to display a failure message to the users.

Now that you have created a service, you need to consume the service inside your component.

## Open App.js:

`nano src/components/App/App.js`

Add a form element surrounding an input and a submit button:

import React, { useEffect, useState } from 'react';
import './App.css';
import { getList } from '../../services/list';

function App() {
const [list, setList] = useState([]);

useEffect(() => {
let mounted = true;
getList()
.then(items => {
if(mounted) {
setList(items)
}
})
return () => mounted = false;
}, [])

return(

<div className="wrapper">
<h1>My Grocery List</h1>
<ul>
{list.map(item => <li key={item.item}>{item.item}</li>)}
</ul>
<form>
<label>
<p>New Item</p>
<input type="text" />
</label>
<button type="submit">Submit</button>
</form>
</div>
)
}

export default App;

Be sure to surround the input with a label so that the form is accessible by a screen reader. It’s also a good practice to add a type="submit" to the button so that it’s clear the role is to submit the form.

## Save the file. When you do, the browser will refresh and you’ll find your form.

## Next, convert the input to a controlled component. You’ll need a controlled component so that you can clear the field after the user successfully submits a new list item.

First, create a new state handler to hold and set the input information using the useState Hook:

api-tutorial/src/components/App/App.js

import React, { useEffect, useState } from 'react';
import './App.css';
import { getList } from '../../services/list';

function App() {
const [itemInput, setItemInput] = useState('');
const [list, setList] = useState([]);

useEffect(() => {
let mounted = true;
getList()
.then(items => {
if(mounted) {
setList(items)
}
})
return () => mounted = false;
}, [])

return(

<div className="wrapper">
<h1>My Grocery List</h1>
<ul>
{list.map(item => <li key={item.item}>{item.item}</li>)}
</ul>
<form>
<label>
<p>New Item</p>
<input type="text" onChange={event => setItemInput(event.target.value)} value={itemInput} />
</label>
<button type="submit">Submit</button>
</form>
</div>
)
}

export default App;

After creating the state handlers, set the value of the input to itemInput and update the value by passing the event.target.value to the setItemInput function using the onChange event handler.

Now your users can fill out a form with new list items. Next you will connect the form to your service.

## Create a function called handleSubmit. handleSubmit will take an event as an argument and will call event.preventDefault() to stop the form from refreshing the browser.

Import setItem from the service, then call setItem with the itemInput value inside the handleSubmit function. Connect handleSubmit to the form by passing it to the onSubmit event handler:

api-tutorial/src/components/App/App.js

import React, { useEffect, useState } from 'react';
import './App.css';
import { getList, `setItem` } from '../../services/list';

function App() {
const [itemInput, setItemInput] = useState('');
const [list, setList] = useState([]);

useEffect(() => {
let mounted = true;
getList()
.then(items => {
if(mounted) {
setList(items)
}
})
return () => mounted = false;
}, [])

`const handleSubmit = (e) => { e.preventDefault(); setItem(itemInput) };`

return(

<div className="wrapper">
<h1>My Grocery List</h1>
<ul>
{list.map(item => <li key={item.item}>{item.item}</li>)}
</ul>
<form onSubmit={handleSubmit}>
<label>
<p>New Item</p>
<input type="text" onChange={event => setItemInput(event.target.value)} value={itemInput} />
</label>
<button type="submit">Submit</button>
</form>
</div>
)
}

export default App;

## Save the file. When you do, you’ll be able to submit values. Notice that you’ll receive a successful response in the network tab. But the list doesn’t update and the input doesn’t clear.

## Showing a Success Message

It’s always a good practice to give the user some indication that their action was successful. Otherwise a user may try and resubmit a value multiple times or may think their action failed and will leave the application.

To do this, create a stateful variable and setter function with useState to indicate whether to show a user an alert message. If alert is true, display an <h2> tag with the message Submit Successful.

When the setItem promise resolves, clear the input and set the alert message:

api-tutorial/src/components/App/App.js

import React, { useEffect, useState } from 'react';
import './App.css';
import { getList, setItem } from '../../services/list';

function App() {
const [alert, setAlert] = useState(false);
const [itemInput, setItemInput] = useState('');
const [list, setList] = useState([]);

useEffect(() => {
let mounted = true;
getList()
.then(items => {
if(mounted) {
setList(items)
}
})
return () => mounted = false;
}, [])

const handleSubmit = (e) => {
e.preventDefault();
setItem(itemInput)
.then(() => {
setItemInput('');
setAlert(true);
})
};

return(

<div className="wrapper">
<h1>My Grocery List</h1>
<ul>
{list.map(item => <li key={item.item}>{item.item}</li>)}
</ul>
{alert && <h2> Submit Successful</h2>}
<form onSubmit={handleSubmit}>
<label>
<p>New Item</p>
<input type="text" onChange={event => setItemInput(event.target.value)} value={itemInput} />
</label>
<button type="submit">Submit</button>
</form>
</div>
)
}

export default App;

## Save the file. When you do, the page will refresh and you’ll see a success message after the API request resolves.

There are many other optimizations you can add. For example, you may want to disable form inputs while there is an active request. You can learn more about disabling form elements in How To Build Forms in React.

Now you have alerted a user that the result was successful, but the alert message doesn’t go away and the list doesn’t update. To fix this, start by hiding the alert. In this case, you’d want to hide the information after a brief period, such as one second. You can use the setTimeout function to call setAlert(false), but you’ll need to wrap it in useEffect to ensure that it does not run on every component render.

## Inside of App.js create a new effect and pass the alert to the array of triggers. This will cause the effect to run any time alert changes. Notice that this will run if alert changes from false to true, but it will also run when alert changes from true to false. Since you only want to hide the alert if it is displayed, add a condition inside the effect to only run setTimeout if alert is true:

api-tutorial/src/components/App/App.js

import React, { useEffect, useState } from 'react';
import './App.css';
import { getList, setItem } from '../../services/list';

function App() {
const [alert, setAlert] = useState(false);
const [itemInput, setItemInput] = useState('');
const [list, setList] = useState([]);
...

useEffect(() => {
if(alert) {
setTimeout(() => {
setAlert(false);
}, 1000)
}
}, [alert])

const handleSubmit = (e) => {
e.preventDefault();
setItem(itemInput)
.then(() => {
setItemInput('');
setAlert(true);
})
};

return(

<div className="wrapper">
...
</div>
)
}

export default App;

## Run the setTimeout function after 1000 milliseconds to ensure the user has time to read the change.

## Save the file. Now you have an effect that will run whenever alert changes. If there is an active alert, it will start a timeout function that will close the alert after one second.

## Refreshing Fetched Data

Now you need a way to refresh the stale list of data. To do this, you can add a new trigger to the useEffect Hook to rerun the getList request. To ensure you have the most relevant data, you need a trigger that will update anytime there is a change to the remote data. Fortunately, you can reuse the alert state to trigger another data refresh since you know it will run any time a user updates the data. As before, you have to plan for the fact that the effect will run every time alert changes including when the alert message disappears.

This time, the effect also needs to fetch data when the page loads. Create a conditional that will exit the function before the data fetch if list.length is truthy—indicating you have already fetched the data—and alert is false—indicating you have already refreshed the data. Be sure to add alert and list to the array of triggers:

import React, { useEffect, useState } from 'react';
import './App.css';
import { getList, setItem } from '../../services/list';

function App() {
const [alert, setAlert] = useState(false);
const [itemInput, setItemInput] = useState('');
const [list, setList] = useState([]);

useEffect(() => {
let mounted = true;
if(list.length && !alert) {
return;
}
getList()
.then(items => {
if(mounted) {
setList(items)
}
})
return () => mounted = false;
}, [alert, list])

...

return(
<div className="wrapper">
...
</div>
)
}

export default App;

## Save the file. When you do, the data will refresh after you submit a new item:
