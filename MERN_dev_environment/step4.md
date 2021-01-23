Finally at the root of your project, create a `docker-compose.yml` file and enter the following:

```bash
touch /root/movies-app/docker-compose.yml
```{{execute}}


<pre class="file" data-filename="/root/movies-app/docker-compose.yml" data-target="append">
version: "3.4"
services:
  react-client:
    image: react-client
    stdin_open: true
    ports:
      - "3000:3000"
    networks:
      - movies-app

  app-server:
    image: app-server
    ports:
      - "5000:5000"
    depends_on: 
      - mongo
    networks:
      - movies-app

  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
    networks:
      - movies-app
    volumes:
      - mongo-data:/data/db

networks:
  movies-app:
    driver: bridge

volumes:
  mongo-data:
    driver: local
</pre>

Well...let's see if it works! Enter the following single command to fire up all of your images and provision a DB:

```bash
docker-compose up
```