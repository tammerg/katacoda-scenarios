In our first step, we are going to validate that the environment we loaded up is what we wanted! 

Let's go ahead and check our versions of Ubuntu and Docker.

We can start by checking which version of Ubuntu we are on by entering the following command:

```bash
lsb_release -a
```{{execute}}

You will be greeted with a message letting you know "No LSB modules are available." That isn't important.

On the "Description" line you will see we are running on `Ubuntu 18.04 LTS`. Next run the command:

```bash
docker version
```{{execute}}

You should see that we are running `Version: 19.03.13`. These are the basics of what we need to accomplish our goal.

Great, let's move on to setting up our Dockerfile