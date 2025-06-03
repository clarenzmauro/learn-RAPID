react core concepts
- create react app (create-react-app): the officially supported way to create single-page react apps. this sets up the dev env. to use this, use the command:
    - npx create-react-app my-app
        - wherein my-app is your project name; npx is a package runner tool that comes with npm
- JSX (JavaScript XML): syntax extension for JavaScript that looks very similar to HTML. React uses JSX to describe what the UI should look like. Browsers don't undestand JSX directly, so create-react-app includes tools to compile JSX into regular JavaScript.
- Functional Components: the modern way to write react components. they are javascript functions that accept an optional "props" object and return react elements (typically JSX) describing what should appear on the screen.
- Props (properties): how components pass data to each other, from parent to child. props are read only; a component should never modify its own props.
- State (useState hook): data that a component owns and can change over time. when a component's state changes, react re-renders the component.
    - useState hook is a special function that lets you add react state to functional components. it returns a pair: the curretn state value and a function that lets you update it.

setting up node.js and npm
react development requires node.js and npm (node package manager) which is included with node.js

to check the versions, do:
node -v
npm -v

mini-project:
1. create a new react app
2. navigate into your react app and start the dev server
3. explore the project structure
4. create the question display component
5. use questiondisplay component in app.js
6. check your browser