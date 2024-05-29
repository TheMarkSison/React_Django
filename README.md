# Welcome to the React, Django and Vite Tutorial.

Please carefully follow the steps below to create a minimal application using React & Vite for the frontend and Django for the backend.

## Prerequisites.

* `NodeJS`
  * Currently using LTS Version `20.14.0` at time of writing.
 
### Step 1 - Installing Vite.

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

We can also start installing other `npm` packages we want here. For this example, we also want:

* `axios`
  * A HTTP client for sending requests to the backend.

* `react-router-dom`
  * A Routing library for React.
