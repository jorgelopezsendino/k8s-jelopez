# Create namespace and deployment yaml files
microk8s kubectl create ns hotels --dry-run=client --output=yaml > namespace-hotels.yaml
microk8s kubectl create deploy hotels --image "ghcr.io/go-elevate/k8s4arch-hotels:monolith" -n hotels --replicas=2 --port=80 --dry-run=client --output=yaml > deploy-hotels.yaml

# Apply yaml files
microk8s kubectl apply -f namespace-hotels.yaml
microk8s kubectl apply -f deploy-hotels.yaml

# Apply port-fordward
microk8s kubectl port-forward $podName 8081:80
