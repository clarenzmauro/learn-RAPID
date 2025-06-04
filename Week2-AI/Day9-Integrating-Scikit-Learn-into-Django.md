load a saved scikit-learn model
- joblib.load(): just as joblib.dump() saves your model, joblib.load() loads it back into memory.

for production application, you'd typically load the model once when the django application starts and keep it in memory to avoid reloading it on every API request.

for simplicity, we'll load it directly within the view function, but be aware this isn't optimal for performance under load. a better approach would be to load it globally in views.py file so it's loaded when the module is first imported to django.

making the model file accessible to django (in docker)
- copy it into the docker image
    - modify your django project's dockerfile to copy the .joblib file into the image during build process. this bundles the model within your application.

mini-project
prerequisites:
- your trained model difficulty_prediction_pipeline.joblib
- your django project with docker compose setup.

steps
1. move the model file and add scikit-learn to django's requirements
2. modify dockerfile to copy the model
3. rebuild your django docker image
4. create the prediction view in django
5. add url for the new endpoint
6. start/restart docker compose
7. test the new api 