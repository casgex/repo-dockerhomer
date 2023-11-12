# Static website for my homeservers

### Reason
I will configure a locally hosted static webserver which will run on a docker image, to configure a user friendly website for my future homelab and self hosted systems.

### Source
The Homelab website used is Homer from bastienwirtz(https://github.com/bastienwirtz/homer).

## Step-by-step setup

In this part I will document, for myself, how I configured Homer. This is onyl for learning purposes and protocoll for the future. It also functions as a Disaster Recovery if I have to re-do these containers in the future.

### Prerequisits for Homer

Download Ubuntu und Virtualbox and install them on your device;

Ubuntu: https://ubuntu.com/download/desktop

VirtualBox: https://www.virtualbox.org/wiki/Downloads

### Step 1: Create directories in ~ folder

We need to create a few directories first. For this make sure you're in the home directory of the right user.

Create the genereal Docker directory *docker* with **`mkdir docker`**

Change into the created directory with **`cd docker`**

Create the Dockerimage specific directory called *homer* with **`mkdir homer`**

Change into the *homer* directory with **`cd homer`**

Create the *data* directory with **`mkdir data`**

### Step 2: Create the .yaml file
This is the code that is responsible for the docker image to be deployed and running.

First create the file with **`touch docker-compose.yml`**

After creating the file itself, open it up with **`nano docker-compose.yml`** and copypaste the following code into it:
```
---
version: "2"
services:
  homer:
      image: b4bz/homer
      container_name: homer
      volumes:
        - /home/casimiro/docker/homer:/www/assets
      ports:
        - 8092:8080
      #environment:
      #- UID=1000
      #- GID=1000
      restart: unless-stopped
```

*Change ports accordingly, here we use 8092 to access the website*

### Step 3: Install docker-compose
To use docker-compose we first need to install it on our Ubuntu device. For this we use the command **`sudo apt install docker-compose`** and confirm with **y**.

### Step 4: Run the website with docker-compose
Now we are ready to launch our locally hosted website. First make sure you are in the same directory as the .yaml file. Then start up docker with the command **`sudo docker-compose up -d`**.

### Step 5: Test your docker website
Open up a browser and type in your IP address from the vm running the docker file. Add **`8092`** (the port given in the yaml file) to the end and you should now be able to connect to the website.

#test