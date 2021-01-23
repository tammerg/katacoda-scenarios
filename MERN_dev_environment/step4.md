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
  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
</pre>

Wow! That seems like a lot, bit it is actually quite a bit of repetition. Let's start at the top. Our `services` are the 3 containers we would like to run, our `react-client`, `app-server`, and `mongo`. The first property in each of the services is the `image` we want to create the container based on. In this instance we use the two builds we made, `react-client` and `app-server`. 

For mongo, we use DockerHub to pull the `latest` version of `mongo`. What does the `latest` tag denote? Well, the `latest` tag will pull the current LTS version of an image from DockerHub

Next, with the `ports` option we expose and set the public ports for port binding. 

The only other difference between services is in our `react-client` container we use the `stdin_open: true` option to keep it open for requests after starting our environment. The last step for us is to set the `depends_on` option in `app-server` to `- mongo`. This is because our server needs to connect to MongoDB, we can specify this depends on so that `mongo` will start first. Well...thats it! Let's enter that final command at the root of `MERN_app_unsolved`:

```bash
docker-compose up
```{{execute}}