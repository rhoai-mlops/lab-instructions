## Kubeflow Pipelines (KfP)

Kubeflow Pipelines (KfP) is a platform designed for building and deploying portable, scalable machine learning pipelines using containers (and no, it's not related to Kung Fu Panda 🐼). KfP provides advanced capabilities such as versioning, metadata tracking, and resource management, which enable teams to monitor and optimize their pipelines efficiently—features that we currently lack in Elyra.

While Elyra was great for quick experimentation, KfP offers the robustness we need for running pipelines continuously. With KfP, we can have better logging, error handling, retry logic, and other production-level features. Essentially, this will become our production-grade training pipeline. And it will be automatically triggered based on source code updates, the arrival of new data, or alerts signaling unusual model behavior. (spoiler, spoiler🤭🤭)

1. You can find the pipeline definition in the `3-prod_datascience` folder.

    If you explore the files in this folder, you'll notice that they largely mirror the steps we previously executed in our notebooks. However, these steps have been broken down into individual functions and organized into separate files to improve modularity. This makes the pipeline easier to update and maintain over time.

    ![kfp.png](./images/kfp.png)

2. As we mentioned, we are not supposed to trigger this pipeline manually but just to test the functionality and view the output, let's run it by clicking ▶️ on the file `prod_train_save_pipeline.py`

    ![kfp-run.png](./images/kfp-run.png)

    You need to see an output like this:

    <div class="highlight" style="background: #f7f7f7">
    <pre><code class="language-yaml">
        Connecting to Data Science Pipelines: https://ds-pipeline-dspa.<USER_NAME>>.svc:8443
        /opt/app-root/lib64/python3.11/site-packages/kfp/dsl/component_decorator.py:121: FutureWarning: The default base_image used by the @dsl.component decorator will switch from 'python:3.8' to 'python:3.9' on Oct 1, 2024. To ensure your existing components work with versions of the KFP SDK released after that date, you should provide an explicit base_image argument and ensure your component works as intended on Python 3.9.
        return component_factory.create_component_from_func(
        /opt/app-root/lib64/python3.11/site-packages/kfp/client/client.py:159: FutureWarning: This client only works with Kubeflow Pipeline v2.0.0-beta.2 and later versions.
        warnings.warn(
        <IPython.core.display.HTML object><IPython.core.display.HTML object>
    </code></pre></div>


3. Go to OpenShift AI UI. Select `Experiments` from the left menu and go to `Experiments and runs`. You'll see there is one run with the status `Running`. Click to see the details of the pipeline run.

    ![experiments.png](./images/experiments.png)

    You'll be able to get many details such as;

    - the relationship between the steps
    - the output of each step
    - the artifacts that are generated
    - the metrics and graphs 

    ![experiments-2.png](./images/experiments-2.png)

    Feel free to spend some time in this view to explore more! 

4. Next step is to prepare the environment for MLOps practices 🙌