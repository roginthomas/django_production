# Django, uWSGI and Nginx in a container, using Supervisord

#### RUN DJANGO USING GUNICORN
* `sudo apt install gunicorn`
* `gunicorn django_rog.wsgi:application --bind localhost:8000`

#### GUNICORN SCRIPT FOR STARTUP SERVICE
edit the file "django_gunicorn_service" in root directory
* `chmod +x django_gunicorn_service`
* `./django_gunicorn_service`

#### RUN WITH THE HELP OF SUPERVISOR
* `sudo apt install python-pip`
* `sudo apt install nginx`
* `sudo apt install supervisor`
* `./django_gunicorn_service`


### How to insert your application

In /app currently a django project is created with startproject. You will
probably want to replace the content of /app with the root of your django
project. Then also remove the line of django-app startproject from the 
Dockerfile

uWSGI chdirs to /app so in uwsgi.ini you will need to make sure the python path
to the wsgi.py file is relative to that.
