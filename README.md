# Counter API with Python and Flask

This repo contains files needed to create an API using Python and Flask, in order to count webpage hits. The application is bundled into a container and deployed to a kubernetes cluster. The backend database is Redis.

# API functionality

Description: Retrives number of hits for the current deployment.

Request:       `GET /`

Response:     `HTTP/1.1 200 OK`
`Holla! we have hit <n> times`

### Details

The app is written in Python, using Flask framework 

 - `app.py` is the actual app code
 - `requirements.txt` are the dependencies required to run the app
 - `Dockerfile` is used to build docker container
 
 ### Building/testing steps

Clone this repository:
<br>
`git@github.com:Sushant75/count-app.git`

Go to the newly created directory
`cd count-app`

Build and tag your docker image

    $ docker build -t <docker_hub_id>/<image_name> . 

Make sure to push the image to docker hub:

Use this command to login to the docker hub:

    $ docker login

Now run this command to push the newly made docker image to your docker hub repository:
    
    $ docker push <docker_hub_id>/<image_name>

You can test your application and its dependency (Redis) using docker-compose.

    We will make use of docker-compose to build our app. Docker compose will create a default network in which we will deploy our application and database server.
    
    Use this command to deploy your app in docker-compose:
    
    $ docker-compose up -d

    Use this command to check the status of your deployed containers:
    
    $ docker-compose ps
    
    Hit the app bu using curl or access via internet by browsing <localhost> :
    

    $ curl localhost
    Holla! we have hit 1 times.
    
    $ curl localhost
    Holla! we have hit 2 times.
    
    $ curl localhost
    Holla! we have hit 3 times.

 # Deployment our app on minikube

 <p> Now we will deploy our app on k8s by using minikube</p>

 ## Use this command to start the minikube cluster

 *<p>minikube start</p>*

 <b>
 
 <p>Thereafter, run this command to make sure that minikube cluster is up and running</p>

 *<p>minikube status</p>*

<br>

<p>Get into the 'k8s' directory</p>

*<p>cd k8s</p>*

<br>

<p>Run this command to run the deployment.yml template. It will create a deployment that will create 4 pods. 3 pods that will gather our application app and 1 pod that will gather our redis database.<p>

*<p>kubectl apply -f deployment.yml </p>*
<br>

<p> Now, use this command to get all pods</p>
<br>

*<p>kubectl get pods</p>*
<br>
<p>You will see that all pods with running status. Now, we will create a service to abstract the network access to your application's pods. Run this command to run the services.yml template. It will create a service.</p>

*<p>kubectl apply -f services.yml </p>*

<br>
<p> Now, use this command to get all services</p>
<br>

*<p>kubectl get svc</p>*

<br>
<p>You will see that all services with running status.</p>
<br>
<p>Now, we have the "external port", but we still need to find the  external IP. Minikube provides a utility we can use to easily access the Service. Use this command to get the port and ip of the service and hit that ip with the port provided with this command</p>
<br>

*<p>minikube service  <app_name with type Load Balancer> --url</p>*

<br>

<p>You will get this response</p>

*<p>Holla! we have hit <n> times.</p>*

 # Deployment the web app on EKS Cluster

 








