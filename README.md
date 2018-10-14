### Building and running Vue app development environment in Docker
Create Dockerfile for app:
```
FROM node:10-alpine

WORKDIR /usr/src/app

RUN npm install -g @vue/cli
```

Build node image and install @vue/cli globally:
```
$ docker-compose build
```

After installation, we will have access to the vue binary in command line so that we can create Vue project template inside our image:
```
$ docker-compose run --rm app vue create .
```

After that Vue project template is ready, we just need to add command to `docker-compose.yml` for starting development server automatically:
``` 
app:
    build: ./app
    command: npm run serve
    env_file:
      - .env
    volumes:
      - ./app:/usr/src/app
    ports:
      - '3000:3000'
```
Of course we can later change and adjust the paths in `docker-compose.yml` if we are going to add more microservices.
