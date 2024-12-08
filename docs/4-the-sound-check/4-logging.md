## Aggregated Logging

> OpenShift’s built in logging is deployed as an operator using the LokiStack. By default collects all output from all containers that are logging to system out. This means no logging needs to be configured explicitly in the application. Logs are collected using a collector running on each nodes, then popped into LokiStack where they are indexed in a timeseries as JSON. OpenShift has a built in visualisation UI, but you can also use an external Grafana as well.


1. OpenShift magic provides a great way to collect logs across services, anything that’s pumped to STDOUT or STDERR is collected and added to LokiStack. This makes indexing and querrying logs very easy. Let’s take a look at OpenShift Logs UI now.

    ![openshift-logging](./images/openshift-logging.png)


2. Let’s filter the information, look for the logs specifically for jukebox apps running in the test nameaspace by adding this to the query bar. Click `Show Query`, paste the below and then hit `Run Query`.

    ```bash
    { log_type="application", kubernetes_pod_name=~"jukebox-ui.*", kubernetes_namespace_name="<USER_NAME>-test" }
    ```

    ![openshift-logging-2.png](./images/openshift-logging-2.png)


3. Container logs are ephemeral, so once they die you’d loose them unless they’re aggregated and stored somewhere. Let’s generate some messages and query them from the UI. Connect to UI pod via rsh and generate logs.

    ```bash
    oc project <USER_NAME>-test
    oc rsh `oc get po -l app.kubernetes.io/name=jukebox-ui -o name -n <USER_NAME>-test`
    ```

    Then inside the container you’ve just remote logged on to we’ll add some nonsense messages to the logs:

    ```bash
    echo "🦄🦄🦄🦄" >> /tmp/custom.log
    tail -f /tmp/custom.log > /proc/1/fd/1 &
    echo "🦄🦄🦄🦄" >> /tmp/custom.log
    echo "🦄🦄🦄🦄" >> /tmp/custom.log
    echo "🦄🦄🦄🦄" >> /tmp/custom.log
    echo "🦄🦄🦄🦄" >> /tmp/custom.log
    exit
    ```

4. Back on OpenShift UI > Observe > Logs. We can filter and find these messages with another query:

    ```bash
    { log_type="application", kubernetes_pod_name=~"jukebox-ui.*", kubernetes_namespace_name="<USER_NAME>-test" } |= `🦄🦄🦄🦄` | json
    ```

    ![openshift-logging-3.png](./images/openshift-logging-3.png)