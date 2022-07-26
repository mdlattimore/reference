# Django

[Back to Table of Contents](./index.md)

### Set Up Project

Create directory for project and then create and activate a virtual environment  

    python3 -m pip install django  # Optionally add version
    django-admin startproject django_project .  # DO NOT forget the period
    python3 manage.py startapp <<app_name>>
    python3 manage.py migrate

After setting up the directory, time to tweak some initial settings ...

First, register the app in django_project/settings.py

    # django_project/settings.py
    ...
    INSTALLED_APPS = [
        ...
        "<<app_name>>.apps.<<app_name in Capital Case>>Config",
    ]

Run ```python3 manage.py runserver``` to make sure everything is working.

Create superuser account to use with Django Admin  

    python3 manage.py createsuperuser
    # Then follow prompts


### Set Up Models

Next, set up your Database Models. This is an example with a blog app called blog:  

    # blog/models.py
    from django.db import models
    from django.urls import reverse
    
    
    class Post(models.Model):
        title = models.CharField(max_length=200)
        author = models.ForeignKey("auth.User", on_delete=models.CASCADE,)
        body = models.TextField()
    
        def __str__(self):
            return self.title  # This is what will appear in the
                               # admin dashboard    
        def get_absolute_url(self):
            return reverse("post_detail", kwargs={"pk": self.pk})  
        
        # The __str__ creates the representation of the entry in the
        # Admin dashboard. "post_detail" is the name of a view to be
        # created that will display content from the posts.  

Then we have to register the model with Admin in order for it to appear in dashboard. Working in  <<app>>/admin.py  

    # <<app>>/admin.py
    from django.contrib import admin
    from .models import <<Name of model Class>>
    
    admin.site.register(<<Name of model Class)

After the model is finished, migrate changes to take effect:

    python3 manage.py makemigrations <<app>>
    python3 manage.py migrate

## Set Up urls

Set up urls. This must be done in two places. The project/urls.py file and the app/urls.py (which you must create) 
