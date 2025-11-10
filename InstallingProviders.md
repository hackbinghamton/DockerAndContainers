The easiest way to experiment with containers will be to use Docker's standard tools, available on all major PC operating systems.

Follow the instructions on the [docker website](https://docs.docker.com/get-started/introduction/get-docker-desktop/) to install Docker Desktop on your device. Check that it works by opening a shell and running `docker --version`.

> Most (though not all) containers are designed to run using the Linux kernel. On a Linux device, the docker engine uses the system's kernel, but on MacOS or Windows devices, some form of virtualization must be employed—either a full virtual machine or a translation layer like WSL.

If you are interested in diving deeper, you might also check out [podman](https://podman.io/docs/installation). The command-line interface should be compatible, but there might be some problems with edge cases.
