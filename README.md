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

	#with specific access

	1. EC2 access : It is virtual machine

	2. ECR: Elastic Container registry to save your docker image in aws


	#Description: About the deployment

	1. Build docker image of the source code

	2. Push your docker image to ECR

	3. Launch Your EC2 

	4. Pull Your image from ECR in EC2

	5. Lauch your docker image in EC2

	#Policy:

	1. AmazonEC2ContainerRegistryFullAccess

	2. AmazonEC2FullAccess

	
## 3. Create ECR repo to store/save docker image
    - Save the URI: 566373416292.dkr.ecr.us-east-1.amazonaws.com/chicken

	
## 4. Create EC2 machine (Ubuntu) 

## 5. Open EC2 and Install docker in EC2 Machine:
	
	
	#optinal

	sudo apt-get update -y

	sudo apt-get upgrade
	
	#required

	curl -fsSL https://get.docker.com -o get-docker.sh

	sudo sh get-docker.sh

	sudo usermod -aG docker ubuntu

	newgrp docker
	
# 6. Configure EC2 as self-hosted runner:
    setting>actions>runner>new self hosted runner> choose os> then run command one by one


# 7. Setup github secrets:

    AWS_ACCESS_KEY_ID=

    AWS_SECRET_ACCESS_KEY=

    AWS_REGION = us-east-1

    AWS_ECR_LOGIN_URI = demo>>  566373416292.dkr.ecr.ap-south-1.amazonaws.com

    ECR_REPOSITORY_NAME = simple-app