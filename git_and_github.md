# Git and GitHub

[Back to Table of Contents](./index.md)

## Initial Setup
Initialize a new git repository within the active folder or, if using virtualenv, within that virtualenv. Create a .gitignore file in the directory to specify what files should not be tracked:  

    git init
    git add -A
    git commit -m "intial commit"

To push to GitHub, first create a repository on GitHub and make note of the url for the repository.  Then ...  

    git remote add origin <<url to repository>>
    git branch -M main
    git push -u origin main

## Branching
    git branch <<name of branch>>  
    git checkout <<name of branch>>  #switches branch
