# Lab Record

---

# Program 9: ReactJS – Hooks and Sharing Data Between Components

## 9a. Importance of Hooks

### Aim
To write a React program that shows the importance of Hooks by building a counter first as a **class component** (without hooks) and then as a **functional component** (with the `useState` hook).

### Description
Hooks are special functions in React that let functional components use state and other React features without writing classes.

| Hook | Purpose |
|---|---|
| `useState()` | Manages local state |
| `useEffect()` | Handles side effects (e.g., fetching data) |
| `useContext()` | Accesses global/shared state |
| `useReducer()`, `useRef()` | Complex state logic, DOM references |

**Why hooks are important:**
- Less code than class components (no constructor, no `this`)
- Logic is easier to read and reuse
- State can be used directly inside functional components

### Procedure
1. Create a new React app and start it:
```bash
npx create-react-app react-hooks-demo
cd react-hooks-demo
npm start
```
The app runs at `http://localhost:3000`.

2. Create `src/CounterClass.js` (without hooks).
3. Create `src/CounterHook.js` (with hooks).
4. Update `src/App.js` to display both components.

### Program

**src/CounterClass.js** (without hooks)
```jsx
import React, { Component } from "react";

class CounterClass extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <h2>Class Component</h2>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increase</button>
      </div>
    );
  }
}
export default CounterClass;
```

**src/CounterHook.js** (with hooks)
```jsx
import React, { useState } from "react";

function CounterHook() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Functional Component with Hook</h2>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
export default CounterHook;
```

**src/App.js**
```jsx
import React from "react";
import CounterClass from "./CounterClass";
import CounterHook from "./CounterHook";

function App() {
  return (
    <div>
      <h1>React Hooks Example</h1>
      <CounterClass />
      <CounterHook />
    </div>
  );
}
export default App;
```

### Output

**Initial screen**
```
React Hooks Example

Class Component
Count: 0
[ Increase ]

Functional Component with Hook
Count: 0
[ Increase ]
```

**After clicking "Increase" once in each section**
```
Class Component                  Functional Component with Hook
Count: 1                         Count: 1
```
The count increases by 1 on every click in both components.

### Result
Both components produce the same output, but the hook version needs much less code. The program was executed successfully.

---

## 9b. Sharing Data Between Components

### Aim
To create a React application that demonstrates data sharing between components using props, callback functions and lifted state.

### Description
React follows **unidirectional data flow** (parent → child). When two child components need to share data, the common parent component holds the shared state. This technique is called **Lifting State Up**.

| Direction | Technique |
|---|---|
| Parent → Child | Props |
| Child → Parent | Callback functions |
| Sibling → Sibling | Shared state in the parent |

In this program, **ChildA** sends a message to the **Parent** through a callback function, and the Parent passes it to **ChildB** through props.

### Procedure
1. Create a new React app and start it:
```bash
npx create-react-app share-data-demo
cd share-data-demo
npm start
```
2. Create three components inside `src/`: `ParentComponent.js`, `ChildA.js`, `ChildB.js`.
3. Update `App.js` to include the parent component.
4. Run the app with `npm start`. (If you created the project with Vite, use `npm run dev` instead.)

### Program

**src/ParentComponent.js** (holds the shared data)
```jsx
import React, { useState } from "react";
import ChildA from "./ChildA";
import ChildB from "./ChildB";

function ParentComponent() {
  const [message, setMessage] = useState("Hello from Parent!");

  const updateMessage = (newMsg) => {
    setMessage(newMsg);
  };

  return (
    <div style={{ border: "2px solid blue", padding: "10px", margin: "10px" }}>
      <h2>Parent Component</h2>
      <p>Shared Message: {message}</p>
      <ChildA onUpdate={updateMessage} />
      <ChildB message={message} />
    </div>
  );
}
export default ParentComponent;
```

**src/ChildA.js** (sends data to parent)
```jsx
import React, { useState } from "react";

function ChildA({ onUpdate }) {
  const [inputValue, setInputValue] = useState("");

  return (
    <div style={{ border: "2px solid green", padding: "10px", margin: "10px" }}>
      <h3>Child A (Sender)</h3>
      <input
        type="text"
        placeholder="Type message for Child B"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
      />
      <button onClick={() => onUpdate(inputValue)}>Send</button>
    </div>
  );
}
export default ChildA;
```

**src/ChildB.js** (receives data from parent)
```jsx
import React from "react";

function ChildB({ message }) {
  return (
    <div style={{ border: "2px solid red", padding: "10px", margin: "10px" }}>
      <h3>Child B (Receiver)</h3>
      <p>Received Message: {message}</p>
    </div>
  );
}
export default ChildB;
```

**src/App.js** (main file)
```jsx
import React from "react";
import ParentComponent from "./ParentComponent";

function App() {
  return (
    <div>
      <h1>React – Sharing Data Between Components</h1>
      <ParentComponent />
    </div>
  );
}
export default App;
```

### Output

**Initial screen**
```
React – Sharing Data Between Components

Parent Component
Shared Message: Hello from Parent!

  Child A (Sender)
  [ Type message for Child B ]  [ Send ]

  Child B (Receiver)
  Received Message: Hello from Parent!
```

**After typing "Welcome to React" in Child A and clicking Send**
```
Parent Component
Shared Message: Welcome to React

  Child A (Sender)
  [ Welcome to React ]  [ Send ]

  Child B (Receiver)
  Received Message: Welcome to React
```

### Result
Data was shared successfully: Child A sent the message to the Parent through a callback, and the Parent passed it to Child B through props.

---

# Program 11: MongoDB – Databases, Collections and Records

## 11a. Create and Drop Databases and Collections

### Aim
To write MongoDB queries to create and drop databases and collections.

### Description
MongoDB is a NoSQL database that stores data as documents inside collections. A database is created when you switch to it and insert data into it. Collections can be created explicitly with `createCollection()` and removed with `drop()`. A whole database is removed with `dropDatabase()`.

### Queries and Output

**1. Create a database**
```js
use myDatabase
```
Output:
```
switched to db myDatabase
```

**2. Create a collection**
```js
db.createCollection("myCollection")
```
Output:
```
{ ok: 1 }
```

**3. Drop a collection**
```js
db.myCollection.drop()
```
Output:
```
true
```

**4. Drop a database**
```js
db.dropDatabase()
```
Output:
```
{ ok: 1, dropped: 'myDatabase' }
```

### Result
The database and collection were created and dropped successfully.

---

## 11b. Working with Records: find(), limit(), sort(), createIndex(), aggregate()

### Aim
To write MongoDB queries to work with records using `find()`, `limit()`, `sort()`, `createIndex()` and `aggregate()`.

### Description

| Method | Purpose |
|---|---|
| `find()` | Retrieves documents from a collection |
| `sort()` | Arranges documents by one or more fields (`1` = ascending, `-1` = descending) |
| `createIndex()` | Creates an index to speed up searching and retrieval |
| `aggregate()` | Processes data through a pipeline and returns computed results (sum, avg, count, min, max) |
| `limit()` | Restricts the number of documents returned |

### Insert sample data
```js
db.EX7.insertMany([
  { name: "Alice",   age: 25, status: "A" },
  { name: "Bob",     age: 30, status: "B" },
  { name: "Charlie", age: 35, status: "A" },
  { name: "David",   age: 40, status: "B" },
  { name: "Eve",     age: 45, status: "A" },
  { name: "Frank",   age: 50, status: "B" },
  { name: "Grace",   age: 55, status: "A" },
  { name: "Hank",    age: 60, status: "B" },
  { name: "Irene",   age: 65, status: "A" },
  { name: "Jack",    age: 70, status: "B" }
])
```
Output:
```
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('...'),
    '1': ObjectId('...'),
    ...
    '9': ObjectId('...')
  }
}
```

### 1. find()
**Syntax:** `db.collection.find(query)`

Query:
```js
db.EX7.find({ status: "A" })
```
Output:
```
{ name: 'Alice',   age: 25, status: 'A' }
{ name: 'Charlie', age: 35, status: 'A' }
{ name: 'Eve',     age: 45, status: 'A' }
{ name: 'Grace',   age: 55, status: 'A' }
{ name: 'Irene',   age: 65, status: 'A' }
```

### 2. sort()
**Syntax:** `db.collection.find().sort({ field: 1 })`
- `1` → ascending order (smallest to largest, A–Z)
- `-1` → descending order (largest to smallest, Z–A)

Query:
```js
db.EX7.find().sort({ age: 1 })
```
Output:
```
{ name: 'Alice',   age: 25, status: 'A' }
{ name: 'Bob',     age: 30, status: 'B' }
{ name: 'Charlie', age: 35, status: 'A' }
{ name: 'David',   age: 40, status: 'B' }
{ name: 'Eve',     age: 45, status: 'A' }
{ name: 'Frank',   age: 50, status: 'B' }
{ name: 'Grace',   age: 55, status: 'A' }
{ name: 'Hank',    age: 60, status: 'B' }
{ name: 'Irene',   age: 65, status: 'A' }
{ name: 'Jack',    age: 70, status: 'B' }
```

### 3. createIndex()
Indexing improves the speed of searching and retrieving documents. An index stores the values of a specific field in an organized structure, so MongoDB can find matching records without scanning the entire collection.

**Syntax:** `db.collection.createIndex({ field: 1 })`
- `1` → ascending index
- `-1` → descending index

Query:
```js
db.EX7.createIndex({ age: 1 })
```
Output:
```
age_1
```

To verify the index:
```js
db.EX7.getIndexes()
```
Output:
```
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { age: 1 }, name: 'age_1' }
]
```

### 4. aggregate()
Aggregation processes data from multiple documents and returns computed results. It can group documents by a field and perform operations such as sum, average, count, minimum and maximum.

**Syntax:**
```js
db.collection.aggregate([
  { $stage1: { ... } },
  { $stage2: { ... } }
])
```

Query:
```js
db.EX7.aggregate([
  {
    $group: {
      _id: "$status",
      averageAge: { $avg: "$age" },
      count: { $sum: 1 }
    }
  }
])
```
Output:
```
{ _id: 'A', averageAge: 45, count: 5 }
{ _id: 'B', averageAge: 50, count: 5 }
```

### 5. limit()
The `limit()` method restricts the number of documents returned by a query.

**Syntax:** `db.collection.find().limit(number)`

Query:
```js
db.EX7.find().limit(3)
```
Output:
```
[
  {
    _id: ObjectId('64f24c5e9a2b3f001e3a0001'),
    name: 'Alice',
    age: 25,
    status: 'A'
  },
  {
    _id: ObjectId('64f24c5e9a2b3f001e3a0002'),
    name: 'Bob',
    age: 30,
    status: 'B'
  },
  {
    _id: ObjectId('64f24c5e9a2b3f001e3a0003'),
    name: 'Charlie',
    age: 35,
    status: 'A'
  }
]
```

### Result
The MongoDB queries using `find()`, `sort()`, `createIndex()`, `aggregate()` and `limit()` were executed successfully and the expected output was obtained.
