# Inventory DevOps Pipeline

## Project Overview

This project demonstrates a simple Continuous Integration pipeline for a Dockerized inventory application using GitHub Actions.

The pipeline automatically runs whenever code is pushed to the `main` branch, installs the application dependencies, and builds the Docker image to verify that the project can be packaged successfully.

This project is designed to show practical DevOps workflow automation using GitHub-hosted runners.

## Architecture Overview

The CI pipeline begins when code is pushed to GitHub. GitHub Actions then starts a workflow that checks out the repository, sets up a Node.js environment, installs dependencies, and builds the Docker image.

This ensures that changes to the application are automatically validated and that the Docker build process remains consistent.

## Step 1: Create the project folder locally. 

If you already copied your Docker project, you can skip this.
- Move into where you have your Docker project.
~~~
cd ~/Downloads
~~~
- Copy your Docker project into a new folder called Inventory devops pipeline.
~~~
cp -r dockerized-inventory-system inventory-devops-pipeline
~~~
- Move into the Inventory devops pipeline.
~~~
cd inventory-devops-pipeline
~~~

## Step 2: Create the GitHub Actions folders
- Inside the project folder, i.e inventory devops pipeline,
run:
~~~
mkdir -p .github/workflows
~~~
This will create your .github and workflows folder.
~~~
.github/
.github/workflows/
~~~

## Step 3: Create the workflow file

- Create the file:
~~~
touch .github/workflows/docker-build.yml
~~~
- Open the file:
~~~
  nano .github/workflows/docker-build.yml
~~~

Paste this exact code:

~~~
name: Docker Build Pipeline

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Verify files
        run: ls -la

      - name: Build Docker image
        run: docker build -t inventory-app .

      - name: List Docker images
        run: docker images
~~~


## Pipeline Stages

1. Checkout repository code  
2. Set up Node.js  
3. Install project dependencies  
4. Build Docker image  
5. Verify Docker image creation  

---

## Technologies Used

- GitHub Actions  
- Docker  
- Node.js  
- Express.js  
- Git  

---

## Skills Demonstrated

This project demonstrates practical DevOps skills including:

- Creating CI workflows using GitHub Actions  
- Automating dependency installation  
- Building Docker images in a pipeline  
- Verifying application packaging automatically  
- Triggering workflows on code push  

---

## Trigger Events

The workflow runs on:

- push to `main`
- manual execution using `workflow_dispatch`

---

## Project Structure

```
inventory-devops-pipeline/
├── .github/
│   └── workflows/
│       └── docker-build.yml
├── public/
│   └── index.html
├── app.js
├── Dockerfile
├── .dockerignore
├── package.json
└── package-lock.json
```

---

## Example Workflow

```
name: Docker Build Pipeline

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Verify files
        run: ls -la

      - name: Build Docker image
        run: docker build -t inventory-app .

      - name: List Docker images
        run: docker images
```

---

## Outcome

This project shows how Continuous Integration can help automate repetitive validation tasks and improve consistency in the software delivery process.

It also provides a strong foundation for future improvements such as automated deployment to AWS EC2 or pushing Docker images to a container registry.

---

## Future Improvements

Potential next steps for this project include:

- pushing Docker images to Docker Hub
- deploying automatically to AWS EC2
- adding test stages before Docker build
- extending the workflow into a full CI/CD pipeline
