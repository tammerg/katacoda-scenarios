The first thing we should do is cover what the status of our project is, and where we want to go.

We have a MERN application that doesn't run because we have none of the technologies installed, and we want to be able to run that same application without having to make any installs. Sounds like quite the problem.

Here comes Docker with the solution. We will create two seperate containers, one for our frontend client and one for our backend server. That will allow us to have the necessary technologies to run our app. Let's get started.

```bash
cd client
```{{execute}}

We first need to create a new Dockerfile:

```bash
touch Dockerfile
```{{execute}}

Now we need to open it:

```bash
Dockerfile
```{{open}}

Copy the following code into your Dockerfile, then we will cover what we entered:

<pre class="file" data-filename="file" data-target="append">
FROM node:14-slim

WORKDIR /usr/src/app

COPY ./package.json ./
COPY ./yarn.lock ./

RUN yarn install

COPY . .

EXPOSE 3000

CMD ["yarn", "start"]
</pre>

