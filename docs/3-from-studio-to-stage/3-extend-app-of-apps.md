# Extend Application of Applications

We need to add two more application to our MLOps toolings in order to run our continous training pipeline successfull; KubeFlow Registry & Data Science Pipelines Application (DSPA).

These two were already installed in your dev environment. Now we need to bring them in with GitOps.

1. Add the below yaml to `mlops-gitops/toolings/values.yaml` for KubeFlow Registry.

    ```yaml
      # KubeFlow Model Registry
      - name: model-registry
        enabled: true
        source: https://github.com/kubeflow/model-registry/
        source_path: manifests/kustomize/overlays/db
        source_ref: v0.2.7-alpha
        kustomize: true
    ```

2. And deploy Data Science Pipeline Application by copying the yaml to `mlops-gitops/toolings/values.yaml`

    ```yaml
      # Data Science Pipeline Application
      - name: dspa
        enabled: true
        source: https://<GIT_SERVER>/<USER_NAME>/mlops-helmcharts.git
        source_path: charts/dspa
        source_ref: "main"
    ```

3. Before we push our changes - we would like to sync our changes AS SOON AS updates hit the git repo! But Argo CD has a cycle time of about 3ish mins by default - this is too slow for us. However we can make Argo CD sync our changes instantly. For that, let’s add a webhook to connect Argo CD to our GitOps repository. Get ArgoCD URL with following:

    ```bash
    echo https://$(oc get route argocd-server --template='{{ .spec.host }}'/api/webhook  -n <USER_NAME>-mlops)
    ```
4. Go to Gitea > `mlops-gitops` repository > Settings from top left. From the Settings page, click Webhooks and add a new Webhook as Gitea type.

![gitea-argocd-webhook.png](./images/gitea-argocd-webhook.png)

5. Copy the Argo CD URL you get from the previous command as `Target URL` and hit Add Webhook.

![gitea-argocd-webhook-2.png](./images/gitea-argocd-webhook-2.png)


6. And now, let's push the changes to our GitOps repository.

    ```bash
    cd /opt/app-root/src/mlops-gitops
    git add .
    git commit -m  "😻 ADD - Model Registry and DSPA 😻"
    git push
    ```

7. Check Argo CD to see the deployed applications :)

![model-registry-dspa.png](./images/model-registry-dspa.png)