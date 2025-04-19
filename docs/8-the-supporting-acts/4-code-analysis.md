# Sonarqube

> Sonarqube is a tool that performs static code analysis. It looks for pitfalls in coding and reports them. It’s great tool for catching vulnerabilities!

## Deploy Sonarqube using GitOps

1. Create a `sonarqube` folder under `mlops-gitops/toolings` folder

    ```bash
    mkdir /opt/app-root/src/mlops-gitops/toolings/sonarqube
    touch /opt/app-root/src/mlops-gitops/toolings/sonarqube/config.yaml
    ```

2. Open up the `sonarqube/config.yaml` file and paste the below yaml to `config.yaml`. It contains the information about where Argo CD can find the helm chart of SonarQube, and the values we'd like to provide to this helm chart. 

    ```yaml
    repo_url: https://github.com/redhat-cop/helm-charts.git
    chart_path: charts/sonarqube
    fullnameOverride: sonarqube
    account:
      username: admin
      password: <PASSWORD>
      currentAdminPassword: admin
    plugins:
      install:
        - https://github.com/checkstyle/sonar-checkstyle/releases/download/10.9.3/checkstyle-sonar-plugin-10.9.3.jar
        - https://github.com/dependency-check/dependency-check-sonar-plugin/releases/download/3.1.0/sonar-dependency-check-plugin-3.1.0.jar
    ```

    _Yup, we'd like to update the default admin password of SonarQube AND we are aware that it is not sensible to store credentials as plaintext here but we haven't discussed Secret Management with GitOps, so hang in there!🫣_

3. Push the changes and let Argo CD to deploy SonarQube:

    ```bash
    cd /opt/app-root/src/mlops-gitops
    git pull
    git add .
    git commit -m  "🦇 ADD - sonarqube 🦇"
    git push 
    ```

4. Connect to [SonarQube UI](https://sonarqube-<USER_NAME>-toolings.<CLUSTER_DOMAIN>/) to verify if the installation is successful (username `admin` & password `<PASSWORD>`).

    _It may take a few minutes to configure SonarQube._

    ```bash
    echo https://$(oc get route sonarqube --template='{{ .spec.host }}' -n <USER_NAME>-toolings)
    ```

    _And in case you logged out from the cluster, use below commands to login again._

    ```bash
    export CLUSTER_DOMAIN=<CLUSTER_DOMAIN>
    oc login --server=https://api.${CLUSTER_DOMAIN##apps.}:6443 -u <USER_NAME> -p <PASSWORD>
    ```

5. Before extending the pipeline witn SonarQube, we can run the code quality checks from our IDE. Fist, let's install the `pysonar` library.

    ```bash
    pip install pysonar-scanner
    ```

    and trigger a scan:

    ```bash
    pysonar-scanner -Dsonar.host.url=http://sonarqube.<USER_NAME>-toolings.svc.cluster.local:9000 -Dsonar.projectKey=jukebox -Dsonar.login=admin -Dsonar.password=<PASSWORD>
    ```

6. When the analysis completed, go back to [SonarQube UI](https://sonarqube-<USER_NAME>-toolings.<CLUSTER_DOMAIN>/), refresh the page and see that `jukebox` is under  `Projects`

    ![sonarqube-1.png](./images/sonarqube-1.png)

    Click on `jukebox` project and see the results of the analysis.

    ![sonarqube-2.png](./images/sonarqube-2.png)

    You can drill down on the issues that SonarQube identified.

    ![sonarqube-3.png](./images/sonarqube-3.png)

## Extend Pipeline

1. Now that we saw how SonarQube works, let's extend our pipeline to perform static code analysis check every time. Again, let's open up `mlops-gitops/toolings/ct-pipeline/config.yaml` and add `static_code_analysis: true` flag to introduce [the task](https://<GIT_SERVER>/<USER_NAME>/mlops-helmcharts/src/branch/main/charts/pipelines/templates/tasks/static-code-analysis.yaml).

    ```yaml
    chart_path: charts/pipelines
    USER_NAME: <USER_NAME>
    cluster_domain: <CLUSTER_DOMAIN>
    git_server: <GIT_SERVER> 
    alert_trigger: true 
    apply_feature_changes: true
    unit_tests: true
    linting: true 
    static_code_analysis: true # 👈 add this
    ```

2. Commit the changes to the repo:

    ```bash
    git pull
    cd /opt/app-root/src/mlops-gitops
    git add .
    git commit -m "🧦 ADD - static code analysis step 🧦"
    git push
    ```

3. Go to OpenShift Console > Pipelines in `<USER_NAME>-toolings` namespace > verify that the task is included in the Pipeline.

    ![sonarqube-task.png](./images/sonarqube-task.png)

4. _Optional_: Now you can make an empty commit to see the changes on the pipeline. However you can also continue to grow it with more exciting toolings! 

    ```bash
    cd /opt/app-root/src/jukebox
    git commit --allow-empty -m "🐹 trigger pipeline for SonarQube scan 🐹"
    git push
    ```

    ![sonarqube-task-success.png](./images/sonarqube-task-success.png)