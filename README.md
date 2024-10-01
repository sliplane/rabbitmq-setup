# Sliplane RabbitMQ Setup

This repo is an example on how to use RabbitMQ with a client on Sliplane

It consists of two parts:

1. A RabbitMQ container that runs the RabbitMQ server
2. A sample Go application that publishes messages to the RabbitMQ server

## RabbitMQ Server

The server's dockerfile is in `rabbitmq.Dockerfile`, the configuration is in `rabbitmq.conf`.

## Sample Application

The application's dockerfile is in `sample-app/Dockerfile`. It builds a small webserver that listens on port 8080 for requests and publishes messages to the RabbitMQ server.

## Creating Sliplane Services

First, create a new service for the RabbitMQ server:

Important settings:

- Dockerfile Path: `rabbitmq.Dockerfile`
- Context Directory: `.`

Select a public http service if you want to be able to access the RabbitMQ management UI. It will be protected by the username and password you set in the environment variables below.

Environment Variables:

- SEED_USERNAME: `pick a username`
- SEED_USER_PASSWORD: `pick a password`
- PORT: `15672`

**If you don't set these environment variables the deployment will fail.**

Now, create a new service for the sample application:

Important settings:

- Dockerfile Path: `sample-app/Dockerfile`
- Context Directory: `.`

Environment Variables:

- RABBITMQ_URL: `amqp://username:password@rabbitmq:5672/`
- PORT: `8080`

Make sure to change the username and password to the ones you set in the RabbitMQ server service. The host is the name of the RabbitMQ service you created earlier. If you named it `rabbitmq` you can just use `rabbitmq` as the host! This is internal docker networking and will not be exposed outside of your server.

## Support

If you need any help getting started, please write us at support@sliplane.io!
