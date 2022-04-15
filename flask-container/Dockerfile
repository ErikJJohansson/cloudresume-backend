FROM python:3.8-alpine
LABEL maintainer="ErikJJohansson"

# install git
RUN apk add git

# SHA will change when there is a new commit
ARG SHA=$(curl -s 'https://api.github.com/repos/ErikJJohansson/cloudresume-frontend/commits' | grep sha | head -1)
RUN SHA=${SHA} \
    git clone https://github.com/ErikJJohansson/cloudresume-frontend.git /app/templates

#RUN cp -r cloudresume-frontend /app

# We copy just the requirements.txt first to leverage Docker cache
COPY ./requirements.txt /app/requirements.txt

WORKDIR /app

RUN pip install -r requirements.txt

COPY ./app.py /app/app.py

# configure the container to run in an executed manner
ENTRYPOINT [ "python" ]

CMD ["app.py"]