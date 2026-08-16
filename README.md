# CLI Commands Reference
A bookmark of essential command-line commands for a software engineer's daily tasks 📑
- Source code: [**tungbq/cmd**](https://github.com/tungbq/cmd) ⭐
- Website: [**https://tungbq.github.io/cmd**](https://tungbq.github.io/cmd)
- Contributing guideline: [**here**](https://github.com/tungbq/cmd/blob/main/CONTRIBUTING.md) 📖

## Table of Contents
- [Linux ](#linux)
- [Text Processing ](#text-processing)
- [Networking and Troubleshooting ](#networking-and-troubleshooting)
- [SSH ](#ssh)
- [Tmux ](#tmux)
- [JQ ](#jq)
- [Git ](#git)
- [GitHub CLI ](#github-cli)
- [Docker ](#docker)
- [Kubernetes ](#kubernetes)
- [Helm ](#helm)
- [Ansible ](#ansible)
- [Terraform ](#terraform)
- [PostgreSQL ](#postgresql)
- [MySQL ](#mysql)
- [Redis ](#redis)
- [Python ](#python)
- [Node.js and NPM ](#nodejs-and-npm)
- [Make ](#make)
- [AWS CLI ](#aws-cli)
- [Azure CLI ](#azure-cli)
- [OpenSSL and Certificate ](#openssl-and-certificate)
- [Powershell ](#powershell)
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

# Interactive process viewer (nicer than top, may need install)
htop

# Check memory and swap usage in human readable format
free -h

# Check how long the system has been running and the load average
uptime

# List processes and filter by name
ps aux | grep nginx

# Find the PID listening on a port
sudo lsof -i :8080
sudo ss -lptn 'sport = :8080'

# Kill a process (use -9 only when the normal kill does not work)
kill PID
kill -9 PID

# Kill all processes matching a name
pkill -f "python my_script.py"

# Run a command in the background and keep it alive after logout
nohup ./long_running.sh > out.log 2>&1 &

# Re-run a command every 2 seconds to watch its output change
watch -n 2 kubectl get pods

# Show which binary will be executed and where it lives
which python3
type -a python3

# Show and set environment variables for the current shell
printenv
export MY_VAR="value"

# Run a single command with an extra environment variable
MY_VAR=value ./script.sh

# Create a symbolic link
ln -s /path/to/original /path/to/link

# Sync directories locally or over SSH (resumable, only copies changes)
rsync -avz /local/dir/ user@1.2.3.4:/remote/dir/

# Check inode usage (disk can be "full" even when df -h looks fine)
df -i

# Find the biggest files/directories under the current path
du -ah . | sort -rh | head -n 20

# Compare two files
diff -u file1.txt file2.txt

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

## Text Processing Commands

```bash
# Search recursively, show line numbers, ignore case
grep -rni "error" /var/log/

# Show 3 lines of context around each match
grep -C 3 "timeout" app.log

# Count matches instead of printing them
grep -c "500" access.log

# Exclude matches (useful to filter noise out of logs)
grep -v "healthcheck" access.log

# Find files by name, then by extension
find . -name "config.yaml"
find . -type f -name "*.log"

# Find files modified in the last 24 hours
find . -type f -mtime -1

# Find and delete files older than 7 days (dry run first without -delete)
find /tmp -type f -mtime +7
find /tmp -type f -mtime +7 -delete

# Run a command on every file found (safe with spaces in names)
find . -name "*.tmp" -print0 | xargs -0 rm -f

# Replace text in a file (in place, keep a .bak backup)
sed -i.bak 's/old-value/new-value/g' config.yaml

# Print a specific line or range of lines
sed -n '10p' file.txt
sed -n '10,20p' file.txt

# Print selected columns from whitespace separated output
awk '{print $1, $4}' access.log

# Sum a column
awk '{sum += $2} END {print sum}' data.txt

# Cut fields from a delimited file
cut -d',' -f1,3 data.csv

# Sort, deduplicate and count occurrences (top talkers in a log)
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head

# Count lines, words and characters
wc -l file.txt

# Show output on screen and write it to a file at the same time
./deploy.sh | tee deploy.log

# Join long output with a pager
kubectl get pods -A | less
```

[Back to top 🔝](#cli-commands-reference)

## Networking and Troubleshooting Commands

```bash
# Show listening ports with the owning process (modern replacement for netstat)
sudo ss -lptn

# Show all TCP connections
ss -at

# Check whether a remote port is reachable
nc -zv example.com 443

# Show response headers only
curl -I https://example.com

# Verbose request, useful to debug TLS and redirects
curl -v https://example.com

# Follow redirects and save the response to a file
curl -L -o output.html https://example.com

# POST JSON with a bearer token
curl -X POST https://api.example.com/items \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"name":"demo"}'

# Print only the HTTP status code (handy in scripts and healthchecks)
curl -s -o /dev/null -w "%{http_code}\n" https://example.com

# Show timing breakdown (DNS, connect, TTFB, total)
curl -s -o /dev/null -w "dns=%{time_namelookup} connect=%{time_connect} ttfb=%{time_starttransfer} total=%{time_total}\n" https://example.com

# Retry a flaky endpoint
curl --retry 3 --retry-delay 2 https://example.com

# Call through a specific IP without changing DNS (test before cutover)
curl --resolve example.com:443:1.2.3.4 https://example.com

# DNS lookups
dig +short example.com
dig example.com MX
dig @8.8.8.8 example.com

# Reverse DNS lookup
dig -x 1.2.3.4

# Trace the network path to a host
traceroute example.com
mtr example.com

# Capture traffic on a port (Ctrl+C to stop)
sudo tcpdump -i any port 443 -nn

# Show local IP addresses and routes
ip a
ip route

# Show the public IP of the current machine
curl -s https://ifconfig.me
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

# Generate a modern ed25519 key with a comment
ssh-keygen -t ed25519 -C "your.email@example.com"

# Show the public key fingerprint
ssh-keygen -lf ~/.ssh/id_ed25519.pub

# Add a key to the running ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# List keys loaded in the agent
ssh-add -l

# Run a single remote command without opening a session
ssh user@1.2.3.4 "df -h"

# Connect through a bastion/jump host
ssh -J user@bastion-ip user@private-ip

# Local port forward: reach a remote service on localhost:5432
ssh -L 5432:db-host:5432 user@1.2.3.4

# Remote port forward: expose your local port 3000 on the remote host
ssh -R 3000:localhost:3000 user@1.2.3.4

# SOCKS proxy for browsing through the remote host
ssh -D 1080 user@1.2.3.4

# Debug a failing connection
ssh -vvv user@1.2.3.4

# Remove a stale host key after a server rebuild
ssh-keygen -R 1.2.3.4

# Reusable host config: ~/.ssh/config
## Host myserver
##   HostName 1.2.3.4
##   User ubuntu
##   IdentityFile ~/.ssh/mykey.pem
##   ServerAliveInterval 60
## Then simply: ssh myserver
```

[Back to top 🔝](#cli-commands-reference)

## Tmux Commands

```bash
# TIPS: the default prefix key is `Ctrl + b`, press it before each shortcut below.

# Start a new named session (keeps running after you disconnect)
tmux new -s mysession

# List sessions
tmux ls

# Attach to an existing session
tmux attach -t mysession

# Detach from the current session
## Prefix, then: d

# Kill a session
tmux kill-session -t mysession

# Split panes
## Prefix, then: %   (vertical split)
## Prefix, then: "   (horizontal split)

# Move between panes
## Prefix, then: arrow key

# Create / switch / rename windows
## Prefix, then: c   (create)
## Prefix, then: n   (next window)
## Prefix, then: ,   (rename window)

# Scroll back through the output (q to quit scroll mode)
## Prefix, then: [
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

# Extract a raw string without the surrounding quotes (good for shell variables)
TOKEN=$(curl -s http://api.example.com/auth | jq -r '.token')

# Pick several fields into a new object
jq '{name: .name, version: .version}' package.json

# Map over an array and print one field per line
jq -r '.items[].name' file.json

# Filter an array by condition then count the result
jq '[.items[] | select(.status == "failed")] | length' file.json

# Sort an array by a field
jq '.items | sort_by(.created_at)' file.json

# Convert JSON to CSV/TSV
jq -r '.items[] | [.id, .name] | @csv' file.json

# Get the keys of an object
jq 'keys' file.json

# Merge two JSON files
jq -s '.[0] * .[1]' base.json override.json

# Pass a shell variable into a jq filter safely
jq --arg env "prod" '.configs[] | select(.env == $env)' file.json
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
git fetch
git checkout origin/<other-branch> -- <path_to_folder>/
git checkout origin/<other-branch> -- <path_to_file>

# Clone only the latest commit (much faster on big repos)
git clone --depth 1 https://github.com/REPO_OWNER/repo.git

# Switch branches (modern alternative to checkout)
git switch main
git switch -c new-branch

# See what changed, before and after staging
git diff
git diff --staged

# Compact history graph
git log --oneline --graph --decorate --all

# Show who changed each line of a file
git blame file_name

# Search the whole history for a string
git log -S "search_term" --oneline

# Amend the last commit (only if it has NOT been pushed/shared)
git commit --amend -m "New message"

# Put work aside temporarily, then bring it back
git stash push -m "wip: refactor"
git stash list
git stash pop

# Update the local branch on top of the latest main
git fetch origin
git rebase origin/main

# Take one commit from another branch
git cherry-pick <commit_hash>

# Undo a pushed commit safely (creates a new commit)
git revert <commit_hash>

# Discard local changes of a file (destructive)
git restore file_name

# Reset the branch to the remote state (destructive, drops local commits)
git reset --hard origin/main

# Remove untracked files/directories (add -n first to preview)
git clean -nfd
git clean -fd

# Work on two branches at once in separate folders
git worktree add ../repo-hotfix hotfix-branch
git worktree list

# Tags and releases
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0

# Manage remotes
git remote -v
git remote add upstream https://github.com/UPSTREAM_OWNER/repo.git

# Sync a fork with the upstream repository
git fetch upstream
git merge upstream/main

# Delete a branch locally and on the remote
git branch -d old-branch
git push origin --delete old-branch

# Find the commit that introduced a bug
git bisect start
git bisect bad
git bisect good <commit_hash>
git bisect reset
```

[Back to top 🔝](#cli-commands-reference)

## GitHub CLI Commands

```bash
# Login and check the current account
gh auth login
gh auth status

# Clone a repository
gh repo clone REPO_OWNER/repo

# Create a pull request from the current branch
gh pr create --base main --title "Your title" --body "Your description"

# Create a draft PR
gh pr create --draft

# List, view and check out pull requests
gh pr list
gh pr view 123
gh pr view 123 --web
gh pr checkout 123

# Show the CI status of the current PR
gh pr checks

# Review, approve and merge
gh pr review 123 --approve
gh pr merge 123 --squash --delete-branch

# Work with issues
gh issue list --label "good first issue"
gh issue create --title "Bug: ..." --body "Steps to reproduce ..."
gh issue view 10
gh issue close 10

# Watch and debug GitHub Actions runs
gh run list
gh run watch
gh run view <run_id> --log-failed
gh run rerun <run_id> --failed

# Trigger a workflow manually
gh workflow run deploy.yml --ref main

# Manage repository secrets and variables
gh secret set MY_SECRET
gh variable set MY_VAR --body "value"

# Call the GitHub API directly
gh api repos/REPO_OWNER/repo --jq '.stargazers_count'

# Create a release
gh release create v1.0.0 --generate-notes
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

# Run a container in the background with port and volume mapping
docker run -d --name web -p 8080:80 -v $(pwd):/app your-image-name

# Run a throwaway container and clean it up on exit
docker run --rm -it alpine sh

# Pass environment variables
docker run -e APP_ENV=prod --env-file .env your-image-name

# Follow container logs (last 100 lines, then live)
docker logs -f --tail 100 container-name

# Restart a container
docker restart container-name

# Show live resource usage of running containers
docker stats

# Inspect a container and query a specific field
docker inspect container-name
docker inspect container-name | jq -r '.[0].NetworkSettings.IPAddress'

# Copy files in and out of a container
docker cp container-name:/app/log.txt ./log.txt
docker cp ./config.yaml container-name:/app/config.yaml

# Build with a specific Dockerfile, target and build args
docker build -f Dockerfile.prod --target runtime --build-arg VERSION=1.0 -t your-image-name .

# Build without cache (when a layer is stale)
docker build --no-cache -t your-image-name .

# Tag and push to a registry
docker login registry.example.com
docker tag your-image-name registry.example.com/your-image-name:1.0.0
docker push registry.example.com/your-image-name:1.0.0

# Pull a specific image tag
docker pull nginx:1.27-alpine

# Show the layer history of an image (find what makes it big)
docker history your-image-name

# Networks and volumes
docker network ls
docker network create my-net
docker volume ls
docker volume inspect my-volume

# Targeted cleanup (safer than a full prune)
docker container prune
docker image prune -a
docker volume prune

# Remove all stopped containers at once
docker rm $(docker ps -aq)

## Docker Compose
# Start up containers as defined in the Docker Compose file
docker compose up

# Start up containers in detached mode
docker compose up -d

# Stop running containers
docker compose down

# Rebuild images before starting
docker compose up -d --build

# Show status of compose services
docker compose ps

# Follow logs of one service
docker compose logs -f service-name

# Run a command inside a running service
docker compose exec service-name /bin/bash

# Restart a single service
docker compose restart service-name

# Stop and also remove named volumes (destructive)
docker compose down -v
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

# Work with contexts (switching between clusters)
kubectl config get-contexts
kubectl config current-context
kubectl config use-context my-context

# Set the default namespace for the current context
kubectl config set-context --current --namespace=your_namespace

# Wide output shows node and pod IP
kubectl get pods -o wide

# Dump the full manifest of a resource
kubectl get deployment my-app -o yaml

# Watch resources as they change
kubectl get pods -w

# Filter by label
kubectl get pods -l app=my-app

# Sorted cluster events, the fastest way to see why something fails
kubectl get events --sort-by=.metadata.creationTimestamp

# Logs of a previous (crashed) container, and of a specific container in the pod
kubectl logs pod-name --previous
kubectl logs pod-name -c container-name
kubectl logs -f deployment/my-app

# Logs of all pods behind a label
kubectl logs -l app=my-app --tail=100

# Scale a deployment
kubectl scale deployment my-app --replicas=3

# Restart all pods of a deployment (rolling)
kubectl rollout restart deployment my-app

# Rollout status and rollback
kubectl rollout status deployment my-app
kubectl rollout history deployment my-app
kubectl rollout undo deployment my-app

# Update the image of a deployment
kubectl set image deployment/my-app container-name=your-image-name:1.0.1

# Resource usage (requires metrics-server)
kubectl top nodes
kubectl top pods -n your_namespace

# Create resources quickly from the CLI
kubectl create namespace your_namespace
kubectl create secret generic my-secret --from-literal=password=example
kubectl create configmap my-config --from-file=config.yaml

# Decode a secret value
kubectl get secret my-secret -o jsonpath='{.data.password}' | base64 -d

# Generate a manifest without applying it
kubectl create deployment my-app --image=nginx --dry-run=client -o yaml > deploy.yaml

# Apply a kustomize overlay
kubectl apply -k ./overlays/prod

# Edit a live resource
kubectl edit deployment my-app

# Copy files to/from a pod
kubectl cp pod-name:/app/log.txt ./log.txt

# Start a temporary debug pod with network tools
kubectl run tmp-shell --rm -it --image=nicolaka/netshoot -- /bin/bash

# Check what your user is allowed to do
kubectl auth can-i create deployments -n your_namespace

# Node maintenance
kubectl cordon node-name
kubectl drain node-name --ignore-daemonsets --delete-emptydir-data
kubectl uncordon node-name

# Force delete a stuck pod
kubectl delete pod pod-name --grace-period=0 --force

# Explain the fields of a resource (built-in API docs)
kubectl explain deployment.spec.template.spec
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

# Install or upgrade in one idempotent command (the usual CI/CD pattern)
helm upgrade --install release-name repo-name/chart-name -n your_namespace --create-namespace

# Install with custom values
helm install release-name repo-name/chart-name -f values.yaml --set image.tag=1.0.1

# Preview the rendered manifests without touching the cluster
helm template release-name repo-name/chart-name -f values.yaml

# Dry run against the cluster (validates against the API server)
helm upgrade --install release-name repo-name/chart-name --dry-run --debug

# Show the default values of a chart
helm show values repo-name/chart-name

# Show the values actually used by an installed release
helm get values release-name

# Show all manifests of an installed release
helm get manifest release-name

# Roll back to the previous revision
helm rollback release-name
helm rollback release-name 2

# Wait for resources to become ready and roll back automatically on failure
helm upgrade --install release-name repo-name/chart-name --atomic --timeout 5m

# Download a chart locally (to inspect or vendor it)
helm pull repo-name/chart-name --untar

# Lint a local chart
helm lint ./my-chart

# Manage chart dependencies
helm dependency update ./my-chart
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

# Dry run: show what would change without changing anything
ansible-playbook playbook.yml --check --diff

# Limit the run to one host or group
ansible-playbook playbook.yml --limit web-servers

# Run only tasks with a given tag (or skip them)
ansible-playbook playbook.yml --tags deploy
ansible-playbook playbook.yml --skip-tags slow

# Pass extra variables
ansible-playbook playbook.yml -e "app_version=1.0.1"
ansible-playbook playbook.yml -e @vars.yml

# Ask for the sudo (become) password
ansible-playbook playbook.yml --ask-become-pass

# Start the play from a specific task (useful after a mid-run failure)
ansible-playbook playbook.yml --start-at-task "Deploy application"

# Check syntax and list what would run
ansible-playbook playbook.yml --syntax-check
ansible-playbook playbook.yml --list-tasks
ansible-playbook playbook.yml --list-hosts

# Ad-hoc commands
ansible all -m shell -a "df -h"
ansible web-servers -m copy -a "src=./app.conf dest=/etc/app.conf" --become

# Show all facts gathered from a host
ansible target-host -m setup

# Ansible Vault: encrypt, edit and use secret files
ansible-vault create secrets.yml
ansible-vault edit secrets.yml
ansible-vault view secrets.yml
ansible-playbook playbook.yml --ask-vault-pass

# Install roles/collections from a requirements file
ansible-galaxy install -r requirements.yml
ansible-galaxy collection install community.general

# Lint a playbook
ansible-lint playbook.yml
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
terraform apply -auto-approve

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

# Reinstall providers/modules after changing versions
terraform init -upgrade

# Format all files recursively and check formatting in CI
terraform fmt -recursive
terraform fmt -check -recursive

# Plan/apply only one resource (escape hatch, avoid in normal workflow)
terraform plan -target=module.network.aws_vpc.main

# Plan the destroy without running it
terraform plan -destroy

# Destroy without the confirmation prompt (use with care)
terraform destroy -auto-approve

# Show outputs
terraform output
terraform output -raw instance_ip
terraform output -json

# Inspect the state
terraform state list
terraform state show aws_instance.web

# Move or remove a resource in the state (refactoring)
terraform state mv aws_instance.web module.compute.aws_instance.web
terraform state rm aws_instance.web

# Import an existing resource into the state
terraform import aws_instance.web i-1234567890abcdef0

# Replace (recreate) a single resource
terraform apply -replace="aws_instance.web"

# Workspaces (separate state per environment)
terraform workspace list
terraform workspace new staging
terraform workspace select staging

# Evaluate expressions interactively against the current state
terraform console

# Visualize the dependency graph
terraform graph | dot -Tsvg > graph.svg

# Update the provider lock file for multiple platforms (fixes CI checksum errors)
terraform providers lock -platform=linux_amd64 -platform=darwin_arm64
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

# Connect using a connection URL
psql "postgresql://username:password@hostname:5432/database_name"

# Avoid typing the password interactively (scripts/CI)
export PGPASSWORD="your_password"

# Run a single query and exit
psql -h hostname -U username -d database_name -c "SELECT count(*) FROM users;"

# Run a SQL file
psql -h hostname -U username -d database_name -f script.sql

# Output query results as CSV
psql -d database_name -c "SELECT * FROM users" --csv > users.csv

# Compressed dump and restore (recommended for big databases)
pg_dump -h hostname -U username -Fc database_name > backup.dump
pg_restore -h hostname -U username -d database_name backup.dump

# Dump only the schema, or only the data
pg_dump -s database_name > schema.sql
pg_dump -a database_name > data.sql

# Useful meta commands inside psql
## \l          list databases
## \c dbname   connect to another database
## \dt         list tables
## \d table    describe a table
## \du         list users and roles
## \dn         list schemas
## \x          toggle expanded output (readable wide rows)
## \timing     show query execution time
## \q          quit

# See current connections and running queries
psql -c "SELECT pid, usename, state, query FROM pg_stat_activity WHERE state <> 'idle';"

# Cancel or kill a query by pid
psql -c "SELECT pg_cancel_backend(PID);"
psql -c "SELECT pg_terminate_backend(PID);"

# Database and table sizes
psql -c "SELECT pg_size_pretty(pg_database_size('database_name'));"
psql -c "SELECT relname, pg_size_pretty(pg_total_relation_size(relid)) FROM pg_catalog.pg_statio_user_tables ORDER BY pg_total_relation_size(relid) DESC LIMIT 10;"

# Check the query plan before optimizing
psql -c "EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'a@b.com';"
```

[Back to top 🔝](#cli-commands-reference)

## MySQL Commands

```bash
# Connect to a MySQL server (prompts for the password)
mysql -h hostname -u username -p database_name

# Run a single query and exit
mysql -u username -p -e "SHOW DATABASES;"

# Run a SQL file
mysql -u username -p database_name < script.sql

# Backup a database / all databases
mysqldump -u username -p database_name > backup.sql
mysqldump -u username -p --all-databases > all_backup.sql

# Backup only the schema
mysqldump -u username -p --no-data database_name > schema.sql

# Restore from a backup file
mysql -u username -p database_name < backup.sql

# Useful statements inside the mysql shell
## SHOW DATABASES;
## USE database_name;
## SHOW TABLES;
## DESCRIBE table_name;
## SHOW CREATE TABLE table_name;
## SHOW PROCESSLIST;              -- current connections and queries
## KILL <id>;                     -- stop a stuck query
## EXPLAIN SELECT * FROM users;   -- inspect the query plan
## SHOW INDEX FROM table_name;

# Create a user and grant privileges
mysql -u root -p -e "CREATE USER 'new_user'@'%' IDENTIFIED BY 'password';"
mysql -u root -p -e "GRANT ALL PRIVILEGES ON database_name.* TO 'new_user'@'%'; FLUSH PRIVILEGES;"

# Check the server status and version
mysqladmin -u root -p status
mysql -u root -p -e "SELECT VERSION();"
```

[Back to top 🔝](#cli-commands-reference)

## Redis Commands

```bash
# Connect to a Redis server
redis-cli -h hostname -p 6379
redis-cli -h hostname -p 6379 -a your_password

# Check that the server answers
redis-cli ping

# Run a single command and exit
redis-cli GET my_key

# Basic key operations
## SET my_key "value"
## GET my_key
## DEL my_key
## EXISTS my_key
## EXPIRE my_key 60      -- expire in 60 seconds
## TTL my_key            -- remaining lifetime

# Scan keys by pattern (SCAN is safe on production, KEYS is not)
redis-cli --scan --pattern "session:*"

# Server information and memory usage
redis-cli INFO
redis-cli INFO memory
redis-cli DBSIZE

# Find the biggest keys
redis-cli --bigkeys

# Watch commands as they run (debugging, do not leave running)
redis-cli MONITOR

# Show slow queries
redis-cli SLOWLOG GET 10

# Flush the current database (destructive)
redis-cli FLUSHDB
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

# Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate       # Linux/macOS
.venv\Scripts\activate          # Windows

# Leave the virtual environment
deactivate

# Check the interpreter and version actually in use
which python3
python3 --version

# Run a module as a script
python3 -m pip install --upgrade pip
python3 -m pytest

# Serve the current directory over HTTP (quick file sharing / static preview)
python3 -m http.server 8000

# Pretty print JSON from a file or a pipe
python3 -m json.tool file.json
curl -s http://api.example.com/data | python3 -m json.tool

# Show details of an installed package
pip show package-name

# List outdated packages
pip list --outdated

# Testing, formatting and linting
pytest -v
pytest tests/test_api.py::test_login
pytest --cov=my_package
black .
ruff check .

# Start the interactive debugger at a failure point
python3 -m pdb my_script.py

# Run an isolated CLI tool without polluting the environment
pipx install black
uvx ruff check .
```

[Back to top 🔝](#cli-commands-reference)

## Node.js and NPM Commands

```bash
# Check versions
node --version
npm --version

# Start a new project
npm init -y

# Install all dependencies from package.json
npm install

# Clean, reproducible install for CI (uses package-lock.json)
npm ci

# Add a dependency / dev dependency / exact version
npm install express
npm install --save-dev jest
npm install express@4.18.2

# Remove a package
npm uninstall express

# Install a CLI tool globally
npm install -g typescript

# Run scripts defined in package.json
npm run build
npm test
npm start

# List the scripts available in the project
npm run

# Run a package binary without installing it globally
npx create-react-app my-app

# List installed packages (top level only)
npm list --depth=0

# Check for outdated packages and update them
npm outdated
npm update

# Audit and fix known vulnerabilities
npm audit
npm audit fix

# Clear the npm cache (fixes weird install errors)
npm cache clean --force

# Yarn equivalents
yarn install
yarn add express
yarn remove express
yarn run build

# Pnpm equivalents
pnpm install
pnpm add express
pnpm run build

# Manage Node versions with nvm
nvm install 20
nvm use 20
nvm ls
```

[Back to top 🔝](#cli-commands-reference)

## Make Commands

```bash
# Run the default target (the first one in the Makefile)
make

# Run a specific target
make build
make test

# List the targets defined in the Makefile
grep -E '^[a-zA-Z_-]+:' Makefile

# Pass variables to a target
make deploy ENV=prod

# Show what would run without executing it (dry run)
make --dry-run deploy

# Use a Makefile from another location
make -f build/Makefile build

# Run targets in parallel
make -j4

# Force a rebuild even if targets look up to date
make -B build
```

[Back to top 🔝](#cli-commands-reference)

## AWS CLI Commands

```bash
# Configure credentials and check the identity currently in use
aws configure
aws sts get-caller-identity

# Use a named profile and a region
aws configure --profile my-profile
aws s3 ls --profile my-profile --region ap-southeast-1

# S3: list, copy, sync, remove
aws s3 ls s3://my-bucket
aws s3 cp file.txt s3://my-bucket/file.txt
aws s3 cp s3://my-bucket/file.txt ./file.txt
aws s3 sync ./local-dir s3://my-bucket/prefix/
aws s3 rm s3://my-bucket/file.txt

# Generate a temporary download link
aws s3 presign s3://my-bucket/file.txt --expires-in 3600

# EC2: list instances in a readable table
aws ec2 describe-instances \
  --query "Reservations[].Instances[].{ID:InstanceId,Name:Tags[?Key=='Name']|[0].Value,State:State.Name,IP:PrivateIpAddress}" \
  --output table

# EC2: start and stop instances
aws ec2 start-instances --instance-ids i-1234567890abcdef0
aws ec2 stop-instances --instance-ids i-1234567890abcdef0

# Connect to an instance without SSH keys or a public IP
aws ssm start-session --target i-1234567890abcdef0

# EKS: update kubeconfig to access a cluster
aws eks update-kubeconfig --name my-cluster --region ap-southeast-1

# ECR: login to the registry
aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin <account_id>.dkr.ecr.ap-southeast-1.amazonaws.com

# Secrets Manager / SSM Parameter Store
aws secretsmanager get-secret-value --secret-id my-secret --query SecretString --output text
aws ssm get-parameter --name /app/db/password --with-decryption --query Parameter.Value --output text

# CloudWatch: tail logs live
aws logs tail /aws/lambda/my-function --follow

# Lambda: invoke a function
aws lambda invoke --function-name my-function --payload '{"key":"value"}' response.json

# IAM: list roles / users
aws iam list-roles --output table
aws iam list-users --output table
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

# Create and delete a resource group
az group create --name my-rg --location southeastasia
az group delete --name my-rg --yes --no-wait

# List resources inside a resource group
az resource list --resource-group my-rg --output table

# AKS: get credentials to access a cluster with kubectl
az aks get-credentials --resource-group my-rg --name my-aks-cluster

# AKS: list clusters and scale a node pool
az aks list --output table
az aks scale --resource-group my-rg --name my-aks-cluster --node-count 3

# ACR: login and list images
az acr login --name myregistry
az acr repository list --name myregistry --output table

# Virtual machines
az vm list --output table
az vm start --resource-group my-rg --name my-vm
az vm stop --resource-group my-rg --name my-vm
az vm list-ip-addresses --resource-group my-rg --output table

# Storage: list containers and upload a blob
az storage container list --account-name mystorage --output table
az storage blob upload --account-name mystorage --container-name my-container --name file.txt --file ./file.txt

# Key Vault secrets
az keyvault secret list --vault-name my-vault --output table
az keyvault secret show --vault-name my-vault --name my-secret --query value --output tsv

# App Service: tail application logs
az webapp log tail --resource-group my-rg --name my-webapp

# Service principals and role assignments
az ad sp create-for-rbac --name my-sp --role Contributor --scopes /subscriptions/SUBSCRIPTION_ID
az role assignment list --assignee <object_id> --output table

# Show what a command supports (built-in help)
az vm create --help
```

[Back to top 🔝](#cli-commands-reference)

## OpenSSL and Certificate Commands

```bash
# Check the certificate served by a website (issuer, subject, chain)
openssl s_client -connect example.com:443 -servername example.com

# Show only the expiry dates of a live certificate
echo | openssl s_client -connect example.com:443 -servername example.com 2>/dev/null | openssl x509 -noout -dates

# Inspect a local certificate file
openssl x509 -in certificate.crt -text -noout

# Show the expiry date of a local certificate
openssl x509 -in certificate.crt -noout -enddate

# Generate a private key and a certificate signing request (CSR)
openssl req -new -newkey rsa:2048 -nodes -keyout private.key -out request.csr

# Generate a self-signed certificate for local development
openssl req -x509 -newkey rsa:2048 -nodes -keyout private.key -out certificate.crt -days 365

# Verify that a key and a certificate match (the two hashes must be equal)
openssl rsa -noout -modulus -in private.key | openssl md5
openssl x509 -noout -modulus -in certificate.crt | openssl md5

# Convert between formats
openssl pkcs12 -export -out bundle.pfx -inkey private.key -in certificate.crt
openssl pkcs12 -in bundle.pfx -out certificate.pem -nodes

# Verify a certificate against a CA chain
openssl verify -CAfile ca-chain.crt certificate.crt

# Base64 encode/decode
echo -n "text" | base64
echo "dGV4dA==" | base64 -d

# Generate a random password/secret
openssl rand -base64 32

# Hash a file and verify its checksum
sha256sum file.zip
sha256sum -c file.zip.sha256
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

# Safe script header: stop on error, on undefined variable, and on failed pipe
set -euo pipefail

# Shebang for a bash script
#!/usr/bin/env bash

# Default value when a variable is not set
NAME="${1:-world}"

# Fail fast when a required variable is missing
: "${API_TOKEN:?API_TOKEN is required}"

# Command substitution
CURRENT_BRANCH=$(git rev-parse --abbrev-ref HEAD)

# Check the exit code of the previous command
if ! ./deploy.sh; then
  echo "Deploy failed"
  exit 1
fi

# File and string tests
if [ -f "config.yaml" ]; then echo "file exists"; fi
if [ -d "/var/log" ]; then echo "directory exists"; fi
if [ -z "$VAR" ]; then echo "variable is empty"; fi
if [ -n "$VAR" ]; then echo "variable is set"; fi

# Numeric comparison
if [ "$COUNT" -gt 10 ]; then echo "more than ten"; fi

# Case statement
case "$1" in
  start) echo "starting" ;;
  stop)  echo "stopping" ;;
  *)     echo "usage: $0 {start|stop}"; exit 1 ;;
esac

# Loop over the lines of a file
while IFS= read -r line; do
  echo "$line"
done < input.txt

# Loop over files matching a pattern
for file in ./logs/*.log; do
  echo "Processing $file"
done

# Arrays
SERVICES=("api" "worker" "web")
for svc in "${SERVICES[@]}"; do
  echo "Restarting $svc"
done

# Number of arguments passed to the script
echo "Arg count: $#"
echo "All args: $@"

# Exit code of the last command
echo "Last exit code: $?"

# Cleanup on exit, even if the script fails
trap 'rm -f /tmp/lockfile' EXIT

# Retry a command up to 3 times
for i in {1..3}; do
  curl -sf https://example.com && break || sleep 5
done

# Write to stderr
echo "something went wrong" >&2

# Timestamp for log lines and file names
date +"%Y-%m-%d %H:%M:%S"
date +"%Y%m%d-%H%M%S"

# Check a script for common mistakes
shellcheck script.sh
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

# Delete all content of file
# (Not in insert mode) Press ggdG

# Copy (yank) line
yy

# Paste
p

# Undo
u

# Redo
Ctrl + r

# Go to the first / last line of the file
gg
G

# Go to a specific line number
:42

# Jump to the start / end of the current line
0
$

# Delete N lines starting from the cursor
5dd

# Copy N lines / paste above the cursor
5yy
P

# Search backwards, then jump between matches
?term
n
N

# Search and replace in the whole file (add 'c' to confirm each change)
:%s/old/new/g
:%s/old/new/gc

# Show line numbers
:set number

# Turn off search highlighting
:noh

# Indent / unindent the current line
>>
<<

# Select text (visual mode), then use d, y or > on the selection
v
## Select whole lines
V

# Open another file, and reload the current one from disk
:e path/to/file
:e!

# Save without exiting
:w

# Save a file that needs root permissions
:w !sudo tee %
```
[Back to top 🔝](#cli-commands-reference)
