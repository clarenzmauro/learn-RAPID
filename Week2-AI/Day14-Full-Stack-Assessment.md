- OS: Linux - the foundation for running backend services in a stable and efficient environment

- Version Control: Git & Github - manages the codebase, tracks changes, facilitate collaboration, host the remote repository.

- Containerization: Docker - packages django application and postgresql database into isolated portable containers. ensures concistency between development and deployment.

- Orchestration: Docker Compose - defines and manages multi-container application locally, making it easy to spin up, connect, and manage these services together.

- CI/CD: Github Actions - automates tasks like building Django Docker image whenever you push code, potentially running tests, and deploying the application

- Frontend: React - provides the user interface for students to take assessments and for faculty to manage questions or view AI-driven insights. Runs in the user's browser.

- Backend: Django - the central hub.:
    - serves API endpoints that react consumes
    - handles business logic
    - interacts with the postgresql database to store and retrieve data
    - loads and uses your trained scikit-learn/pytorch models to provide ai features
    - could potentially trigger or interact with pyspark jobs for more extensive data analysis.

- Database: PostgreSQL - persistently stores all structured data for your application.

- Machine Learning: Scikit-learn / Pytorch:
    - Scikit-learn: used for traditional ML tasks. 
    - PyTorch: used for deep learning.

- Data Pipeline: PySpark - for processing larger datasets, performing complex data transformations, or running batch analytics that might be too slow for django to handle correctly.

