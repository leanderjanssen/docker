## Exercise 1 – Running a container

### Task 1 - The obligatory 'hello world'
On your terminal type:
```
docker run ubuntu:14.04 echo "Hello World"
```

### Task 2 - Run another container
Then type:
```
docker run ubuntu:14.04 ps -ef
```
Observe the output. And notice the much faster execution time. This is due to the fact that the image is now available locally. Also notice that within the container the `ps -ef` command was running as PID 1

### Task 3 - List running containers
```
docker ps
```
There should not be running any active containers.

### Task 4 - List both running and stopped containers
```
docker ps -a
```
Now you should all running and stooped containers.

### Task 5 - The immutable container
Create another container.
```
docker run -i -t ubuntu:14.04 bash
```
Notice that the prompt has changed to something like `root@a23213...:/#`  
Inside this container create a file called `testfile`
```
touch testfile
```
Run `ls` to verify that the file has been created.  

Exit the container by typing:
```
exit
```

List the running containers again and notice how there is nothing running

Create another container using the same `docker run` command as in the beginning of this task.  

Run `ls` again and try to find the file `testfile` that you created previously.  

Did you find it? Why not?

### Task 6 - Run a container in detached mode
Create a container doing 50 pings.
```
docker run -d ubuntu:14.04 ping 127.0.0.1 -c 50
```
List the running containers using `docker ps`  
You should see a container running that is pinging 127.0.0.1.

Wait for about a minute and run `docker ps` again.  
You'll notice that the container has stopped.  

Why do you think it has stopped?

### Task 7 - Exposing ports to the outside world
Create a container running the nginx webserver
```
docker run -d -p 80:80 --name nginx nginx:alpine
```
Open a webbrowser on your laptop and enter the public ip of your AWS instance in the url field, e.g. `http://52.208.236.81`  

nginx should welcome you.  

Execute an additional proces in a running container:
```
docker exec -it nginx /bin/sh
```
Notice how the prompt changes to `/ #`  
You're now inside the container that runs nginx.  
Try to run the `ps -ef` command and notice the output.  

Exit out of the container by typing `exit`  
Is the container still running? Why is that?

Show container logs:
```
docker logs nginx
```
You should see the logs of the `nginx` container.  
Notice the log entries of you accessing the nginx webserver with your browser.

### Task 8 - Cleaning up

Stopping the nginx container
```
docker stop nginx
```
Verify that the container has indeed stopped.

Try to start a container again:
```
docker start nginx
```
And verify if it indeed runs again.

Remove the nginx container:
```
docker rm nginx
```
Oops, that didn't work.  

Let's try it with a bit of force:
```
docker rm -f nginx
```

Cleaning up all stopped containers using a single command:
```
docker rm $(docker ps -aq)
```
