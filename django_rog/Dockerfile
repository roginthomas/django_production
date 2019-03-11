FROM ubuntu:18.04

RUN apt-get update && \
	apt-get install -y nginx && \
    apt-get upgrade -y && \ 
    apt-get install -y \
    gunicorn -y \
	git \
	gunicorn \
	python \
	python-dev \
	python-setuptools \
	python-pip \
	libmysqlclient-dev \
	supervisor

RUN \
  apt-get install -y nginx && \
  rm -rf /var/lib/apt/lists/*

WORKDIR 'var/www/html/django_production/django_rog'

ADD requirements.txt .

RUN pip install -r requirements.txt

COPY django_gunicorn_supervisor.conf /etc/supervisor/conf.d

COPY default /etc/nginx/sites-available/

COPY . .

#RUN chmod 777 /var/www/html/django_production/django_rog/django_gunicorn_supervisor.conf
#RUN chmod 777 /var/www/html/django_production/django_rog/django_gunicorn_service
#RUN chmod 777 /etc/supervisor/conf.d/django_gunicorn_supervisor.conf
#RUN chmod 777 -R /var/www/html/django_production/django_rog/run

#CMD ["python", "manage.py", "makemigrations"]

#CMD ["python", "manage.py", "migrate"]
#CMD ./django_gunicorn_service
#CMD ["gunicorn", "--bind", ":3000", "django_rog.wsgi:application"]
#CMD ["service","supervisor","start"]
#CMD ["service","nginx","start"]
#CMD ["nginx"]
#RUN service nginx start
CMD ["supervisord","-n"]
#CMD ["supervisord","-n"]
#CMD ["supervisorctl","restart","all"]
#CMD ["/usr/bin/supervisord"]


EXPOSE 8000
EXPOSE 443
