

observe the fetch data changes from S3

make the change in the pipeline file

push the changes (pipeline change + dvc file)

+ observe model registry for the update



1. Go back to your Jupyter Notebook and Open up `jukebox/3-prod_datascience/prod_train_save_pipeline.py` file. We will update `fetch_data` step to use DVC now. 

    We need to repla

    ```python
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

