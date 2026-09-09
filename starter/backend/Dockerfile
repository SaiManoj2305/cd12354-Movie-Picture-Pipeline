FROM public.ecr.aws/docker/library/python:3.10-alpine@sha256:6e67d897508774ad8f2250bbf0c414e029d3bc612b565017fba334b6193a798d

RUN adduser -u 1000 -D app

RUN apk update && \
  apk add \
  pcre \
  pcre-dev \
  build-base \
  gcc \
  linux-headers \
  openssl \
  libffi-dev \
  && pip install pipenv

WORKDIR /app

COPY Pipfile* /app/
RUN pipenv install --system --skip-lock

COPY . /app/

RUN chown -R app:app /app

USER app

EXPOSE 5000

CMD ["gunicorn", "--bind", "0.0.0.0:5000", "wsgi:app"]