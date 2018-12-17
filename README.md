
# What is this container?

This container contains a docker-compose.yml with which you start the images of your app and the configuration files

## Run your app via docker-compose

Example `docker-compose.yml`:


```console
version: '3'

services:

  mongo:
    image: mongo
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example
    ports:
      - 27017:27017

  backend:
    image: reportaongd/backend:latest
    depends_on:
      - mongo
    volumes:
      - /my/own/datadir:/var/lib/backend/files
    ports:
      - 3000:3000
    env_file:
      - backend_env.list

  frontend:
    image: reportaongd/frontend:latest
    depends_on:
      - backend
    volumes:
      - /my/own/datadir:/var/lib/frontend/files
    ports:
      - 4200:80
    env_file:
      - frontend_env.list
```

Run docker `docker-compose up`, wait for it to initialize completely, and visit http://localhost:8080 .


## Accessing the Application

Currently, the default user and password is admin@admin.com/admin

## Environment Variables

When you start the docker-compose , you can adjust the configuration of the instance changing defautl values in backend-env.list and frontend-env.list file.

All those environment varibles can be overwriten in the file:


1. backend-env.list file:

### `DB_CONECTION`

	This variable sets the conection with mongo database 'mongodb://root:example@mongo:27017/'.

	user: root
	password: example

	@mongo is the name of the service of the docker-compose.yml file

	user and password are the same as in the docker-compose.yml file

### `MAIL_SERVICE`

	This sets the mail service with which the application sends emails.

### `MAIL_USER`

	This is the user mail of for MAIL_SERVICE

### `MAIL_PASSWORD`

	This is the password of mail for the MAIL_SERVICE

### `CLIENT_ID`

This variable sets the Client Id for the Oauth communication between Gong a Gong-Reporte.

### `CLIENT_SECRET`

This variable sets the Client Password for the Oauth communication between Gong a Gong-Reporte.


### `ACCESS_TOKEN_URI`

This variable sets the token for the Oauth communication between Gong a Gong-Reporte.

### `AUTHORIZATION_URI`

This variable sets the authorization for the Oauth communication between Gong a Gong-Reporte.

# License



