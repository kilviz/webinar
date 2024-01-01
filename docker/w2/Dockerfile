FROM python

ENV PYTHONUNBUFFERED 1

RUN mkdir -p /src && \
    mkdir -p /src/public/static && \
    mkdir -p /src/public/media

WORKDIR /src/app

RUN git clone https://github.com/kilviz/webinar.git /src/app
RUN git checkout remotes/origin/main


RUN cp example.env .env

RUN pip install -r requirements.txt

RUN apt-get update && apt-get install ffmpeg libsm6 libxext6 -y

WORKDIR /src/app/backend
RUN python manage.py makemigrations
RUN python manage.py migrate

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]