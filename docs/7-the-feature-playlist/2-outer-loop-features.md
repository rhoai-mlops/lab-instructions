# GitOps Feast

Now let's set up Feast so we can use it in our outer loop.  
We will start by adding our feast-database to Argo.  

```bash
mkdir /opt/app-root/src/mlops-gitops/toolings/feast-database
touch /opt/app-root/src/mlops-gitops/toolings/feast-database/config.yaml
```

```yaml
chart_path: charts/feast-database
USER_NAME: <USER_NAME>
git_server: <GIT_SERVER>
```

```bash
cd /opt/app-root/src/mlops-gitops
git add .
git commit -m  "🍕 ADD - Feast Database 🍕"
git push
```

This feast database is a simple postgressql database, and it will act as both our feature store registry (where we keep track of what features we have and where they are stored) and our online store (for real-time feature retrieval).  

Run this to get access to the UI and browse your features:
```bash
echo https://$(oc get route feast-ui --template='{{ .spec.host }}' -n <USER_NAME>-mlops)
```

# Feast in our training pipeline


# Automatically apply new changes


# Automatically materialize new data


Feast is now fully set up and working in your MLOps environment!  
Let's deploy a model that can use the online feature store.