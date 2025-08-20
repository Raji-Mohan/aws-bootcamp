# Week 1 — App Containerization

# Add Dockerfile
Create a file here: backend-flask/Dockerfile

    FROM python:3.10-slim-buster
    
    WORKDIR /backend-flask
    
    COPY requirements.txt requirements.txt
    RUN pip3 install -r requirements.txt
    
    COPY . .
    
    ENV FLASK_ENV=development
    
    EXPOSE ${PORT}
    CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]

# Run without docker from terminal
    cd backend-flask    
    ls -l    
    pip3 install -r requirements.txt    
    python -m flask run --host=0.0.0.0 --port=4567

click the ports tab to see url running in port

# Run with docker
    cd ..    
    docker build -t  backend-flask ./backend-flask    
    docker run --rm -p 4567:4567 -it backend-flask
  
error message as the env variables FRONTEND_URL, BACKEND_URL defined in app.py values are not set

    docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask

append to the url to /api/activities/home on the ports tab to get the json file

# docker command
    docker ps
    docker images
    docker ps -a (shows docker containers not running and not destroyed)
    docker run --rm (destroys containers as soon as the container stops
    
# frontend docker changes
    cd frontend-react-js
    npm i
    cd..
    
create  frontend-react-js/Dockerfile

    FROM node:16.18
    
    ENV PORT=3000
    
    COPY . /frontend-react-js
    WORKDIR /frontend-react-js
    RUN npm install
    EXPOSE ${PORT}
    CMD ["npm", "start"]

# Build and run docker
    docker build -t frontend-react-js ./frontend-react-js
    docker run -p 3000:3000 -d frontend-react-js

# Docker compose
Create docker-compose.yml at the root of your project. 

To run right click docker-compose.yml file and (click compose up) or on TERMINAL (docker compose up) or (docker-compose up) command

    version: "3.8"
    services:
      backend-flask:
        environment:
          FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
          BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
        build: ./backend-flask
        ports:
          - "4567:4567"
        volumes:
          - ./backend-flask:/backend-flask
      frontend-react-js:
        environment:
          REACT_APP_BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
        build: ./frontend-react-js
        ports:
          - "3000:3000"
        volumes:
          - ./frontend-react-js:/frontend-react-js
    
    # the name flag is a hack to change the default prepend folder
    # name when outputting the image names
    networks: 
      internal-network:
        driver: bridge
        name: cruddur
