The first thing we should do is cover what the status of our project is, and where we want to go.

We have a MERN application that doesn't run because we have none of the technologies installed, and we want to be able to run that same application without having to make any installs. Sounds like quite the problem.

Here comes Docker with the solution. We will create two seperate containers, one for our frontend client and one for our backend server. That will allow us to have the necessary technologies to run our app. Let's get started by checking where we are:

```bash
pwd
```{{execute}}

You'll see we are in `/root/movies-app/server`

We can create a new Dockerfile with:

```bash
touch Dockerfile
```{{execute}}

Now we need to open it in our editor:

```bash
Dockerfile
```{{open}}

Copy the following code into your Dockerfile, then we will cover what we entered:

<pre class="file" data-filename="Dockerfile" data-target="append">
FROM node:14-slim

WORKDIR /usr/src/app

COPY ./package.json ./
COPY ./yarn.lock ./

RUN yarn install

COPY . .

EXPOSE 5000

CMD ["index.js"]
</pre>

Excellent! We provisioned a node container with none of the frills by adding the `-slim` option.

Next we set our WORKDIR and copied the contents of our `package.json` and `yarn.lock` into our WORKDIR.

We run `yarn install` and copy the subsequent contents into our WORKDIR. 

Because we would like to run this server on port 5000 we expose that port and then give the CMD of `index.js`. This Dockerfile will properly build our backend server for use! The frontend client is going to look extremely similar, with the only changes being the EXPOSEd port and the CMD.

```bash
cd ..
pwd
cd client
touch Dockerfile
```{{execute}}

Next:

```bash
Dockerfile
```{{open}}

Finally, copy the following:

<pre class="file" data-filename="Dockerfile" data-target="append">
FROM node:14-slim

WORKDIR /usr/src/app

COPY ./package.json ./
COPY ./yarn.lock ./

RUN yarn install

COPY . .

EXPOSE 3000

CMD ["yarn", "start"]
</pre>

Anddd we're done! Actually, we only need to do one more step. We are going to use `docker-compose` to run our two images in tandem, and provision us an instance of `MongoDB` at the same time. See you in our final step!