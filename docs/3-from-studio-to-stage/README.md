# Exercise 3 - From Studio to Stage
> Introduction to MLOps: a set of practices that automate and simplify machine learning workflows and deployments. 

## 👨‍🍳 Exercise Intro
In this exercise we will create our MLOps environment where the continuous training pipeline and the supporting toolings will be running.

## 🖼️ Big Picture

![big-picture-pipeline.jpg](./images/big-picture-pipeline.jpg)

## 🔮 Learning Outcomes

- [ ] Get familiar with MLOps concept
- [ ] Deploy the necessary toolings to build & deploy models automatically
- [ ] Understand tracking important metadata

## 🔨 Tools used in this exercise
* <span style="color:blue;">[OpenShift GitOps](https://argoproj.github.io/argo-cd/)</span> - A controller which continuously monitors application and compares the current state against the desired state
* <span style="color:blue;">[OpenShift Pipelines](https://tekton.dev/)</span> -  Cloud Native CI/CD tool, allowing us to build, test, and deploy anywhere
* <span style="color:blue;">[Kubeflow Model Registry](https://www.kubeflow.org/docs/components/model-registry/)</span> - Provides a central index for Machine Learning model metadata