# List of good references

This is a list of good references and reading material you can refer to throughout the workshop.  
You will also find a glossary in case there are any words you are unsure of.  


## References
- [ai-on-openshift](https://ai-on-openshift.io/) - A great resource for deploying and managing AI applications on OpenShift, often using Red Hat's AI suite.
- [ai-on-openshift/gitops](https://ai-on-openshift.io/odh-rhoai/gitops/) - How to create OpenShift AI resources through Kubernetes yaml files.
- [Data Science Tutorial](https://www.w3schools.com/datascience/default.asp) - Code and guides for how you can use Python for Data Science with executable examples.
- [How Neural Networks Work Playlist](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) - A fantastic video guide that covers the basics of Neural Networks.
- [Tensorflow Playgrounds](https://playground.tensorflow.org/) - Tensorflow Plagrounds lets you play around with different settings and data for a small neural network to get a better understanding how it works.
- [Made With ML](https://madewithml.com/) - A extensive guide on ML and its lifecycle.
- [Google MLOps Blog](https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning) - Blog on the different stages of MLOps maturity, how you can transition between them and what you can see included in each stage.
- [Cookie Cutter Project Structure](https://cookiecutter-data-science.drivendata.org/) - A tool to initialize a data science project with a good project structure.

## Docs for AI Tools used
- [OpenShift AI](https://docs.redhat.com/en/documentation/red_hat_openshift_ai_self-managed/2-latest)
- [Kubeflow Pipelines](https://www.kubeflow.org/docs/components/pipelines/)
    - [Kubeflow Pipelines SDK](https://kubeflow-pipelines.readthedocs.io/en/sdk-2.12.0/)
    - [Kubeflow Pipelines Kubernetes SDK](https://kfp-kubernetes.readthedocs.io/en/kfp-kubernetes-1.4.0/)
- [TrustyAI](https://github.com/trustyai-explainability)
- [DVC](https://dvc.org/doc)
- [ModelScan](https://github.com/protectai/modelscan)
- [KServe](https://kserve.github.io/website/master/modelserving/control_plane/)
- [Feast](https://docs.feast.dev/)

## Glossary
- **MLOps** - The practices, culture, and tools that aim to reliably and efficiently build, deploy and maintain AI models in production.
- **ETL (Extract, Transform, Load)** - A process to collect (extract), clean/wrangle (transform), and store (load) data.
- **EDA (Exploratory Data Analysis)** - Analyzing data to understand patterns and issues.
- **Data Feature** - Individual, measurable, properties of data used in a model (e.g., age, temperature, transaction amount).
- **Feature Store** - A centralized system to manage and serve data features.
- **Feature Engineering** - Creating and modifying data features to improve models.
- **Neural Network** - A machine learning model built of multiple layers of "neurons", allowing it to handle great complexity.
- **Hyperparameter Tuning** - Adjusting general model settings, such as number of layers or learning rate, to improve performance.
- **Pipeline** - A sequence of automated steps which we can use to process data, train, and deploy models.
- **Training** - Teaching a machine learning model using data.
- **Inference** - Using a trained model to make predictions.
- **Kubeflow** - A library of tools for managing ML workflows on Kubernetes.
- **Argo CD** - A GitOps tool for automating deployments.
- **Model Registry** - A system to keep track of and manage different versions of models.
- **Canary Deployment** - Releasing a new model to a small group before full rollout.
- **Shadow Deployment** - Running a new model in parallel without affecting users.
- **Data Drift** - The data we are making predictions on starts looking significantly different than the data we trained on.
- **Bias Detection** - Identifying unfair or unintended biases in models.
- **SHAP (Shapley Additive Explanations)** - A method to explain model predictions by telling you how much each feature contributed to the prediction.
- **Counterfactuals** - Testing a variety of "what-if" changes to the input to see if any of them can change the output/prediction in a desired way.

## Diagrams