key react concepts for API interaction
- fetch API: fetch() is used to make GET requests to /api/questions and POST requests to /api/submit_answer/
- useEffect hook: lets you perform "side effects" in functional components. common side effects include data fetching, setting up subscriptions and manually changing the DOM.
    - this will be used to fetch the questions from the api when the App component first mounts.
    - basic syntax for running an effect once on monunt is: useEffect(() => { /* effect code */ }, []); (the empty dependency array [] is key)
- useState hook: this will be used to store the list of questions fetched from the api, manage loading states, handle error stats, store user input for the answer.

CORS (Cross-Oigin Resource Sharing) - a security mechanism built into web browsers. By default, browsers restrict web pages from making requests to a different domain (origin) than the one that served the web page.

to allow cors in django backend, use django-cors-headers package.

mini-project
1. ensure django backend is running via docker compose
2. ensure react dev server is running
3. modify src/App.js in react project
4. implement cors fix for django backend