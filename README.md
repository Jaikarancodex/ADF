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

---

# 💥 1.4 Azure Storage Account (Types)
Azure Storage Account offers multiple storage services suited for different workloads.

---

## ✔  1.4.1 Blob Storage
Used for storing **unstructured data** such as:
- Images, videos  
- CSV, JSON, logs  
- Backups  
- Data Lake files  

Best for analytics, large-scale storage, and data lake solutions.

---

## ✔ 1.4.2 File Storage
Cloud-based **SMB file shares**.

Use cases:
- Shared file systems for VMs  
- On-prem file server migration  
- Lift-and-shift applications needing shared storage  

---

## ✔ 1.4.3 Table Storage
A NoSQL **key-value** store.

Use cases:
- IoT metadata  
- App configuration  
- Semi-structured datasets  

---

## ✔  1.4.4 Queue Storage
Message queueing for asynchronous communication.

Use cases:
- Background job processing  
- Event-based systems  
- Decoupling between app components  

---

# 💥 1.5 Azure Data Factory (ADF)

## ✔  Introduction to ADF
ADF is Azure’s **ETL / ELT orchestration tool** that:
- Moves data  
- Transforms data  
- Connects cloud, on-prem, and SaaS systems  

---

## ✔  Key Components

### **Pipelines**
A workflow container holding activities.

### **Datasets**
Represents the **data source/structure** (CSV file, SQL table, JSON, etc.).

### **Linked Services**
Connection configuration for:
- Databases  
- Storage  
- APIs  
- SaaS apps  

---

# 💥 1.6 Azure Key Vault

## ✔  1.6.1 Securely Store and Manage Sensitive Information
Stores:
- Secrets  
- Keys  
- Certificates  

Prevents hardcoding sensitive values in:
- Apps  
- Pipelines  
- Functions  

Integrates with ADF, AKV, Functions, SQL, etc.

---

# 💥 1.7 Integration with Azure Services

## ✔  1.7.1 Dataset & Linked Service
- **Linked Service** → connection info (e.g., SQL connection)  
- **Dataset** → representation of data (table, file)

Example:  
Linked Service → Azure SQL  
Dataset → Sales table inside it.

---

## ✔  1.7.2 Integration Runtimes (IR)
ADF uses IR to perform data movement.

Types:
- **Azure IR** – cloud to cloud  
- **Self-hosted IR** – on-prem to cloud  
- **SSIS IR** – for SSIS package execution  

---

## ✔  1.7.3 Triggers & Monitoring

### Triggers
Start pipelines based on:
- Schedule  
- Event  
- Manual  

### Monitoring
You can view:
- Pipeline run history  
- Logs  
- Failures  
- Data movement statistics  

---

# 💥 1.8 Activities in ADF
Activities are **tasks** inside a pipeline. A pipeline can contain one or many activities that run in sequence or parallel.

---

# 💥 1.8.1 Data Movement Activity
Handles **copying data** from a source to a destination (sink).

## ✔ 1.8.1.1 Azure Blob Storage Source/Sink
Used when reading/writing:
- CSV  
- JSON  
- Parquet  
- Unstructured files in Blob Storage  

Example:  
Copy data from **Blob Storage → Data Lake**.

## ✔ 1.8.1.2 Azure SQL Database Source/Sink
Read or write directly to SQL tables.

Examples:
- Load CSV → SQL table  
- Export SQL table → Blob or Data Lake  

---

# 💥 1.8.2 Execution Control Activities
Manage execution and logic inside pipelines.

## ✔ 1.8.2.1 Execute Pipeline Activity
Runs another pipeline from inside the current pipeline.

Use case:  
Main pipeline → calls **child ETL pipelines**.

---

## ✔ 1.8.2.2 If Condition Activity
Runs activities **based on a condition** (true/false).

Example:  
If file exists → copy it  
Else → send an alert

---

## ✔ 1.8.2.3 ForEach Activity
Loops over a list (files, tables, values) and executes activities inside.

Example:  
Loop through **all files in a folder** and copy each file.

---

## ✔ 1.8.2.4 Web Activity
Sends HTTP calls to APIs.

Use cases:
- Trigger external REST API  
- Send notifications  
- Call Logic App  
- Start external jobs  

---

# 💥 1.8.3 Control Flow Activities
Used to control how pipelines behave.

## ✔ 1.8.3.1 Wait Activity
Pauses pipeline execution for a set time.

Example:  
Wait 30 seconds before calling next API.

---

## ✔ 1.8.3.2 Until Activity
Repeats execution **until a condition becomes true**.

Example:  
Check if a file has arrived.  
If not → wait 1 minute → check again.

---

## ✔ 1.8.3.3 Get Metadata Activity
Fetches metadata like:
- File size  
- Last modified date  
- Folder content  

Example:  
Get file size before copying it.

---

## ✔ 1.8.3.4 Lookup Activity
Executes a query or reads JSON/CSV metadata.

Example:  
Fetch **list of tables** to loop over in ForEach.

---

## ✔ 1.8.3.5 Stored Procedure Activity
Executes a stored procedure inside SQL Database.

Example:  
Run `usp_CleanSalesData` before copying data.

---

# 💥 1.8.4 Pipelines & Triggers

## ✔ Pipelines
A pipeline is a **workflow** containing activities.

Example:  
Daily ETL pipeline → Copy → Transform → Load → Notification.

---

## ✔ Triggers
Triggers **start** the pipeline.

Types:
- **Schedule Trigger** – run daily/hourly  
- **Event Trigger** – file arrival  
- **Manual Trigger** – run anytime from portal  

Example:  
Run pipeline every day at 1 AM.

---

# 💥 1.9 Azure Notebooks
Azure Notebooks allow interactive execution of:
- **Python**
- **SQL**
- **Scala**

Used for:
- Data exploration  
- ETL development  
- Machine learning  
- Interactive Spark-based analysis  

---

##  ✔  1.9.1 Overview of Azure Databricks Notebooks Integration
Databricks notebooks integrate seamlessly with Azure services.

Features:
- Unified workspace for SQL, Python, Scala  
- Autoscaling Spark clusters  
- Easy integration with:
  - Azure Data Factory  
  - Azure Storage / ADLS  
  - Azure SQL  
  - Azure Key Vault  

### ✔ Example  
ADF Pipeline → Databricks Notebook Activity → Spark transforms input CSVs → Writes cleaned data to ADLS.

---

##  ✔  1.9.2 Notebook Orchestration
ADF orchestrates Databricks notebooks by:
- Passing parameters  
- Triggering cluster execution  
- Monitoring notebook runs  
- Handling retries and failure logic  

### ✔ Example Flow  
1. File arrives in ADLS → Event Trigger  
2. ADF executes Databricks Notebook  
3. Notebook cleans data and outputs Parquet  
4. ADF loads the result into Azure SQL or another sink  

---

# 💥 1.10 Azure DevOps, CI/CD Integration
Azure DevOps enables **automation of builds, tests, and deployments**.

Components:
- **Repos** → source code  
- **Pipelines** → CI/CD automation  
- **Artifacts** → package storage  
- **Boards** → agile management  

---

## 1.10.1 Continuous Integration & Continuous Deployment (CI/CD)

###  ✔  Continuous Integration (CI)
Runs automatically when code is pushed:
- Builds the application  
- Runs test cases  
- Validates changes  
- Generates deployment-ready packages  

Goal: Catch issues early.

---

###  ✔  Continuous Deployment (CD)
Automatically deploys application or infrastructure to environments like:
- Dev  
- Test  
- Staging  
- Production  

### ✔ Example CI/CD Flow  
1. Developer pushes code to Git repo  
2. **CI Pipeline** builds & tests  
3. **CD Pipeline** deploys:
   - ADF pipelines  
   - Function Apps  
   - Databricks notebooks  
   - ARM/Bicep/Terraform resources  

Benefits:
- Faster releases  
- Fewer manual errors  
- Fully automated deployments  



