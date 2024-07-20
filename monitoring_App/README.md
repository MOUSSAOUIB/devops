
# Monitoring application 

Deploy a monitoring application in a k8s Cluster on  AWS

## Table of Contents

- [Run the application locally](#run-the-application-locally)
- [AWS resources provisioning](#aws-resources-provisioning)
- [Build Docker image](#build-docker-image)

## Run the application locally 

1. **Clone the repository:**
    ```sh
    git clone https://github.com/MOUSSAOUIB/devops.git
    cd monitoring_App
    ```

2. **Set up the environment & execute:**
      ```sh
      pip3 install -r requirements.txt
      python3 monitoring_app.py
      ```
3. **Access the application:**
      ```sh
      http://127.0.0.1:5000/
      ```



## AWS resources provisioning

1. **Create ERC Repository:**
    - Install and configure  aws CLI
    ```sh
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"                                                         
    unzip awscliv2.zip
    sudo ./aws/install

    ```

    - Create ECR 
        ```sh
        # use ecr.tf
        terraform init & terraform apply

        # Authenticate your Docker client to your registry 
        aws configure
            AWS Access Key ID [None]: ****
            AWS Secret Access Key [None]: ****
            Default region name [None]: eu-west-1

        ```
    

2. **Create AWS E2C instance:**
      ```sh
      # Create E2c instance using main.tf file
        terraform init & terraform apply    
      ```

## Build Docker image

1. **Build the image:**
      ```sh
      # Create E2c instance using main.tf file
        docker build -t monitoring_app .
      ```

2. **Push the image to ECR:**
      ```sh
      # Create E2c instance using main.tf file
        docker tag monitoring_app:v1 erc_user/respo_name:latest

        docker push erc_user/respo_name:latest
      ```