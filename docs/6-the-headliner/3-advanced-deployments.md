# Advanced Deployments

Machine Learning models often need to integrate with existing systems, and ensure security and compliance. Advanced deployment practices, such as CI/CD pipelines, canary releases, and model versioning, enable faster updates, minimize downtime, and reduce risks.

## Canary Deployments

Traffic splitting in test - promote one to prod

    ```bash
    canary:
      trafficPercent: 10
    ```

    This will redeploy the previous version automatically do split the traffic based on the percentage we provided above. 

    ```bash
    oc get isvc -n <USER_NAME>-test
    ```

    ```bash
        NAME      URL                                                 READY   PREV   LATEST   PREVROLLEDOUTREVISION     LATESTREADYREVISION       AGE
        jukebox   https://jukebox-<USER_NAME>-test.<CLUSTER_DOMAIN>   True    90     10       jukebox-predictor-00013   jukebox-predictor-00014   25h
    ``` 


    Let's use the locust script again to generate some traffic and verify the both deployments receive traffic. We can use on monitoring for that.

    We can incrementally increase the traffic percantage towards the latest version by updating the values file and set it `100` when we decide to use the latest version only. 

