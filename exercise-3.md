## Exercise 3 – Persistent Storage

### Task 1 - Create a Docker Volume
Create a volume called test1
```
docker volume create --name test1
```

Verify if you can see the volume
```
docker volume ls
```

Create a container and mount the volume
```
docker run -it -v test1:/www/website ubuntu:14.04 bash
```

Inside the container change the directory to `/www/website`  

Create a file called `test.txt` inside the `/www/website` directory.  
Exit the container without stopping it by pressing `CTRL + p + q`  

Commit the updated container as a new image and call it `test:1.0`
```
docker commit <container id> test:1.0
```
Create another container using your newly created image and run the `bash` command.  
Inside this container, verify that the `/www/website` directory exists, but does not contain any files.  

Exit the container.

### Task 2 - Finding your volume

Find the volume you've created on the docker host.
```
docker volume inspect test1
```
The `Mountpoint` field contains the path to your volume.  

Elevate your privileges to root, by typing `sudo -i`  

Change directory into the volume path (`/var/lib/docker/volumes/...`).  
Run `ls` and verify you can see the `test.txt` file you've created earlier.  

Create another file called `test2.txt`.  
Exit from the root shell, by typing `exit`.  

Use `docker exec` to get back into the shell of your first container.
```
docker exec -it <container id> bash
```
Inside the container change directory into `/www/website`.  

Do you see the `test2.txt` file?
