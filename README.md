# Django

[Edureka tutorial](https://www.youtube.com/watch?v=zuxzE7--RYM&t=1036s), [Edureka complete tutorial](https://www.youtube.com/watch?v=HRLIEgwYSHc&t=1865s)

[Tutuorialspoint](https://www.tutorialspoint.com/django/index.htm)

## Web Development Algorithm

1. Environment- Install django and set up database
2. Project creation- Create and set up project  
3. Apps life cycle- Create app
4. Admin interface

## Step 1: Environment

Django development environment consists of installing and setting up Python, Django and a Database System. Since Django deals with web application, it's worth mentioning that we would need a web server setup as well.

### Install django

    $ pip install django

### Database Setup
    
Django supports several major database engines and you can set up any of them based on your comfort.

* MySQL (http://www.mysql.com/)
* PostgreSQL (http://www.postgresql.org/)
* SQLite 3 (http://www.sqlite.org/)
* Oracle (http://www.oracle.com/)
* MongoDb (https://django-mongodb-engine.readthedocs.org)
* GoogleAppEngine Datastore (https://cloud.google.com/appengine/articles/django-nonrel)
* You can refer to respective documentation to installing and configuring a database of your choice.

Note − Number 5 and 6 are NoSQL databases.

## Step 2: Create a Project

Now that we have installed Django, let's start using it. In Django, every web app we want to create is called a project; and a project is a sum of applications. An application is a set of code files relying on the MVT pattern. As example let's say we want to build a website, the website is our project and, the forum, news, contact engine are applications. This structure makes it easier to move an application between projects since every application is independent.

### Create a Project

Whether you are on Windows or Linux, just get a terminal or a cmd prompt and navigate to the place you want your project to be created, then use this code:

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

* The “DEMOPROJECT” subfolder : This folder is the actual python package of our project. It contains 4 files −

__init__.py : Just for python, treat this folder as package.

settings.py : As the name indicates, our project settings.

urls.py : All links of your project and the function to call. A kind of ToC of our project.

wsgi.py : If we need to deploy our project over WSGI.
    
* manage.py: This file is kind of your project local django-admin for interacting with your project via command line (start the development server, sync db...). 

### Setting Up Our Project

Our project is set up in the subfolder myproject/settings.py.

    DEBUG = True

This option tells whether project is in debug mode or not. Debug mode help us to get more information about our project's error. Never set it to ‘True’ for a live project. However, this has to be set to ‘True’ if we want the Django light server to serve static files. Do it only in the development mode.


    DATABASES = {
       'default': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': 'database.sql',
          'USER': '',
          'PASSWORD': '',
          'HOST': '',
          'PORT': '',
       }
    }
    
Database is set in the ‘Database’ dictionary. The example above is for SQLite engine. Before setting any new engine, make sure we have the correct db driver installed. We can also set others options like: TIME_ZONE, LANGUAGE_CODE, TEMPLATE…

Now that your project is created and configured make sure it's working :

    $ cd DEMOPROJECT
    $ python manage.py runserver

<img src="Images/django2.PNG" width="500" height="400">

## Step 3: Apps Life Cycle

A project is a sum of many applications. Every application has an objective and can be reused into another project, like the contact form on a website can be an application, and can be reused for others. See it as a module of your project.

### Create an Application

We assume you are in your project folder. In our main “DEMOPROJECT” folder, the same folder then manage.py:

     $python manage.py startapp DEMOAPP { Here, DEMOAPP = App name }
     
We just created DEMOAPP application and like project, Django create a “DEMOAPP” folder with the application structure:

    DEMOAPP/
       __init__.py
       admin.py
       models.py
       tests.py
       views.py
       
* __init__.py − Just to make sure python handles this folder as a package.

* admin.py − This file helps you make the app modifiable in the admin interface.

* models.py − This is where all the application models are stored.

* tests.py − This is where your unit tests are.

* views.py − This is where your application views are.
        
<img src="Images/django3.PNG" width="500" height="400">

### Get the Project to Know About Our Application

At this stage we have our "DEMOAPP" application, now we need to register it with our Django project "DEMOPROJECT". To do so, update INSTALLED_APPS tuple in the settings.py file of our project (add our app name):

    INSTALLED_APPS = (
       'django.contrib.admin',
       'django.contrib.auth',
       'django.contrib.contenttypes',
       'django.contrib.sessions',
       'django.contrib.messages',
       'django.contrib.staticfiles',
       'DEMOAPP',
    )
    
## Step 4: Admin Interface

Django provides a ready-to-use user interface for administrative activities. We all know how an admin interface is important for a web project. Django automatically generates admin UI based on your project models.

### Starting the Admin Interface
   
The Admin interface depends on the django.countrib module. To have it working you need to make sure some modules are imported in the INSTALLED_APPS and MIDDLEWARE_CLASSES tuples of the myproject/settings.py file.

For MIDDLEWARE_CLASSES:

    MIDDLEWARE_CLASSES = (
   'django.contrib.sessions.middleware.SessionMiddleware',
   'django.middleware.common.CommonMiddleware',
   'django.middleware.csrf.CsrfViewMiddleware',
   'django.contrib.auth.middleware.AuthenticationMiddleware',
   'django.contrib.messages.middleware.MessageMiddleware',
   'django.middleware.clickjacking.XFrameOptionsMiddleware',
    )
    
### Initiate Database

Before launching our server, to access our Admin Interface, we need to initiate the database:

    $ python manage.py migrate
    
Database:

    $ python manage.py shell
    $ from DEMOAPP.models import AllCourses, details
    $ AllCourses.objects.all()
    $ a=AllCourses(coursename="Python",insname="XYZ")
    $ a.save()
    $ a.coursename

syncdb will create necessary tables or collections depending on our db type, necessary for the admin interface to run. Even if we don't have a superuser, we will be prompted to create one.

If we already have a superuser or have forgotten it, we can always create one using the following code:

    $ python manage.py createsuperuser
    
 Now to start the Admin Interface, we need to make sure we have configured a URL for our admin interface. Open the myproject/url.py and you should have something like:
 
    from django.conf.urls import patterns, include, url

    from django.contrib import admin
    admin.autodiscover()

    urlpatterns = patterns('',
       # Examples:
       # url(r'^$', 'myproject.views.home', name = 'home'),
       # url(r'^blog/', include('blog.urls')),

       url(r'^admin/', include(admin.site.urls)),
    )

Now just run the server.

    $ python manage.py runserver
    
And your admin interface is accessible at: http://127.0.0.1:7000/admin/
