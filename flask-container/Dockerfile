FROM ubuntu:20.04
LABEL maintainer="ErikJJohansson"

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

RUN apt-get update -y && apt-get install -y python3-pip
RUN apt-get install -y git

# SHA will change when there is a new commit
ARG SHA=$(curl -s 'https://api.github.com/repos/ErikJJohansson/cloudresume-frontend/commits' | grep sha | head -1)
RUN SHA=${SHA} \
    git clone https://github.com/ErikJJohansson/cloudresume-frontend.git /app/templates

#RUN cp -r cloudresume-frontend /app

# We copy just the requirements.txt first to leverage Docker cache
#COPY ./requirements.txt /app/requirements.txt
#COPY ./app.py /app
ADD . /app/

WORKDIR /app

RUN /bin/bash -c "pip3 install --no-cache-dir -r requirements.txt"

EXPOSE 5000

CMD ["gunicorn", "-b", "0.0.0.0:5000", "wsgi:app"]