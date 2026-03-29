# Analytics App (Operationalize a Service)

This project operationalizes a Python analytics service using Docker, Amazon ECR, AWS CodeBuild, and Kubernetes on Amazon EKS.  
The application is containerized using a Dockerfile and dependencies are installed via requirements.txt.  
A CodeBuild project builds the Docker image in AWS (privileged mode enabled) and pushes the image to an ECR repository.  
Kubernetes manifests are stored in the deployments/ folder and include the application deployment/service, a Postgres deployment/service, and separate ConfigMap and Secret resources.  
Plain configuration values are stored in a ConfigMap, while sensitive values (such as database password) are stored in a Secret.  
The application deployment pulls the container image from ECR and connects to Postgres using the internal Kubernetes service name.  
After applying the manifests, the cluster runs both the analytics application pod and the Postgres pod.  
Verification is done using kubectl get pods, kubectl get svc, and kubectl describe for both the app deployment and database service.  
CloudWatch Container Insights is used to review logs and confirm that the service runs without errors.  
Screenshots of ECR images, CodeBuild success, kubectl outputs, and CloudWatch logs are included for review.