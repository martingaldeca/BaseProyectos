# base image
FROM node:10.15.0

# set working directory
RUN mkdir /frontend && chown node:node /frontend/
WORKDIR /frontend

# add `/frontend/node_modules/.bin` to $PATH
ENV PATH /frontend/node_modules/.bin:$PATH

# install and cache app dependencies
COPY --chown=node:node frontend/package.json /frontend/package.json
COPY --chown=node:node frontend/package-lock.json /frontend/package-lock.json
RUN npm install --quiet
RUN npm install -g @vue/cli
