# Operationalizing Machine Learning Project

This is a project for the Udacity Azure ML Course. We first train an AutoML model on the bank marketing dataset which is provided, deploy it, consume it and check its documentation using swagger. Then, we also create a pipeline that uses an AutoML module with the same dataset. The pipeline endpoint is also published.  

## Architectural Diagram
![Steps](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/step_diagram.png)

The key steps are mentioned below along with the necessary screenshots.

## Key Steps

### Authentication
I am using a company Azure account, which means that I dont have owner rights needed to create SP, and so I have skipped this step. 

### Automate ML Experiment
I upload the csv file bankmarketing_train.csv to the Azure ML Studio and create a dataset. 

![Dataset](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/dataset.png)

The next step involves creating an AutoML run. I create the run, run it on my compute and it runs various different algorithms to find the best one. 

![Completed Exp](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/experiment_AutoML.png)

The run creates a bunch of different models 

![Model](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/models.png)

The VotingEnsemble model turns out to be the best. This makes sense since Voting Ensemble uses a mixture of different models to get the best results. 

![Best Model](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/best_AutoML_Model.png)

### Deploy the Best Model 
The VotingEnsemble model is then deployed to create a REST Endpoint. Loggin is enabled which uses the logs.py file provided, and the Application Insights are also turned on. The file below shows the log output on the console.

![Log](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/logs.png)

The script also enables the Application Insights which can be checked in the studio. 

![Insights](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/activate_application_insights.png)

### Swagger Documentation
The next step is to deploy swagger UI to clearly interact with the deployed model. It tells you how do the inputs and outputs of the deployed model look like. 

![Swagger](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/swagger.PNG)

### Consume Model Endpoint
To consume the endpoint, I use the endpoint.py file, updating it with the REST Endpoint and the primary key. The endpoint returns the output as follows - 

![Endpoint](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/endpoint.png)

Although optional, I still run the benchmarking for the model, and none of the sent requests fail with quick response times.

![Benchmark 1](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/benchmark_1.PNG)
![Benchmark 2](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/benchmark_2.PNG)
![Benchmark 3](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/benchmark_3.PNG)

### Create and publish a pipeline <a name="publish" />
The next step is to create a pipeline out of the whole above process. This is done through the notebook which is in the repo. It imports various libraries, creates the compute, experiment, AutoML config and then creates a pipeline. 

Here we see the pipeline being created - 
![Pipeline Creation](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/pipeline_creation.png)

The pipeline once created can be called using a REST API endpoint. The pipeline endpoint and the details are below - 

![Pipeline Detail](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/automl_with_bankmarketing_dataset.PNG)

![Pipeline Endpoints](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/pipeline_endpoint.png)

![Published Pipeline](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/pipeline_REST.png)

The pipeline run is created as an experiment and can be seen here with a nice visualization of the pipeline- 
![Experiment](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/scheduled_run_pipeline.png)

The RunDetails widget gives us details in the notebook itself - 
![Widget Run](https://github.com/Neo96Mav/Azure_ML_Project_2/blob/main/screenshots/widget_running.png)

### README and Screencast

I created the ReadMe file containing the screenshots and the ScreenCast. The screencast can be found by clicking [here](https://youtu.be/0GNnMe4ju4w). I demonstrate all the working aspects of my project. 
  
## Suggestions for Future Work 
For future work, I think a good aspect would be to create a PythonScriptStep which involves cleaning the data, and then doing an AutoML run. Perhaps, a Hyperdrive run could be added to a good performing algorithm to increase the performance even more. I believe such steps will make the project more interesting. 
