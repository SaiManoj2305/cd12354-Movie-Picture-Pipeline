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
    && pip install --no-cache-dir pipenv gunicorn

WORKDIR /app

COPY Pipfile* /app/
RUN pipenv install --system --deploy --dev --skip-lock || pipenv install --system --skip-lock

# Ensure gunicorn is in the system Python packages
RUN pip install --no-cache-dir gunicorn

COPY . /app/

RUN chown -R app:app /app

USER app

ENV PATH="/home/app/.local/bin:/usr/local/bin:${PATH}"

EXPOSE 5000

CMD ["python", "-m", "gunicorn", "--bind", "0.0.0.0:5000", "wsgi:app"]