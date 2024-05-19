
# Software Engineering - 2024 Lab 2

## To-Do App with React

## Set Up Your React Project

### Install Node.js
Make sure you have Node.js installed. You can download it from [Node.js official website](https://nodejs.org/).

### Create a React App
Open your terminal and run:
```bash
npx create-react-app todo-app
cd todo-app
```

## Project Structure

- `node_modules/`: contains all your project's dependencies.
- `public/`: static files like `index.html` where your React app is injected.
- `src/`: your React components and code.

## Start Project
Start the development server:
```bash
npm start
```
This will open your new React app in the browser at [http://localhost:3000](http://localhost:3000).


### Remove unnecessary files

* Delete everything in `src` except `index.js` and `App.js`.
* Remove Unnecessary imports from Index.js (like index.css and reportwebVitols) 
* Modify `App.js` to a simple functional component:

```jsx
import React from 'react';

const App = () => {
  return (
    <div>
      <h1>To-Do App</h1>
    </div>
  );
}

export default App;
```

### Create Components
Create components: `TodoList`, `TodoItem`, and `TodoForm`.

#### TodoList Component
`src/components/TodoList.js`
```jsx
import React from 'react';
import TodoItem from './TodoItem';

const TodoList = ({ todos, toggleComplete, deleteTodo }) => {
  return (
    <ul>
      {todos.map(todo => (
        <TodoItem 
          key={todo.id} 
          todo={todo} 
          toggleComplete={toggleComplete}
          deleteTodo={deleteTodo}
        />
      ))}
    </ul>
  );
}

export default TodoList;
```

#### TodoItem Component
`src/components/TodoItem.js`
```jsx
import React from 'react';

const TodoItem = ({ todo, toggleComplete, deleteTodo }) => {
  return (
    <li style={{ textDecoration: todo.completed ? 'line-through' : 'none' }}>
      <span onClick={() => toggleComplete(todo.id)}>{todo.text}</span>
      <button onClick={() => deleteTodo(todo.id)}>Delete</button>
    </li>
  );
}

export default TodoItem;
```

#### TodoForm Component
`src/components/TodoForm.js`
```jsx
import React, { useState } from 'react';

const TodoForm = ({ addTodo }) => {
  const [inputValue, setInputValue] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    addTodo(inputValue);
    setInputValue('');
  }

  return (
    <form onSubmit={handleSubmit}>
      <input 
        type="text" 
        value={inputValue} 
        onChange={(e) => setInputValue(e.target.value)}
      />
      <button type="submit">Add</button>
    </form>
  );
}

export default TodoForm;
```

### Update `App.js` to use new added components
`src/App.js`
```jsx
import React, { useState } from 'react';
import TodoList from './components/TodoList';
import TodoForm from './components/TodoForm';

const App = () => {
  const [todos, setTodos] = useState([]);

  const addTodo = text => {
    const newTodo = { id: Date.now(), text, completed: false };
    setTodos([ ...todos, newTodo ]);
  };

  const toggleComplete = id => {
    setTodos(todos.map(todo =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    ));
  };

  const deleteTodo = id => {
    setTodos(todos.filter(todo => todo.id !== id));
  };

  return (
    <div>
      <h1>To-Do App</h1>
      <TodoForm addTodo={addTodo} />
      <TodoList 
        todos={todos} 
        toggleComplete={toggleComplete} 
        deleteTodo={deleteTodo} 
      />
    </div>
  );
}

export default App;
```

Build for Production
To build your app for production, run:
```bash
npm run build
```
This creates an optimized build of your app in the `build` folder, ready for deployment.

Follow [Deploy React App](https://create-react-app.dev/docs/deployment/) for more

_Note : if build file does not run on local server try putting `"homepage": ".",` on **package.json** file_


