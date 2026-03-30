# Analytics App (Operationalize a Service)

This project operationalizes a Python analytics service using Docker, Amazon ECR, AWS CodeBuild, and Kubernetes (Amazon EKS).  
The application is containerized using a Dockerfile, and dependencies are installed via requirements.txt.  
An AWS CodeBuild project builds the Docker image in AWS (with privileged mode enabled) and pushes the image to an Amazon ECR repository.  
Kubernetes manifests are stored in the deployments/ folder and include the application Deployment/Service, a Postgres Deployment/Service, and separate ConfigMap and Secret resources.  
Plain configuration values are stored in a ConfigMap, while sensitive values (such as the database password) are stored in a Secret.  
The application Deployment pulls the container image from ECR and connects to Postgres using the internal Kubernetes Service name.  
Verification is performed using kubectl commands (get pods, get svc, and describe) for both the application Deployment and the database Service.  
CloudWatch Container Insights is used to review logs and confirm the service runs without errors.  
Screenshots of the ECR image, CodeBuild success, kubectl outputs (or environment limitations), and CloudWatch logs are included for review.

## Note on Kubernetes Execution (Udacity Voclabs IAM Restrictions)

This project was developed using the Udacity Voclabs AWS environment, which applies explicit IAM deny policies on certain Amazon EKS actions.  
While EKS cluster and node group setup steps were attempted, kubectl context configuration and node group inspection were restricted by sandbox permissions (explicit deny).  
As a result, full cluster connection/verification from the workspace may be limited.  
All required Kubernetes manifests, Docker configuration, CI/CD pipeline configuration, and ECR image artifacts are provided in accordance with the project rubric.

## Evidence (Screenshots)

The screenshots folder/evidence includes:
- Amazon ECR repository showing the pushed image (analytics-app:latest)
- AWS CodeBuild build history showing a successful build and push to ECR
- EKS / IAM restriction evidence (explicit deny) when applicable
- kubectl configuration/connection attempts from the workspace when applicable
- CloudWatch (Container Insights / logs) showing application logs (when available)

Additionally, EKS managed node group creation failed in the Udacity Voclabs environment (NodeCreationFailure: unhealthy nodes), preventing worker nodes from joining the cluster and kubectl from establishing a context.
