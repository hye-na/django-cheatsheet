# django-cheatsheet

## How to create a new Django project
```bash
django-admin startproject projectname
```
## How to start the Django development server
```bash
python3 manage.py runserver
```

## How to stop Django server
```bash
ctrl + C
```

## How to create a new application in the project
```bash
python3 manage.py startapp main_app
```
## Make the repo for the project
* Go to folder containing project
* Go to github and create a new repository - do not initiliaze
* Follow instructions - make sure to do `git add -A` before committing

## Django Directory Structure
```
djangoproject
 |
 |-djangoproject
 |  |
 |  |- settings.py: Main settings for project (db, apps, config, etc.)
 |  |- urls.py: Main URLs for entire project
 |
 |- application_name
 |  |- static: (dir) Holds all static files (css, js, images, aux, forms)
 |  |- templates: (dir) Holds all HTML template files
 |  |- migrations: (dir) This holds all data migration files
 |  |- admin.py: This is where we register data models
 |  |- models.py: This is where we put all data models
 |  |- views.py: This is where we put the functions that run our routes
 |  |- urls.py: Every URL for our site is defined here
 |
 |- manage.py: Let's us manage everything about our project
```
## Make sure you are in the correct version of Python:
* Python 3.7

## How to make URLs with the path() function: (This is inside the urls.py)
```python
from django.urls import path
from . import views

urlpatterns = [
 path('route1/', views.route1_name, name="route1_name"),
 path('route2/<string_variable>', views.route2_name, name="route2_name"),
 path('route3/<int:variable_name>', views.route3_name, name="route3_name"),
]

# The first route is empty since it is the root.
```
## How to make a view function:
```python
 def route1_name(request):
  return render(request, 'template.html')
  
 def route2_name(request, string_variable):
  return render(request, 'template2.html', {'data': string_variable})
  
 def route3_name(request, variable_name):
  return render(request, 'template3.html', {'data': variable_name})
```

### Then Create a templates and make a base.html
- In the body 
{% block content %}
{% endblock %}

### Django folder urls.py
```
from django.urls import path, include

urlpatterns = [
  path('', include('main_app.urls')),
]
```

## Static files
in the base.html
```
{% load staticfiles %}

In the heading:
    <link rel="stylesheet" type="text/css" href="{% static 'style.css' %}">

```

## Create a PostgreSQL Database
```
createdb cats
```
### Update settings.py to use PostgreSQL
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': ('cats'),
    }
}
```

## Models in Django - in models.py
```
class Cat(models.Model):
    name = models.CharField(max_length=100)
    breed = models.CharField(max_length=100)
    description = models.TextField(max_length=250)
    age = models.IntegerField()
```

## How to make migrations
```
python3 manage.py makemigrations
```
* Use the above after making the postgresql database
```
python3 manage.py makemigrate
```

## How to open databases
* Use Postico to open


## How to test CRUD in python interactive shell
```
python3 manage.py shell
from main_app.models import Cat
```

## To see all our objects:
```
Cat.objects.all()
```

## How to create a database
* dropdb cats
* createdb cats
* python3 manage.py migrate
* python3 manage.py createsuperuser

## Whenever you change a model
* Whenever you change a model
 * Add new model to the models.py
 * make sure to add the __str__
 * makemigration
 * migrate
 * go to admin.py
    * import the Model title
    * admin.site.register(ModelTitle)
 * go to urls.py
    * add new paths
 * go to views.py
    * add the methods from the paths (Create, Update, Delete)
    * import Model
 * now go make the templates


