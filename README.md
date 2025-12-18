<<<<<<< HEAD
Preparación del cluster Minikube y ArgoCD
1) Crear namespaces de ambientes

kubectl create namespace dev
kubectl create namespace test
kubectl create namespace argocd

2) Instalar ArgoCD

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl rollout status deploy/argocd-server -n argocd      #se utiliza para monitorear el progreso de un despliegue (deployment) específico en Kubernetes. 

3) Exponer ArgoCD en Minikube

kubectl -n argocd patch svc argocd-server -p '{"spec": {"type": "NodePort"}}'
kubectl -n argocd get svc argocd-server
minikube service argocd-server -n argocd --url

4) Obtener contraseña inicial

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

Estructura de Helm y manifiestos GitOps
1) Árbol de infra-gitops (ejemplo)

infra-gitops/
├─ charts/
│  ├─ service-a/
│  │  ├─ Chart.yaml
│  │  ├─ templates/deployment.yaml
│  │  ├─ templates/service.yaml
│  │  └─ values.yaml
│  └─ service-b/
│     ├─ Chart.yaml
│     ├─ templates/deployment.yaml
│     ├─ templates/service.yaml
│     └─ values.yaml
├─ environments/
│  ├─ dev/
│  │  ├─ values-service-a.yaml
│  │  ├─ values-service-b.yaml
│  │  └─ apps/
│  │     ├─ app-service-a.yaml
│  │     └─ app-service-b.yaml
│  └─ test/
│     ├─ values-service-a.yaml
│     ├─ values-service-b.yaml
│     └─ apps/
│        ├─ app-service-a.yaml
│        └─ app-service-b.yaml
└─ README.md










=======
#infra-k8s
#Kubernetes
>>>>>>> 6566602dcbc40948766ff3d45e64c0aba3b1f4a5
