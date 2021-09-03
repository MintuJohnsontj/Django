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

    $cd DEMOPROJECT
    $python manage.py runserver

<img src="Images/django2.PNG" width="500" height="400">

Create new app in project:

     $python manage.py startapp DEMOAPP { Here, DEMOAPP = App name }
        
<img src="Images/django3.PNG" width="500" height="400">
