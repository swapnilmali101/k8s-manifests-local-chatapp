
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
 2 cd .\k8s-manifests\
   3 clear
   4 kubectl get pods
   5 kubectl get ns
   6 kubectl create -f .\namespace.yaml
   7 kubectl get ns
   8 kubectl apply -f .\mongodb-pv.yaml
   9 kubectk apply -f .\mongodb-pvc.yaml
  10 kubectl apply -f .\mongodb-pvc.yaml
  11 kubectl pvc -n k8s-chatapp
  12 kubectl get pvc -n k8s-chatapp
  13 kubectl get pvc,pv -n k8s-chatapp
  14 clear
  15 kubectl apply -f .\mongodb-deployment.yaml
  16 kubectl apply -f .\mongodb-service.yaml
  17 kubectl apply -f .\backend-deployment.yaml
  18 kubectl get pods
  19 kubectl get pods -n k8s-chatapp
  20 kubectl apply -f .\secrets.yaml
  21 kubectl apply -f .\backend-deployment.yaml
  22 kubectl get pods -n k8s-chatapp
  23 kubectl get pods -n k8s-chatapp
  24 kubectl apply -f .\backend-service.yaml
  25 kubectl apply -f .\frontend-deployment.yaml
  26 kubectl apply -f .\frontend-service.yaml
  27 kubectl get pods -n k8s-chatapp
  28 kubectl get svc -n k8s-chatapp
  29 kubectl apply -f .\ingress.yaml
  30 kubectl get svc -n ingress-nginx
  31 kubectl get validatingwebhookconfigurations
  32 kubectl delete validatingwebhookconfiguration ingress-nginx-admission
  33 kubectl apply -f .\ingress.yaml
  34 kubectl get pods -n k8s-chatapp
  35 kubectl get svc -n k8s-chatapp
  36 kubectl get ingress -n k8s-chatapp
  37 kubectl get pods -n ingress-nginx
  38 kubectl port-forward service/backend k8s-chatapp 5001:5001
  39 kubectl port-forward service/backend k8s-chatapp 5001:5001
  40 kubectl get svc -n k8s-chatapp
  41 ipconfig /flushdns
  42 ping k8s-chatapp.com
  43 kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/st... 
  44 kubectl get pods -n ingress-nginx --watch
  45 kubectl get ingress
  46 kubectl get ingress -n k8s-chatapp
  47 kubectl get ns
  48 kubectl delete namespace k8s-chatapp
  49 kubectl get ns
  50 kubectl create -f .\namespace.yaml
  51 kubectl apply -f .\mongodb-pv.yaml
  52 kubectl apply -f .\mongodb-pvc.yaml
  53 kubectl apply -f .\mongodb-deployment.yaml
  54 kubectl apply -f .\mongodb-service.yaml
  55 kubectl apply -f .\secrets.yaml
  56 kubectl apply -f .\backend-deployment.yaml
  57 kubectl apply -f .\backend-service.yaml
  58 kubectl apply -f .\frontend-deployment.yaml
  59 kubectl apply -f .\frontend-service.yaml
  60 kubectl apply -f .\ingress.yaml
  61 kubectl get pods -n k8s-chatapp
  62 kubectl get svc -n k8s-chatapp
  63 kubectl get ingress -n k8s-chatapp
  64 kubectl get pods -n ingress-nginx
  65 kubectl get svc -n ingress-nginx
  66 kubectl get svc -n ingress-nginx
  67 ping k8s-chatapp.com
  68 kubectl get svc -n ingress-nginx
  69 kubectl delete -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/s... 
  70 kubectl get svc -n ingress-nginx
  71 kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/st... 
  72 kubectl get svc -n ingress-nginx
  73 kubectl get svc -n ingress-nginx
  74 kubectl get svc -n ingress-nginx
  75 kubectl port-forward gsvc/ingress-nginx-controller -n ingress-nginx 80:80
  76 kubectl port-forward svc/ingress-nginx-controller -n ingress-nginx 80:80
  77 kubectl delete namespace k8s-chatapp
  78 kubectl get ns
```