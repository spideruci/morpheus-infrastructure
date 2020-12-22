FROM python:3.8-slim AS compile-image
RUN apt-get update
RUN apt-get install -y --no-install-recommends build-essential gcc git

WORKDIR /app
RUN git clone https://github.com/kajdreef/spidertools .
RUN git checkout v0.1.0
RUN python -m venv /app
ENV PATH="/app/bin:$PATH"
RUN pip install .


FROM python:3.8-slim
RUN mkdir /usr/data/
WORKDIR /app
COPY --from=compile-image /app /app
ENV PATH="/app/bin:$PATH"

ADD requirements.txt .
RUN python -m pip install -r requirements.txt
ADD gunicorn_config.py .

ENTRYPOINT ["gunicorn", "--config", "gunicorn_config.py", "spidertools.runners.server_cli:create_app('/usr/data/research.sqlite')"]