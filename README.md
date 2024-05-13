# EduWave-deploy

EduWave is a microservices-based application deployed on Kubernetes. It consists of several services including `api-gateway`, `cms-service`, `learner-service`, and `notification-service`.

## Architecture

The application uses a microservices architecture, with each service running in its own container. The `api-gateway` service acts as the entry point to the application, routing requests to the appropriate microservices based on the request path.

The application is deployed on a Kubernetes cluster, which provides features like automatic scaling, self-healing, and service discovery.

## Prerequisites

- Docker
- Kubernetes
- Minikube (for local development)
- kubectl

## Setup and Deployment

### Mac

1. Install Docker: https://docs.docker.com/desktop/mac/install/
2. Install Kubernetes: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/
3. Install Minikube: https://minikube.sigs.k8s.io/docs/start/

### Windows

1. Install Docker: https://docs.docker.com/desktop/windows/install/
2. Install Kubernetes: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
3. Install Minikube: https://minikube.sigs.k8s.io/docs/start/

## Creating Secrets

Some services require secrets to be created in Kubernetes. For example, the `notification-service` requires an `email-credentials` secret with `address` and `password` keys, and the `api-gateway` requires a `db-credentials` secret with a `url` key.

You can create a secret using the `kubectl create secret` command. For example:

```bash
kubectl create secret generic email-credentials --from-literal=address=<your-email-address> --from-literal=password=<your-email-password>
kubectl create secret generic db-credentials --from-literal=url=<your-db-url>
```

Replace `<your-email-address>`, `<your-email-password>`, and `<your-db-url>` with your actual values.

Access the secrets folder on terminal and and enter 

```bash
kubectl apply -f jwt-secret.yml`
```

Remember to create all required secrets before deploying your services.

## Running the Application

1. Start Minikube: minikube start
2. Create required secrets: kubectl create secret... (repeat for each secret)
3. Deploy the services: kubectl apply -f <service-deployment-file>
4. Expose the API gateway: minikube service api-gateway

Replace `<service-deployment-file>` with the path to your Kubernetes deployment configuration and service files.

## Accessing the Application

Once the API gateway is exposed, you can access the application by sending requests to the URL provided by the `minikube service api-gateway` command.

For example, to register a user, you would send a POST request to `http://<api-gateway-url>/api/cms/user/register`.

Replace `<api-gateway-url>` with the URL provided by the `minikube service api-gateway` command.