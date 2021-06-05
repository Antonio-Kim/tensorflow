# Basic image of tensorflow. This should've been downloaded alread
FROM tensorflow/tensorflow

# Setting up new work director inside the container
WORKDIR /usr/app

# Copy the hello.py code to the directory
COPY hello.py . 

# Run hello world
CMD ["python", "hello.py"]