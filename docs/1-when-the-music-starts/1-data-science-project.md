## Data Science Project

1. Login to [OpenShift AI](https://rhods-dashboard-redhat-ods-applications.<CLUSTER_DOMAIN>). The link and the credentials will be provided by your instructor. You'll see there are already two `Data Science Projects` created for you. 

![datascienceproject.png](./images/datascienceproject.png)

2. Click on the <USER_NAME> project. This project will be the place where we create our Jupyter Notebook environment, train our model and deploy our model.

![datascienceproject-2.png](./images/datascienceproject-2.png)


3. Let's create a notebook. Click `Create a Workbench`. OpenShift AI UI is pretty intiutive, isn't it? :)

   Select a name you want, could be something like `<USER_NAME>-hitmusic-wb` 🎺

    For Notebook Image: 

    - Image selection: `Standard Data Science`

    - Version selection: `2024.2`

    - Container size: `Small`
    - Cluster storage: `Create new persistent storage` with size `20 GB`. 
    
    - Check `Use a data connection` and choose the second option `Use existing data connection`
    
      From the dropdown menu, select `models`
       

    And finally, hit `Create workbench`.

4. When the status of the new workbench indicates 'Running', click `Open`.

    ![create-a-workbench.png](./images/create-a-workbench.png)

   It will redirect you to the Jupyter Notebook UI. You need to use your credentials again to log in. If you see the below screen, click `Allow selected permissions`. That will redirect you to your Jupyter Notebook.

    ![create-a-workbench-4.png](./images/create-a-workbench-4.png)

5. There are a couple of Git repositories already set up under your username in Gitea server. You can verify them by logging in Gitea [here](https://<GIT_SERVER>):

    ```bash
    https://<GIT_SERVER>
    ```
6. Use the same credentials to login and verify that you have 4 repositories waiting to be user for the upcoming exercises. Spoiler alert: be on the watch out for GitOps 🦄🔥

  ![gitrepositories.png](./images/gitrepositories.png)

7. Now, we'll begin by cloning the `Jukebox` repository, which contains the model source code. Go back to your Jupyter Notebook, click the Git icon, and copy the GitHub link to **clone** the repository.

    ```bash
    https://<GIT_SERVER>/<USER_NAME>/jukebox.git
    ```

    ![notebook-clone-repo.png](./images/notebook-clone-repo.png)

    After cloning the repository, you should see the `jukebox` folder in the left-hand panel.

    ![jupyter-notebook-ui.png](./images/jupyter-notebook-ui.png)

8. Before we begin, let’s review the type of S3 storage environment available for our experimentation. 🫡