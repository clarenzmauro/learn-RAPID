django models - defining your data structure

in django, a model is the single, definitive source of information about your data. it contains the essential fields and behaviors of the data you're storing. each model maps to a single database table.

common field types
- CharField: for short strings. requires max_length.
- TextField: for long strings.
- IntegerField: for integers.
- FloatField: for floating-point numbers
- BooleanField: for true/false values
- DateField, DateTimeField: for dates and datetimes.
- ForeignKey: to define a many-to-one relationship.
- ManyToManyField: to define a many-to-many relationship
- OneToOneField: to define a one-to-one relationship

migrations - this tells django to create or update the actual database tables. this is done through a two-step process:
1. python manage.py makemigrations <app_name>: django inspects your models and creates migration files that describe the changes.
2. python manage.py migrate: django applies these migration files to your database, creating/altering tables.

docker compose - a tool for defining and running multi-container docker apps. with compose, you use a YAML file(docker-compose.yml) to configure your application's services. Then, with a single command, you can create and start all the services from your configuration.

key docker-compost.yml concepts:
- version: specifies the compose file format version
- services: defines the different containers that make up your application
- image or build: specifies the image for a service. build tells compose to build an image from a dockerfile
- ports: maps ports between the host and the container (similar to docker run -p)
- volumes: mounts host paths or named volumes into containers (similar to docker run -v)
- environment: sets environment variables for the service
- depends_on: specifies dependencies between services

mini-project:
1. define django models
2. add psycopg2-binary to requirements.txt
3. create docker-compose.yml
4. configure django settings.py to use postgresql
5. add your app to INSTALLED_APPS
6. build and run with docker compose
7. run migrations using docker-compose exec
8. verify
9. stop docker compose