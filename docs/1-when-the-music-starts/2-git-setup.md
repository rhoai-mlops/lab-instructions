## Setup GitLab

Now we’ll setup our git projects to store our code and configuration. Spoiler alert: be on the watch out for GitOps 🦄🔥


1. Use the same credentials to login to GitLab [here](https://<GIT_SERVER>):

    ```bash
    https://<GIT_SERVER>
    ```

2. Now lets create the git repository that we are going to use to store out Notebooks. Hit `New project` button on the right hand side
    ![gitlab-new-project](images/gitlab-new-project.png)

3. On the new view, use `jukebox` as Project Name, select **Internal** for Visibility level, then hit Create project.
    ![gitlab-new-project](images/gitlab-new-project-2.png)

4. Now let's go back to Jupyter Notebook. On the Launcher page, click `Terminal` at the bottom left and run below commands to push the `jukebox` code to the GitLab server.

    ![jupyter-terminal.png](images/jupyter-terminal.png)

5. Let's push our code to the GitLab server. Run the below commands:

    ```bash
    cd /opt/app-root/src/jukebox
    git remote set-url origin https://<GIT_SERVER>/<USER_NAME>/jukebox.git
    ```

    Use your username and password when you are prompted for the password (this will be cached).

    ```bash
    git push -u origin --all
    ```

    Now we are almost there with our initial setup!

    <p class="tip">
    ⛷️ <b>TIP</b> ⛷️ - If your credentials are cached incorrectly, you can try clearing the cache using: <strong>git credential-cache exit</strong>
    </p> 