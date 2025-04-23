# Todo List Node.js App - CI/CD with GitHub Actions & Docker

* This project demonstrates how to set up a **CI/CD pipeline** using **GitHub Actions**, **Docker**, and **Docker Hub** for a simple Node.js Todo List app.
* The app is containerized and deployed locally using Docker.

# Project Overview

- **Frontend & Backend**: Node.js (Express)
- **CI/CD Tool**: GitHub Actions
- **Containerization**: Docker
- **Registry**: Docker Hub
- **Deployment**: Local system using `docker run`

# Folder Structure

Todo-List-nodejs/ ├── index.js ├── package.json ├── Dockerfile ├── .github/ │ └── workflows/ │ └── ci-cd.yml

# Tools Used

- **GitHub** - Version control and project repository
- **GitHub Actions** - CI/CD pipeline automation
- **Docker** - Containerization of the Node.js app
- **Docker Hub** - Registry to store and pull Docker images
- **Node.js & Express** - Backend framework for the Todo app

# Step-by-Step Guide

# Step 1: Clone the Repository
  
git clone https://github.com/asma-naaz/Todo-List-nodejs.git
cd Todo-List-nodejs

# Step 2: Setting up the Dockerfile
Why: A Dockerfile defines the environment where the app will run. By using Docker, we ensure that the app runs consistently across different environments (development, testing, production).

** How: The Dockerfile includes the following steps:

* FROM node:18-alpine: Starts with a lightweight Node.js base image.

* WORKDIR /app: Sets the working directory for subsequent commands inside the container.

* *COPY package.json ./**: Copies the package.json and package-lock.json files to the container.

* RUN npm install: Installs the dependencies defined in the package.json.

* COPY . .: Copies the entire project to the container.

* EXPOSE 4000: Exposes port 4000 for the application to be accessed.

* CMD ["node", "index.js"]: Starts the app using Node.js when the container runs.

# Step 3: Setting up the GitHub Actions Workflow
Why: GitHub Actions automates the process of building, testing, and deploying your app every time a change is made to the codebase. This creates a seamless CI/CD pipeline.

How: Create a file .github/workflows/ci-cd.yml with the following content:

yaml

name: CI/CD Pipeline

on:
  push:
    branches: [ "master" ]

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout source
      uses: actions/checkout@v2

    - name: Log in to Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Build Docker image
      run: docker build -t asmanaaz025/todo-list-nodejs:latest .

    - name: Push Docker image
      run: docker push asmanaaz025/todo-list-nodejs:latest
      
# Explanation of the workflow:

* on.push: The workflow runs whenever code is pushed to the master branch.

* actions/checkout: Checks out the code from the repository.

* docker/login-action: Logs into Docker Hub using the credentials stored in GitHub Secrets.

* docker build: Builds the Docker image from the Dockerfile.

* docker push: Pushes the image to Docker Hub under your account.

* Important: Ensure you store your Docker Hub credentials (username & password) in GitHub Secrets under DOCKER_USERNAME and DOCKER_PASSWORD.

# Step 4: Running the Docker Container Locally
Why: Running the app in a Docker container allows you to test it in an isolated environment, replicating production conditions on your local machine.

How: After the image is built and pushed, you can run the app locally with the following command:

* docker run -p 4000:4000 asmanaaz025/todo-list-nodejs:latest
This command:
* Runs the container based on the todo-list-nodejs:latest image.
* Maps the container's port 4000 to your machine's port 4000.

You should see the following message in the terminal:

Yupp! Server is running on port 4000
Now, open your browser and visit:
http://localhost:4000

# Deliverables
GitHub repository with CI/CD workflows for building, testing, and pushing the Docker image.

https://github.com/asma-naaz/Todo-List-nodejs/actions

Docker image pushed to Docker Hub: Link to Docker Hub

https://hub.docker.com/repository/docker/asmanaaz025/todo-list-nodejs/general

GitHub Actions Workflow Results: View your build and push logs under the "Actions" tab on GitHub.

![Screenshot 2025-04-23 202407](https://github.com/user-attachments/assets/e7ec1732-fb14-414d-b87f-42047f84bc36)


App running locally: Accessible via http://localhost:4000

![Screenshot 2025-04-23 202328](https://github.com/user-attachments/assets/f6c17868-fe4f-4b15-bc13-d8f6736a045f)


Asma Naaz
AWS DevOps Intern | Learning CI/CD | Docker & GitHub Actions
📍 Hyderabad
🌐 GitHub: @asma-naaz
