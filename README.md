# Django

[Edureka tutorial](https://www.youtube.com/watch?v=zuxzE7--RYM&t=1036s), [Edureka complete tutorial](https://www.youtube.com/watch?v=HRLIEgwYSHc&t=1865s)

[Tutuorialspoint](https://www.tutorialspoint.com/django/index.htm)

## Web Development Algorithm

1. Environment- Install django and set up database.
2. Project creation- Create and set up project.  
3. Apps life cycle- Create app and get the project to know about application.
4. Admin interface- Start the admin interface and initiate database.
5. Views - Render function and passing parameter.
6. URL mapping
7. Template System
8. Models

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

    $ django-admin startproject <project-name> { Here, project-name = DEMOPROJECT }
    
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

     $ python manage.py startapp DEMOAPP { Here, DEMOAPP = App name }
     
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
    $ exit()

syncdb will create necessary tables or collections depending on our db type, necessary for the admin interface to run. Even if we don't have a superuser, we will be prompted to create one.

If we already have a superuser or have forgotten it, we can always create one using the following code:

    $ python manage.py createsuperuser
    
Now enter email and password.
    
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

## Step 5: Views

A view function, or “view” for short, is simply a Python function that takes a web request and returns a web response. This response can be the HTML contents of a Web page, or a redirect, or a 404 error, or an XML document, or an image, etc. Example: You use view to create web pages, note that you need to associate a view to a URL to see it as a web page.

In Django, views have to be created in the app views.py file.

### Simple View

    from django.http import HttpResponse

    def hello(request):
       text = """<h1>welcome to my app !</h1>"""
       return HttpResponse(text)

In this view, we use HttpResponse to render the HTML (as you have probably noticed we have the HTML hard coded in the view). To see this view as a page we just need to map it to a URL.

### Render Function

We used HttpResponse to render the HTML in the view before. This is not the best way to render pages. Django supports the MVT pattern so to make the precedent view, Django - MVT like, we will need:

    from django.shortcuts import render
    from django.http import HttpResponse
    from django.template import loader
    from .models import AllCourses

    def Courses(request):
        ac = AllCourses.objects.all()
        template = loader.get_template('DEMOAPP/Courses.html')
        context = {'ac': ac }
        return HttpResponse(template.render(context, request))

### Passing paramater

Views can also accept parameters:

    def detail(request, course_id):
        return HttpResponse('<h2>These are course details for course id' +str(course_id)+'</h2>')
        
When linked to a URL, the page will display the number passed as a parameter. Note that the parameters will be passed via the URL (discussed in the next chapter).

## Step 6: URL mapping

Now that we have a working view as explained in the previous chapters. We want to access that view via a URL. Django has his own way for URL mapping and it's done by editing your project url.py file (DEMOPROJECT/url.py). The url.py file looks like:

    from django.contrib import admin
    from django.urls import path

    urlpatterns = [
        path('admin/', admin.site.urls),
    ]

When a user makes a request for a page on your web app, Django controller takes over to look for the corresponding view via the url.py file, and then return the HTML response or a 404 not found error, if not found. In url.py, the most important thing is the "urlpatterns" tuple. It’s where you define the mapping between URLs and views. A mapping is a tuple in URL patterns like:

    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', include('DEMOAPP.urls')),
    ]
..
    from django.urls import path
    from . import views

    urlpatterns = [
        path('<int:course_id>/', views.detail, name='detail'),
        path('', views.Courses, name = 'home-page'),
    ]
    
### Sending Parameters to Views


## Step 7: Template System

Django makes it possible to separate python and HTML, the python goes in views and HTML goes in templates. To link the two, Django relies on the render function and the Django Template language.

### The Render Function

This function takes three parameters −

* Request − The initial request.

* The path to the template − This is the path relative to the TEMPLATE_DIRS option in the project settings.py variables.

* Dictionary of parameters − A dictionary that contains all variables needed in the template. This variable can be created or you can use locals() to pass all local variable declared in the view.

### Django Template Language (DTL)

Django’s template engine offers a mini-language to define the user-facing layer of the application.

#### Displaying Variables

A variable looks like this: {{variable}}. The template replaces the variable by the variable sent by the view in the third parameter of the render function.

    <html>

       <body>
          Hello World!!!<p>Today is {{today}}</p>
       </body>

    </html>
    
Then our view will change to:

    def hello(request):
       today = datetime.datetime.now().date()
       return render(request, "hello.html", {"today" : today})

As you have probably noticed, if the variable is not a string, Django will use the __str__ method to display it; and with the same principle you can access an object attribute just like you do it in Python. For example: if we wanted to display the date year, my variable would be: {{today.year}}.

## Step 8: Models

A model is a class that represents table or collection in our DB, and where every attribute of the class is a field of the table or collection. Models are defined in the app/models.py (in our example: DEMOAPP/models.py)
