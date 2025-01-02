## Update Continuous Training Pipeline with Data Versioning


1. Now that we are introducing DVC, we need to update our pipeline to stop fetching all the data from GitHub and fetch the data based on the dvc file we have at our `Jukebox` git repository instead. Therefore, we need to commentout the initial `fetch_data()` function and introduce a new one that calls dvc commands.
   
    In your Jupyter Notebook, open `jukebox/3-prod_datascience/prod_train_save_pipeline.py`, and comment out below line by putting ＃ in front of it, or when you are on that line, hit CTRL (Command) + Shift. 

    ```python
    ...
    def training_pipeline(hyperparameters: dict, model_name: str, version: str, cluster_domain: str, model_storage_pvc: str, prod_flag: bool):
        ### 🐶 Fetches Data from GitHub
        fetch_task = fetch_data() # 👈 Comment out this one
    ...
    ```

2. After you comment it out, add the below function right under it. You'll see the `🍇 Fetches data from DVC` comment there.

    ```python
        ### 🍇 Fetches data from DVC
        fetch_task = fetch_data_from_dvc(
            cluster_domain = cluster_domain,
            git_version = version
        )
        kubernetes.use_field_path_as_env(
            fetch_task,
            env_name='namespace',
            field_path='metadata.namespace'
        )

        kubernetes.use_secret_as_env(
            fetch_task,
            secret_name='aws-connection-data',
            secret_key_to_env={
                'AWS_S3_ENDPOINT': 'AWS_S3_ENDPOINT',
                'AWS_ACCESS_KEY_ID': 'AWS_ACCESS_KEY_ID',
                'AWS_SECRET_ACCESS_KEY': 'AWS_SECRET_ACCESS_KEY',
                'AWS_S3_BUCKET': 'AWS_S3_BUCKET',
            },
        )
    ```



3. Let's persist the changes in Git. On Jupyter Notebook commandline, 

    ```bash
    cd /opt/app-root/src/jukebox/
    git add 3-prod_datascience/prod_train_save_pipeline.py
    git comment -m "🍇 fetch data via DVC 🍇"
    git push
    ```

4. This push triggers our training pipeline, however since we haven't pushed any dvc config file to `Jukebox` repository, the pipeline will fail. We don't want to commit the dvc files manually everytime there is a change in our data. We want to automate this as well. Therefore, we need to introduce yet another pipeline: ETL pipeline.


### Data Pipeline with DVC Versioning

1. In your Jupyter Notebook, open up `5-data-versioning/4-data_pipeline_with_dvc_versioning.py` file and run this by clicking ▶️ button.

    This time, instad of triggering a pipeline, it created a YAML file. If you open up folder `5-data-versioning/` , refresh it by hitting Refresh button, you should see `song-properties-etl.yaml`

    Let's download this file and store locally. 

    ![data-pipeline-download.gif](./images/data-pipeline-download.gif)

2. In OpenShift AI Dashboard, go to `Data Science Pipelines`, click `Import pipeline`. Use `data-pipeline-with-dvc` as Pipeline name and upload the YAML file you just downloaded to your local. 

TODO: explanation + a diagram for the pipeline

3. Ideally next thing we can do is to setup a reoccuring run of this pipeline by scheduling it, let's say once in every day however for the sake of the exercise, let's just create a run for now. 


4. If you check `Jukebox` git repository now, you should be able to see a `.dvc/config` folder and a `song_properties.parquet.dvc` file. DVC files were pushed by the data pipeline, which means Continuous Training Pipeline must have been triggered. 

    Now that apart from code change and alerts, the pipeline gets triggered when there is fresh data.

