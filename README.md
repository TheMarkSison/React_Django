# Welcome to the React, Django and Vite Tutorial.

Please carefully follow the steps below to create a minimal application using React & Vite for the frontend and Django for the backend.

## Prerequisites.

* `NodeJS`

  * Currently using LTS Version `20.14.0` at time of writing.
 
### Step 1 - Installing Vite and Creating a React application.

Install `create-vite` globally using `npm` which is the Vite version of `create-react-app`.

```bash
npm install -g create-vite
```

Create your new React application using `create-vite`.

```bash
npm create vite@latest
```

Follow the instructions on creating the project. In this example we are using React and Vanilla JavaScript and simply call the project `frontend`.

```bash
✔ Project name: … frontend
✔ Select a framework: › React
✔ Select a variant: › JavaScript
```

Once the project has been created, follow the instructions to start your development server.

```bash
cd frontend
npm install
npm run dev
```

Visit `http://localhost:5173` to see check if the React app is now working.

We can also start installing other `npm` packages we want here. For this example, we also want:

* `axios`
  * A HTTP client for sending requests to the backend.

* `react-router-dom`
  * A Routing library for React.

```bash
npm install axios react-router-dom
```

### Step 2 - Updating our React application.

Within our new React application, we create a new React component called `Home.jsx`.

```
frontend/
|
+---src/
    |
    +---App.jsx
    +---...
    +---Home.jsx
```

Then we can add the follow code:

```jsx
import React, { useState, useEffect } from 'react';
import { useNavigate } from "react-router-dom";
import axios from 'axios';

const Home = () => {
  const [message, setMessage] = useState('');
  const navigate = useNavigate();

  const goToContact = () => {
      navigate('/contact');
  }

  useEffect(() => {
    axios.get('http://localhost:8000/api')
      .then(response => {
        setMessage(response.data.message);
      })
      .catch(error => {
        console.log(error);
      });
  }, []);

  return (
      <>
          <h1>Welcome to Vite & React & Django.</h1>
          <p>{message}</p>
          <button onClick={goToContact}>Contact Us.</button>
      </>
  );
}

export default Home;
```

Do not worry about the request to `http://localhost:8000/api`, we will build that using Django in the next section.

Let's create a second React component called `Contact.jsx` to test our routing.

```
frontend/
|
+---src/
    |
    +---App.jsx
    +---...
    +---Home.jsx
    +---Contact.jsx
```


```jsx
import React, {useEffect, useState} from 'react';
import axios from "axios";
const Contact = () => {
    const [user, setUser] = useState('');

    useEffect(() => {
    axios.get('http://localhost:8000/api/contact/')
      .then(response => {
        setUser(response.data.user);
      })
      .catch(error => {
        console.log(error);
      });
    }, []);

    return (
        <>
            <h1>Contact Us.</h1>
            <ul>
                <li>{user}.</li>
            </ul>
        </>
    )
}

export default Contact;
```

Again, let's not worry about the request to `http://localhost:8000/api/contact/`.

Finally, let's update our `App.js` to render our new components.

```jsx
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Home from './Home';
import Contact from './Contact';

function App() {
  return (
    <div>
      <Router>
          <Routes>
              <Route path="/" element={<Home />}></Route>
              <Route path="/contact" element={<Contact />}></Route>
          </Routes>
      </Router>
    </div>
  );
}

export default App;
```
