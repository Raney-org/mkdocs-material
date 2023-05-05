---
tags:
  - DOCKER
  - TUTORIAL
---

# Step 5 — Running a `Docker` Container

The `hello-world` container you ran in the previous step is an example of a container that runs and exits after emitting a test message. Containers can be much more useful than that, and they can be interactive. After all, they are similar to virtual machines, only more resource-friendly.

As an example, let’s run a container using the latest image of Ubuntu. The combination of the `-i` and `-t` switches gives you interactive shell access into the container:

``` sh
docker run -it ubuntu
```

Your command prompt should change to reflect the fact that you’re now working inside the container and should take this form:

``` sh title="Output"
root@d9b100f2f636:/#
```

???+ note
    Note the container id in the command prompt. In this example, it is d9b100f2f636. You’ll need that container ID later to identify the container when you want to remove it.

Now you can run any command inside the container. For example, let’s update the package database inside the container. You don’t need to prefix any command with sudo, because you’re operating inside the container as the root user:

``` sh
apt update
```

Then install any application in it. Let’s install Node.js:

``` sh
apt install nodejs
```

This installs Node.js in the container from the official Ubuntu repository. When the installation finishes, verify that Node.js is installed:

``` sh
node -v
```

You’ll see the version number displayed in your terminal:

``` sh title="Output"
v12.22.9
Any changes you make inside the container only apply to that container.

To exit the container, type exit at the prompt.
```

Let’s look at managing the containers on our system next.
