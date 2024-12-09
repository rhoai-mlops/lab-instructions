# Inner loop Data Version
[dvc + quick little guide on how to version data]  
Let's start by looking at Data Versioning using DVC in the inner loop. We will later move on to the outer loop by modifying our pipelines to automatically account for data version.  

### (tiny) ETL

Before we start versioning the data, we need to have it somewhere we control.  
Besides GitHub not being the best place for storing data, because of the max storage limit they have, we may also want to store it inside our cluster.  
For this, we will have a S3 bucket that can hold our data, and we will version the data inside that bucket.  

Let's start by moving some data into the bucket.  

Open up the Jupyter Notebook workbench and navigate to `5-data-versinoing`.  
Inside here you will find a file called `1-data_pipeline_url_to_s3.py`.  
This pipeline will move the data we currently have in GitHub over to our S3 bucket. Later on we will also let the pipeline automatically version our data, but for now we just need to get some data.  

Click on Run button to start the pipeline.

### Data Versioning

Now that we have the data in an S3 bucket, we can go ahead and go through the two notebooks...