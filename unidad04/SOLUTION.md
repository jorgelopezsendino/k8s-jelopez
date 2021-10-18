# Apply labels
microk8s kubectl label deployment hotels app=hotels tier=monolith release=v1 --overwrite -n hotels
microk8s kubectl label pod $podName app=hotels tier=monolith release=v1 --overwrite -n hotels

# Rollback strategy and add rollout paramenters
mk rollout history deploy hotels -n hotels
mk rollout undo deploy hotels --to-revision 1 -n hotels

# Add liveness and readiness probes

# Create report cronJob
microk8s kubectl create cronjob hotels-report --image "ghcr.io/go-elevate/k8s4arch-hotels-backend:slim" -n hotels --schedule="0 2 * * *"  --dry-run=client --output=yaml -- "python report.py" > cronjob-hotels-report.yaml

# Apply cronjob
microk8s kubectl apply -f cronjob-hotels-report.yaml
