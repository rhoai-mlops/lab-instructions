## Feast Server and UI

```bash
mkdir /opt/app-root/src/mlops-gitops/toolings/feast-server
touch /opt/app-root/src/mlops-gitops/toolings/feast-server/config.yaml
```

```yaml
repo_url: https://github.com/feast-dev/feast.git
target_revision: v0.40.1
chart_path: infra/charts/feast-feature-server
feature_store_yaml_base64: cHJvamVjdDogbXVzaWMKcHJvdmlkZXI6IGxvY2FsCnJlZ2lzdHJ5OgogICAgcmVnaXN0cnlfdHlwZTogc3FsCiAgICBwYXRoOiBwb3N0Z3Jlc3FsOi8vZmVhc3Q6ZmVhc3RAZmVhc3Q6NTQzMi9mZWFzdAogICAgY2FjaGVfdHRsX3NlY29uZHM6IDYwCiAgICBzcWxhbGNoZW15X2NvbmZpZ19rd2FyZ3M6CiAgICAgICAgZWNobzogZmFsc2UKICAgICAgICBwb29sX3ByZV9waW5nOiB0cnVlCm9ubGluZV9zdG9yZToKICAgIHR5cGU6IHBvc3RncmVzCiAgICBob3N0OiBmZWFzdAogICAgcG9ydDogNTQzMgogICAgZGF0YWJhc2U6IGZlYXN0CiAgICBkYl9zY2hlbWE6IGZlYXN0CiAgICB1c2VyOiBmZWFzdAogICAgcGFzc3dvcmQ6IGZlYXN0Cm9mZmxpbmVfc3RvcmU6CiAgICB0eXBlOiBmaWxlCmVudGl0eV9rZXlfc2VyaWFsaXphdGlvbl92ZXJzaW9uOiAyCg==
```

```bash
mkdir /opt/app-root/src/mlops-gitops/toolings/feast-ui
touch /opt/app-root/src/mlops-gitops/toolings/feast-ui/config.yaml
```

```yaml
chart_path: charts/feast-ui
feast-feature-server:
  feature_store_yaml_base64: cHJvamVjdDogbXVzaWMKcHJvdmlkZXI6IGxvY2FsCnJlZ2lzdHJ5OgogICAgcmVnaXN0cnlfdHlwZTogc3FsCiAgICBwYXRoOiBwb3N0Z3Jlc3FsOi8vZmVhc3Q6ZmVhc3RAZmVhc3Q6NTQzMi9mZWFzdAogICAgY2FjaGVfdHRsX3NlY29uZHM6IDYwCiAgICBzcWxhbGNoZW15X2NvbmZpZ19rd2FyZ3M6CiAgICAgICAgZWNobzogZmFsc2UKICAgICAgICBwb29sX3ByZV9waW5nOiB0cnVlCm9ubGluZV9zdG9yZToKICAgIHR5cGU6IHBvc3RncmVzCiAgICBob3N0OiBmZWFzdAogICAgcG9ydDogNTQzMgogICAgZGF0YWJhc2U6IGZlYXN0CiAgICBkYl9zY2hlbWE6IGZlYXN0CiAgICB1c2VyOiBmZWFzdAogICAgcGFzc3dvcmQ6IGZlYXN0Cm9mZmxpbmVfc3RvcmU6CiAgICB0eXBlOiBmaWxlCmVudGl0eV9rZXlfc2VyaWFsaXphdGlvbl92ZXJzaW9uOiAyCg==
  feast_mode: ui
```

```bash
cd /opt/app-root/src/mlops-gitops
git add .
git commit -m  "🎁 ADD - Feast Server and UI 🎁"
git push
```

# New model runtime

Now that we train with a feature store, we also want to serve with a feature store.
We can use KServe transformers before to get features from feast at inference time.

## Go to your notebook and send a request?

# Deploy and try new app
