## Data Science Inner Loop

As in traditional software development world, here the inner loop represents the iterative process of building, testing, and refining machine learning models.

This inner loop is essential in data science because it allows for continuous improvement and optimization of machine learning models. The principal stages we usually see in building ML models are as below:

- Data Preparation: Gathering, cleaning, and transforming data into a suitable format for model training.
- Model Development: Selecting and implementing appropriate machine learning algorithms.
- Model Training: Feeding the prepared data into the model and adjusting its parameters to learn patterns and relationships.
- Model Evaluation: Assessing the model's performance using metrics like accuracy, precision, recall, and F1-score.
- Model Refinement: Iterating on the previous steps to improve the model's accuracy and generalization capabilities.

Let's get some experience on these stages by following the steps in the notebooks we cloned to our workbench. It all starts with getting familiar with the dataset at hand, so we will start with `jukebox/1-data_exploration/1-data_exploration.ipynb` notebook.

In a notebook, each box is called a `cell`. There are three kinds of cell: code cells, where you can write and execute code; markdown cells, where you can add documentation; and raw cells, which we don't need to worry about here. When you execute a code cell, it's output is shown directly below the cell. Select the first code cell and execute it by clicking ▶️ button on the top bar or typing Shift+Enter. This will execute the cell and advance to the next cell. Work through all the cells sequentially.

At the end, we have a working model saved in Minio and we can serve it from OpenShift AI. 

![jupyter_notebook.png](./images/jupyter_notebook.png)

Now it's time to start executing the `jukebox/1-data_exploration/1-data_exploration.ipynb` notebook. Be sure to read all instruction - including th instructions at the end which tell you what follow-on notebooks to execute. You will execute the following notebooks in order:

1. `jukebox/1-data_exploration/1-data_exploration.ipynb`
2. `jukebox/2-dev_datascience/1-experiment-train.ipynb`
3. `jukebox/2-dev_datascience/2-save_model.ipynb`

Once you have executed the last notebook, you should have a model saved in the `models` bucket in Minio, now come back here to follow the next steps 😁

![model_in_bucket.png](./images/model_in_bucket.png)


### Model Serving

Now that we have our model artifacts saved in the bucket, we can deploy it in our data science project and serve it from a container. The beauty of OpenShift AI, and the underlying KServe technology, we don't have to worry about the containerization of the model. All we have to do is select the right runtime for our model and point where to model is. Let's give it a try:

1. Go to your data science project > Models > Select Single-Model Serving Platform by clicking Deploy Model.

![single-model-serving.png](./images/single-model-serving.png)

2. Fill out the form by the following information:

- Model name: `jukebox`
- Serving runtime: `OpenVino Model Server`
- Model framework: `onnx -1`
- Model server replicas: `1`
- Compute resources per replica: `Small`
- Model location: 
    -  Select from existing data connection and pick `models`
    - Path: `models/jukebox`

..and hit `Deploy`

![jukebox.png](./images/jukebox.png)

3. It will take some time (cause in the background, OpenShift AI pulls the runtime image, downloads your model from Minio bucket, copies to the right folder and starts the runtime), but eventually you'll get an endpoint that enable you to interract with the model! You will need to click on ```Internal Service``` link to get the endpoint URL.

![jukebox-deployed.png](./images/jukebox-deployed.png)

4. Copy that URL and go back to your Workbench. Open up the `jukebox/2-dev_datascience/3-request_model.ipynb` notebook and follow the instructions to make some sweet predictions ✨