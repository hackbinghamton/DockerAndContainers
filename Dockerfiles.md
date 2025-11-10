If your interests go beyond running other people's programs, you'll need to know how to use an OCI builder.

First, we need a program to *containerize*. Lets write a small script, `program.sh`:
```bash
#!/bin/sh
echo 'WORKING!'
cat myfile.txt
```
Make sure that this file is executable. You may have to run `chmod +x program.sh`.

And create a small file `myfile.txt` with the following contents:
```
Hello world! This is a file.
```

Now, we need to write a recipe for our image. Open a new file called `Dockerfile`. Our first example will be extremely simple, and we'll look at each line as we go:

`FROM alpine`: this tells our builder to use the `alpine` image as our base—any changes we make will be layered on top of alpine.
`WORKDIR /app`: this command doesn't change anything about the image, but tells certain following instructions to execute inside this directory in the image.
`COPY . .`: this command copies everything from our *build context* (where you run the build command on your host system) to our `WORKDIR`
`CMD /app/program.sh`: this sets the default behavior of our image.

Together, we have:
```
FROM alpine
WORKDIR /app
COPY . .
CMD /app/program.sh
```

Now, run `docker build .` Check your images with `docker image ls`—you should see one built a few seconds ago! Copy its id for the next step.

Use `docker history <image-id>` to see the steps used in the creation of your image—they should roughly match your `Dockerfile`

Finally, we can run our program with `docker run <image-id>`. Congratulations on making your first image!

Once you're done, clean up your image with `docker image rm <image-id>`.

# Additional Info
Run `docker build` with `-t <tag>` to add a tag to your image. You can also add a tag after building with `docker tag`

Try running `docker inspect <image-id>` to get a detailed look at the image contents.

You can use the `RUN` instruction to run commands during the build process. **Exercise**: Try installing some commands during the above build process, and use them in your `program.sh`.
