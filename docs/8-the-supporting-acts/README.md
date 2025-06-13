# Exercise 8 - The Supporting Acts
>  Continuous Delivery needs rapid and reliable feedback. Investing in continuous testing is a worthwhile activity.


## 👨‍🍳 Exercise Intro
In this exercise, we’ll enhance the reliability and security of our continuous training pipeline by incorporating essential quality assurance practices. You’ll add unit tests to validate code functionality, introduce linting and static code analysis to maintain code quality, and scan both the trained model and its container image for known vulnerabilities.


## 🖼️ Big Picture

![big-picture-quality-gate.jpg](./images/big-picture-quality-gate.jpg)

## 🔮 Learning Outcomes
- [ ] Add security gates to pipeline
- [ ] Add testing gates to pipeline
- [ ] Add static code analysis gates to pipeline
- [ ] Store secrets in Git securely
- [ ] Scan the modelcar images
- [ ] Add image signing to the pipeline
- [ ] Generate and store SBOMs

## 🔨 Tools used in this exercise
 * <span style="color:blue;">[Sonarqube](https://www.sonarqube.org/)</span> - Add static code analysis to the pipelines.
* Code Linting - <span style="color:blue;">[black](https://github.com/psf/black)</span> , <span style="color:blue;">[flake8](https://flake8.pycqa.org/en/latest/)</span> , <span style="color:blue;">[pylint](https://pypi.org/project/pylint/)</span>  - Static code linter.
* Kube Linting - <span style="color:blue;">[kube-linter](https://docs.kubelinter.io/#/)</span> , <span style="color:blue;">[helm lint](https://helm.sh/docs/helm/helm_lint/)</span>  Validate K8s YAMLs against best practices.
* Image Security - <span style="color:blue;">[Stackrox](https://www.redhat.com/en/technologies/cloud-computing/openshift/advanced-cluster-security-kubernetes)</span> - Finding vulnerabilities inside the images and hosts with StackRox
* ModelScan - <span style="color:blue;">[modelscan](https://github.com/protectai/modelscan)</span> - scans models to determine if they contain unsafe code.
* SealedSecrets - <span style="color:blue;">[sealed-secrets](https://github.com/bitnami-labs/sealed-secrets)</span> - encrypt your Secret into a SealedSecret, which is safe to store.
* Image Signing - <span style="color:blue;">[sigstore](https://www.sigstore.dev/)</span> - Sign your images with cosign.
* SBOMs - <span style="color:blue;">[Syft](https://github.com/anchore/syft)</span> - Generate a Software Bill of Materials (SBOM) from container images.
