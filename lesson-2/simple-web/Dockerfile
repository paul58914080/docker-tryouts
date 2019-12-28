# Specify the base image
FROM node:alpine
# Download and install dependencies
WORKDIR /usr/app/simpleweb
COPY ./package.json ./
RUN npm i
COPY ./ ./
# Bootstrap command
CMD ["npm", "start"]