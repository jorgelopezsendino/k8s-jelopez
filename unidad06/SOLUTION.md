# Create job
microk8s kubectl create job hotels-migrations -n hotels-migrations --image "ghcr.io/go-elevate/k8s4arch-hotels-backend:slim"  --dry-run=client --output=yaml > job-hotels-migrations.yaml

# Add command and change restartPolicy on job
# Create pv
# Create pvc
# Add volume and volumemount to job and deploy

# Apply yaml
mk apply -f cm-hotels-config.yaml
mk apply -f pv-hotels-db.yaml
mk apply -f pvc-hotels-db.yaml
mk apply -f job-hotels-migrations.yaml
mk apply -f deploy-hotels-frontbackend-6.yaml
