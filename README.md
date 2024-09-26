# gc-enforcement-chart-poc
The POC will demonstrate how the charts are  released  automatically when the chart code changes (by Dev) or when new image tags are published (DevOps).
## Goal
As a customer, I want the ability to install the HELM chart with one of the major versions: v49, v50, or v51. For example, the following command: ```helm install my-release my-org.github.io/my-chart --version ~v49.0.0```  will install the latest available version within the v49.0.0 series. If versions like v49.1.0, v49.2.0, and v49.3.0 exist, it will install v49.3.0.

## Requirements
1. The ```Chart.appVersion``` represents the image tag, which is tagged and aligned with the chart’s major version.  For example, image v51.28483.1234 corresponds to chart releases in the v51.0.0 series.  
Here are examples of v49 and v51 releases:  
```
apiVersion: v2
name: gc-kube
description: Guardicore visibility and enforcement
version: 49.0.1
appVersion: v49.4335.123.4

apiVersion: v2
name: gc-kube
description: Guardicore visibility and enforcement
version: 49.0.2
appVersion: v49.4847.123.4

apiVersion: v2
name: gc-kube
description: Guardicore visibility and enforcement
version: 51.0.1
appVersion: v51.1111.222.1

apiVersion: v2
name: gc-kube
description: Guardicore visibility and enforcement
version: 51.0.2
appVersion: v51.3653.123.1
```

3. The chart will be hosted in GitHub.io and will use GitHub Actions
4. A corresponding HELM chart will be released Each time a new image build is published. For example, if image v51.9837.333.0 is released, a new chart version 51.0.3 will be created with appVersion v51.9837.333.0.   *(Note: see the releases  above)*
```
apiVersion: v2
name: gc-kube
description: Guardicore visibility and enforcement
version: 51.0.3
appVersion: v51.9837.333.0
```
5. If the HELM chart code itself is updated, a new version will also be released with the same appVersion. For example, if a new label is added to the v51 major version, the chart version will bump to v51.1.3 (from v51.0.3).
```
apiVersion: v2
name: gc-kube
description: Guardicore visibility and enforcement
version: 51.1.3
appVersion: v51.9837.333.0
```
7. **In summary**, bumping the chart versioning (*X.Y.Z*):  
    *X*: Major version  
    *Y*: Bumped when the HELM chart code is changed  
    *Z*: Bumped when updating artifacts (image tags)  