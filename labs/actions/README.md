# Running Containers in Pods

GitHub Actions gives you the flexibility to build an automated software development lifecycle workflow. You can use multiple Kubernetes actions to deploy to containers from Azure Container Registry (ACR) to Azure Kubernetes Service (AKS) with GitHub Actions.


## Fork and update the repositary

Navigate to the [actions-demo](https://github.com/Fasttrack-Azure/action-demo) repository and select Fork.

- Update the deployment.yaml to use your-name in your deployment
```
spec:
      containers:
      - name: sidapp01
        image: psacr02.azurecr.io/<your-name>app01:latest
```

## Create Screts

- Navigate to your GitHub repository settings and select Security > Secrets and variables > Actions.

- For each secret, select New Repository Secret and enter the name and value of the secret.
```
ACR_CREDENTIALS : gnyEpg0ZZApoepRJfMKv+Mldhyg1WQQh+7Hjz8Tzjc+ACRC/Li9N
KUBECONFIG : [kubeconfig-ss](/kubeconfig-ss)

```

## Create Actions file

- In your repository, create a .github/workflows/cicd.yml and paste in the following contents:
```
name: cicd pipeline

on:
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]

jobs:

  build_push_image:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Build the Docker image
      run: docker build . --file Dockerfile --tag psacr02.azurecr.io/<your-name>app01:latest
      
    - name: Azure Container Registry Login
      uses: Azure/docker-login@v1
      with:
        # Container registry username
        username: psacr02
        # Container registry password
        password: ${{secrets.ACR_CREDENTIALS}}
        # Container registry server url
        login-server: psacr02.azurecr.io
        
    - name: Push Image  
      run: docker push psacr02.azurecr.io/<your-name>app01:latest
      
  deploy:
    runs-on: ubuntu-latest
    needs: build_push_image # Will wait for the execution of the previous job 
    
    steps:
    - uses: actions/checkout@v2

    - name: Kubernetes set context
      uses: Azure/k8s-set-context@v1
      with:
        kubeconfig: ${{secrets.KUBECONFIG}} # Grab the auth token from GitHub secrets
      id: login
      
    # Declarative Deployment-02
    - name: Kubernetes Deployment
      run: kubectl apply -f deployment.yaml
    - name: Service Deployment
      run: kubectl apply -f service.yaml

```

- Commit the .github/workflows/cicd.yml file to your repository.
- In your repository, select Actions and confirm a workflow is running. Then, confirm the workflow has a green checkmark and the updated application is deployed to your cluster.
