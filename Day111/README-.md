![Alt texts](../Images/p1.png)

# Day 111 | Use Docker build Nginx | Flask | React


```sh
npx create-react-app my-react-app
cd my-react-app


npm start
```

```sh

# Use the official Node.js base image
FROM node:16 as build-stage

# Set working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the app's source code
COPY . .

# Build the app for production
RUN npm run build

# Stage 2 - Serve the React build with Nginx
FROM nginx:alpine as production-stage

# Copy the React build from the previous stage to Nginx's default public directory
COPY --from=build-stage /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]

```

```sh
docker build -t my-react-app .

docker run -d -p 80:80 my-react-app

docker ps

```

# Flask App

```sh
mkdir my-flask-app
cd my-flask-app

```

```sh
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)

```


## Step 2: Set Up the Project Requirements
Create a requirements.txt file
```sh
Flask==2.0.3
```
```sh
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 5000 available to the world outside this container
EXPOSE 5000

# Define environment variable
ENV FLASK_APP=app.py

# Run the Flask app
CMD ["flask", "run", "--host=0.0.0.0", "--port=5000"]

```


```sh
docker build -t my-flask-app .

docker run -d -p 5000:5000 my-flask-app

```