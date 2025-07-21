# k8s-hello-world

This is a simple "Hello World" application to be deployed on Kubernetes.

## Deployment with Argo CD

To deploy this application using Argo CD, you can use the following `deployment.yaml` file:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: gcr.io/google-samples/hello-app:1.0
        ports:
        - containerPort: 8080
```

### Create the Argo CD Application

1.  Open the ArgoCD UI.
2.  Click on "+ NEW APP".
3.  Fill in the following details:
    *   **Application Name**: `hello-world`
    *   **Project**: `default`
    *   **Sync Policy**: `Automatic`
    *   **Repository URL**: `<your-git-repo-url>`
    *   **Path**: `.`
    *   **Cluster URL**: `https://kubernetes.default.svc`
    *   **Namespace**: `default`
4.  Click on "CREATE".
