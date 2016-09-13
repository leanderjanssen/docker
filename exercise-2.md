## Exercise 2 – Building an image

### Task 1 - Making changes to a container
Create a container using the Ubuntu image
```
docker run -it ubuntu:14.04 bash
```

Inside the container, update the package repository
```
apt-get update
```

Install some additional packages.
```
apt-get install -y wget
apt-get install -y vim
```

Exit the container by typing `exit`  

Find the container id using `docker ps -lq`  
Show the differences between the orginal image and the container.
```
docker diff <container id>
```

### Task 2 - Building a new image
Save your container as a new image, using the same container id as in Task 1.
```
docker commit <container id> myapp:1.0
```
Show the locally available images:
```
docker images
```
You should see the image you've just created.  

Create a container using your freshly baked image.
```
docker run -it myapp:1.0 bash
```
Inside the container, verify that `vim` and `wget` are installed.
```
which vim
which wget
```
Create another file inside your container.
```
touch testfile
```
Exit out from the container and lookup the container id.  
Commit the changes to a new image, use the tag `myapp:1.1`

Try to show the differences in this container as well.

### Task 3 - Create a Dockerfile
Create a new directory on your docker host
```
mkdir myimage
```
Change to the newly created directory, by typing `cd myimage`  
Create the `Dockerfile`, by typing `touch Dockerfile`  
Edit the Dockerfile and write the following lines:
```
FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -u wget
```
You can use `vim` or `nano` as your editor.  

### Task 4 - Build an image using a Dockerfile
Create an image using the Dockerfile you've just created.
```
docker build -t myimage .
```
Please notice the dot at the end of the command.  
And observe the output of the `build` command.  
Verify that you're image has been created.  
Verify that `wget` is installed.
```
docker run myimage which wget
```

### Task 5 - Please obey my cmd
Verify that you're still in the /home/docker/myimage directory.  
You can use the `pwd` command for this.
Add the following line to the end of your existing Dockerfile.
```
CMD ["ping", "127.0.0.1", "-c", "30"]
```
Build a new image, using the tag `myimage:1.0`  
Create a new container using this new image.  
Ping! Ping! What output did you get?
