# Django and PostgreSQL

building websites involves a lot of repetitive tasks. 

You need to handle incoming web requests, figure out what the user wants, get data from a database, put that data into an HTML page, and send it back.

Django's fundamental purpose is to provive a safe and logical structure for these repetitive tasks. A pre-built chassis for your web app.

# The three core concepts: Model-View-Template architecture.

1. Models: the blueprint for your data. It's the "what." Before you can store data, you have to define its shape. A model is just a python class that describes your data. For example, a tweet model would define that a tweet has text content and a creation date. 

2. Views: the brain. It's the "how." A view is a python function that takes a web request and returns a web response. It contains the logic. When a user wants to see all their tweets, a view function is what handles that request, ask the Model for the data, and decides what to do with it.

3. Templates: the face. It's the "look." A template is an HTML file with special placeholders. The view gets the data and then injects it into the template to generate the final HTML page that the user sees in their browser. 

Django's core loop:

User's browser sends a request to a URL > Django's router maps that URL to a specific View > View runs its logic, possibly using a Model to fetch data > View passes that data to a Template > Template generates the final HTML, which the View sends back as that response.

---

# Models

Storing data in a variable is like leaving your food outside hoping it will still be there tomorrow. 

If the server restarts, that data is gone. This is why you need a database.

A Model is an abstraction. It lets you define the structure of your data using only Python. Django then handles the job of translating your Python code into the necessary SQL for you.

Think of a Model as the single source of truth for your data's structure. It's a python class that inherits from django.db.models.Model. Each attribute you define in the class represents a column in your database table.

```
from django.db import models
from django.contrib.auth.models import user

class Post(models.Model):
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Post by {self.author.username} at {self.created_at}"
```

`class Post(models.Model)` defines the piece of data called a Post. It's a "Model", so Django knows to create a database table for it.

`author = models.ForeignKey(User, on_delete=models.CASCADE)` A post must have an author. This field creates a relationship to another data model, the built-in `User` model. It's a fundamental link between two pieces of data.

`content = models.TextField()` A post must have content. This defines this as a text field, which can hold a lot of text.

`created_at = models.DateTimeField(auto_now_add=True)` A post needs a timestamp. We're defining a field to store the date and time. `auto_now_add=True` tells Django to automatically set this value the moment a new post is created.

This system of Django generating the correct SQL for you is called an Object-Relational Mapper (ORM). It "maps" your Python objects to rows in a relational database table.

```
# To create a new post (like writing INSERT INTO...)
new_post = Post.objects.create(author=some_user, content="First principles thinking is powerful.")

# To get a specific post (like writing SELECT * FROM ... WHERE id=1)
my_post = Post.objects.get(id=1)

# To update it
my_post.content = "A new, updated thought."
my_post.save() # This writes the change to the database

# To delete it
my_post.delete()
```

---

# Migrations

"How do we make the database's structure match our Python blueprint in a safe and repeatable way? And more imporatntly, how do we update the database later when we change our models, without losing all our data?"

This is where migrations come in. A migration is a record of change. Sort of like version control (like Git) for your database schema. Each migration file is a script that describes a specific change: creating a table, adding a column, deleting a field, etc.

The process is a simple, two-step command:

Step 1: `makemigrations`
When you run the command `python manage.py makemigrations`, you're telling Django: "Compare my current `models.py` file with the state of the last migration you know about. Figure out what changed, and write down the instructions to apply for those changes." 

Django then generates a new Python file in `migrations/` directory. For example, if you added a `likes_count` field to your `Post` model, it might create a file named `0002_post_likes_count.py`. This file contains the code to add that specific column.

Crucially, this command does not touch your database. It only creates the instruction file, the plan.

Step 2: `migrate`
When you run `python manage.py migrate`, you're telling Django: "Okay, now take all the migration plans that haven't been applied yet and actually execute them on the database."

Django connects to your PostgreSQL database, reads the migration files one by one, translates the Python instructions into the correct PostgreSQL-specific SQL and runs it.

It also keeps a special table in your database called `django_migrations` to track which migration files it has already run, so it never accidentally applies the same change twice.

Workflow is always:
1. Change your models.py
2. Run `python manage.py makemigrations` to create the migration script.
3. Run `python manage.py migrate` to apply that script to the database.

PERSONAL NOTE: Migrations simply is a version-controlled way to evolve the database.

---

# PostgreSQL

Django Models = Python blueprints.

Migrations = instructions for building the database structure.

PostgreSQL = A highly organized, super-secure warehouse for your data.

PostgreSQL is a relational database.

It means it stores data in tables with rows and coluns, just like a spreadsheet.

Your `Post` model becomes a `post` table.

Each instance of a `Post` you create becomes a new row. The `content` and `created_at` attributes become columns.

This structure is perfect for Django because Django's Models are desined to describe these exact kinds of tables and the relationships between them.

So why choose PostgreSQL over other databases?

1. Data Integrity. It has a system that guarantees that a set of operations either all succeed or all fail together. Think of a bank transfer: you can't have the money leave one account without it arriving in the other. PostgreSQL ensures this level of reliability for your data, which is critical for any serious application.

2. Concurrency. It's designed from the ground up to handle many people trying to read and write data at the same time without tripping over each other or corrupting the data. This is a non-negotiable for a website.

Django and PostgreSQL's connection is made in two places:

First, in Django `settings.py` file. This is where you input your address and login credentials for your PostgreSQL database.

```
# settings.py

DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "my_database_name",
        "USER": "my_username",
        "PASSWORD": "my_password",
        "HOST": "localhost",  # or the server's IP address
        "PORT": "5432",
    }
}
```

Second, a Python library, usually psycopg2, which acts as an adapter. Django's ORM gives its command to psycopg2, and psycopg2 translates them into the raw SQL that PostgreSQL understands.

Flow:
Python code > Django's ORM > psycopg2 translator > PostgreSQL database.

---

# Views and Templates

This answers the question: "how do we handle a user's request, fetch the data we've stored, and present it to them in a useful way?"

A view is the core logic of your application. It's just a Python function that does one simple job: it takes a web request and returns a web response. That's it.

The "magic" is what you do inside that function. The view is the middleman that connects everything. It's where you use your Models to talk to the database.

Imagine a user wants to see a list of all posts.

In your views.py:
```
from django.shortcuts import render
from .models import Post # Import our data blueprint

def post_list_view(request):
    # 1. The Logic: Use the Model to get data from PostgreSQL
    all_posts = Post.objects.all().order_by("-created_at")

    # 2. The Response: Pass that data to a Template to be displayed
    context = {
        "posts": all_posts,
    }
    return render(request, "posts/post_list.html", context)
```

1. It recieves the `request` object, which contains info about the user's request.
2. It uses `Post` model to query the database: `Post.objects.all()`. This is the Django ORM in action, generating `SELECT * FROM post ...` SQL behind the scenes.
3. It gets a list of `Post` objects back from the database. But we can't just send Python objects to a browser. We need HTML.

This is where Templates come in.

A template solves the problem of mixing your presentation (HTML) with your logic (Python). It's an HTML file with special placeholders for your data.

What `post/post_list.html` template might look like:
```
<!DOCTYPE html>
<html>
  <head>
    <title>All Posts</title>
  </head>
  <body>
    <h1>Latest Posts</h1>
    <hr />

    {% for post in posts %}
    <div>
      <p>{{ post.content }}</p>
      <small>By {{ post.author.username }} on {{ post.created_at }}</small>
    </div>
    <hr />
    {% endfor %}
  </body>
</html>
```

Special parts:

1. `{% for post in posts %}`: This is a tag. It's a piece of logic that says "loop through the list of things called `posts` that the View gave me"
2. `{{ post.content }}`: This is a variable. It says "in this spot, insert the `content` attribute of the current `post` object from the loop."

The `render` function in our view is the glue. It makes the template file, takes the `context` dictionary (`{"posts": all_posts}`), and merges them to create the final HTML that gets sent to the user.

Flow:
1. User's browser requests a URL like `/posts/`.
2. Django's router maps this URL to our `post_list_view` View.
3. The View runs. It uses the `Post` Model to query the PostgreSQL database.
4. The database sends the data back to the View.
5. The View passes this data to the `post_list.html` Template.
6. The Template engine renders the final HTML, which the View sends back as the response.

---

# Django Forms

Getting data from a user is messy. You have to render an HTML form, validate the data they submit to make sure it's not garbage, protect against common security attacks, and then, if there are errors, show them the form again with their data still filled in and helpful error messages.

Doing this manually for every form is a nighmare of repetitive code.

Django's solution is the Form class. Just like a `Model` is a Python blueprint for your database table, a `Form` is a Python blueprint for your HTML form. It centralizes three jobs into one clean object:
1. Rendering: generates the HTML <input> fields.
2. Validation: checks the submitted data aginst a set of rules.
3. Cleaning: converts the submitted data into the correct Python data types.

forms.py:
```
# forms.py
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ["content"] # We only want the user to input the content
```

This tells Django to create a form based on the `Post` model, but we only want to show the `content` field. Django already knows `content` should be a large text area because of how we defined it in the model.

Now, how do we use this in a view? A view handles a form needs to handle two different scenarios: the user vising the page for the first time (a `GET` request) and the user submitting the form (a `POST` request)

views.py:
```
from django.shortcuts import render, redirect
from .models import Post
from .forms import PostForm

def create_post_view(request):
    if request.method == "POST":
        # Scenario 2: User submitted the form
        form = PostForm(request.POST)
        if form.is_valid():
            # It's valid! Save the data.
            # We need to add the author manually since it's not in the form.
            new_post = form.save(commit=False)
            new_post.author = request.user
            new_post.save()
            return redirect("post_list_url") # Redirect after success
    else:
        # Scenario 1: User is just visiting the page
        form = PostForm()

    return render(request, "posts/create_post.html", {"form": form})
```

The `form.is_valid()` calls is the magic. It runs all the validation checks automatically. If the data is good, we save it and redirect the user. If it's bad, Django automatically attaches error messages to the form object, and we just render the page again.

Finally, create_post.html:
```
<h1>Create a New Post</h1>

<form method="post">
  {% csrf_token %} {{ form.as_p }}
  <button type="submit">Post</button>
</form>
```

- `method="post"` tells the browser to send the data in a `POST` request.
- `{% csrf_token %}` is a crucial security feature. Django puts a hidden, unique token in the form. When the form is submitted, Django checks that the token matches. This prevents a malicious website from tricking your logged-in users into submitting this form without their knowledge.
- `{{ form.as_p }}` is Django's magic for rendering. It tells the form object to render itself as a series of HTML paragraphs (<p> tags), complete with labels and input fields. If there are validation errors, it will display them here automatically.

--- 

# Django Admin

Django Admin is a professional, secure, ready-to-use administrative interface generated entirely from your models.

Activating it is very simple.

Django creates a file for you called `admin.py` in your app directory. All you have to do is tell it which models you want to manage.

admin.py:
```
from django.contrib import admin
from .models import Post

# Register your models here.
admin.site.register(Post)
```

With just that one line of code, `admin.site.register(Post)`, you get a full CRUD interface for your `Post` model.

If you start your server and go tot he `/admin/` URL, you can log in as a superuser and you'll see a "Posts" section. Clicking on it gives you:
- A list view of all your posts, with pagination.
- A search bar to find specific posts.
- The ability to filter posts by date or other fields.
- A button to "Add Post," which gives you a full form to create a new one.
- The ability to click on any post to edit or delete it.

Django automatically creates sensible forms for all field types.

A `TextField` becomes a large text area, a `DateTimeField` gets a nice date/time picker, and a `ForeignKey` becomes a dropdown list of all related objects.

You can even customize your forms by creating a `ModelAdmin` class.

Say in the list view, you want to see the author and creation date, not just the post's default setting representation.

admin.py:
```
from django.contrib import admin
from .models import Post

class PostAdmin(admin.ModelAdmin):
    list_display = ("__str__", "author", "created_at")
    search_fields = ("content", "author__username")

admin.site.register(Post, PostAdmin)
```

This tells Django: "When you build the admin for the `Post` model, use these custom options from the `PostAdmin` class"

- `list_display` controls the columns shown in the list view
- `search_fields` tells the search bar which fields to look in. We can even search through related models, like author's username.

---

# Class-Based Views (CBVs)

As your app grows, you'll notice you're writing the same patterns over and over. A view to list all posts llook very similar to a view to list all comments. A view to create a post is structured just like a view to create a comment.

The problem is repetition. 

The answer comes from object-oriented programming: inheritance. Instead of writing a new function from scratch, we can use a pre-built "blueprint" class that already knows how to do 90% of the job, and we can just tell it the specific details.

These blueprints are Django's generic Class-Based Views.

instead of the old function-based view:
```
# The old function-based view
def post_list_view(request):
    all_posts = Post.objects.all().order_by("-created_at")
    context = {"posts": all_posts}
    return render(request, "posts/post_list.html", context)
```

do this:
```
# The new class-based view
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    model = Post
    template_name = "posts/post_list.html"
    context_object_name = "posts"
    ordering = ["-created_at"]
```

We're not writing the logic ourselves; we're just configuring the `ListView` blueprint.

- `model = Post` tells ListView which model to use. It automatically handles the `Post.objects.all()` query for us.
-  `template_name = "posts/post_list.html"` tells it which template to render
- `context_object_name = "posts"` tells it to use the name `posts`
- `ordering = ["-created_at"]` specifies the ordering

CBVs have a steeper learning curve than simple functions, but they make your code more structured, reusable, and scalable. You're no longer writing the "how"; you're just declaring the "what."

---

# Advanced ORM & Query Optimization

The most common performance killer in Django is the N+1 Query Problem. It's incredibly easy to create by accident.

Imagine post_list.html template where we loop through posts and show the author's name:
```
{% for post in posts %}
<p>{{ post.content }} by {{ post.author.username }}</p>
{% endfor %}
```

and in our view, we fetch posts like this:
```
# The naive, slow way
def post_list_view(request):
    posts = Post.objects.all() # This is the problem line
    return render(request, "posts/post_list.html", {"posts": posts})
```

this is what happens behind the scenes:
1. Django executes 1 query to get all the `Post` objects
2. Then, the template starts looping. The first time it sees `{{ post.author.username }}`, it realizes that it doesn't have the author data for that post. So it makes a new query to the database to fetch that specific author.
3. It does this for the second post, and third, and so on.

This will cripple your app's performance.

The solution is to tell Django ahead of time what related data you're going to need.

1. `select_related` - Use this for `ForeignKey` and `OneToOneField` relationships. It tells the database, "When you get the posts, also grab the related author data in the same trip using a SQL `JOIN`."

```
# The efficient way
def post_list_view(request):
    posts = Post.objects.select_related("author").all()
    return render(request, "posts/post_list.html", {"posts": posts})
```

Now, Django executes a single, slightly more compelx SQL query that gets all the post and author data at once. 1 query instead of 101.

2. `prefetch_related` - Use this for `ManyToManyField` or reverse `ForeignKey` relationships. For exmaple, if each post could have multiple tags.

`prefetch_related` is smarter. It doesn't do one giant `JOIN`. Instead, it makes two separate, efficient queries:
1. It gets all the posts
2. It then makes a second query to get all the tags for all of those posts at once.
3. Finally, it stitches the data together in Python

The result is 2 queries instead of N+1.

---

# REST API

REST APIs exposes your application's data and functionality over the web using a standardized set of rules.

You can build these APIs via Django REST Framework (DRF). It's the "Django for APIs"

DRF introduces a few core concepts that mirror what we already know:

1. Serializers (The Translator) - A Django `Form` takes user input, validates it, and turns it into a Python object. A DRF Serializer does the exact same thing but for API data.

It's primary job is to translate complex data, like your Django model instances, into a simple format like JSON, and vice-versa. It's the blueprint for your API's data representation.

serializers.py:
```
# serializers.py
from rest_framework import serializers
from .models import Post

class PostSerializer(serializers.ModelSerializer):
    author_username = serializers.CharField(source="author.username", read_only=True)

    class Meta:
        model = Post
        fields = ["id", "content", "created_at", "author_username"]
```

This looks a lot like `ModelForm`. We're telling DRF to create a serializer based on our `Post` model. We specify the fields we want to expose and can add custom fields like pulling in the author's username from the related `User` model.

2. ViewSets (The Bundled Logic)
In Django, we have ListView, CreateView, UpdateView, etc. DRF combines all of this common functionality into a single class called a ViewSet.

A `ModelViewSet` automatically provides the logic for all the standard CRUD operatiosn for a model.

views.py
```
# views.py
from rest_framework import viewsets
from .models import Post
from .serializers import PostSerializer

class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.select_related("author").all()
    serializer_class = PostSerializer
    # DRF handles permissions and authentication here, but we'll skip for now.
```
This one class now contains all the logic needed to List, Create, Retrieve, Update, and Delete a post/s.

3. Routers (The Automated URL Generator)
Manually creating a URL pattern for every action in the ViewSet would be repetitive. DRF provides `Routers` to do this automatically.

urls.py:
```
# urls.py
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from .views import PostViewSet

# Create a router and register our viewset with it.
router = DefaultRouter()
router.register(r"posts", PostViewSet, basename="post")

# The API URLs are now determined automatically by the router.
urlpatterns = [
    # ... your other urls
    path("api/", include(router.urls)),
]
```

By registering our `PostViewSet` with the router, DRF automatically generates all conventional RESTful URLs for us.

Now, if you run your server and go to /api/posts/ in your browser, DRF gives you another amazing feature: the Browsable API. It's a user-friendly HTML interface for your API that lets you see the data and even submit new data through forms, making development and testing incredibly easy.