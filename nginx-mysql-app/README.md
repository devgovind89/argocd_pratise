# Argo CD Demo Application

This repository contains a demo application for Argo CD with two components:
- A MySQL database (healthy)
- A custom Nginx web server (intentionally misconfigured to demonstrate failure)

## Prerequisites

- Docker installed locally
- kubectl configured to access your EKS cluster
- Argo CD CLI installed and configured
- Access to a container registry (Docker Hub, ECR, etc.)

## Building and Pushing the Nginx Image

1. Build the Nginx image:
   ```bash
   docker build -t your-username/nginx-crash:latest nginx/
   ```

2. Push the image to your container registry:
   ```bash
   docker push your-username/nginx-crash:latest
   ```

3. Update the image in `manifests/nginx.yaml` with your image name and tag.

## Deploying with Argo CD

1. Commit and push your changes to your Git repository.
2. Apply the Argo CD Application manifest:
   ```bash
   kubectl apply -f argocd-application.yaml -n argocd
   ```

## Expected Behavior

- The MySQL pod should start successfully and remain in a Running state.
- The Nginx pod will go into a CrashLoopBackOff state due to the intentional misconfiguration.
- Both pods will be visible in the Argo CD UI as part of the `demo-app` application.

## Troubleshooting

To check the status of the pods:
```bash
kubectl get pods -n demo-app
```

To view logs from the failing Nginx pod:
```bash
kubectl logs -n demo-app deployment/nginx --previous
```
