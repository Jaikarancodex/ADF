# 🛠 ADF

# 💥 1.1 Global Data Centers
Azure operates worldwide **data centers** grouped into **Regions**.  
Each region has multiple datacenters for:
- High availability  
- Low latency  
- Disaster recovery  

### ✔ Example  
Deploy a VM in *Central India* so nearby users get faster access.

---

# 💥 1.2 Azure Subscription & Resource Groups

### What is a Subscription?
A Subscription = **billing boundary** + **access boundary**.  
Everything you deploy is billed under this.

### What is a Resource Group (RG)?
A Resource Group = **logical container** for Azure resources.  
Used to group, manage, secure, and delete resources together.

---

## ✔ 1.2.1 Creating an Azure Subscription
Ways to create:
- **Azure Portal**  
- **Free Trial**, **Pay-As-You-Go (PAYG)**, **Azure for Students**  

### ✔ Example  
Activate a **Student Subscription** → Deploy VMs and Storage without a credit card.

---

## ✔ 1.2.2 Managing Resources in Resource Groups
You can:
- Deploy resources (VMs, SQL, VNet, Storage)
- Apply RBAC permissions
- Add tags
- Delete entire RG → deletes all resources

### ✔ Example  
Create `MyProject-RG` → Put VM + SQL Database + VNet inside it.

---

# 💥 1.3 Azure Workspace & User Interface (UI)

Azure Portal = web UI to manage all services.

---

## ✔ 1.3.1 Navigating the Azure Portal
Main navigation sections:
- **Home**  
- **All Services**  
- **Resource Groups**  
- **Dashboard**  
- **Search Bar (most used)**  

### ✔ Example  
Search “Storage Account” → Click “Create” → Deploy instantly.

---

## ✔ 1.3.2 Dashboard & Resource Management

### Dashboard
Your customizable workspace. Add tiles, charts, shortcuts.

### Resource Management
Manage everything from one screen:
- Start/stop VMs  
- Check storage files  
- Monitor logs and performance  
- Apply security settings  

### ✔ Example  
Pin your VM CPU chart to the Dashboard → monitor performance live.

---

## ✔ 1.3.3 Azure CLI & PowerShell

### Azure CLI
Command-line tool for Azure. Works on Windows, Mac, Linux.

### PowerShell
Scripting and automation tool (Azure-specific modules).

---

## ✔ 1.3.4 Command-Line Interface Options
Use Azure from:
- **Azure CLI**  
- **PowerShell**  
- **Cloud Shell (Browser-based Bash/PowerShell)**  

### ✔ Example  
List all Resource Groups:
```
az group list -o table
```

---

## ✔ 1.3.5 Scripting with PowerShell
Automate repetitive tasks using `.ps1` scripts.

### ✔ Example  
Start a VM:
```
Start-AzVM -Name MyVM -ResourceGroupName MyRG
```

Great for:
- Automated deployments  
- Bulk operations  
- Scheduled tasks  

