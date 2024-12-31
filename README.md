#### Prerequisite
1. Install ingress controller
2. ```
   minikube addons enable ingress
   kubectl get pods -n ingress-nginx
   ```
3. Install metallb(optional)
   ```
   kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/main/config/manifests/metallb-native.yaml
   kubectl get pods -n metallb-system
   ```
4. Install argocd
   ```
   brew install argocd
   ```
   
#### Steps
1. kubectl apply -f k8s/namespace.yaml
2. kubectl create namespace argocd
3. kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
4. kubectl get pods -n argocd
5. kubectl port-forward --address 0.0.0.0 svc/argocd-server -n argocd 8181:443
6. kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode
7. argocd admin initial-password -n argocd (brew install argocd)
8. argocd login localhost:8181
9. argocd repo add git@github.com:masiur-rahaman/argocd-spike.git --ssh-private-key-path ~/.ssh/id_rsa_github_personal
10. argocd repo list
11. open http://localhost:8181
12. kubectl apply -f argocd/dev-app.yaml
13. kubectl apply -f argocd/staging-app.yaml
14. access the application using the ingress controller
```bash
minikube tunnel
curl --resolve "my-app-dev.local:80:127.0.0.1" -i http://my-app-dev.local
```



#### Additional commands
1. kubectl delete all --all --all-namespaces
2. kubectl delete namespace --all
3. kubectl get namespaces
4. kubectl get po -n kube-system

#### configure metallb(optional)
1. minikube addons enable metallb
2. kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/namespace.yaml
3. kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/metallb.yaml
4. kubectl apply -f k8s/metallb_config_map.yaml