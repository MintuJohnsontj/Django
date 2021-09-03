# Django

[Edureka tutorial](https://www.youtube.com/watch?v=zuxzE7--RYM&t=1036s)

## Step 1: Installing Django
IDE Commandline:

    $pip install django

## Step 2: Database Setup
    
Django supports several major database engines and you can set up any of them based on your comfort.

* MySQL (http://www.mysql.com/)
* PostgreSQL (http://www.postgresql.org/)
* SQLite 3 (http://www.sqlite.org/)
* Oracle (http://www.oracle.com/)
* MongoDb (https://django-mongodb-engine.readthedocs.org)
* GoogleAppEngine Datastore (https://cloud.google.com/appengine/articles/django-nonrel)
* You can refer to respective documentation to installing and configuring a database of your choice.

Note − Number 5 and 6 are NoSQL databases.

## Step 3: Create a Project

    $django-admin startproject <project-name> { Here, project-name = DEMOPROJECT }
    
<img src="Images/django1.PNG" width="500" height="400">

     DEMOPROJECT/
        DEMOPROJECT/
            __init__.py
            settings.py
            urls.py
            wsgi.py
        manage.py
### The Project Structure

The “DEMOPROJECT” folder is just our project container, it actually contains two elements −

    * The “myproject” subfolder − This folder is the actual python package of your project. It contains four files −

    __init__.py − Just for python, treat this folder as package.

    settings.py − As the name indicates, our project settings.

    urls.py − All links of your project and the function to call. A kind of ToC of our project.

    wsgi.py − If we need to deploy our project over WSGI.
    
    * manage.py: This file is kind of your project local django-admin for interacting with your project via command line (start the development server, sync db...). 




    $cd DEMOPROJECT
    $python manage.py runserver

<img src="Images/django2.PNG" width="500" height="400">

Create new app in project:

     $python manage.py startapp DEMOAPP { Here, DEMOAPP = App name }
        
<img src="Images/django3.PNG" width="500" height="400">
