<h2 align="center">
  <br>
  <p align="center"><img width=50% src="https://raw.githubusercontent.com/kha7iq/gitlab-k8s/master/.github/img/gitlab-k8s.png"></p>
</h2>

## About

These manifests can be used  run GitLab on Kubernetes when you have related resources `postgres`, `redis`, `minio`, `tls certificates` etc already available in your environment.

You can find complete details in this [article](https://lmno.pk/post/gitlab-installation-kubernets/)

* Render kubernetes manifest

```bash
GITLAB_URL=gitlab.example.com \
GITLAB_REGISTRY_URL=registry.example.com \
GITLAB_PAGES_URL=pages.example.com \
GITLAB_POSTGRES_HOST=192.168.1.90 \
GITLAB_POSTGRES_PORT=5432 \
GITLAB_POSTGRES_USER=gitlab \
GITLAB_POSTGRES_DB_NAME=gitlabhq_production \
GITLAB_REDIS_HOST=192.168.1.91:6379 \
GITLAB_GITALY_STORAGE_SIZE=15Gi \
GITLAB_STORAGE_CLASS=local-path \
subvars dir --input gitlab-k8s-1.0 --out dirName
```
Change into `dirName/gitlab-k8s-1.0` you can have a look to confirm if everything is in order before applying this in cluster.

* Create the namespace `gitlab` and build with kustomize or kubectl.

* Namespace
```bash
kubectl create namespace gitlab
```

* Apply the final manifest
```bash
kustomize build gitlab-k8s-1.0/ | kubectl apply -f -
```

* Note: 
   Default passwords
   > Gitlab 'root' user's password configured as secret
   ```bash
   LAwGTzCebner4Kvd23UMGEOFoGAgEHYDszrsSPfAp6lCW15S4fbvrVrubWsua9PI
   ```
   > Postgres password configured as secret
   ```bash
    ZDVhZDgxNWY2NmMzODAwMTliYjdkYjQxNWEwY2UwZGMK
   ```
