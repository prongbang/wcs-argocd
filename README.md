# wcs-argocd

https://argo-cd.readthedocs.io/en/stable/getting_started/

### Install Argo CD

```shell
kubectl create namespace wcs-argocd
kubectl apply -n wcs-argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Download Argo CD CLI

```shell
brew install argocd
```

### Access The Argo CD API Server

```shell
kubectl patch svc argocd-server -n wcs-argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

### Get EXTERNAL-IP from service

```shell
kubectl get service -n wcs-argocd
```

### Login Using The CLI

```shell
kubectl -n wcs-argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

### Update password

```shell
brew install argocd
```

- Generating a bcrypt hash

```shell
argocd account bcrypt --password <YOUR-PASSWORD-HERE>
```

- Apply the new password hash

```shell
# bcrypt(password)=$2a$10$rRyBsGSHK6.uc8fntPwVIuLVHgsAhAX7TcdrqW/RADU0uh7CaChLa
kubectl -n argocd patch secret argocd-secret \
  -p '{"stringData": {
    "admin.password": "$2a$10$rRyBsGSHK6.uc8fntPwVIuLVHgsAhAX7TcdrqW/RADU0uh7CaChLa",
    "admin.passwordMtime": "'$(date +%FT%T%Z)'"
  }}'
```

### Login

user: admin
pass: *****

https://IP/login

### Creating Apps Via UI

https://argo-cd.readthedocs.io/en/stable/getting_started/#creating-apps-via-ui

