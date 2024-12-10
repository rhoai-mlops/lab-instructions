# Exercise 5 - The Data Tracks
>  Data versioning is the practice of keeping track of different versions of a dataset as it changes over time.

## 👨‍🍳 Exercise Intro
In this exercise, we’ll enhance traceability by introducing versioning for our training data. Next, we’ll build a scheduled ETL pipeline that versions the updated training data and pushes the version information to the Jukebox repository. This action will automatically trigger the training pipeline to use the newly versioned data for model training.

## 🖼️ Big Picture

![big-picture-dvc.jpg](./images/big-picture-dvc.jpg)

## 🔮 Learning Outcomes
- [ ] Can use DVC to version the data 
- [ ] Can schedule a pipeline

## 🔨 Tools used in this exercise
* <span style="color:blue;">[DVC](https://dvc.org/)</span> - Manage and version data