1. [optinal] Create k8s cluster, for example dev (so we'll connect an env to it)
```
~/view/projects/gitops/demo/script/create.sh effi-dev
```
2. Init app and create 2 new repos: `seymour-config` and `seymour-env`
```
appctl init seymour-config \
    --app-config-repo github.com/effoeffi/seymour-config /
    --deployment-repo github.com/effoeffi/seymour-env /
    --config-path kubernetes
```
3. add new env `dev` and connect to `dev` cluster
```
appctl env add dev --cluster effi-dev
```
4. [optional] see commit logs - `appctl env add` commited a new `dev` env
```
git log
```
5. [optional] see seymour-config tree
```
tree
```
6. Copy k8s yaml into `seymour-config/kubernetes/base`
7. Update `seymour-config/kubernetes/base/kustomization.yaml` with path to created file
8. Dry run config
```
kubectl apply -k kubernetes/base/ --dry-run -o yaml
```
9. tag changes
```
git tag 1
git push origin --tags
```
10. Prepare env PR
```
appctl prepare dev --from-tag 1
```
Message with created PR in seymour-env
12. Run `apply` without merge the PR -> deny
```
appctl apply dev --from-tag 1
```
13. Merge PR in seymour-env and see created `dev` branch
14. Rerun apply (12)
15. Open GCP and see GKE/Applications
