## 🔹 Step 1: Login

```bash
az login
```

---

## 🔹 Step 2: Create Resource Group

```bash
az group create \
  --name myRG \
  --location eastus
```

---

## 🔹 Step 3: Create Azure VM (Username + Password)

```bash
az vm create \
  --resource-group myRG \
  --name myVM \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --admin-password 'Password@123'
```

✅ This single command creates:

* VM
* VNet
* Subnet
* NSG
* Public IP
* NIC

---

## 🔹 Step 4: Allow SSH (Port 22)

```bash
az vm open-port \
  --resource-group myRG \
  --name myVM \
  --port 22
```

---

## 🔹 Step 5: Connect Using Password

```bash
ssh azureuser@<PUBLIC-IP>
```

When prompted, enter:

```
Password@123
```

---

## ⚠️ Password Rules (IMPORTANT)

Your password **must** have:

* At least **12 characters**
* **1 uppercase**
* **1 lowercase**
* **1 number**
* **1 special character**

Example ✅
`Azure@123456`

---

### 🧠 Ultra-short version (copy-paste)

```bash
az vm create -g myRG -n myVM --image Ubuntu2204 \
--admin-username azureuser \
--admin-password 'Azure@123456'
```

