# Autoscaling

Autoscaling ensures optimal performance during high-demand periods by provisioning additional resources while minimizing costs by scaling down during low activity. This is important for us because Machine Learning workloads, such as model training and inference, often experience fluctuating resource requirements. 

Luckily for us, autoscaling based on the incoming request load is quite easy with KServe and OpenShift.

1. Let's enable autoscaling in `InferenceService` for test environment by updating `mlops-gitops/model-deployments/test/jukebox/config.yaml` on `<USER_NAME>-mlops-toolings` workbench (code-server). Add `autoscaling: true` to the config file.

    ```bash
    ---
    chart_path: charts/model-deployment/music-transformer
    name: jukebox
    version: 4562a17c17 # 🚩⚠️ this value can be different for you
    image_repository: image-registry.openshift-image-registry.svc:5000
    image_namespace: <USER_NAME>-test
    autoscaling: true # 👈 add this
    ```

    This will update the `InferenceService` by adding the below annotation, and trigger a new model deployment with autoscaling capability! 

    <div class="highlight" style="background: #f7f7f7">
    <pre><code class="language-yaml">
    ---
    apiVersion: serving.kserve.io/v1beta1
    kind: InferenceService
    metadata:
    annotations:
      openshift.io/display-name: jukebox
      serving.knative.openshift.io/enablePassthrough: 'true'
      sidecar.istio.io/inject: 'true'
      sidecar.istio.io/rewriteAppHTTPProbers: 'true'
      autoscaling.knative.dev/target: "1" ### 👈 this does the magic 🔮
    </code></pre></div>

2. Push the changes:

    ```bash
    cd /opt/app-root/src/mlops-gitops
    git pull
    git add .
    git commit -m  "💸 UPDATE - autoscaling enabled 💸"
    git push
    ```
    
3. Wait for the model to be redeployed, you can keep track of the pods like before: `oc get po -n <USER_NAME>-test -w` (Ctrl+C to cancel out of it).

4. Let's test the autoscaling by generating some load. Go to your Jupyter Notebook `<USER_NAME>-hitmusic-wb` workbench (Standard Data Science) and go through Notebook `jukebox/6-advanced_deployment/1-test_autoscale.ipynb`.  

> ⚠️ When entering the inference endpoint, make sure to enter the one for your model served in `<USER_NAME>-test`.

5. Go to `OpenShift Dashboard` in Administrator view > `<USER_NAME>-test` project > `Workloads` > `Pods` and observe that a new pod is coming up.

    ![autoscaling-1.png](./images/autoscaling-1.png)

6. Since this is *auto*scaling, the extra resources will be automatically removed once they are no longer needed—that is, when there are no concurrent requests. After a short while, you'll notice that the same pod will begin terminating.

    ![autoscaling-2.png](./images/autoscaling-2.png)
