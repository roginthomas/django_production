FROM ubuntu:18.04

RUN apt-get update && \
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

RUN apt-get install nginx -y

WORKDIR 'usr/apps/django_production/django_rog1'

ADD requirements.txt .

RUN pip install -r requirements.txt

COPY django_gunicorn_supervisor.conf /etc/supervisor/conf.d

COPY default /etc/nginx/sites-available

COPY . .

RUN chmod 777 /usr/apps/django_production/django_rog1/django_gunicorn_supervisor.conf
RUN chmod 777 /usr/apps/django_production/django_rog1/django_gunicorn_service
RUN chmod 777 /etc/supervisor/conf.d/django_gunicorn_supervisor.conf
RUN chmod 777 -R /usr/apps/django_production/django_rog1/run

CMD ["python", "manage.py", "makemigrations"]

CMD ["python", "manage.py", "migrate"]

#CMD ["gunicorn", "--bind", ":5000", "django_rog1.wsgi:application"]
#CMD ["service","supervisor","start"]
CMD ["service","nginx","start"]
#CMD ["supervisord","-n"]
CMD ["/usr/bin/supervisord"]