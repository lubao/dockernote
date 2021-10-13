# Docker Note
Note for Docker Command

## Docker Run with PORT CPU MEM and overide ENTRYPOINT
```
sudo docker run -it -p 8080:80 --cpus=1 --memory=512m --entrypoint /bin/bash $DOCKER_IMAGE
```

## How to continue a Docker container which has exited
```
sudo docker start -a -i `sudo docker ps -q -l`
````
Explanation:
* __docker start__ start a container (requires name or ID)
  * -a attach to container
  * -i interactive mode
* __docker ps__ List containers
  * -q list only container IDs
  * -l list only last created container

## Remove none images
```
sudo docker system prune
```
```
sudo docker image prune
```

## Stop all running containers
```
sudo docker stop $(sudo docker ps -a -q)
```

## Delete all stopped containers
```
sudo docker rm $(sudo docker ps -a -q)
```

## Push to Public ECR
1. Retrieve an authentication token and authenticate your Docker client to your registry.
Use the AWS CLI:
```
aws ecr-public get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $PUBLIC_ECR_URL
```
2. Build your Docker image using the following command. 
```
sudo docker build -t $YOUR_TAG ./Dockerfile
```
3. After the build completes, tag your image so you can push the image to this repository:
```
sudo docker tag $YOUR_TAG $ECR_REPO
```
4. Run the following command to push this image to your newly created AWS repository:
```
sudo docker push $ECR_REPO
```

