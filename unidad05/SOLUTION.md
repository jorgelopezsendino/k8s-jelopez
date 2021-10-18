# Create deploy
microk8s kubectl create deploy hotels-backend --image "ghcr.io/go-elevate/k8s4arch-hotels-backend:slim" -n hotels --replicas=4 --port=5000 --dry-run=client --output=yaml > deploy-hotels-backend-5.1.yaml

# Create cm
microk8s kubectl create cm hotels -n hotels-config --from-literal=DB_PATH=/db/hotels.json --from-literal=DB_TABLE=hotels --dry-run=client --output=yaml > cm-hotels.yaml

# Modify with labels, probes and rollout

# Add requirements

