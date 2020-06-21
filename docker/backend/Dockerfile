# Get the last python image version and update all the repositories
FROM python
RUN apt-get update && apt-get install -y wget && apt-get clean

# Install dockerize to avoid startup problems (waiting for DB to start)
ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz -O - | tar -C /usr/local/bin -xzv

# Set the external path for the docker container
ARG PROJECT_EXTERNAL_PATH=backend/src/

# Prepare work directory
RUN mkdir backend
WORKDIR backend

# Install all the requirements
ADD ${PROJECT_EXTERNAL_PATH}/requirements.txt /backend/
RUN pip install --upgrade pip && pip install -r requirements.txt

##Load source code from the repository or local to the container
COPY ${PROJECT_EXTERNAL_PATH}/ /backend/

# Load executors
COPY docker/backend/post_deploy.sh /backend/

# Make sure scripts are in unix style
RUN apt-get install dos2unix
RUN dos2unix ./post_deploy.sh
