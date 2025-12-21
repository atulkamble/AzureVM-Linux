<div align="center">

**🚀 AzureVM-Linux** | Built with ❤️ by [Atul Kamble](https://github.com/atulkamble)

[![GitHub](https://img.shields.io/badge/GitHub-atulkamble-181717?logo=github)](https://github.com/atulkamble)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-atuljkamble-0A66C2?logo=linkedin)](https://www.linkedin.com/in/atuljkamble/)

**Version 1.0.0** | Last Updated: December 2025

</div>

---

# 🐧 Azure VM Linux Guide

A comprehensive guide for working with Linux on Azure Virtual Machines, including essential commands and best practices.

## 📋 Table of Contents
- [Prerequisites & Essential Linux Commands](#prerequisites--essential-linux-commands)
- [Azure VM Setup](#azure-vm-setup)
- [SSH Connection](#ssh-connection)
- [Basic Linux Commands Practice](#basic-linux-commands-practice)
- [Package Management](#package-management)
- [Development Environment Setup](#development-environment-setup)
- [Additional Resources](#additional-resources)

---

## 🔧 Prerequisites & Essential Linux Commands

Before working with Azure VMs, you should be familiar with these fundamental Linux commands:

### Navigation & File Operations
| Command | Description | Example |
|---------|-------------|---------|
| `pwd` | Print working directory | `pwd` |
| `ls` | List directory contents | `ls -la` |
| `cd` | Change directory | `cd /home/user` |
| `mkdir` | Create directory | `mkdir myproject` |
| `rmdir` | Remove empty directory | `rmdir oldproject` |
| `rm -rf` | Remove directory and contents | `rm -rf myproject` |
| `touch` | Create empty file | `touch newfile.txt` |
| `cp` | Copy files/directories | `cp file1.txt file2.txt` |
| `mv` | Move/rename files | `mv oldname.txt newname.txt` |
| `find` | Search for files | `find . -name "*.txt"` |

### File Content Operations
| Command | Description | Example |
|---------|-------------|---------|
| `cat` | Display file content | `cat file.txt` |
| `less` | View file page by page | `less longfile.txt` |
| `head` | Show first lines of file | `head -10 file.txt` |
| `tail` | Show last lines of file | `tail -20 file.txt` |
| `grep` | Search text in files | `grep "error" logfile.txt` |
| `nano` | Simple text editor | `nano config.txt` |
| `vim` | Advanced text editor | `vim script.py` |

### Permissions & Ownership
| Command | Description | Example |
|---------|-------------|---------|
| `chmod` | Change file permissions | `chmod 755 script.sh` |
| `chown` | Change file ownership | `sudo chown user:group file.txt` |
| `sudo` | Execute as superuser | `sudo apt update` |
| `su` | Switch user | `sudo su - otheruser` |

### System Information
| Command | Description | Example |
|---------|-------------|---------|
| `whoami` | Current username | `whoami` |
| `uname -a` | System information | `uname -a` |
| `df -h` | Disk space usage | `df -h` |
| `free -h` | Memory usage | `free -h` |
| `ps aux` | Running processes | `ps aux \| grep nginx` |
| `top` | Real-time process viewer | `top` |
| `history` | Command history | `history \| grep ssh` |

### Network & Connectivity
| Command | Description | Example |
|---------|-------------|---------|
| `ping` | Test connectivity | `ping google.com` |
| `wget` | Download files | `wget http://example.com/file.zip` |
| `curl` | Transfer data from servers | `curl -I http://example.com` |
| `ssh` | Secure shell connection | `ssh user@hostname` |

---

## ⚙️ Azure VM Setup

### VM Configuration
- **Operating System**: Ubuntu Server 24.04 LTS
- **Recommended Size**: Standard_B2s (2 vCPUs, 4 GB RAM) for testing
- **Authentication**: SSH public key (recommended) or password

### Network Security Group (NSG) Rules
Configure these essential ports:

| Port | Protocol | Service | Description |
|------|----------|---------|-------------|
| `22` | TCP | SSH | Secure Shell access |
| `80` | TCP | HTTP | Web traffic |
| `443` | TCP | HTTPS | Secure web traffic |
| `3389` | TCP | RDP | Remote Desktop (if needed) |

### Azure CLI Commands for VM Creation
```bash
# Create resource group
az group create --name myResourceGroup --location eastus

# Create VM
az vm create \
  --resource-group myResourceGroup \
  --name myUbuntuVM \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys \
  --size Standard_B2s

# Open HTTP port
az vm open-port --port 80 --resource-group myResourceGroup --name myUbuntuVM
```

---

## 🔐 SSH Connection

### 1. Set Key Permissions (Local Machine)
```bash
cd Downloads  # or wherever your key file is located
chmod 400 your-key.pem
```

### 2. Connect to Azure VM
```bash
# Basic connection
ssh -i "your-key.pem" username@<PUBLIC_IP>

# Example with specific key and user
ssh -i "azure-vm-key.pem" azureuser@20.42.123.456

# Connect with verbose output for troubleshooting
ssh -v -i "your-key.pem" username@<PUBLIC_IP>
```

### 3. SSH Configuration (Optional)
Create `~/.ssh/config` file for easier connections:
```bash
Host myazurevm
    HostName 20.42.123.456
    User azureuser
    IdentityFile ~/.ssh/azure-vm-key.pem
    Port 22
```

Then connect with: `ssh myazurevm`

---

## 🐧 Basic Linux Commands Practice

Once connected to your Azure VM, practice these essential commands:

```bash
# Clear screen and get oriented
clear
whoami
pwd
hostname

# Basic file operations
ls -la                    # list all files with details
mkdir myproject           # create directory
touch README.md          # create empty file
ls

# File manipulation
echo "Hello Azure!" > hello.txt    # create file with content
cat hello.txt                      # display content
cp hello.txt backup.txt           # copy file
mv hello.txt myproject/           # move file
ls myproject/

# Navigate directories
cd myproject/
pwd
ls -la
cd ..                    # go back one directory
ls

# File editing
nano hello.txt          # edit with nano (beginner-friendly)
# OR
vim hello.txt           # edit with vim (advanced)

# View file content
cat hello.txt           # display entire file
head -5 hello.txt       # first 5 lines
tail -5 hello.txt       # last 5 lines
less hello.txt          # page through content (press 'q' to quit)

# Search within files
grep "Azure" hello.txt   # find lines containing "Azure"

# File permissions
chmod +x script.sh       # make file executable
chmod 644 hello.txt      # set read/write for owner, read for others

# Cleanup
rm backup.txt           # remove file
rm -rf myproject/       # remove directory and contents
history                 # show command history
```

---

## 📦 Package Management

### Update System
```bash
# Update package list
sudo apt update

# Upgrade installed packages
sudo apt upgrade -y

# Update and upgrade in one command
sudo apt update && sudo apt upgrade -y
```

### Essential Package Installations
```bash
# Development tools
sudo apt install -y git curl wget vim nano htop tree

# Python development
sudo apt install -y python3 python3-pip python3-venv

# Node.js development
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs

# Docker
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER  # Add user to docker group

# Nginx web server
sudo apt install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
```

### Snap Packages (Alternative Package Manager)
```bash
# Install snap if not present
sudo apt install snapd -y

# Install packages via snap
sudo snap install code --classic        # VS Code
sudo snap install docker               # Docker
sudo snap install tree                 # Tree view utility
```

---

## 🛠️ Development Environment Setup

### Git Configuration
```bash
# Configure Git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Verify configuration
git config --list

# Initialize repository
git init
touch README.md
echo "# My Azure Project" > README.md
git add README.md
git commit -m "Initial commit"

# Connect to remote repository
git remote add origin https://github.com/username/repository.git
git branch -M main
git push -u origin main
```

### Python Virtual Environment
```bash
# Create virtual environment
python3 -m venv myproject-env

# Activate environment
source myproject-env/bin/activate

# Install packages
pip install flask requests pandas

# Save requirements
pip freeze > requirements.txt

# Deactivate environment
deactivate
```

### Working with Repositories
```bash
# Clone existing repository
git clone https://github.com/atulkamble/AzureVM-Linux.git
cd AzureVM-Linux

# Pull latest changes
git pull origin main

# Run Python application
python3 helloworld.py

# Edit file
nano helloworld.py

# Test changes
python3 helloworld.py

# Commit and push changes
git add .
git commit -m "Updated application"
git push origin main
```

---

## ✅ Verification Commands

### Check Installed Versions
```bash
# System information
lsb_release -a          # Ubuntu version
uname -r                # Kernel version

# Development tools
python3 --version       # Python version
pip3 --version          # pip version
git --version           # Git version
docker --version        # Docker version
node --version          # Node.js version
npm --version           # npm version

# Services status
sudo systemctl status nginx    # Nginx status
sudo systemctl status docker   # Docker status
```

### System Health Checks
```bash
# System resources
df -h                   # Disk usage
free -h                 # Memory usage
htop                    # Process monitor (press 'q' to quit)

# Network connectivity
ping -c 4 google.com    # Test internet connectivity
curl -I http://localhost # Test local web server
```

---

## 🔗 Additional Resources

- **Azure VM Documentation**: [https://docs.microsoft.com/azure/virtual-machines/](https://docs.microsoft.com/azure/virtual-machines/)
- **Azure CLI Reference**: [https://docs.microsoft.com/cli/azure/](https://docs.microsoft.com/cli/azure/)
- **Linux Command Cheatsheet**: [Azure-VM-Linux-Cheatsheet.md](Azure-VM-Linux-Cheatsheet.md)
- **Ubuntu Server Guide**: [https://ubuntu.com/server/docs](https://ubuntu.com/server/docs)

---

## 🤝 Contributing

Feel free to contribute to this guide by:
1. Forking the repository
2. Creating a feature branch
3. Making your improvements
4. Submitting a pull request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Happy coding on Azure! 🚀**
