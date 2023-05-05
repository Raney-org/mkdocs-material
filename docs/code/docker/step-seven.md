---
tags:
  - DOCKER
  - TUTORIAL
---

# Step 7-Committing Changes in a Container to a `Docker` Image

When you start up a `Docker` image, you can create, modify, and delete files just like you can with a virtual machine. The changes that you make will only apply to that container. You can start and stop it, but once you destroy it with the `#!shell docker rm` command, the changes will be lost for good.

This section shows you how to save the state of a container as a new Docker image.

After installing Node.js inside the Ubuntu container, you now have a container running off an image, but the container is different from the image you used to create it. But you might want to reuse this Node.js container as the basis for new images later.

Then commit the changes to a new Docker image instance using the following command.

``` sh
docker commit -m "What you did to the image" -a "Author Name" container_id repository/new_image_name
```

The `-m` switch is for the `commit` message that helps you and others know what changes you made, while `-a` is used to specify the author. The `container_id` is the one you noted earlier in the tutorial when you started the interactive Docker session. Unless you created additional repositories on [Docker Hub], the repository is usually your Docker Hub username.

For example, for the user `sammy`, with the container ID of `d9b100f2f636`, the command would be:

``` sh
docker commit -m "added Node.js" -a "sammy" d9b100f2f636 sammy/ubuntu-nodejs
```

When you commit an image, the new image is saved locally on your computer. Later in this tutorial, you’ll learn how to push an image to a `Docker registry` like [Docker Hub] so others can access it.

Listing the Docker images again will show the new image, as well as the old one that it was derived from:

``` sh
docker images
```

You’ll see output like this:

``` sh title="Output"
REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
sammy/ubuntu-nodejs   latest              7c1f35226ca6        7 seconds ago       179MB
...
```

In this example, `ubuntu-nodejs` is the new image, which was derived from the existing ubuntu image from Docker Hub. The size difference reflects the changes that were made. And in this example, the change was that NodeJS was installed. So next time you need to run a container using Ubuntu with NodeJS pre-installed, you can just use the new image.

You can also build Images from a `Dockerfile`, which lets you automate the installation of software in a new image. However, that’s outside the scope of this tutorial.

Now let’s share the new image with others so they can create containers from it.
