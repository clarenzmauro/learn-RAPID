# RAPID Stack: 14-Day Learning Plan for [Redacted Module Name]

This plan aims to provide a basic to advanced understanding of the RAPID stack (React, AI (PyTorch/Scikit-learn), PostgreSQL, Integration, Django) through daily mini-projects relevant to a "[Redacted Module Name]" internship.

## Week 1: Building the [Redacted Module Name] Web Foundation

### Day 1: Linux & Git Essentials for [Redacted Module Name]
*   **Topics:** Basic Linux commands (navigation, file/directory management, permissions). Git setup, fundamental commands: `git init`, `add`, `commit`, `push`, `clone`, basic branching. Creating a GitHub repository.
*   **Mini-Project:** Set up your Linux environment (or WSL on Windows). Create a new GitHub repository named `bsu_[redacted]_module`. Clone it to your local machine, add a `README.md` file describing its purpose, then commit and push your changes to GitHub.

### Day 2: Python & Django Setup for the [Redacted Module Name] Backend
*   **Topics:** Python virtual environments (`venv`) for project isolation. Using `pip` for package management. Installing Django, initiating a new Django project (`django-admin startproject`), and creating a Django app (`python manage.py startapp`).
*   **Mini-Project:** Create a Django project called `[redacted]_platform`. Inside this project, create a new Django app named `[redacted]_api`.

### Day 3: Django Models & PostgreSQL for [Redacted Module Name] Data
*   **Topics:** Defining Django Models (e.g., `CharField`, `TextField`, `IntegerField`, `ForeignKey`). Understanding and applying database migrations (`makemigrations`, `migrate`). Configuring your Django project to connect with a PostgreSQL database.
*   **Mini-Project:** In your `[redacted]_api` app, define two core models:
    *   `Question` with fields like `question_text`, `question_type` (e.g., 'MCQ', 'Essay'), and `difficulty_level`.
    *   `Submission` with `student_identifier`, a foreign key to `Question`, `answer_text`, and a nullable `score`.
    Connect your Django project to a local PostgreSQL instance and run the database migrations.

### Day 4: Django API for Managing [Redacted Module Name]
*   **Topics:** Crafting Django function-based views to handle requests. Defining URL patterns in `urls.py` to route requests to views. Returning structured data using `JsonResponse`.
*   **Mini-Project:** Implement two API endpoints in your `[redacted]_api`:
    *   A `GET` endpoint at `/api/questions/` that retrieves and returns a list of all `Question` objects from the database.
    *   A `POST` endpoint at `/api/submit_answer/` that accepts student input, creates a new `Submission` record in PostgreSQL based on the provided question and answer.

### Day 5: React Basics for the [Redacted Module Name] Interface
*   **Topics:** Initializing a React project (`create-react-app`). Understanding JSX syntax. Creating reusable functional components. Passing data between components using props. Managing component-specific data with the `useState` hook.
*   **Mini-Project:** Create a new React application. Develop a basic `QuestionDisplay` component that accepts `question_text` and `question_type` as props and renders them on the screen. Populate your `App.js` with a few static `QuestionDisplay` instances.

### Day 6: React & Django: Taking a [Redacted Module Name]
*   **Topics:** Asynchronous data fetching in React using the `fetch` API (or Axios). Using the `useEffect` hook to perform side effects like data loading. Handling user input with HTML forms in React and sending data to the backend.
*   **Mini-Project:** Modify your React application to:
    1.  Fetch the list of questions from your Django `/api/questions/` endpoint.
    2.  Display one question at a time (e.g., just the first one for simplicity).
    3.  Include a text input field for the answer and a "Submit" button. Upon submission, send the answer along with the question identifier to your Django `/api/submit_answer/` endpoint.

### Day 7: GitHub Actions for [Redacted Module Name] Backend CI
*   **Topics:** Introduction to Continuous Integration (CI) with GitHub Actions. Creating a workflow file (`.github/workflows/your-workflow.yml`). Defining triggers (e.g., on `push` events). Running basic shell commands within a workflow.
*   **Mini-Project:** Create a GitHub Actions workflow for your `[redacted]_platform` Django project. Configure it to automatically run `python manage.py check` (Django's built-in sanity check) every time you push code to your GitHub repository, ensuring basic code health.

## Week 2: AI in [Redacted Module Name] & Data Handling

### Day 8: Scikit-learn for Basic [Redacted Module Name] AI (e.g., Difficulty Prediction)
*   **Topics:** Introduction to Scikit-learn, common ML tasks like classification. Basic text feature extraction techniques (e.g., `CountVectorizer`). Training a simple classification model (e.g., `LogisticRegression` or `NaiveBayesClassifier`).
*   **Mini-Project:** Create a small, simplified dataset (e.g., a CSV file with `question_text` and a manually assigned `difficulty_level` (1, 2, or 3)). Train a Scikit-learn classifier to predict the `difficulty_level` from the `question_text`. Save this trained model to a file using `joblib` or `pickle`.

### Day 9: Integrating Scikit-learn into Django for AI-Powered [Redacted Module Name]
*   **Topics:** Loading a previously saved Scikit-learn model within a Django view. Creating a new API endpoint that accepts input features and uses the loaded model to return an AI-driven prediction.
*   **Mini-Project:** Create a new Django API endpoint, for example, `/api/predict_difficulty/`. This endpoint should load your saved Scikit-learn difficulty prediction model. It will take `question_text` as input from a POST request, use the model to predict the difficulty, and return the predicted level as a JSON response.

### Day 10: React Frontend for AI [Redacted Module Name] Feature
*   **Topics:** Building forms in React to capture user input for AI features. Sending `POST` requests from the React frontend to your new Django ML API endpoint. Displaying the AI's prediction to the user.
*   **Mini-Project:** Enhance your React application by adding a new interface for a faculty member. This interface should allow them to type in a new `question_text`. Upon submission, the text is sent to your Django `/api/predict_difficulty/` endpoint, and the AI's suggested difficulty level is displayed back to the user.

### Day 11: PySpark Introduction for Analyzing [Redacted Module Name] Results
*   **Topics:** Understanding the role of PySpark for large-scale data processing. Setting up a local PySpark environment. Working with PySpark DataFrames: reading data (e.g., from CSV), basic DataFrame operations like `show()`, `select()`, `filter()`, `groupBy()`, `avg()`, and `count()`.
*   **Mini-Project:** Create a dummy CSV file containing sample `Submission` data (e.g., `student_id`, `question_id`, `score`). Write a PySpark script that:
    1.  Reads this CSV into a DataFrame.
    2.  Calculates the average score for each `question_id`.
    3.  Counts the total number of submissions for each question.
    Display the results.

### Day 12: PyTorch Basics - Tensors for [Redacted Module Name] Data
*   **Topics:** Introduction to PyTorch. Creating PyTorch tensors. Performing fundamental tensor operations like addition, multiplication, and indexing. A conceptual understanding of `torch.autograd` for automatic differentiation.
*   **Mini-Project:** Represent a small set of numerical [Redacted Module Name] data (e.g., scores for 3 students across 5 questions) as a PyTorch tensor. Perform various tensor manipulations:
    *   Add a constant value to all scores.
    *   Multiply scores by a weighting factor.
    *   Select specific rows or columns.

### Day 13: PyTorch - Simple Model Definition for [Redacted Module Name] Tasks
*   **Topics:** Defining a basic neural network layer using `torch.nn.Linear`. Understanding the `forward` pass, which defines how input data flows through the network. (Focus on architecture, not training).
*   **Mini-Project:** Define a very simple PyTorch neural network model as a Python class inheriting from `torch.nn.Module`. This model could have one input layer, one hidden `Linear` layer, and an output layer. Instantiate the model and pass a random tensor (representing hypothetical [Redacted Module Name] features) through its `forward` method to observe the output tensor's shape.

### Day 14: Full Stack [Redacted Module Name] - Putting It All Together (Conceptual)
*   **Topics:** A comprehensive review of how all components of the RAPID stack (React, AI (PyTorch/Scikit-learn), PostgreSQL, Integration, Django, Linux, Git & GitHub, GitHub Actions) can be orchestrated to build a robust "[Redacted Module Name]." Discuss data flow and inter-component communication.
*   **Mini-Project:** Create a diagram (on paper, whiteboard, or using a digital tool) and a short explanatory document (e.g., a markdown file in your repo) illustrating the complete data flow and interaction for a specific AI-powered [Redacted Module Name] feature. For instance:
    *   How a student's essay answer (from React) is sent to Django.
    *   How Django then calls a PyTorch model to perform basic sentiment analysis or keyword matching for scoring.
    *   How the score is saved in PostgreSQL.
    *   How PySpark could later analyze aggregated scores to identify commonly missed concepts for faculty, possibly displayed via another Django view.