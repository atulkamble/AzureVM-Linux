# Azure VM Linux Cheatsheet

This comprehensive cheatsheet provides essential Azure CLI commands for managing Linux Virtual Machines on Microsoft Azure.

## Prerequisites
- Azure CLI installed (`az --version` to check)
- Logged in to Azure (`az login`)
- Appropriate subscription selected (`az account set --subscription "subscription-id"`)

---

## 1. VM Creation & Basic Operations

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az vm create` | Creates a new virtual machine | `az vm create --resource-group myRG --name myVM --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys` |
| `az vm list` | Lists all VMs in subscription/resource group | `az vm list --resource-group myRG --output table` |
| `az vm show` | Shows detailed information about a VM | `az vm show --resource-group myRG --name myVM` |
| `az vm delete` | Deletes a virtual machine | `az vm delete --resource-group myRG --name myVM --yes` |
| `az vm deallocate` | Deallocates VM (stops billing for compute) | `az vm deallocate --resource-group myRG --name myVM` |
| `az vm start` | Starts a deallocated/stopped VM | `az vm start --resource-group myRG --name myVM` |
| `az vm stop` | Stops a running VM | `az vm stop --resource-group myRG --name myVM` |
| `az vm restart` | Restarts a running VM | `az vm restart --resource-group myRG --name myVM` |

---

## 2. VM Sizes & Images

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az vm list-sizes` | Lists available VM sizes for a location | `az vm list-sizes --location eastus --output table` |
| `az vm image list` | Lists popular VM images | `az vm image list --output table` |
| `az vm image list --all` | Lists all available VM images | `az vm image list --all --publisher Canonical --offer 0001-com-ubuntu-server-focal` |
| `az vm list-usage` | Shows VM quota usage in a region | `az vm list-usage --location eastus --output table` |
| `az vm resize` | Changes VM size | `az vm resize --resource-group myRG --name myVM --size Standard_D4s_v3` |

---

## 3. VM Status & Monitoring

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az vm list --show-details` | Shows VMs with power state and IPs | `az vm list --show-details --output table` |
| `az vm get-instance-view` | Gets detailed runtime information | `az vm get-instance-view --resource-group myRG --name myVM` |
| `az vm run-command invoke` | Executes commands on VM remotely | `az vm run-command invoke --resource-group myRG --name myVM --command-id RunShellScript --scripts 'sudo apt update'` |
| `az vm boot-diagnostics get-boot-log` | Retrieves boot diagnostics | `az vm boot-diagnostics get-boot-log --resource-group myRG --name myVM` |
| `az vm boot-diagnostics enable` | Enables boot diagnostics | `az vm boot-diagnostics enable --resource-group myRG --name myVM` |

---

## 4. Networking & Security

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az network nsg create` | Creates a network security group | `az network nsg create --resource-group myRG --name myNSG` |
| `az network nsg rule create` | Creates NSG rule for firewall | `az network nsg rule create --resource-group myRG --nsg-name myNSG --name SSH --protocol tcp --priority 1000 --destination-port-range 22` |
| `az network public-ip create` | Creates a public IP address | `az network public-ip create --resource-group myRG --name myPublicIP --allocation-method Static` |
| `az vm open-port` | Opens a network port on VM | `az vm open-port --resource-group myRG --name myVM --port 80` |
| `az network nic list` | Lists network interfaces | `az network nic list --resource-group myRG --output table` |
| `az network nic show` | Shows NIC details including private IP | `az network nic show --resource-group myRG --name myVMVMNic` |

---

## 5. Storage & Disks

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az disk create` | Creates a managed disk | `az disk create --resource-group myRG --name myDisk --size-gb 128 --sku Premium_LRS` |
| `az vm disk attach` | Attaches disk to VM | `az vm disk attach --resource-group myRG --vm-name myVM --name myDisk` |
| `az vm disk detach` | Detaches disk from VM | `az vm disk detach --resource-group myRG --vm-name myVM --name myDisk` |
| `az disk list` | Lists all disks | `az disk list --resource-group myRG --output table` |
| `az vm update` | Updates VM configuration (e.g., disk caching) | `az vm update --resource-group myRG --name myVM --set storageProfile.osDisk.caching=ReadWrite` |

---

## 6. VM Extensions & Configuration

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az vm extension set` | Installs VM extension | `az vm extension set --resource-group myRG --vm-name myVM --name CustomScript --publisher Microsoft.Azure.Extensions` |
| `az vm extension list` | Lists installed extensions | `az vm extension list --resource-group myRG --vm-name myVM --output table` |
| `az vm user update` | Updates VM user credentials | `az vm user update --resource-group myRG --name myVM --username azureuser --ssh-key-value ~/.ssh/id_rsa.pub` |
| `az vm user reset-ssh` | Resets SSH configuration | `az vm user reset-ssh --resource-group myRG --name myVM` |

---

## 7. Backup & Snapshots

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az snapshot create` | Creates disk snapshot | `az snapshot create --resource-group myRG --name mySnapshot --source myDisk` |
| `az backup vault create` | Creates backup vault | `az backup vault create --resource-group myRG --name myVault --location eastus` |
| `az backup protection enable-for-vm` | Enables backup for VM | `az backup protection enable-for-vm --resource-group myRG --vault-name myVault --vm myVM --policy-name DefaultPolicy` |
| `az backup job list` | Lists backup jobs | `az backup job list --resource-group myRG --vault-name myVault` |

---

## 8. Scaling & Availability

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az vmss create` | Creates VM Scale Set | `az vmss create --resource-group myRG --name myVMSS --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys` |
| `az vmss scale` | Scales VM Scale Set | `az vmss scale --resource-group myRG --name myVMSS --new-capacity 5` |
| `az vm availability-set create` | Creates availability set | `az vm availability-set create --resource-group myRG --name myAvailSet` |
| `az vmss list-instances` | Lists VMSS instances | `az vmss list-instances --resource-group myRG --name myVMSS --output table` |

---

## 9. Troubleshooting & Diagnostics

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az vm repair create` | Creates repair VM for troubleshooting | `az vm repair create --resource-group myRG --name myVM --repair-username repairadmin --repair-password 'ComplexP@ssw0rd!'` |
| `az vm repair run` | Runs repair scripts | `az vm repair run --resource-group myRG --name myVM --run-id win-hello-world` |
| `az vm repair restore` | Restores repaired VM | `az vm repair restore --resource-group myRG --name myVM` |
| `az network watcher test-connectivity` | Tests network connectivity | `az network watcher test-connectivity --source-resource myVM --dest-resource targetVM --resource-group myRG` |

---

## 10. Cost Management & Tags

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `az tag create` | Creates a tag | `az tag create --name Environment` |
| `az resource tag` | Tags a resource | `az resource tag --tags Environment=Production --resource-group myRG --name myVM --resource-type Microsoft.Compute/virtualMachines` |
| `az consumption usage list` | Shows usage and costs | `az consumption usage list --start-date 2023-01-01 --end-date 2023-01-31` |
| `az advisor recommendation list` | Lists cost optimization recommendations | `az advisor recommendation list --category Cost` |

---

## Common VM Creation Templates

### Basic Ubuntu VM
```bash
az vm create \
  --resource-group myRG \
  --name myUbuntuVM \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys \
  --size Standard_B2s
```

### VM with Custom Storage
```bash
az vm create \
  --resource-group myRG \
  --name myVM \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys \
  --size Standard_D2s_v3 \
  --storage-sku Premium_LRS \
  --os-disk-size 128
```

### VM with Public IP and NSG
```bash
az vm create \
  --resource-group myRG \
  --name myVM \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys \
  --public-ip-address myPublicIP \
  --nsg myNSG \
  --nsg-rule SSH
```

---

## 11. Post-SSH Linux Commands for Azure VM

After SSH-ing into your Azure Linux VM (`ssh azureuser@<public-ip>`), here are essential commands to try:

### System Information & Status

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `uname -a` | Shows kernel and system information | `uname -a` |
| `hostnamectl` | Displays system hostname and OS info | `hostnamectl` |
| `lsb_release -a` | Shows Linux distribution details | `lsb_release -a` |
| `uptime` | Shows system uptime and load average | `uptime` |
| `whoami` | Shows current logged-in user | `whoami` |
| `id` | Shows user ID and group memberships | `id` |
| `sudo -l` | Lists sudo privileges for current user | `sudo -l` |

### System Resource Monitoring

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `htop` / `top` | Real-time process and resource monitoring | `htop` (install: `sudo apt install htop`) |
| `free -h` | Shows memory usage in human-readable format | `free -h` |
| `df -h` | Shows disk space usage | `df -h` |
| `du -sh /*` | Shows directory sizes in root | `du -sh /var /home /tmp` |
| `lscpu` | Shows CPU architecture information | `lscpu` |
| `lsmem` | Shows memory ranges and their online status | `lsmem` |
| `iostat` | Shows CPU and I/O statistics | `iostat -x 1` (install: `sudo apt install sysstat`) |
| `iotop` | Shows real-time disk I/O usage by process | `sudo iotop` (install: `sudo apt install iotop`) |

### Process Management

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `ps aux` | Shows all running processes | `ps aux \| grep apache` |
| `pstree` | Shows process tree hierarchy | `pstree` |
| `jobs` | Lists active jobs in current session | `jobs` |
| `nohup command &` | Runs command in background, survives logout | `nohup python3 app.py &` |
| `screen` / `tmux` | Terminal multiplexer for persistent sessions | `screen -S mysession` |
| `kill -9 <PID>` | Forcefully terminates a process | `kill -9 1234` |
| `pkill <process>` | Kills processes by name | `pkill firefox` |

### Network Diagnostics

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `ip addr show` | Shows network interfaces and IP addresses | `ip addr show` |
| `ip route show` | Shows routing table | `ip route show` |
| `netstat -tuln` | Shows listening ports and connections | `netstat -tuln` |
| `ss -tuln` | Modern replacement for netstat | `ss -tuln` |
| `ping <host>` | Tests connectivity to remote host | `ping google.com` |
| `traceroute <host>` | Shows network path to destination | `traceroute google.com` |
| `curl -I <url>` | Tests HTTP connectivity | `curl -I http://example.com` |
| `wget <url>` | Downloads files from web | `wget http://example.com/file.zip` |
| `nslookup <domain>` | DNS lookup utility | `nslookup google.com` |

### File System Operations

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `ls -la` | Lists files with detailed permissions | `ls -la /var/log` |
| `find / -name "*.log"` | Finds files by name pattern | `find /var -name "*.log" 2>/dev/null` |
| `locate <filename>` | Quickly finds files (requires updatedb) | `locate nginx.conf` |
| `which <command>` | Shows path of executable | `which python3` |
| `file <filename>` | Determines file type | `file /etc/passwd` |
| `stat <file>` | Shows detailed file information | `stat /etc/hosts` |
| `ln -s <target> <link>` | Creates symbolic link | `ln -s /var/log/nginx /home/user/logs` |

### Log Analysis

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `journalctl -f` | Follow systemd journal logs in real-time | `journalctl -f` |
| `journalctl -u <service>` | Shows logs for specific service | `journalctl -u ssh.service` |
| `tail -f /var/log/syslog` | Follow system log in real-time | `tail -f /var/log/syslog` |
| `grep -i error /var/log/*` | Search for errors in log files | `grep -i error /var/log/syslog` |
| `dmesg \| tail` | Shows recent kernel messages | `dmesg \| tail -20` |
| `last` | Shows login history | `last -10` |
| `lastlog` | Shows last login for all users | `lastlog` |

### Service Management (systemd)

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `systemctl status <service>` | Shows service status | `systemctl status nginx` |
| `systemctl start <service>` | Starts a service | `sudo systemctl start apache2` |
| `systemctl stop <service>` | Stops a service | `sudo systemctl stop apache2` |
| `systemctl restart <service>` | Restarts a service | `sudo systemctl restart ssh` |
| `systemctl enable <service>` | Enables service at boot | `sudo systemctl enable nginx` |
| `systemctl disable <service>` | Disables service at boot | `sudo systemctl disable apache2` |
| `systemctl list-units --type=service` | Lists all services | `systemctl list-units --type=service --state=running` |

### Package Management

#### Ubuntu/Debian (apt)
| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `sudo apt update` | Updates package repository cache | `sudo apt update` |
| `sudo apt upgrade` | Upgrades installed packages | `sudo apt upgrade` |
| `sudo apt install <package>` | Installs a package | `sudo apt install nginx` |
| `sudo apt remove <package>` | Removes a package | `sudo apt remove apache2` |
| `apt list --installed` | Lists installed packages | `apt list --installed \| grep nginx` |
| `apt search <keyword>` | Searches for packages | `apt search web server` |

#### RHEL/CentOS (yum/dnf)
| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `sudo yum update` | Updates all packages | `sudo yum update` |
| `sudo yum install <package>` | Installs a package | `sudo yum install nginx` |
| `sudo yum remove <package>` | Removes a package | `sudo yum remove httpd` |
| `yum list installed` | Lists installed packages | `yum list installed \| grep kernel` |
| `yum search <keyword>` | Searches for packages | `yum search "web server"` |

### Security & Permissions

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `sudo su -` | Switch to root user | `sudo su -` |
| `chmod 755 <file>` | Changes file permissions | `chmod 755 /home/user/script.sh` |
| `chown user:group <file>` | Changes file ownership | `sudo chown www-data:www-data /var/www/html` |
| `passwd` | Changes user password | `passwd` |
| `sudo passwd <user>` | Changes another user's password | `sudo passwd azureuser` |
| `sudo visudo` | Edits sudoers file safely | `sudo visudo` |
| `umask` | Shows/sets default file permissions | `umask 022` |

### Disk & Storage Management

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `lsblk` | Lists block devices in tree format | `lsblk` |
| `fdisk -l` | Shows disk partitions | `sudo fdisk -l` |
| `mount` | Shows mounted filesystems | `mount \| grep ^/dev` |
| `sudo mount <device> <mountpoint>` | Mounts a filesystem | `sudo mount /dev/sdb1 /mnt/data` |
| `sudo umount <mountpoint>` | Unmounts a filesystem | `sudo umount /mnt/data` |
| `sudo fsck <device>` | Checks filesystem for errors | `sudo fsck /dev/sdb1` |
| `sudo mkfs.ext4 <device>` | Creates ext4 filesystem | `sudo mkfs.ext4 /dev/sdb1` |

### Azure-Specific Commands

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `sudo waagent -version` | Shows Azure Linux Agent version | `sudo waagent -version` |
| `curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2021-02-01"` | Gets Azure VM metadata | `curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2021-02-01" \| jq` |
| `ls /var/lib/waagent/` | Shows Azure agent files | `ls -la /var/lib/waagent/` |
| `sudo systemctl status walinuxagent` | Checks Azure Linux Agent status | `sudo systemctl status walinuxagent` |
| `dmesg \| grep -i azure` | Shows Azure-related kernel messages | `dmesg \| grep -i azure` |

### Performance Troubleshooting

| Command | Significance | Usage Example |
|---------|-------------|---------------|
| `vmstat 1` | Shows system statistics every second | `vmstat 1 5` |
| `sar -u 1 5` | Shows CPU utilization | `sar -u 1 5` |
| `sar -r 1 5` | Shows memory utilization | `sar -r 1 5` |
| `sar -d 1 5` | Shows disk I/O statistics | `sar -d 1 5` |
| `netstat -i` | Shows network interface statistics | `netstat -i` |
| `lsof -i` | Shows open network connections | `lsof -i :80` |

---

## Important Notes

1. **Resource Groups**: Always specify the correct resource group for your resources
2. **Regions**: Ensure all resources are in the same region for best performance
3. **SSH Keys**: Use `--generate-ssh-keys` for automatic key generation or specify your own with `--ssh-key-values`
4. **Pricing**: Use `az vm list-sizes` to check available sizes and their costs
5. **Security**: Always configure NSG rules appropriately for your security requirements
6. **Backup**: Enable backup for production VMs using Azure Backup
7. **Monitoring**: Use Azure Monitor and Log Analytics for comprehensive monitoring

---

## Quick Reference Commands

| Task | Command |
|------|---------|
| Login to Azure | `az login` |
| Set subscription | `az account set --subscription "subscription-name"` |
| List locations | `az account list-locations --output table` |
| Create resource group | `az group create --name myRG --location eastus` |
| SSH into VM | `ssh azureuser@<public-ip>` |
| Get VM IP | `az vm show --resource-group myRG --name myVM --show-details --query publicIps --output tsv` |

This cheatsheet covers the most commonly used Azure CLI commands for managing Linux VMs in Azure. Keep it handy for quick reference during your Azure VM management tasks!