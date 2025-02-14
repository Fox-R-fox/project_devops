# Documentation of the Project 

## This project consists of the following techstacks, and they are combined to form the DevOps Structure

## Technoliges used & integrated

| **Technology/Tool** | **Purpose**                                                                                      |
|----------------------|--------------------------------------------------------------------------------------------------|
| **Python FastAPI**   | For Authentication RestAPI Development                                                          |
| **MongoDB**          | For database generated by FastAPI, i.e., User data                                              |
| **Docker**           | For creating the custom image of the application and containerization                           |
| **GitHub**           | For storing the application and other source code                                             |
|                      | For storing the AWS Secrets and EC2 Key-Pair values                                           |
| **GitHub Actions**   | For running the CI/CD pipeline                                                                  |
| **AWS Cloud**        | For EC2 instances of MongoDB database, K8s cluster node, and worker node                      |
|                      | For AWS ECR as a container registry and docker image storage in a private repository          |
|                      | For AWS IAM and Security Groups policy execution                                              |
|                      | For AWS S3 for storage of Terraform state files                                               |
| **Terraform**        | For AWS infrastructure configuration management                                                 |
| **Kubernetes**       | For container orchestration and application deployment over pods                                |
| **Helm Charts**      | For Kubernetes package management and installing packages                                       |
| **ArgoCD**           | For continuous deployment of the applications                                                   |


## How to run this project locally or setup locally for FastAPI testing 

### Clone the Code 
```bash 
# use the below link to clone the file in your local environment
git clone git@github.com:abhigyan-709/project_devops.git
```

### Option 1 - Setup the Application via Virtual Environment 
#### Activate the Virtual Environment to run this code
```bash 
# considering the mac system as the code is developed in mac environment
python3 -m venv venv
# activate the virtual environment
source ./venv/bin/activate
```

```bash 
# intsall the requirements of the application 
# path/to/requirements.txt directory
pip3 install -r requirements.txt
```

```bash
> # Setup MongoDB locally  
1. Create the .env file in ./app project directory 
2. Paste the locally hosted mongoDB URI in .env file as
MONGO_URI=mongodb://localhost:27017/
```

```bash
# Run the application 
uvicorn run main:app --reload
```

### Option 2 - Use the docker-compose.yaml for multicontainer application deployment
#### This method uses the docker-compose.yaml file for easy deployment

```bash
> # Setup MongoDB locally  
1. Create the .env file in ./app project directory 
2. Paste the locally hosted mongoDB URI in .env file as
MONGO_URI=mongodb://localhost:27017/
```

```bash 
# run the app with docker-compose with live or containerised mongodb in your local system
# if you are intended to run the application in the multicontainer 
# to run locally replace .env mongodb uri with mongodb://localhost:27017 or just enter the live database URI of mongodb

root-dir/docker-compose build
root-dir/docker-compose up -d #-d is for deatching the container from the terminal

```


## Setting up the application on the cloud

### Considering the app is developed & coded
We will consider the following steps to deploy the application

1. Install the AWS CLI in your local system - refer to the documentation of AWS CLI 
2. Configure the AWS CLI 

```bash 
# get the AWS ACCESS ID & Secret by creating manually via AWS console in AWS IAM indentity center.
# be cautious to not to store the root ID in AWS CLI, for test purpose i have done so, and I have already reset those keys
aws configure
AWS Access Key ID [**********]:
AWS Secret Access Key [***********]:
Default region name [ap-south-1] # my region is ap-south-1(mumbai) change it accordingly
Default output format [None]: # json or txt
```

3. Use the terraform to deploy the application - here for the simplicity of the application deployment I have used the admin privileged policy in AWS
```bash 
# SETTING UP THE BACKEDN.tf file for storage of the statefiles in S3
1. setup backend.tf and s3.tf
machine@mac project_devops/infrastructure % terraform init
machine@mac project_devops/infrastructure % terraform plan
machine@mac project_devops/infrastructure % terraform apply  
```

We have setup this backend in such a way that we will not face the problem of "Resource Already exists" when we will apply the next terraform setup it will not make a clash

4. Deploying other terraform setups

