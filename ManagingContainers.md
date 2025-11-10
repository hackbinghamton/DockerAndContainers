We'll now review a few more tools useful for managing images and containers.

# Images
We can pull versions of an image using `docker pull <repository>:<tag>`. The default is `latest` (which often, but not always, means the latest version), but we can view other available versions by visiting Docker Hub.

We can also pull *specific* versions using its digest—a hash of the contents. You can list digests with `docker image ls --digests`, and pull with `docker pull <repository>@<digest>`.

# Containers
The `--detach` flag will run an image in the background.

The `--name` flag sets 

The `-p <host-port>:<container-port>` flag opens certain ports on your device and redirect any connections to them into the container. This is useful for web servers, but be careful, as Docker will usually ignore your firewall configuration.

## Starting programs
There are three subtly different ways of telling a container where to start execution:
- `ENTRYPOINT` instruction in the Dockerfile: A default command that cannot be overridden after the image creation.
- `CMD` instruction in the Dockerfile: A default command, but one that can be changed during deployment.
- a command-line argument: the last argument to `docker run` will override the `CMD` instruction if used.

## Connecting to containers
- Try running `docker run --detach alpine sh -c "while true; do echo running; sleep 1; done"`: this will create an container that keeps running in the background, executing a simple command in a loop. Check that it exists with `docker container ls`.
- Now, try running `docker attach <container-name>`—you should start getting output. Close the container with `Ctrl-C`
- But suppose we want to run another command—first, start the container detached again. Now, run `docker exec -it <container-name> sh`. You can poke around the image as you like, and exit with `Ctrl-D`, and your main task should keep running in the background until you stop or kill it.
