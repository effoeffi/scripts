1. Create k8s cluster, for example dev (so we'll connect an env to it)
```
gcloud beta container clusters create ${CLUSTER_NAME} \
  --cluster-version 1.15.11-gke.3 \
  --num-nodes=1 \
  --machine-type=n1-standard-4 \
  --addons ApplicationManager \
  --quiet \
  --preemptible
```
2. Init app and create 2 new repos: `seymour-config` and `seymour-env`
```
appctl init seymour-config \
    --app-config-repo github.com/effoeffi/seymour-config \
    --deployment-repo github.com/effoeffi/seymour-env \
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
10. Prepare env PR (response with created PR in seymour-env)
```
appctl prepare dev --from-tag 1
```
11. Run `apply` without merge the PR -> deny
```
appctl apply dev --from-tag 1
```
12. Merge PR in seymour-env and see created `dev` branch
13. Rerun apply (12)
14. Open GCP and see GKE/Applications

Refreances:
- https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/
- https://cloud.google.com//kubernetes-engine/docs/how-to/add-on/application-delivery
- https://github.com/kubernetes-sigs/kustomize/tree/master/docs
- Sync: https://cloud.google.com/kubernetes-engine/docs/add-on/config-sync/how-to
