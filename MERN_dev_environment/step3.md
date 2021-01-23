The first thing we should do is cover what the status of our project is, and where we want to go.

We have a MERN application that doesn't run because we have none of the technologies installed, and we want to be able to run that same application without having to make any installs. Sounds like quite the problem.

Here comes Docker with the solution. We will create two seperate containers, one for our frontend client and one for our backend server. That will allow us to have the necessary technologies to run our app. Let's get started by checking where we are:

```bash
pwd
```{{execute}}

You'll see we are in `/root/movies-app/server`

We can start by first getting our server setup. Let's create a new Dockerfile:

```bash
touch /root/movies-app/server/Dockerfile
```{{execute}}

Now we need to open it in our editor:

```bash
/root/movies-app/server/Dockerfile
```{{open}}

**Note**: If the above command does not open /server/Dockerfile, manually navigate to the newly created Dockerfile in the file tree on the right hand side of the screen.

Copy the following code into your Dockerfile, then we will cover what we entered:

<pre class="file" data-filename="/root/movies-app/server/Dockerfile" data-target="replace">
FROM node:14-slim

WORKDIR /usr/src/app

COPY ./package.json ./
COPY ./yarn.lock ./

RUN yarn install

COPY . .

EXPOSE 5000

CMD ["index.js"]
</pre>

Great! Now let's quickly take a look at the code we entered.

First, we chose the base image from which we would like to build `FROM`. In this case we chose `node:14-slim`. The `-slim` tag denotes we are obtaining an image that contains only the necessities to run `node`.

Next we set our `WORKDIR` or working directory to be `/usr/src/app`. This directory is where `RUN`, `CMD`, and `COPY` instructions will execute. So, we then copy all of the contents of `package.json` and `yarn.lock` into our `WORKDIR` via `./`.

We can then run `yarn install`. After its complete we `COPY` all of the contents from our src `.` and get it all copied to our container `.`. By using the `EXPOSE` instruction we can let Docker know the container needs to listen on the exposed port when we run our dockerfile. Finally, just like we would do normally we use the `CMD` or command instruction to run `index.js`.

This Dockerfile will properly build our backend server for use! The frontend client is going to look extremely similar, with the only changes being the EXPOSEd port and the CMD.

```bash
cd ..
sleep 3
pwd
cd client
sleep 3
touch /root/movies-app/client/Dockerfile
```{{execute}}

Due to some browser limitations, let's close the Dockerfile we just completed before we open our newly created one.

```bash
/root/movies-app/client/Dockerfile
```{{open}}

**Note**: If the above command does not open /server/Dockerfile, manually navigate to the newly created Dockerfile in the file tree on the right hand side of the screen.

Finally, copy the following:

<pre class="file" data-filename="/root/movies-app/client/Dockerfile" data-target="replace">
FROM node:14-slim

WORKDIR /usr/src/app

COPY ./package.json ./
COPY ./yarn.lock ./

RUN yarn install

COPY . .

EXPOSE 3000

CMD ["yarn", "start"]
</pre>

Now let's build our Docker images from these newly made `Dockerfiles`. Run the following commands:

```bash
cd ..
sleep 3
docker build -t react-client ./client/
```{{execute}}

The build process can take anywhere from a few seconds to a few minutes. Once complete you will see a line like the following:

```bash
Successfully tagged react-client:latest
```

Once complete, go ahead and build the backend image:

```bash
docker build -t app-server ./server/
```{{execute}}

When this is complete you should see a line like the following:

```bash
Successfully tagged app-server:latest
```

Anddddddd we're done! Actually...we need to complete one more step. We are going to use `docker-compose` to run our two images in tandem, and provision us an instance of `MongoDB` at the same time. See you in our final step!