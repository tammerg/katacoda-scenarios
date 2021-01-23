To dockerize a MERN application...we first need a...MERN application!

Let's go ahead and clone down a basic MERN application we can work with

```bash
git clone https://github.com/tammerg/movies-app.git
cd movies-app
ls -a
```{{execute}}

Excellent! Now that we have cloned the project, we can start our server and be on our way!

```bash
cd server/
node index.js
```{{execute}}

Hmmmm...Node doesn't seem to be installed on this environment. Let's see if other technologies we would need are installed, like MongoDB:

```bash
mongod
```{{execute}}