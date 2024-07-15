# Kidney-Disease-Classification-MLflow-DVC

## Contents
1. Introduction and Github Repository Setup
2. Project Template Creation
3. Project Setup and Requirements Installation
4. Logging, Utils and Exception Module
5. Project Workflows
6. All Components Notebook Experiment
7. All Components Modular Code Implementation
8. Training Pipeline
9. MLFlow (MLOps Tool) - Experiments tracking and Model Registration
10. DVC (MLOps Tool) - Pipeline tracking and implementation
11. Prediction Pipeline and User App Creation
12. Docker
13. Final CI/CD Deployment on AWS

### 1. Introduction and Github Repository Setup
Create the github repository

### 2. Project Template Creation
- Create template.py
- Add list of componen on the templates (list_of_files)
- run tempalate to create components <br>
  `python template.py`

### 3. Project Setup and Requirements Installation
- install requirements
  `pip install -r requirements.txt`

### 4. Logging, Utils and Exception Module
- Create main.py
  `python main.py`
  output
  [2024-07-03 20:48:35,780: INFO: main: Welcome to our custom log]
- Create common.py in utils directory
- create trials.ipynb in research directory

### 5. Project Workflows
#### Workflows
1. Update config.yaml
2. Update secrets.yaml [Optional]
3. Update params.yaml
4. Update the entity
5. Update the configuration manager in src config
6. Update the components
7. Update the pipeline
8. Update the main.py
9. Update the dvc.yaml
10. app.py

##### Prepare Base Model
- Running stage_02_prepare_base_model.py
  ```python main.py  ```

##### Model Training
- Running stage_03_prepare_base_model.py
  ```python main.py  ```

##### Model Evaluation
- Create 04_model_evaluation_with_mlflow.ipynb in research directory
- Integrate Dagshub with github repository
- Click REMOTE green button on repository
  ```
  import dagshub
  dagshub.init(repo_owner='wildenali11', repo_name='Kidney-Disease-Classification-EndToEnd', mlflow=True)

  import mlflow
  with mlflow.start_run():
    mlflow.log_param('parameter name', 'value')
    mlflow.log_metric('metric name', 1)
  ```
- Generate token
  export MLFLOW_TRACKING_URI=https://dagshub.com/wildenali11/Kidney-Disease-Classification-EndToEnd.mlflow
  export MLFLOW_TRACKING_USERNAME=wildenali11
  export MLFLOW_TRACKING_PASSWORD=d64de539b652532cafea03ac7fddec87bd9ee4f3
- Export to os environment
  os.environ["MLFLOW_TRACKING_URI"]="https://dagshub.com/wildenali11/Kidney-Disease-Classification-EndToEnd.mlflow"
  os.environ["MLFLOW_TRACKING_USERNAME"]="wildenali11"
  os.environ["MLFLOW_TRACKING_PASSWORD"]="d64de539b652532cafea03ac7fddec87bd9ee4f3"

# DVC (Data Version Control) [dvc.org](https://dvc.org/doc/user-guide)
- Versioning the dataset, code, model
- Create dvc.yaml
- Init the DVC on terminal
  ```dvc init```
- Run the DVC on terminal
  ```dvc repro```

### DVC command
1. dvc init
2. dvc repro
3. dvc dag 

# Create 10. app.py file
- create prediction.py in pipeline directory
- create app.py in Kidney-Disease-Classification-EndToEnd directory
- run
  ```python app.py```

<!-- # Create Docker
- create Dockerfile in Kidney-Disease-Classification-EndToEnd directory

### Create CI/CD with aws
- Create .github/workflows directory
- Create main.yaml in workflows directory -->


# AWS-CICD-Deployment-with-Github-Actions

## 1. Login to AWS console.

## 2. Create IAM user for deployment
  - In Search tab type IAM (Identity and Access Management)
  - In Sidebar collapse the Access management and Click Users
  - Click Create user button on top right
  - fill the User name form named "kidney" then click next
  - In Permissions options choose 'Attach policies directly' then add policy:
    1. AmazonEC2ContainerRegistryFullAccess
    2. AmazonEC2FullAccess
  - Click next and Create user button
  - Click the kidney in the table
  - Click Seciruty credentials tab
  - In Access keys (0) click Create access key
  - In Access key best practices & alternatives choose Command Line Interface (CLI) then click next
  - In Set description tag - optional click Create access key button and do not fill anything on Description tag value
  - Click Download .csv file button in Retrieve access keys then click Done
  - Access key ID     : AKIA4MTWH3E5VEOHMIGR
  - Secret access key : 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

## 3. ECR
  - Type ECR (Elastic Container Registry) on Search 
  - Click Create
  - Visibility settings -> Private
  - Repository name -> 851725244731.dkr.ecr.ap-southeast-2.amazonaws.com/ -> "kidney"
  - Click Create Repository
  - Click Copy URI ```851725244731.dkr.ecr.ap-southeast-2.amazonaws.com/kidney```
  - Region -> Asia Pasific (Sydney) ap-southeast-2

## 4. EC2 (Elastic Compute Code): It is virtual machine
  - Type EC2 on Search 
  - Click Launch instance
  - Name and tags -> "kidney-machine"
  - Choose -> Ubuntu Machine
  - Choose -> Ubuntu Server 22.04 LTS
  - Key pair -> Click -> Create new key pair
  - Key pair name -> kidney
  - Key pair type -> RSA
  - Private key file format -> .pem
  - Create key pair
  - Configure Storage
    - 1x32 GiB
    - gp2
  - Click Launch instance
  - Goto Instance -> https://ap-southeast-2.console.aws.amazon.com/ec2/home?region=ap-southeast-2#Instances:
  - Click Instance ID -> i-07191b02b8fe2d769
  - Click Connect button -> Connect button again
  - go to https://ap-southeast-2.console.aws.amazon.com/ec2-instance-connect/ssh?connType=standard&instanceId=i-07191b02b8fe2d769&osUser=ubuntu&region=ap-southeast-2&sshPort=22#/
  - sudo apt-get update -y
  - sudo apt-get upgrade -y -> just enter if something pop up
  - Install Docker #required
    - curl -fsSL https://get.docker.com -o get-docker.sh
    - sudo sh get-docker.sh
    - sudo usermod -aG docker ubuntu
    - newgrp docker
    - Check is docker install or not -> docker --version
  - Github Setting
    - Click Setting button
    - Click Action -> Runner -> New self-hosted runner
    - Choose Linux
    - Architecture -> x64
    - Create a folder
    - # Create Directory
      - $ mkdir actions-runner && cd actions-runner
    - # Download the latest runner package
      - $ curl -o actions-runner-linux-x64-2.317.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.317.0/actions-runner-linux-x64-2.317.0.tar.gz
    - # Optional: Validate the hash
      - $ echo "9e883d210df8c6028aff475475a457d380353f9d01877d51cc01a17b2a91161d  actions-runner-linux-x64-2.317.0.tar.gz" | shasum -a 256 -c
    - # Extract the installer
      - $ tar xzf ./actions-runner-linux-x64-2.317.0.tar.gz
    - # Create the runner and start the configuration experience
      - $ ./config.sh --url https://github.com/wildenali11/Kidney-Disease-Classification-EndToEnd --token APMI33OXM5JOB7PT3X3ITCDGSVDJY
      - Enter the name of the runner group to add this runner to: [press Enter for Default] -> Just enter
      - Enter the name of runner: [press Enter for ip-172-31-1-72] (fill with) -> self-hosted
      - Enter any additional labels (ex. label-1,label-2): [press Enter to skip] -> Just enter
      - Enter name of work folder: [press Enter for _work] -> Just enter
    - # Last step, run it!
      - $ ./run.sh
    - Back to Runner in github, see status is Idle
    - # Setup github secrets
      - Click Settings
      - Click Secrets and variables -> Actions -> New repository secrets
        - Name: AWS_ACCESS_KEY_ID
        - secret: AKIA4MTWH3E5VEOHMIGR
        - Click Add secret
      - Click Secrets and variables -> Actions -> New repository secrets
        - Name: AWS_SECRET_ACCESS_KEY
        - secret: LbWVGvtECZDKgiHoODVM2Rl1V5OXwh7wrVYIbsAb
        - Click Add secret
      - Click Secrets and variables -> Actions -> New repository secrets
        - Name: AWS_REGION
        - secret: ap-southeast-2
        - Click Add secret
      - Click Secrets and variables -> Actions -> New repository secrets
        - Name: AWS_ECR_LOGIN_URI
        - secret: 851725244731.dkr.ecr.ap-southeast-2.amazonaws.com
        - Click Add secret
      - Click Secrets and variables -> Actions -> New repository secrets
        - Name: ECR_REPOSITORY_NAME
        - secret: kidney    # this one from 851725244731.dkr.ecr.ap-southeast-2.amazonaws.com/kidney
        - Click Add secret