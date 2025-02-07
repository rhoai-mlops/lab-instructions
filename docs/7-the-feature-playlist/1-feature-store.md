# Feast

## What is a Feature, and Why Does it Matter?

Features are measurable properties or characteristics of data that are used to train a model. In our case song attributes such as `danceability`, `energy`, and `valence` are important features that play a critical role to predict the likelihood of a song becoming a hit in which country.


## What is a Feature Store?

A `Feature Store` is a centralized repository where features like those listed above are:

- **Managed:** Each feature (e.g., danceability, tempo) is engineered, versioned, and documented so that its definition is consistent and easy to understand.
- **Stored:** Features are stored in a way that allows fast access during both model training and real-time predictions.
- **Shared:** Features created for one project, such as predicting hit songs, can be reused in another project, like analyzing trends across countries.
  
  In the context of our dataset, a feature store ensures that features like `energy` and `speechiness` are consistent, up-to-date, and they look the same in both training and serving.


## How does Feast work?

Feast (**Fea**ture **St**ore, cool name right?✨) is a framework that registers and keeps track of features and that's what we are going to use in this section.

Feast has three components:
1. **Offline Store:** A long-term storage system for historical feature data, used for training models.
2. **Registry:** A centralized metadata store that defines and tracks all features, their sources, and associated entities in the feature store.
3. **Online Store:** A low-latency storage system optimized for serving features in real-time during model inference.

In our case the `Registry` and `Online Store` will be stored in the same database for simplicity.

## Setting Up and Using Feast in the Inner Loop  

Let’s begin by exploring how to use Feast in the inner loop:  

1. Navigate back to your Jupyter Notebook workbench and open the folder `7-feature_store`.  
2. Inside this folder, locate the `feature_repo` directory. This is where the feature definitions are stored. Open the `features.py` file to review the features we’ve defined.  
3. Next, open the notebook `1-setup_feast.ipynb` located in the `7-feature_store` folder and execute the cells step-by-step. This will set up Feast and demonstrate how it works in the inner loop.  
4. You can also see the features you define in the Feast UI we have set up for the development environment (you will get to deploy it yourself later 💪): [https://feast-ui-<USER_NAME>.<CLUSTER_DOMAIN>](https://feast-ui-<USER_NAME>.<CLUSTER_DOMAIN>)
5. Once you’ve seen how Feast is used for inner loop tasks like feature exploration and training, we’ll move on to its role in the **outer loop**.  

