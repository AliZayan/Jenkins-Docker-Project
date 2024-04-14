# devops-automation
This Jenkins pipeline automates the process of building a Maven-based Java project, creating a Docker image from the built artifacts, pushing the Docker image to a Docker Hub registry, and deploying the image to a Kubernetes cluster.

Here's a brief description of each stage in the pipeline:

    Build Maven:
        This stage checks out the source code of a Maven-based Java project from a Git repository.
        It then executes the Maven command mvn clean install to compile the source code, run tests, and package the project into a distributable artifact.

    Build Docker Image:
        This stage creates a Docker image for the Java application.
        It uses the docker build command to build the Docker image based on the Dockerfile located in the project directory.
        The resulting Docker image is tagged with the name alidevops/devops-integration.

    Push Image to Hub:
        This stage pushes the Docker image to a Docker Hub registry for storage and distribution.
        It uses Docker Hub credentials stored securely in Jenkins using the withCredentials block.
        The docker login command is used to authenticate with Docker Hub, and docker push is used to upload the Docker image.

    Deploy to Kubernetes:
        This stage deploys the Docker image to a Kubernetes cluster.
        It uses the Kubernetes plugin for Jenkins to deploy the image.
        The kubernetesDeploy step specifies the Kubernetes configuration and deployment YAML file (deploymentservice.yaml), as well as the Kubernetes credentials (kubeconfigId: 'ali').

Overall, this pipeline automates the entire process of building a Java project, creating a Docker image, pushing the image to a registry, and deploying it to a Kubernetes cluster. It ensures consistency, reliability, and efficiency in the DevOps workflow.