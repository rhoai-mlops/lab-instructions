# Explainability with TrustyAI

In the earlier section, we used TrustyAI to detect drift and bias, and set up monitoring for those. TrustyAI also provides tools for a variety of responsible AI workflows, such as local and global model explanations. These help us to understand why we get a specific output for a given input. 

We can apply different methods such as counterfactual analysis and SHAP values to get such insights. 

Counterfactual analysis will tell us what values we would have to input to get a different, desired, answer than the one we got.

SHAP (SHapley Additive exPlanations) values will tell us what input features likely had the biggest contribution to making the output what it is. 

Let's get started.

1. We'll use TrustyAI workbench which already has all the necessary libraries and configuration. It'll just make things easier for us. Go to `OpenShift AI Dashboard` >  `Data Science Projects` > `<USER_NAME>-jukebox` > `Workbenches` and click `Create a Workbench`.

  Select a name you want, could be something like `trustyai-wb` 

  For Notebook Image: 

  - Image selection: `TrustyAI`

  - Version selection: `2024.2`

  - Container size: `Small`

  - Cluster storage: Create new persistent storage with size `20 GB`. 

  - For Connections, choose `Attach existing connections`
    
    From the dropdown menu, select `models`

  Leave the rest as it is and hit `Create workbench`.


2. Open up the workbench when it is ready and clone Jukebox again.

  ```bash
    https://<USER_NAME>:<PASSWORD>@<GIT_SERVER>/<USER_NAME>/jukebox.git
  ```

3. Start by going to `jukebox/4-metrics/3-download-artifacts.ipynb` notebook and follow the instructions to download some artifacts from our training pipeline run that we need for the other notebooks. This way we will do explainability analysis on the model we trained and pushed to production.

4. Then go to the `jukebox/4-metrics/4-counterfactuals.ipynb` notebook and follow the instructions to see what input we would need to get some desired output.

5. After that, open up the next notebook `jukebox/4-metrics/5-SHAP.ipynb` to be able to explain the output of our Jukebox model :) 



