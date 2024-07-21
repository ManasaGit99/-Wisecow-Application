![image](https://github.com/user-attachments/assets/c8e4214d-11e8-4a65-838c-4759b1fd5680)
# Wisecow Application

This project containerizes and deploys the Wisecow application in a Kubernetes environment with secure TLS communication. The process includes automatic building and pushing of the Docker image to Docker Hub and deploying the application using GitHub Actions.

#Prerequisites
- A local VM (e.g., Ubuntu)
- Minikube installed
- Docker Hub account
- Domain name (e.g., mrsja.xyz)

# Dockerization
A Dockerfile is provided to create a container image of the Wisecow application.

# Kubernetes Deployment
Kubernetes manifest files (`deployment.yaml`, `service.yaml`, `ingress.yaml`) are provided to deploy the Wisecow application in a Kubernetes environment.

# TLS Implementation
Generate a self-signed certificate:
-	openssl req -newkey rsa:2048 -nodes -keyout wisecow.key -x509 -days 365 -out wisecow.crt
Create a Kubernetes secret for the TLS certificate:
-	kubectl create secret tls wisecow-tls --cert=wisecow.crt --key=wisecow.key

# GitHub Actions Workflow
The GitHub Actions workflow (`.github/workflows/ci-cd.yml`) automates the build and push of the Docker image to Docker Hub and deploys the application to the Kubernetes environment.
## Setting Up Secrets
In your GitHub repository, set up the following secrets:

- `DOCKER_USERNAME`: Your Docker Hub username
- `DOCKER_PASSWORD`: Your Docker Hub password
- `KUBECONFIG`: Your Kubernetes config file content

## Setting Up a Self-Hosted Runner
Follow the [GitHub documentation] to set up a self-hosted runner for your GitHub Actions workflow.

## Deploying the Application
After setting up the repository and secrets, any changes pushed to the `main` branch will trigger the GitHub Actions workflow to:

1. Build the Docker image
2. Push the Docker image to Docker Hub
3. Deploy the updated application to the Kubernetes environment

# Accessing the Application
Update your `/etc/hosts` file with the Minikube IP:
-	<minikube-ip> mrsja.xyz
Replace `<minikube-ip>` with the actual Minikube IP, which you can find using:
-	minikube ip


You can then access the Wisecow application using:
-	curl -k https://mrsja.xyz

### Expected Output

```
<pre> _____________________________________
/ Fine day for friends. So-so day for \
\ you.                                /
 -------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||</pre>
```


![image](https://github.com/user-attachments/assets/58a45646-6163-418a-a1a1-a6a1c66f2813)


