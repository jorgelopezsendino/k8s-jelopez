
# Add initContainer to deploy, volume and volumemounts

# Apply yaml
mk apply -f cm-hotels-config.yaml
mk apply -f deploy-hotels-frontbackend-6.yaml
