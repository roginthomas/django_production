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

WORKDIR 'var/www/html/django_production/django_rog1'

ADD requirements.txt .

RUN pip install -r requirements.txt

COPY django_gunicorn_supervisor.conf /etc/supervisor/conf.d

COPY default /etc/nginx/sites-available/

COPY . .

CMD ["supervisord","-n"]

EXPOSE 5000
EXPOSE 443
