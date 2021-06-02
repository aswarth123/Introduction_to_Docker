# Introduction to Docker
This repo deals with the building of a flask app then containerise it using docker and deploying the resulting docker image onto heroku. The following instructions assume that you have already installed docker and heroku-cli if not then follow the instructions in the pre-requisites section for doing so.

## Pre-requisites
### Docker
Follow the steps 1 and 2 and then check your installation by doing step 3 in the following [Link](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04).
### Heroku-cli
For heroku-cli installation in ubuntu 16+ versions use the following command
``` 
sudo snap install --classic heroku
```
## Procedure
### STEP 1:
Clone this repo using the following command:
```
git clone https://github.com/aswarth123/Introduction_to_Docker.git
```
and then cd to this repo using ```cd Introduction_to_Docker```
This repo has the following directory structure:
```
Introduction_to_Docker
      ---templates
         ---index.html
      ---Dockerfile
      ---LICENSE
      ---README.md
      ---app.py
      ---requirements.txt
```
### STEP 2:
Now we will create the Docker image of the app in the following manner:
```
docker image build -t intro_to_docker .
```
The ```-t``` flag is used here to give the name of the newly created image.
Note: This command may take 10-15 mins to execute depending upon your internet connectivity speed.

After the execution of the above command use 
```
docker image ls
``` 
command to list out all the docker images you have and now you will be able to see the ```intro_to_docker``` image as well.

### STEP 3:
In this step we will be running our docker image using the following command 
```
docker run -p 5000:5000 -d intro_to_docker
```
Now click on this [link](http://localhost:5000/) to see whether the docker app is running in your local machine and you will be able to see the ```Hello world to Docker``` on your screen.

### STEP 4:
Now stop the container running at Localhost at port 5000 using the following commands:
```
docker container stop <container id>
docker system prune
```
Note: The container id you will get from the output of the previous commands that you executed.
### STEP 5:
This step deals with the deployment of your docker container onto heroku.
#### Login
At first you need to login to heroku using the following command 
```
heroku container:login
```
This would open the browser and prompt you to log in with your Heroku credentials. If you succeed in logging, you will receive a message “Login Succeeded”.
#### App creation
For a creating a heroku app use the following command and give it a name.
```
heroku create <name-for-your-app>
```
After executing the following command you will get the following link as an output which is a link to your heroku app that you created.
```https://<name-for-your-app>.herokuapp.com/```

#### Pushing the container to heroku
Use the below command to do so.
```
heroku container:push web --app <name-for-your-app>
```
Note: The succesful execution of this command may take some time (~20 mins) depending on your internet connectiviy.

#### Deploying the app
At this point, the docker container is pushed to Heroku, but not deployed or released. The following command would deploy the container:
```
heroku container:release web --app <name-for-your-app>
```
Now, the app is released and is running on Heroku and you can view it on the below link.<br>
```https://<name-for-your-app>.herokuapp.com/```

Thus, we successfully dockerized and deployed our Python Flask app onto Heroku.

