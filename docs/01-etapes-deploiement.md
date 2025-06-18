# Étapes de déploiement

1. **Installer et démarrer Minikube**  
   ```bash
   minikube start --driver=docker
   ```

2. **Builder et push des images Docker**  
   ```bash
   docker build -t frontend:latest frontend/
   docker build -t backend:latest backend/
   ```

3. **Appliquer les manifests Kubernetes**  
   ```bash
   kubectl apply -f k8s/namespace.yaml
   kubectl apply -f k8s/
   ```

4. **Vérifier le statut**  
   ```bash
   kubectl get pods,svc,hpa -n scalable-app
   ```

5. **Test de montée en charge**  
   ```bash
   kubectl run load-test --image=busybox --rm -i -- /bin/sh
   # dans le shell busybox :
   while true; do wget -q -O- http://<minikube-ip>/api; done
   ```
