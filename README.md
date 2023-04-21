# DOCKER MAIN COMMANDS:

1. Create a Dockerfile inside the folder containing the dockerized app
2. Build an DIY image:
> docker build -t image_name ./
3. Docker run -p 3000:80 -d --name <container-name> --rm <image-name>
4. To run docker with named volume:
    a. docker run -d 
    -p 3000:80 
    --name <container-name>
    -v <host_name_folder>:<container_name_path>
    --rm
    <image-name>
Esempio:
    docker run -d 
    -p 3000:80 
    --name feedback-app 
    -v feedback:/app/feedback 
    --rm 
    feedback-node:volume
5. To show the log of container: docker logs <container-name>
6. To stop a container: docker stop <container-name>
7. To list all images: docker image ls
8. To list all containers: docker ps -a
9. To list all volumes: docker volume ls
10. To remove an image: docker rmi <image-name>
11. To remove an image: dockerrmi-f$(dockerimages-aq)

# A Simple Docker file:
> FROM node:12<br>
>
> WORKDIR /app<br>
>
> COPY package.json /app
> 
> RUN npm install
> 
> COPY . /app
> 
> EXPOSE 80
>  
> VOLUME [ "/app/feedback" ]
> 
> CMD ["node", "server.js"]

# A Docker-compose file to start MongoDB, Node.js backend and React frontend

> version: '3.8'<br>
> services:<br>
>   mongodb: <br>
>     image: 'mongo'<br>
>     container_name: 'mongodb'<br>
>     volumes:<br>
>       - data:/data/db<br>
>   
>   backend:<br>
>     build: <br>
>       context: ./backend/<br>
>       dockerfile: Dockerfile<br>
>     container_name: 'node-app'<br>
>     ports:<br>
>       - "80:80"<br>
>     volumes:<br>
>       - logs:/app/logs<br>
>       - ./backend:/app<br>
>       - /app/node_modules<br>
>     depends_on:<br>
>       - mongodb<br>
>   
>   frontend:<br>
>     build:<br>
>       context: ./frontend/<br>
>       dockerfile: Dockerfile<br>
>     container_name: 'react-app'<br>
>     ports:<br>
>       - "3000:3000"<br>
>     depends_on:<br>
>       - mongodb<br>
>     
> 
> volumes:
>   data:
>   logs:
