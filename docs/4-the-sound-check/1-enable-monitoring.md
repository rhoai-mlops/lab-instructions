## User Workload Monitoring

> OpenShift’s has monitoring capabilities built in. It deploys the Prometheus stack and integrates into the OpenShift UI for consuming cluster metrics. 

1. If click on `jukebox` model, you can see the graphs about incoming requests, CPU and memory consumption to give you an idea about the model utilization. 

#### TODO: insert graph here

2. There are other metrics OpenShift collects out of the box. You can run queries for the existing metrics easily with `promql`, a query language for Prometheus. On the OpenShift UI, go to Observe, it should show basic health indicators just like OpenShift AI UI.


3. Run a promql query to get some info about the successfull requests to `jukebox` in your test environment.

    ```bash
    ovms_requests_success{namespace="<USER_NAME>-test", interface="REST"}
    ```

_You can generate some traffic by running some querries from the Jukebox UI 🎶_


### Deploy Grafana

> Let's create some more dashboards with specific information about our model!

1. Let's deploy a Grafana instance in our `mlops` environment. Yet another tooling to support the end to end journey of Jukebox! Therefore we need to install it through `mlops-gitops/toolings/values.yaml`

    ```bash
      # Grafana
      - name: grafana
        enabled: true
        source: https://gitea-gitea.apps.cluster-75vtz.75vtz.sandbox1169.opentlc.com/user1/mlops-helmcharts.git
        source_path: charts/grafana
        source_ref: "main"
    ```

2. Commit the changes to the repo as you’ve done before.

    ```bash
    cd /opt/app-root/src/mlops-gitops
    git add .
    git commit -m "📈 Grafana added 📈"
    git push
    ```

3. Once this change has been sync’d (you can check this in Argo CD), let’s login to Grafana and view the predefined dashboards for Jukebox;

    ```bash
    # get the route and open it in your browser
    echo https://$(oc get jukebox-grafana --template='{{ .spec.host }}' -n <USER_NAME>-mlops)

    ```


Use `Log in with OpenShift` to login and display the dashboards. As we define the dashboards as code, all the changes you make here will be temproary, they won't persist. True GitOps 👻

4. Let's generate some more loads to populate the dashboards. You can use one of the popular load generating tools to send concurrent load to the model as below:


```bash
echo "example request body here" > /tmp/input.json
hey -z 30s -c 5 -m 443 -host jukebox-<USER_NAME>-test.<CLUSTER_DOMAIN> -D /tmp/input.json https://jukebox-<USER_NAME>-test.<CLUSTER_DOMAIN>
```

5. There are some dashboards that are not being populated and it is because we haven't enabled yet another exciting tool; Trusty AI. 