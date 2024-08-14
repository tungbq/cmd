# CLI Commands Reference

## Overview

This repository is a collection of the most commonly used command-line commands for daily work.
<br>
Source code: [tungbq/cmd](https://github.com/tungbq/cmd) ⭐ Contributing guideline: [here](https://github.com/tungbq/cmd/blob/main/CONTRIBUTING.md) 📖

## Table of Contents

- [Linux Commands](#linux-commands)
- [SSH Commands](#ssh-commands)
- [JQ Commands](#jq-commands)
- [Git Commands](#git-commands)
- [Docker Commands](#docker-commands)
- [Kubernetes Commands](#kubernetes-commands)
- [Helm Commands](#helm-commands)
- [Ansible Commands](#ansible-commands)
- [Terraform Commands](#terraform-commands)
- [PostgreSQL Commands](#postgresql-commands)

---

## Linux Commands

```bash
# Clear terminal output
clear

# List files in the current directory with details
ls -la

# Check system stats
df -h
cat /etc/os-release
cat /proc/meminfo
nproc

# Working with linux service
systemctl status target_service
systemctl start target_service
systemctl stop target_service
journalctl -u target_service

# Change file mode
chmod +x some_file.sh

# Change directory owner
chown 0600 /path/to/directory

# Create new directory
mkdir -p /path/to/directory

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

# Check system metric (CPU/RAM/...)
top
```

[Back to top 🔝](#cli-commands-reference)

## SSH Commands

```bash
# Generate SSH keys
ssh-keygen -t rsa

# SSH to a server using username/password
ssh user@1.2.3.4

# SSH to a server using key
ssh -i user_key.pem user@1.2.3.4

# Use locally available keys to authorise logins on a remote machine
ssh-copy-id user@1.2.3.4
```

[Back to top 🔝](#cli-commands-reference)

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

[Back to top 🔝](#cli-commands-reference)

## Git Commands

```bash
# Clone repo via HTTPS
git clone https://github.com/REPO_OWNER/repo.git

# Clone repo via SSH
git clone git@github.com:REPO_OWNER/repo.git

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

[Back to top 🔝](#cli-commands-reference)

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

## Docker Compose
# Start up containers as defined in the Docker Compose file
docker compose up

# Start up containers in detached mode
docker compose up -d

# Stop running containers
docker compose down
```

[Back to top 🔝](#cli-commands-reference)

## Kubernetes Commands

```bash
# Export KUBECONFIG to access the cluster
export KUBECONFIG=/path/to/kubeconfig.conf

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

[Back to top 🔝](#cli-commands-reference)

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

[Back to top 🔝](#cli-commands-reference)

## Ansible Commands

```bash
# Run an Ansible playbook
ansible-playbook playbook.yml -i inventory.ini

# Run a single Ansible ad-hoc command
ansible all -m ping

# List all available Ansible roles
ansible-galaxy list

# Install a role from Ansible Galaxy
ansible-galaxy install role-name

# Test an Ansible inventory file
ansible-inventory --list -i inventory.ini

# Run an Ansible playbook with increased verbosity
ansible-playbook playbook.yml -vvv
```

[Back to top 🔝](#cli-commands-reference)

## Terraform Commands

```bash
# Initialize a Terraform configuration directory
terraform init

# Plan the changes required by the Terraform configuration
terraform plan

# Apply the changes required by the Terraform configuration
terraform apply

# Create a Terraform execution plan and save it to a file (recommended)
terraform plan -out="tfplan.out"

# Apply the changes from saved plan
terraform apply "tfplan.out"

# Apply the changes automatically (use with your own risk, suitable for automation tasks)
terraform apply --auto-aprove

# Destroy all the resources managed by Terraform
terraform destroy

# Validate the Terraform configuration files
terraform validate

# Format Terraform configuration files
terraform fmt

# Show the current state of Terraform-managed infrastructure
terraform show

# Refresh the state file with the real infrastructure
terraform refresh

# List the available Terraform providers
terraform providers
```

[Back to top 🔝](#cli-commands-reference)

## PostgreSQL Commands

```bash
# Connect to a PostgreSQL database
psql -h hostname -U username -d database_name

# List all databases
psql -c "\l"

# List all tables in the current database
psql -c "\dt"

# Show the structure of a specific table
psql -c "\d table_name"

# Create a new database
createdb new_database_name

# Drop an existing database
dropdb database_name

# Create a new user
createuser new_user_name

# Drop an existing user
dropuser user_name

# Grant all privileges on a database to a user
psql -c "GRANT ALL PRIVILEGES ON DATABASE database_name TO user_name"

# Revoke all privileges on a database from a user
psql -c "REVOKE ALL PRIVILEGES ON DATABASE database_name FROM user_name"

# Backup a PostgreSQL database to a file
pg_dump database_name > backup_file.sql

# Restore a PostgreSQL database from a backup file
psql database_name < backup_file.sql
```

[Back to top 🔝](#cli-commands-reference)
