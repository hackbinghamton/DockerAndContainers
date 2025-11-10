Now that you have an orchestrator installed, we'll practice using existing containers, while reviewing a few key concepts.

First, we will pull the `hello-world` image.
Run `docker pull hello-world` (you might need to run as root). Check that it worked with `docker image ls`.

> Though the general command line interface is supposed to be agnostic—not preferring one company or resource over anothers—docker has certain defaults, which makes the above command work.

Now, lets create and run a container with `docker run hello-world`. This will initialize a container from the `hello-world` image, run a certain script inside the container, print its output, and then stop and destroy the container. Try `docker container ls`—there shouldn't be anything there!

For a longer-lived container, lets enter `docker run --interactive --tty alpine sh` (or the abbreviated `docker run -it alpine sh`)

> Alpine is an extremely lightweight version of linux, designed with container usage in mind. It is frequently used as the base for other images.
> Note that Alpine does not include the common Bash interpreter, but only a posix-compliant sh shell.

You should see your shell prompt change, as you're now running inside the container! Try poking around a bit—creating some files and running a few commands. Not that nothing you do inside the container should affect your host system, and any changes you make will be deleted when the container stops.

While the container is running, open another shell and run `docker container ls`. You should see exactly one entry, your currently open container.

Alpine includes the Alpine Package Manager under the `apk` program. Try using it to install some common packages (`apk add <package-name>`)—maybe `curl`, which you can use to check that your container has internet access.

You can exit the container by pressing `Ctrl-D`.
