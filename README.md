
###### Project Structure
```bash
.
└── k8s-manifests-local-chatapp/
    ├── k8s-manifests/
    │   ├── backend-deployment.yaml
    │   ├── backend-service.yaml
    │   ├── frontend-deployment.yaml
    │   ├── frontend-service.yaml
    │   ├── ingress.yaml
    │   ├── mongodb-deployment.yaml
    │   ├── mongodb-pv.yaml
    │   ├── mongodb-pvc.yaml
    │   ├── mongodb-service.yaml
    │   ├── namespace.yaml
    │   └── secrets.yaml
    ├── .env
    ├── .gitignore
    ├── docker-compose.yaml
    ├── Jenkinsfile
    ├── LICENSE
    └── README.md
```

###### commands history

```
   $ cd .\k8s-manifests\
   $ kubectl get pods
   $ kubectl get ns
   $ kubectl create -f .\namespace.yaml
   $ kubectl get ns
   $ kubectl apply -f .\mongodb-pv.yaml
   $ kubectk apply -f .\mongodb-pvc.yaml
   $ kubectl get pvc,pv -n k8s-chatapp
   $ kubectl apply -f .\mongodb-deployment.yaml
   $ kubectl apply -f .\mongodb-service.yaml
   $ kubectl apply -f .\secrets.yaml
   $ kubectl apply -f .\backend-deployment.yaml
   $ kubectl get pods -n k8s-chatapp
   $ kubectl apply -f .\backend-service.yaml
   $ kubectl apply -f .\frontend-deployment.yaml
   $ kubectl apply -f .\frontend-service.yaml
   $ kubectl get pods -n k8s-chatapp
   $ kubectl get svc -n k8s-chatapp
   $ kubectl apply -f .\ingress.yaml
   $ kubectl get ingress -n k8s-chatapp
   $ kubectl get pods -n ingress-nginx
   $ kubectl get svc -n ingress-nginx
   $ kubectl port-forward service/backend k8s-chatapp 5001:5001
   $ kubectl port-forward svc/ingress-nginx-controller -n ingress-nginx 80:80
   $ kubectl delete namespace k8s-chatapp
   $ kubectl get ns
```
