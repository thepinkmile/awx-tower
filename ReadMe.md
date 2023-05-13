# Install MiniKube on Windows ( see: [Get Started](https://minikube.sigs.k8s.io/docs/start/) )

```
winget install minikube
```

# Run minikube

Using admin command prompt

```
minikube start
```

# deploy awx ( see: [awx-operator](https://github.com/ansible/awx-operator) )

```
minikube kubctl -- apply -k .
```

# check status

```
minikube kubectl -- get pods -n awx
minikube kubectl -- get pods -n awx -l "app.kubernetes.io/managed-by=awx-operator"
minikube kubectl -- get svc -n awx -l "app.kubernetes.io/managed-by=awx-operator"
```

# get default login credentials

The default login is `admin` and you can find the service url and password using the following commands:

```
minikube kubectl -- get secret -n awx awx-demo-admin-password -o jsonpath="{.data.password}" > data.b64
certutil -decode data.b64 pass.txt
minikube service -n awx awx-demo-service --url
```