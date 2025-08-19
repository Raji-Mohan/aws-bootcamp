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
