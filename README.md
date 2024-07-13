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
- 
