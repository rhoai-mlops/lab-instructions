## Object Storage

Object storage provides a flexible and scalable way to store large amounts of unstructured data efficiently, making it a popular choice for cloud storage, content distribution, and for our usecase as well! We will use object storage to store our datasets and model artifacts.

### Walk through the Object Storage

> MinIO is one of the most popular object storage out there. It is tailored for cloud-native setups so it is fairly quick to spin up an instance for experimentations. It is also compatible with Amazon S3 API, accessible via a RESTful HTTP API, making integration with cloud-native applications and automation pretty straightforward.

1. For simplicity, a MinIO instance is already installed in your dev environment for you. You can access MinIO via UI and check that there are already four buckets created for you. Below is the link to your MinIO instance. You can use the same credentials; `<USER_NAME>` as username, `<PASSWORD>` as password.


MinIO UI: [https://minio-ui-<USER_NAME>.<CLUSTER_DOMAIN>](https://minio-ui-<USER_NAME>.<CLUSTER_DOMAIN>)


![minio-ui.png](./images/minio-ui.png)

The `models` bucket is where we will store our models, and the `pipeline` bucket is to store Data Science pipeline artifacts. The other two (`data` and `data-cache` will be useful a bit later, be patient :))

## Data Connections

1. If you return to the OpenShift AI Dashboard, under `Data Science Projects` > `<USER_NAME>`, there is section called `Connections`. There you’ll notice four `Connections` have already been created for you. These connections are objects that store MinIO endpoint and bucket information. You can view their details by clicking the three dots on the right-hand side and selecting `Edit data connection`.

> Connections also help us to expose bucket information as environment variables to our workbenches, allowing us to use such information without hardcoding them into our code.

![data-connections.png](./images/data-connections.png)

You selected `models` connection while creating the workbench as we will interact with this bucket during our experimentation phase.


 🪄🪄🪄 Now that we have the essential tools to start our journey, let's dive into our dataset! 🪄🪄🪄