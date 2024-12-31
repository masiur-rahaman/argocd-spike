#### Steps
1. kubectl apply -f k8s/namespace.yaml
2. kubectl create namespace argocd
3. kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
4. argocd login localhost:8080
5. argocd repo add git@github.com:masiur-rahaman/argocd-spike.git --ssh-private-key-path ~/.ssh/id_rsa_github_personal
6. argocd repo list
7. kubectl port-forward --address 0.0.0.0 svc/argocd-server -n argocd 8080:443
8. open http://localhost:8080
9. kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode
10. argocd admin initial-password -n argocd (brew install argocd)
11. kubectl apply -f argocd/dev-app.yaml
12. kubectl apply -f argocd/staging-app.yaml
13. kubectl get pods -n argocd



#### Additional commands
1. kubectl delete all --all --all-namespaces
2. kubectl delete namespace --all
3. kubectl get namespaces
4. kubectl get po -n kube-system