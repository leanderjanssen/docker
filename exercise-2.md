## Exercise 2 – Building an image

### Task 1 - Making changes to a container
Create a container using the Ubuntu image
```
docker run -it ubuntu:14.04 bash
```

Update the package repository
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
Show the differences between the orginal image and the current state.
```
docker diff <container id>
```

### Task 2 - Building a new image
Save your container as a new image.
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
Verify that `vim` and `wget` are installed.
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

Try to show the difference on this container as well.
