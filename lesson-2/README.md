## Creating a node application

```dockerfile
# Specify the base image
FROM node:alpine

# Download and install dependencies
WORKDIR /usr/app/simpleweb
COPY ./package.json ./
RUN npm i
COPY ./ ./

# Bootstrap command
CMD ["npm", "start"]
```

### `WORKDIR /usr/app/simpleweb`

Changes the working directory in the container to point to the mentioned directory

### `COPY ./package.json ./`

> copy [**`from directory in your computer`**] [**`to directory in the container`**]

### Linking the ports

**`docker run -p 5000:5000 paul58914080/sampleweb:latest`**

> -p [**`local machine's port`**]:[**`docker machine's port`**]