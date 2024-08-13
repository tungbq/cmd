# CLI Command Reference

This repository is a collection of the most commonly used command-line commands for daily tasks.

## Table of Contents

- [Linux Commands](#linux-commands)
- [Git Commands](#git-commands)
- [Docker Commands](#docker-commands)
- [Kubernetes Commands](#kubernetes-commands)

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
