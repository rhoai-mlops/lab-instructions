# Model Security

We can include model scanning to our pipeline to check Model Serialization Attack

A Model Serialization Attack can be used to execute:

Credential Theft(Cloud credentials for writing and reading data to other systems in your environment)
Data Theft(the request sent to the model)
Data Poisoning(the data sent after the model has performed its task)
Model Poisoning(altering the results of the model itself)


## Include Model Scanning in the pipeline

1. We'll use an open source too called `modelscan` to scan the model to determine if they contain unsafe code. Let's go to Jupyter Notebook workbench to first get familiar with the tool. Open up the notebook `8-securing_ai/1-modelscan.ipynb` and run the cells to install `modelscan` library and initiate a scan. 


2. Now, let's create a task in our pipeline after the model is created but before generating the `modelcar` artifact. If the model has vulnerability to attack, no need to store it in our OCI registry since we are not going to deploy it.

    In order to do that, we need to update out update. Go over to code-server workbench and add below line to `mlops-gitops/toolings/ct-pipeline/config.yaml`. It will enable a Tekton task to run basically the same commands you just ran in the Notebook.


3. Commit and push the changes..

4. Create an empty commit to trigger the pipeline and perform scan.


