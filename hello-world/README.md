# k8s-hello-world

This is a simple "Hello World" application to be deployed on Kubernetes.

## Deployment with Argo CD

The Deployment consist of all necessary resources to deploy a nginx pod that returns 'Hello World', if set up correctly.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  namespace: hello-world
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:stable-alpine
          ports:
            - containerPort: 80
          volumeMounts:
            - name: html
              mountPath: /usr/share/nginx/html
      volumes:
        - name: html
          configMap:
            name: nginx-html
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
