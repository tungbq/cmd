# CLI Command Reference

This repository is a collection of the most commonly used command-line commands for daily tasks.

## Table of Contents

- [Linux Commands](#linux-commands)
- [SSH Commands](#ssh-commands)
- [JQ Commands](#jq-commands)
- [Git Commands](#git-commands)
- [Docker Commands](#docker-commands)
- [Kubernetes Commands](#kubernetes-commands)
- [Helm Commands](#helm-commands)

---

## Linux Commands

```bash
# List files in the current directory with details
ls -la

df -h
cat /etc/os-release

systemctl status target_service
systemctl start target_service
systemctl stop target_service
journalctl -u target_service

# Change file mode
chmod +x some_file.sh

# Change directory owner
chown 0600 /path/to/directory

# Change directory
cd /path/to/directory

# Copy a file or directory
cp source destination

# Move or rename a file or directory
mv old-name new-name

# Remove a file
rm file-name

# Show disk usage of directories and files
du -h --max-depth=1

# Search for a pattern in files
grep -r "pattern" /path/to/search

# Display the current directory's path
pwd

# History
history

# CURL, add '-k' to ignore certificate verification
curl https://abc.example.com

# Check network
netstat -anpt
```

## SSH Commands

```bash
# Generate SSH keys
ssh-keygen -t rsa

# SSH to a server using username/password
ssh user@1.2.3.4

# SSH to a server using key
ssh -i user_key.pem user@1.2.3.4
```

## JQ Commands

```bash
# Pretty-print JSON data
jq '.'

# Extract a specific field from a JSON object
jq '.fieldName' file.json

# Filter JSON data by a specific condition
jq 'select(.fieldName == "value")' file.json

# Parse JSON from an API response
curl -s http://api.example.com/data | jq '.'

# Flatten a nested JSON structure
jq '.[].nestedField' file.json

# Format JSON output into a more readable structure
jq '.' file.json | less
```

## Git Commands

```bash
# Create a new branch
git checkout -b new-branch

# Pull the latest changes from the remote repository
git pull origin main

# Check the status of your working directory
git status

# Add all changes to the staging area
git add .

# Commit changes with a message
git commit -m "Your commit message"

# View log
git log

# Push to remote feature branch
git push origin new-branch

# Reset staging area to match the lastest origin commit
git reset origin/main
```

## Docker Commands

```bash
# List all running containers
docker ps

# List all containers (including stopped ones)
docker ps -a

# Build an image from a Dockerfile
docker build -t your-image-name .

# Run a container from an image
docker run --name container-name your-image-name

# Stop a running container
docker stop container-name

# Remove a stopped container
docker rm container-name

# Remove an image
docker rmi image-name

# Show container logs
docker logs container-name

# List all Docker images
docker images

# Enter a running container's shell
docker exec -it container-name /bin/bash

# Cleanup docker (add `-f` flag to force cleanup)
docker system prune
```

## Kubernetes Commands

```bash
# Check nodes
kubectl get nodes

# Get all pods in the target namespace
kubectl get pods -n your_namespace

# Get all services in the current namespace
kubectl get svc -n your_namespace

# Get all resources in all namespace
kubectl get all -A

# Describe a pod
kubectl describe pod pod-name

# Apply a configuration to a resource by filename or stdin
kubectl apply -f config-file.yaml

# Delete resources by filenames, stdin, resources, and names
kubectl delete -f config-file.yaml

# Get logs from a pod
kubectl logs pod-name

# Execute a command in a container
kubectl exec -it pod-name -- /bin/bash

# Forward a port from a pod to the local machine
kubectl port-forward pod-name 8080:80
```

## Helm Commands

```bash
# Add a Helm repository
helm repo add repo-name https://example.com/repo

# Update all Helm repositories
helm repo update

# Search for charts in a Helm repository
helm search repo repo-name

# Install a Helm chart
helm install release-name repo-name/chart-name

# List all Helm releases across all namespaces
helm list --all-namespaces

# Uninstall a Helm release
helm uninstall release-name

# Upgrade an existing Helm release
helm upgrade release-name repo-name/chart-name

# Get the status of a Helm release
helm status release-name

# Show the history of a Helm release
helm history release-name
```
