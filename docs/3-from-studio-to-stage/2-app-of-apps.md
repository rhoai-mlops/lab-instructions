## Application of Applications

# Get Gitea Ready for GitOps

> In this exercise we'll connect Argo CD (our gitOps controller) to our git repository to enable the GitOps workflow. We will be storing definitions of toolings and model deployments in `mlops-gitops` repository and make Argo CD aware of that repo.

1. Log into Gitea with your credentials. Gitea URL:

    ```bash
    https://<GIT_SERVER>
    ```

    You will see a `mlops-gitops` repository already created for you. It is the git repository that we are going to use for <span style="color:purple;" >GIT</span>Ops purposes. It will serve as a mono-repo holding both our tooling configuration and the model deployment definitions. In the real world, you may want to separate these into different repos! Anyways, let's get started!

    ![gitea-mlops-gitops.png](images/gitea-mlops-gitops.png)

2. Let's go back to terminal and clone the repository.

    ```bash
    cd /opt/app-root/src
    git clone https://<GIT_SERVER>/<USER_NAME>/mlops-gitops.git
    ```

   With our git project cloned - let's start our GitOps Journey 🧙‍♀️🦄!

    <p class="tip">
    ⛷️ <b>TIP</b> ⛷️ - If your credentials are cached incorrectly, you can try clearing the cache using: <strong>git credential-cache exit</strong>
    </p>

3. This `mlops-gitops` repository is actually just another Helm Chart with a pretty neat pattern built in to create App of Apps in Argo CD. Let's get right into it - in the your IDE, Open the `values.yaml` file in the root of the project. Update it to reference the git repo you just created and your team name. This values file is the default ones for the chart and will be applied to all of the instances of this chart we create. The Chart has Argo CD Application definition as a template, just like the one we manually created in the previous exercise when we deployed Minio in the UI of Argo CD.

    ```yaml
    source: "https://<GIT_SERVER>/<USER_NAME>/mlops-gitops.git"
    team: <USER_NAME>
    ```

4. The `values.yaml` file refers to the `toolings/values.yaml` which is where we store all the definitions of things we'll need for our countinuous training pipelines. The definitions for things like Minio, Tekton pipeline, Feast etc will all live in here eventually, but let's start small with two objects. One for boostrapping the cluster with some namespaces and permissions. And another one is Minio, so that we actually have the Minio definition in Git. Because as we said, this is GitOps, definitions have to be stored in ✨Git✨. Update your `toolings/values.yaml` by changing your `\<USER_NAME\>` in the bootstrap section so it looks like this:

    <div class="highlight" style="background: #f7f7f7">
    <pre><code class="language-yaml">
        applications:
        # Bootstrap Project
        - name: bootstrap
          enabled: true
          source: https://redhat-cop.github.io/helm-charts
          chart_name: bootstrap-project
          source_ref: "1.0.1"
          values:
            serviceaccounts: ""
            # student is the GROUP NAME in IDM
            bindings: &binds
              - name: student
                kind: Group
                role: admin
            namespaces:
              - name: <USER_NAME>-mlops
                bindings: *binds
                operatorgroup: true
              - name: <USER_NAME>-test
                bindings: *binds
                operatorgroup: true
              - name: <USER_NAME>-stage
                bindings: *binds
                operatorgroup: true
    </code></pre></div>



5. This is GITOPS - so in order to affect change, we now need to commit things! Let's get the configuration into git, before telling Argo CD to sync the changes for us.

    ```bash
    cd /opt/app-root/src/mlops-gitops
    git add .
    git commit -m  "🦆 ADD - correct project names 🦆"
    git push
    ```

  
  <p class="warn">
    ⛷️ <b>NOTE</b> ⛷️ - It may wait for you to enter your credentials on the top of the screen.
  </p>


6. In order for Argo CD to sync the changes from our git repository, we need to provide access to it. We'll deploy a secret to cluster, for now *not done as code* but in an upcoming section we'll tackle the secret as code and store it encrypted in Git. In your terminal create the Secret in your environment:

    ```bash
    cat <<EOF | oc apply -n <USER_NAME>-mlops -f -
      apiVersion: v1
      data:
        password: "$(echo -n <GIT_PASSWORD> | base64 -w0)"
        username: "$(echo -n <USER_NAME>| base64 -w0)"
      kind: Secret
      type: kubernetes.io/basic-auth
      metadata:
        annotations:
          tekton.dev/git-0: https://<GIT_SERVER>
          sealedsecrets.bitnami.com/managed: "true"
        name: git-auth
    EOF
    ```

7. Install the tooling (only bootstrap, and Minio at this stage..). Once the command is run, open the Argo CD UI to show the resources being created. We’ve just deployed our first AppOfApps!

    ```bash
    cd /opt/app-root/src/mlops-gitops
    helm upgrade --install argoapps --namespace <USER_NAME>-mlops .
    ```

    ![argocd-bootrstrap-tooling](./images/argocd-bootstrap-tooling.png)

8. As Argo CD sync's the resources we can see them in the cluster:

    ```bash
    oc get projects | grep <USER_NAME>
    ```

    ```bash
    oc get pods -n <USER_NAME>-mlops
    ```

🪄🪄 Magic! You've now deployed an app of apps to scaffold our tooling and projects in a repeatable and auditable way (via git!). Next up, we'll prepare our model deployment definitions. 🪄🪄
