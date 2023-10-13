1. FluxCD git branch developer, for multi tenant purpose
```shell
git checkout --orphan dev-team
git rm -rf .
git commit --allow-empty -m "developer team repository"
git push origin dev-team
```
2. SOPS Age 
3. SOPS Age
```shell
age-keygen -o age.agekey

kubectl --kubeconfig=/Users/edwardsuwirya/Downloads/kubeconfig.yaml create secret generic sops-age --namespace=flux-system --from-file=age.agekey

cat age.agekey

sops --age={age.agekey} --encrypt --encrypted-regex '^(data|stringData)$' --in-place home-fluxcd/manifest/modules/registry-secret.yaml

kubectl get secret flux-system --namespace=flux-system -o yaml --kubeconfig=/Users/edwardsuwirya/Downloads/kubeconfig.yaml | sed 's/namespace: .*/namespace: final-project/' | kubectl apply -f - --kubeconfig=/Users/edwardsuwirya/Downloads/kubeconfig.yaml
```
