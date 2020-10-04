FROM python:3.8-alpine

RUN mkdir /app
WORKDIR /app
ADD requirements.txt /app
RUN pip3 install -r requirements.txt
ADD . /app


ENTRYPOINT ["gunicorn", "--config", "gunicorn_config.py", "hello_flask.wsgi:app"]