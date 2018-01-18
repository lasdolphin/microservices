FROM python:2.7.14-alpine3.7

RUN apk update && \
    apk upgrade && \
    apk add build-base

WORKDIR /app
ADD . /app

RUN pip install -r requirements.txt

ENV POST_DATABASE_HOST post_db
ENV POST_DATABASE posts

ENTRYPOINT ["python", "post_app.py"]

