# CLI Commands Reference
A bookmark of essential command-line commands for a software engineer's daily tasks 📑
- Source code: [**tungbq/cmd**](https://github.com/tungbq/cmd) ⭐
- Website: [**https://tungbq.github.io/cmd**](https://tungbq.github.io/cmd)
- Contributing guideline: [**here**](https://github.com/tungbq/cmd/blob/main/CONTRIBUTING.md) 📖

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
- [Python Commands](#python-commands)
- [Azure CLI Commands](#azure-cli-commands)
- [Powershell Commands](#powershell-commands)
- [Bash Scripting](#bash-scripting)
- [Vim Shortcuts](#vim-shortcuts)

---

## Linux Commands

```bash
# TIPS: Press `Ctrl + R` to find your previous commands.

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

# Reload config without restarting the service
systemctl reload target_service

# Change file mode
chmod +x some_file.sh
chmod 0600 /path/to/directory

# Change directory owner
sudo chown -R user:user folder

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

# wget - Download a file from a URL
wget http://example.com/file.zip

# wget - Download a file and save it with a different name
wget -O newfile.zip http://example.com/file.zip

# Check network
netstat -anpt
ping google.com
nslookup google.com
tracepath google.com

# Check system metric (CPU/RAM/...)
top

# Tar
## Compress
tar -cvf sampleArchive.tar /home/sampleArchive

## Extract
tar -xvf sampleArchive.tar
tar -xvf sampleArchive.tar.gz -C /home/ExtractedFiles/

# Unzip
unzip your_file.zip
## Specify the output location
unzip your_file.zip -d target_location

# Control file content
echo "first line" > file.txt
echo "second line" >> file.txt

# SCP commands
## Download file from remote to local machine
scp -r username@IP:/path/on/remote /path/on/local
scp -r -i /path/to/key.pem username@IP:/path/on/remote /path/on/local
scp -r -P 12345 -i /path/to/key.pem username@IP:/path/on/remote /path/on/local

## Send file from local to remote machine
scp -r /path/on/local username@IP:/path/on/remote

# DNS check
dig domain.com

# Working with logs content
cat /var/log/syslog
## Show last 100 lines.
tail -n 100 /var/log/syslog
## Show first 100 lines.
head -n 100 /var/log/syslog
# Monitor logs live (Ctrl+C to exit).
tail -f /var/log/syslog
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
## Copy default key
ssh-copy-id user@1.2.3.4

## Copy specific key
ssh-copy-id -i ~/.ssh/mykey user@host
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
# Configure git info
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Remove '--global' flag if you want to config for project only
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Verify
git config -l

# Clone repo via HTTPS
git clone https://github.com/REPO_OWNER/repo.git

# Clone with username
git clone https://username@github.com/REPO_OWNER/repo.git

# Clone repo via SSH
git clone git@github.com:REPO_OWNER/repo.git

# Create a new branch
git checkout -b new-branch

# Pull the latest changes from the remote repository
git pull origin main

# Check the status of your working directory
git status

# Add changes to the staging area
git add .
git add file_name1 file_name2 folder_name1

# Commit changes with a message
git commit -m "Your commit message"

# View log
git log

# Push to remote feature branch
git push origin new-branch

# Reset staging area to match the lastest origin commit
git reset origin/main

# Checkout content of folder or file from other branch
git checkout your_branch
git checkout origin/<other-branch> -- <path_to_folder>/
git checkout origin/<other-branch> -- <path_to_file>
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
# Linux Export KUBECONFIG to access the cluster
export KUBECONFIG=/path/to/kubeconfig.conf

# Window Export KUBECONFIG to access the cluster
 $env:KUBECONFIG = "\path\to\kubeconfig.conf"

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

# Init and migrate TF state files to another location
terraform init -migrate-state

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

# Apply with secret var
terraform apply -var-file="secret.tfvars"

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

# Unlock Terraform
terraform force-unlock <LOCK_ID>
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

## Python Commands

```bash
# Run a python script
python python_script.py

# Install a package using pip
pip install package-name

# Install a specific version of a package
pip install package-name==1.2.3

# Uninstall a package
pip uninstall package-name

# List all installed packages
pip list

# Freeze installed packages into a requirements file
pip freeze > requirements.txt

# Install packages from a requirements file
pip install -r requirements.txt
```

[Back to top 🔝](#cli-commands-reference)

## Azure CLI Commands

```bash
# Login to Azure
az login

# Login with device code
az login --use-device-code

# Get the details of a subscription
az account show

# Get subscription ID
az account show --query id --output tsv

# List all subscriptions associated with your account
az account list --output table

# Set a specific subscription as default
az account set --subscription "SUBSCRIPTION_ID"

# List all resource groups
az group list --output table

# List location
az account list-locations
```

[Back to top 🔝](#cli-commands-reference)

## PowerShell Commands
```powershell
# Get the current directory
Get-Location

# List files in the current directory with details
Get-ChildItem -Force

# Create a new directory
New-Item -Path "C:\path\to\directory" -ItemType Directory

# Remove a file
Remove-Item -Path "C:\path\to\file.txt"

# Display a message in the console
Write-Host "This is a message displayed in the console."

# Copy a file
Copy-Item -Path "C:\source\file.txt" -Destination "C:\destination\file.txt"

# Move or rename a file
Move-Item -Path "C:\path\to\oldname.txt" -Destination "C:\path\to\newname.txt"

# Check the content of a file
Get-Content -Path "C:\path\to\file.txt"

# Write a line to a file (overwrites existing content)
Set-Content -Path "C:\path\to\file.txt" -Value "This is the first line."

# Append a line to a file
Add-Content -Path "C:\path\to\file.txt" -Value "This is an appended line."

# Search for a string in a file
Select-String -Path "C:\path\to\file.txt" -Pattern "search-string"

# Run a script with elevated privileges
Start-Process powershell -Verb runAs -ArgumentList "-File C:\path\to\script.ps1"

# Test network connection (ping)
Test-Connection google.com

# Download a file from a URL
Invoke-WebRequest -Uri "https://example.com/file.zip" -OutFile "C:\path\to\file.zip"

# Compress files into a ZIP archive
Compress-Archive -Path "C:\path\to\folder\*" -DestinationPath "C:\path\to\archive.zip"

# Extract files from a ZIP archive
Expand-Archive -Path "C:\path\to\archive.zip" -DestinationPath "C:\path\to\extract"

# Get system information
Get-ComputerInfo

# Check the status of a service
Get-Service -Name "ServiceName"

# Start a service
Start-Service -Name "ServiceName"

# Stop a service
Stop-Service -Name "ServiceName"

# Restart a service
Restart-Service -Name "ServiceName"

# List installed software
Get-WmiObject -Class Win32_Product | Select-Object -Property Name, Version
```
 
[Back to top 🔝](#cli-commands-reference)

## Bash Scripting
```bash
# Basic if statement
if [ "$VAR" = "value" ]; then
  echo "Match"
fi

# For loop
for i in {1..5}; do
  echo "Number $i"
done

# While loop
while true; do
  echo "Running..."
  sleep 1
done

# Script arguments
echo "Script name: $0"
echo "First argument: $1"

# Functions
my_func() {
  echo "Hello from function"
}

my_func

# Reading input
read -p "Enter your name: " name
echo "Hello, $name"

# Exit with code
exit 0
```
[Back to top 🔝](#cli-commands-reference)

## Vim Shortcuts
```
# Enter insert mode
i

# Save and exit
:wq
:x!

# Exit without saving
:q!

# Search in file
/term

# Delete line
dd

# Copy (yank) line
yy

# Paste
p

# Undo
u

# Redo
Ctrl + r
```
[Back to top 🔝](#cli-commands-reference)
