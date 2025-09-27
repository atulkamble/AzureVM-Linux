# 🐧 Basic Linux Commands on Azure VM

## 1. Azure VM Setup

* **OS**: Ubuntu Server 24.04 LTS
* **NSG Rules**:

  * `22/tcp` → SSH
  * `80/tcp` → HTTP
  * `443/tcp` → HTTPS

---

## 2. SSH Connection

### First set permissions for your key

```bash
cd Downloads
chmod 400 key.pem
```

### Connect to VM

```bash
ssh -i "key.pem" atul@<PUBLIC_IP>
```

Example:

```bash
ssh -i key.pem atul@172.179.236.162
```

---

## 3. Basic Linux Commands Practice

```bash
clear               # clear screen
ls                  # list files
mkdir project       # create directory
ls
touch a.txt         # create file
ls
mv a.txt project/   # move file
ls
pwd                 # print working dir
cd project/         # change directory
pwd
ls
sudo nano a.txt     # edit file
cat a.txt           # view content
touch b.txt         # create another file
cat b.txt
ls
cp a.txt b.txt      # copy file
ls
cat b.txt           # verify content
ls
rm b.txt            # delete file
ls
cd ..               # go back
ls
rm -rf project/     # remove directory
ls
history             # show command history
```

---

## 4. Install Packages

```bash
sudo apt install snap -y
sudo snap install tree
sudo snap install docker
sudo apt install git -y
```

---

## 5. Verify Versions

```bash
docker --version
git --version
```
```
git init 
touch a.txt 
git add a.txt. 
git commit -m "added code"
git branch -M main
 
git clone https://github.com/atulkamble/AzureVM-Linux.git
cd AzureVM-Linux
git pull 
python3 helloworld.py 
nano helloworld.py 
python3 helloworld.py 
git add .
git commit -m "updated code"
git push origin main

```

---
