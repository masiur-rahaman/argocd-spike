#### Steps
1. kubectl apply -f k8s/namespace.yaml
2. kubectl create namespace argocd
3. kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
4. kubectl port-forward --address 0.0.0.0 svc/argocd-server -n argocd 8080:443
5. open http://localhost:8080
6. kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode
7. argocd admin initial-password -n argocd (brew install argocd)
8. kubectl apply -f argocd/dev-app.yaml
9. kubectl apply -f argocd/staging-app.yaml



#### Additional commands
1. kubectl delete all --all --all-namespaces
2. kubectl delete namespace --all