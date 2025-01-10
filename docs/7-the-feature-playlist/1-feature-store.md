# What is a Feature Store?
A feature store is a central place where teams can manage, store, and access the data features needed for training and serving models. It ensures that features are consistent, up-to-date, and easily reusable across different projects, as well as making sure that they look the same in both training and serving.


# How does Feast work?
Feast is a framework that registers and keeps track of features.

Small map over feast components:
1. Offline store
2. Registry
3. Online store
In this case the Registry and Online store will be stored in the same database.

# Setup and use Feast
Go throgh the inner loop to set up feast in the dev environment

Instructions:

1. Open up the jupyter notebook workbech.
2. Go to the folder 6-feature-store.
3. In here we have a folder called feature_repo with the feature definitions, go into it and open features.py to see what features we are defining.
4. Go back out of the featre_repo folder and into the notebook 1-setup_feast.ipynb and run the cells.
