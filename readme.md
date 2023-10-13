1. FluxCD git branch developer, for multi tenant purpose
```shell
git checkout --orphan dev-team
git rm -rf .
git commit --allow-empty -m "developer team repository"
git push origin dev-team
```
2. Create manifest that needed for application deployment in dev-team branch, for this final project, Helm Chart is used

4. Register domain A record (api.edwardsuwirya.com and www.edwardsuwirya.com) that direct to load balancer 
3. SOPS Age
```shell
age-keygen -o age.agekey

kubectl --kubeconfig=/Users/edwardsuwirya/Downloads/kubeconfig.yaml create secret generic sops-age --namespace=flux-system --from-file=age.agekey

cat age.agekey

sops --age={age.agekey} --encrypt --encrypted-regex '^(data|stringData)$' --in-place home-fluxcd/manifest/modules/registry-secret.yaml
```
5. Commit Push gitops main branch
6. Run this comman to copy secret to final-project namespace
```shell
kubectl get secret flux-system --namespace=flux-system -o yaml --kubeconfig=/Users/edwardsuwirya/Downloads/kubeconfig.yaml | sed 's/namespace: .*/namespace: final-project/' | kubectl apply -f - --kubeconfig=/Users/edwardsuwirya/Downloads/kubeconfig.yaml
```
