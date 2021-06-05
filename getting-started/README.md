# Getting started on Tensorflow using Docker
Reader is assumed that they have Docker installed on their PC. This setup is based on Windows 10 and
Docker in WSL 2. As of time of writing, the version of Docker is 20.10.6 build 370c289, and docker-compose
is 1.29.1 build c34c88b2.

## Requirements
Download the Docker image of tensorflow. To do so, check the official Docker image at hub.docker.com/r/tensorflow/tensorflow.
You can also search for tensorflow by ```docker search tensorflow```.  Now run ```docker pull tensorflow/tensorflow``` for
the latest version of tensorflow on Docker.

## Setting up and running Dockerfile and docker-compose
In reality, setting up docker-compose is not necessary for this example since this is running single container, but
for the simplicity sake, we will setup both Dockerfile and docker-compose. Create a simple hello.py on the same
directory where both Dockerfile and docker-compose.yaml will be
```Python
print("hello, tensorflow!")
```
Now create a Dockerfile (without any extension) with the following:
```Dockerfile
FROM tensorflow/tensorflow

WORKDIR usr/app

COPY hello.py .

CMD ["python", "hello.py"]
```
At this point you can build docker image by ```docker run <username>/hellotensor .``` and then run the container by
```docker run <username>/hellotensor``` (don't do it just yet). But we're going to add docker-compose to run for us:
```
version: "3"
services:
  tensorflow:
    build: .
```
Now type in ```docker-compose up``` and your container should be created and exited with "Hello, tensorflow" and output
value of 0 to indicate success. You can remove the running container by ```docker-compose down```.

## How do I run jupyter-notebook on Docker?
Don't. Or, try not to. The author has personal distaste and bias against jupyter notebook. In all honesty, there's 
nothing wrong with running jupyter on docker container, but at this point, why would you go through all the hassle to
run jupyter notebook on Docker container? Having said that, this is how you would run jupyter on Docker container
```
docker run -it --rm -v $(realpath ~/tensorflow/getting-started):/tf/getting-started -p 8888:8888 tensorflow/tensorflow:latest-jupyter
```
Once you run the command, it should give you an output with a token. Copy that and go to your browser and type "localhost:8888".
It should prompt you to enter password or token. Copy and paste the token onto the browser and you should have access
to your "getting-started" folder. 