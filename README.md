# Deploying-application-in-a-stack-Docker

When running Docker Engine in swarm mode, you can use docker stack deploy to deploy a complete application stack to the swarm. The deploy command accepts a stack description in the form of a Compose file.

Steps to deploy an application as a stack-

```

1. Drain the worker nodes in the swarm cluster to make sure the registry service runs on the manager node
$ sudo docker node ls

2. Use the following command to drain the worker nodes:
$ sudo docker node update --availability drain hostname_Worker_Node
Note: Replace hostname_Worker_Node with the HOSTNAME copied in previous step

3. Start the registry as a service on your swarm
$ sudo docker service create --name registry \
> --publish published=5000,target=5000 registry:2

4. List the running services to check the status of registry service
$ sudo docker service ls

5. Check if registry service is working with curl
$ curl http://localhost:5000/v2/

6. Create a directory for the project
$ mkdir stackdemo
$ cd stackdemo

7. Create a file called app.py in the stackdemo directory. Use the following command to create a project file with the code in this repo:
$ nano app.py

8. Create a file called requirements.txt with the code in this repo
$ nano requirements.txt

9. Use the following command to create a Dockerfile with the code in this repo::
$ nano Dockerfile

10. Use the following command to create the docker-compose.yml file with the code in this repo:
$ nano docker-compose.yml

11. Use the following commands to install docker-compose:
$ sudo curl -L "https://github.com/docker/compose/releases/download/\
> 1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ docker-compose --version

12. Start docker-compose using the following command:
$ sudo docker-compose up -d

13. Use the following commands to check whether the app is running 
$ sudo docker-compose ps
$ curl http://localhost:8000

14. Bring the application down
$ sudo docker-compose down --volumes

15. Push the application to the registry
$ sudo docker-compose push

16. Use the following command to create the stack docker stack deploy:
$ sudo docker stack deploy --compose-file docker-compose.yml stackdemo

17. Check if the stack is running
$ sudo docker stack services stackdemo

18. Test the app again with curl command
$ curl http://localhost:8000
$ curl http://ip-172-31-26-147:8000

19. Use the following command to bring the stack down:
$ sudo docker stack rm stackdemo

```










