The first thing we should do is cover what the status of our project is, and where we want to go.

We have a MERN application that doesn't run because we have none of the technologies installed, and we want to be able to run that same application without having to make any installs. Sounds like quite the problem.

Here comes Docker with the solution. We will create two seperate containers, one for our frontend client and one for our backend server. That will allow us to have the necessary technologies to run our app. Let's get started.

```bash
cd client
```{{execute}}

We first need to create a new Dockerfile and open it in our editor.

```bash
touch Dockerfile
```{{execute}}{{open}}