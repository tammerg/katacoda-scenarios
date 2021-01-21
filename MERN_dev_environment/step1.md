In our first step, we are going to validate that the environment we loaded up is what we wanted! 

Let's go ahead and check our versions of Ubuntu and Docker by entering the following commands:

```bash
lsb_release -a
```{{execute}}

You will be greeted with a message letting you know "No LSB modules are available." That isn't important.

On the "Description" line you will see we are running on `Ubuntu 18.04 LTS`. Next run:

```bash
docker version
```{{execute}}

Great, let's move on to setting up our Dockerfile