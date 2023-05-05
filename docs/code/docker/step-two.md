---
tags:
  - DOCKER
  - TUTORIAL
---

# Step 2 — Executing the `Docker` Command Without Sudo (Optional)

By default, the `docker` command can only be run the root user or by a user in the `docker` group, which is automatically created during `Docker`’s installation process. If you attempt to run the `docker` command without prefixing it with `sudo` or without being in the `docker` group, you’ll get an output like this:

``` shell
Output
docker: Cannot connect to the Docker daemon. Is the docker daemon running on this host?.
See 'docker run --help'.
```

If you want to avoid typing `sudo` whenever you run the `docker` command, add your username to the `docker` group:

``` sh
sudo usermod -aG `docker` ${USER}
```

To apply the new group membership, log out of the server and back in, or type the following:

``` sh
su - ${USER}
```

You will be prompted to enter your user’s password to continue.

Confirm that your user is now added to the `docker` group by typing:

``` sh
groups
```

``` shell title="Output"
sammy sudo docker
```

If you need to add a user to the `docker` group that you’re not logged in as, declare that username explicitly using:

``` shell
sudo usermod -aG docker username
```

The rest of this article assumes you are running the `docker` command as a user in the `docker` group. If you choose not to, please prepend the commands with sudo.

Let’s explore the `docker` command next.
