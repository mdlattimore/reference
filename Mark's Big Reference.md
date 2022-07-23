# Table of Contents

* [Git and Github](#git)
* [Django](#django)
* [Test](#test)

## <a name="git">Git and GitHub</a>

Initialize a new git repository within the active folder or, if using virtualenv, within that virtualenv. Create a .gitignore file in the directory to specify what files should not be tracked:  

    git init
    git add -A
    git commit -m "intial commit"

To push to GitHub, first create a repository on GitHub and make note of the url for the repository.  Then ...  

    git remote add origin <<url to repository>>
    git branch -M main
    git push -u origin main

## <a name="django">Django</a>

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

After the model is finished, migrate changes to take effect:

    python3 manage.py makemigrations <<app>>
    python3 manage.py migrate

Create superuser account to use with Django Admin  

    python3 manage.py createsuperuser
    # Then follow prompts

Then we have to register the model with Admin in order for it to appear in dashboard. Working in  <<app>>/admin.py  

    # <<app>>/admin.py
    from django.contrib import admin
    from .models import <<Name of model Class>>
    
    admin.site.register(<<Name of model Class)

Set up urls. This must be done in two places. The project/urls.py file and the app/urls.py (which you must create) 

## 
