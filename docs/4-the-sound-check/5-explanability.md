# Explanability with TrustyAI

In the earlier section, we used TrustyAI to detect drift and bias, and set up monitoring for those. TrustyAI also provides tools for a variety of responsible AI workflows, such as local and global model explanations. 

To get some idea of why we get a specific output, we can apply different methods such as counterfactual analysis and SHAP values.
Counterfactual analysis will tell us what values we would have to input to get a different, desired, answer than the one we got.
SHAP values will tell us what input features likely had the biggest contribution to making the output what it is

1. Create a workbench with TrustyAI image - v3.9
add models data connection

We'l use TrustyAI workbench which already has all the . Click `Create a Workbench`. OpenShift AI UI is pretty intiutive, isn't it? :)

   Select a name you want, could be something like `trustyai-wb` 

    For Notebook Image: 

    - Image selection: `TrustyAI`

    - Version selection: `2024.2`

    - Container size: `Small`
    - Cluster storage: Create new persistent storage with size `20 GB`. 
    
    - Check `Use a data connection` and choose the second option `Use existing data connection`
    
      From the dropdown menu, select `models`
       

    And finally, hit `Create workbench`.

# add the image to image puller

2. Go through the Notebooks - 
1 - before using TrustyAI
4 - counterfactuals
5 - SHAP



