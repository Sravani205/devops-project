# Jenkins CI/CD Pipeline to Kubernetes

A small end-to-end pipeline: Jenkins builds a Docker image of a static web page, pushes it to Docker Hub, and deploys it to a Kubernetes cluster.

## How it works

1. **Build:** `docker build` creates `sravani205/devops-project:<build number>` from the `Dockerfile` (nginx serving `index.html`).
2. **Push:** the image is pushed to Docker Hub. The Docker Hub login comes from a Jenkins credential (`dockerhub-creds-new`), so no password is stored in the repo.
3. **Deploy:** `kubectl apply` creates the Deployment (2 replicas) and a NodePort Service, then `kubectl set image` rolls out the image from this build and Jenkins waits for the rollout to finish.

## Files

| File | Purpose |
|---|---|
| `Jenkinsfile` | Build, push, and deploy stages |
| `Dockerfile` | nginx image serving the page |
| `Jenkins-image/Dockerfile` | Jenkins LTS image with the Docker CLI installed, so the pipeline can build images |
| `deployment.yaml` | Kubernetes Deployment, 2 replicas |
| `service.yaml` | NodePort Service on port 80 |

## Run it yourself

1. Build the Jenkins image: `docker build -t jenkins-docker Jenkins-image/`
2. Run Jenkins with access to the Docker socket and a kubeconfig at `/var/jenkins_home/.kube/config`.
3. Add a Docker Hub username/password credential with the ID `dockerhub-creds-new`.
4. Create a pipeline job pointing at this repo and run it.

## Built with

Jenkins, Docker, Docker Hub, Kubernetes, kubectl

This was my first end-to-end pipeline (June 2026). The larger follow-up, with tests, Helm, and Argo CD GitOps, is in [Kubernetes-Delivery-Platform](https://github.com/Sravani205/Kubernetes-Delivery-Platform).
