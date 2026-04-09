# Inventory DevOps Pipeline

## Project Overview

This project demonstrates a simple Continuous Integration pipeline for a Dockerized inventory application using GitHub Actions.

The pipeline automatically runs whenever code is pushed to the `main` branch, installs the application dependencies, and builds the Docker image to verify that the project can be packaged successfully.

This project is designed to show practical DevOps workflow automation using GitHub-hosted runners.

## Architecture Overview

The CI pipeline begins when code is pushed to GitHub. GitHub Actions then starts a workflow that checks out the repository, sets up a Node.js environment, installs dependencies, and builds the Docker image.

This ensures that changes to the application are automatically validated and that the Docker build process remains consistent.

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
<img width="447" height="89" alt="Image" src="https://github.com/user-attachments/assets/4add3222-b7a1-46e2-ae62-3e7c1cb129d9" />

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
<img width="486" height="45" alt="Image" src="https://github.com/user-attachments/assets/ebc81def-53cd-40df-aeb4-9b208a9c4f21" />

## Step 3: Create the workflow file

- Create the file:
~~~
touch .github/workflows/docker-build.yml
~~~
<img width="486" height="41" alt="Image" src="https://github.com/user-attachments/assets/27ff2a9b-ccd4-443e-b949-9370ffc37242" />

- Open the file:
~~~
  nano .github/workflows/docker-build.yml
~~~
<img width="609" height="141" alt="Image" src="https://github.com/user-attachments/assets/1fca2ab4-1a7b-494d-83a2-f70eaf450b47" />

- Paste this exact code:
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

Save and Exit with:
~~~
Ctrl + X
Y
Enter
~~~

## Step 4: Connect to GitHub repository
- Run these commands inside your project i.e inventory-devops-pipeline
~~~
git init
git add .
git commit -m "Initial CI pipeline project"
git branch -M main
git remote add origin https://github.com/saidat-tech/inventory-devops-pipeline.git
git push -u origin main
~~~
<img width="736" height="274" alt="Image" src="https://github.com/user-attachments/assets/0abc9b8e-e8eb-4857-b33d-20740575cf4c" />
## Step 5: Check GitHub Actions

- Go to your repository on GitHub.
~~~
Actions
~~~

You should see:
~~~
Docker Build Pipeline
~~~

Open it and watch the steps run.

If all goes well, you will see a green tick.

<img width="785" height="534" alt="Image" src="https://github.com/user-attachments/assets/74e84706-6930-47a7-8058-cfc3073b7416" />

## Step 6: How to rerun the workflow
You have two ways.
- **Option 1**: Push new code
  Any push, to main will trigger the workflow.
  Example:
~~~
git add .
git commit -m "Update workflow or app"
git push
~~~

- **Option 2**: Run manually
Go to GitHub → Actions → Docker Build Pipeline → Run workflow

This works because of the "workflow_dispatch:" in the YAML file.
 
## Errors and fixes in this project.
- **Invalid workflow file**

**Cause**:
duplicate name
duplicate on
bad indentation

**Fix**:
Use the exact YAML above.

- **Workflow not showing on GitHub**

**Cause**:
file is not inside .github/workflows/
wrong extension like .txt

**Fix**:
Make sure it is exactly in:
.github/workflows/docker-build.yml

- **Push permission denied**

**Cause**:
wrong GitHub account logged in

**Fix**:
Push using the right account and correct remote URL.

- **Docker build fails in pipeline**

**Cause**:
missing Dockerfile
broken app code
missing package.json

**Fix**:
Check your project files and test Docker locally first.

## Technologies Used

- GitHub Actions  
- Docker  
- Node.js  
- Express.js  
- Git  

## Skills Demonstrated

This project demonstrates practical DevOps skills including:

- Creating CI workflows using GitHub Actions  
- Automating dependency installation  
- Building Docker images in a pipeline  
- Verifying application packaging automatically  
- Triggering workflows on code push  

## Outcome

This project shows how Continuous Integration can help automate repetitive validation tasks and improve consistency in the software delivery process.

It also provides a strong foundation for future improvements such as automated deployment to AWS EC2 or pushing Docker images to a container registry.

## Future Improvements

Potential next steps for this project include:

- pushing Docker images to Docker Hub
- deploying automatically to AWS EC2
- adding test stages before Docker build
- extending the workflow into a full CI/CD pipeline
# trigger workflow
