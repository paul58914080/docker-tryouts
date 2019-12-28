# Specify the base image
FROM alpine
# Download and install a dependency
RUN apk add --update redis
RUN apk add --update gcc
# Bootstrap command
CMD ["redis-server"]