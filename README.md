# devops-project1
# Java Application Deployment on AWS EKS

A hands-on DevOps project demonstrating Java application containerization, AWS infrastructure provisioning, and Kubernetes deployment.

## Architecture

Java Application → Maven → Docker → Amazon ECR → Amazon EKS → LoadBalancer → Browser

## Technologies Used

- Java 17
- Maven
- Docker
- Terraform
- AWS EC2
- Amazon ECR
- Amazon EKS
- Kubernetes
- Jenkins

## Project Structure

- `src/` — Java application source code
- `pom.xml` — Maven build configuration
- `Dockerfile` — Docker image configuration
- `Jenkinsfile` — Jenkins pipeline
- `terraform/` — AWS infrastructure configuration
- `k8s/deployment.yaml` — Kubernetes Deployment
- `k8s/service.yaml` — Kubernetes Service

## Build and Test

```bash
mvn clean test
mvn package -DskipTests
```

## Build the Docker Image

```bash
docker build -t project1-java-app:v3 .
```

## AWS Deployment

The application image is stored in Amazon ECR and deployed to Amazon EKS.

Configure kubectl:

```bash
aws eks update-kubeconfig --region eu-north-1 --name project1-eks
```

Apply the Kubernetes manifests:

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

Verify the deployment:

```bash
kubectl get pods
kubectl get services
```

The Kubernetes LoadBalancer Service exposes the application on port 80 and forwards traffic to port 8080 in the Java container.

## Terraform

Terraform configuration is provided in `terraform/`.

```bash
cd terraform
terraform init
terraform validate
terraform plan
```

Review the plan carefully before applying infrastructure changes.

## CI/CD Status

A Jenkinsfile is included. Its current pipeline still references the earlier Docker Hub image and Kubernetes deployment; integration with this project's Amazon ECR and EKS resources remains to be completed and tested.

## Cost Management

Amazon EKS, worker nodes, and load balancers can incur AWS charges. After completing your demo, review the resources and destroy any that are no longer needed. Review the Terraform destruction plan before confirming.

## Project Status

- Java HTTP application tested locally
- Docker image pushed to Amazon ECR
- Application deployed and accessed through an AWS load balancer
- Terraform and Kubernetes configurations added to GitHub
- Jenkins-to-ECR/EKS automation remains future work
