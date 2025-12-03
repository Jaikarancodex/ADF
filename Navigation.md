# ADF Day 1 — UI Navigation Cheatsheet

A focused, step‑by‑step **UI walkthrough** (click-by-click) for everything you learned on Day 1. Use this as a quick reference while you work inside the Azure Portal and ADF Studio.

---

## 1. Azure Portal → Resource Group → Storage Account

1. Open **Azure Portal** (portal.azure.com).
2. Left menu → **Resource groups** → click your resource group (example: `myRG-adf`).
3. Inside the RG list, find and click your **Storage account** (example: `mystorageacct123`).

**Inside the Storage Account**

* Left menu → **Data storage** → click **Containers**.
* Click the container you want (example: `pracccontainer`).
* To upload a file: inside the container click **Upload** (top menu) → browse local file → **Upload**.
* To create a new container: **+ Container** → enter name (e.g. `outputcontainer`) → **Create**.
* To create folders inside a container: open container → click **+ Folder** → name folder (e.g. `raw/incoming`).

**Tips:**

* Use container names that reflect lifecycle: `raw`, `staging`, `processed`, `archive`.
* If you don’t see **Containers**, expand the **Data storage** section (it may be collapsed).

---

## 2. Azure Portal → Resource Group → Data Factory → Open ADF Studio

1. In the Resource Group view, click your **Data Factory** resource (example: `myADFWorkshopFactory`).
2. Top center: click **Author & Monitor** (this opens ADF Studio in a new tab).

**Tip:** If the portal shows a button labelled **Open** or **Author & Monitor**, that will also open the Studio.

---

## 3. ADF Studio — Main Areas & How to Open Them

When ADF Studio opens you’ll see a left-side vertical menu and a top bar. Primary sections:

* **Home** (landing page) — quick links and recent items.
* **Author** (pencil icon) — create pipelines, datasets, data flows, linked services.
* **Monitor** (graph icon) — view pipeline & activity runs, re-run, check logs.
* **Manage** (gear icon) — Integration Runtimes, Git configuration, Linked Services management, Triggers.

**Open Author:** click the **Author** icon (pencil) to build pipelines.

---

## 4. Authoring — Create Linked Service (Storage connection)

1. Author view → top-left area shows **Factory Resources** (Pipelines, Datasets, Data flows, etc.).
2. Click the **Manage** icon (gear) on the left to open Manage view.
3. Under Manage → **Linked services** → click **+ New**.
4. Select **Azure Blob Storage** or **Azure Data Lake Storage Gen2**.
5. Choose authentication (for learning: **Account key**) → select the Storage Account from the dropdown or paste details → click **Test connection** → **Create**.

**Note:** Linked Service stores connection and auth; datasets reference a linked service.

---

## 5. Authoring — Create a Dataset (Source / Sink)

1. Click **Author** (pencil) → under **Factory Resources** expand **Datasets** → click **+** → **New dataset**.
2. Choose **Azure Blob Storage** (or ADLS Gen2) → then choose **DelimitedText** (CSV).
3. On dataset configuration:

   * **Linked service:** choose the Linked Service you created (e.g., `AzureBlobStorage1`).
   * **Container:** click the folder icon to **browse** containers and select the file or folder.
   * **Directory / File name:** pick the exact file (for source) or leave File name blank for sink.
   * **First row as header:** toggle on if your CSV has header row.
   * **Import schema:** keep None for now (or import if you want typed schema).
4. Click **OK / Create**.

**Tip:** Use descriptive dataset names like `ds_students_raw` and `ds_students_processed`.

---

## 6. Authoring — Create a Pipeline

1. Author → **Pipelines** → **+** → **Pipeline**.
2. Rename the pipeline (click the title on top-left of canvas) e.g. `PL_CopyStudents`.
3. Left Activities pane → expand **Move & transform** → drag **Copy data** onto canvas.

**Configure Copy Activity:**

* Click the activity → bottom pane shows tabs.
* **Source tab:** choose your source dataset (`ds_students_raw`).
* **Sink tab:** choose your sink dataset (`ds_students_processed`).
* **Mapping:** click **Import schema** if you want ADF to auto-map columns.

**Save changes:** use **Publish all** on the top bar (big blue button) — this deploys your edits.

---

## 7. Debug, Publish, and Trigger

* **Debug:** use the **Debug** button (top toolbar inside the author canvas) to test-run without publishing.
* After Debug success → click **Publish all** (big blue button at top) to persist changes.
* To run the pipeline manually after publish: click **Add trigger** → **Trigger now**.
* To schedule: **Add trigger** → **New/Edit** → set a schedule or event trigger.

**Monitor runs:** Click the **Monitor** icon (left) → click **Pipeline runs** → click a run to see activity details and logs.

---

## 8. Verify Output in Storage

1. Return to the **Azure Portal** tab → Storage account → **Containers** → open the sink container (e.g., `outputcontainer`).
2. Confirm a new file appears (ADF creates the file in the sink container).
3. If the sink dataset left File name blank, ADF may generate a filename (sometimes `.txt`).

---

## 9. Quick UI Checklist (Step-by-step) — Day 1 Flow

1. Azure Portal → Resource groups → select RG
2. RG → click Storage Account → Data storage → Containers → upload `student.csv` to `pracccontainer`
3. RG → click Data Factory resource → **Author & Monitor** → opens Studio
4. Studio → Manage → Linked services → + New → create `AzureBlobStorage1` using Account Key
5. Studio → Author → Datasets → + New → DelimitedText → create `ds_students_raw` (point to `pracccontainer/student.csv`)
6. Studio → Author → Datasets → + New → DelimitedText → create `ds_students_processed` (point to `outputcontainer`, file blank)
7. Studio → Author → Pipelines → + New Pipeline → drag **Copy Data** activity
8. Configure Copy Data: Source = `ds_students_raw`, Sink = `ds_students_processed`
9. Click **Debug** → confirm success → Click **Publish all** → Click **Add trigger → Trigger now**
10. Portal → Storage Account → Containers → `outputcontainer` → verify copied file

---

## 10. Troubleshooting (UI-specific)

* **Can't find Containers**: Expand **Data storage** or search within the storage account left menu.
* **Linked service test fails**: re-check storage account name, keys, or network/firewall settings.
* **ADF shows 0 pipelines**: You must **Publish all** to persist authored objects; use Debug for quick testing.
* **Copy fails**: Open Monitor → click the failed run → read activity error message → check dataset file path and permissions.

---

## 11. Small Tips & Best Practices (UI habits)

* Use consistent naming: prefixes like `ds_`, `ls_`, `pl_` help navigation.
* Keep containers organized: `raw/`, `staging/`, `processed/`.
* Always use **Debug** while developing, then **Publish** when stable.
* Use the folder browser (folder icon) when creating datasets — it prevents path mistakes.

---

# Day 2 — ADF: Step-by-step Azure Portal & ADF Studio Navigation

This file contains precise, click-by-click UI navigation for everything you built on **Day 2** and the Key Vault steps you completed. Use it as a checklist while working in the portal.

---

## Table of contents

1. Day 2 — Ingest & Orchestrate (Portal → ADF Studio)

   * 1.1 Upload practice CSV to Storage
   * 1.2 Create Linked Service in ADF
   * 1.3 Create Source Dataset
   * 1.4 Create Pipeline and Parameters
   * 1.5 Add Get Metadata
   * 1.6 Add If Condition
   * 1.7 Create Sink Dataset
   * 1.8 Add Copy Activity
   * 1.9 Add Pipeline Variables & Set Variable
   * 1.10 Debug, Monitor, Publish
2. Key Vault — Step-by-step (Portal → Configure → ADF)

   * 2.1 Create Key Vault
   * 2.2 Add a Secret
   * 2.3 Fix RBAC if needed (assign roles)
   * 2.4 Grant ADF access (RBAC)
   * 2.5 Create Key Vault Linked Service in ADF
   * 2.6 (Optional) Use Key Vault secret in Storage LS

---

# 1. Day 2 — Ingest & Orchestrate (Portal → ADF Studio)

> All steps assume you are signed-in to the Azure Portal with the subscription that contains your resources.

## 1.1 Upload practice CSV to Storage (Azure Portal)

1. Portal: click **All resources** → open **Storage account** `practice2sa`.
2. In the storage blade (left menu) click **Containers** (under Data storage).
3. Click container name **praccontainer**.
4. Click **Upload** (top menu).

   * Files: choose local file `studentpracticecsvadls.csv`.
   * Destination path: leave blank (file at container root) or type `input/` to upload into a folder.
   * Click **Upload**.
5. Verify: container view shows `studentpracticecsvadls.csv`. Click the file to view properties and size.

> Tip: If you want an `output` folder, create it now from container → + Folder → name `output`.

---

## 1.2 Create Linked Service in ADF (ADF Studio)

1. Portal: open your **Data Factory** resource → click **Open Azure Data Factory Studio**.
2. In ADF Studio left rail click **Manage** (gear icon).
3. Under **Connections** click **Linked services**.
4. Click **+ New** → choose **Azure Data Lake Storage Gen2** (or **Azure Blob Storage** depending on your account type) → **Continue**.
5. Configure:

   * **Name**: `LS_practice2sa`
   * **Authentication**: choose **Account key** (or Managed Identity if you prefer) — for the account key, paste the key from Storage Account → Access keys.
   * Click **Test connection** → **Create**.

---

## 1.3 Create Source Dataset (ADF Studio)

1. In ADF Studio left rail click **Author** (pencil icon).
2. Under **Factory Resources** → **Datasets** → click **+** → **Dataset**.
3. Choose **Azure Data Lake Storage Gen2** → Format **DelimitedText** → **Continue**.
4. **Name**: `ds_studentpractice` → Click **OK**.
5. In **Connection**:

   * Linked service: `LS_practice2sa`
   * Container: `praccontainer`
   * Directory: leave empty (root) or set `input` if you uploaded under `input/`
   * File: `studentpracticecsvadls.csv`
   * First row as header: **On**
   * Import schema: None (OK for now)
6. Click **Preview data** to confirm rows load.
7. Save the dataset (Ctrl+S).

---

## 1.4 Create Pipeline and Parameters

1. In **Author** → under **Pipelines** click **+** → **Pipeline**.
2. Rename pipeline to `PL_DynamicCopy`.
3. On the pipeline properties pane click **Parameters** → **+ New** three times and create:

   * `SourceFolder` (String)
   * `SourceFile` (String)
   * `TargetFile` (String)
4. Save (Ctrl+S).

Expected test values later:

* SourceFolder: (blank)
* SourceFile: `studentpracticecsvadls.csv`
* TargetFile: `output_student.csv`

---

## 1.5 Add Get Metadata Activity

1. From the Activities toolbox expand **General** → drag **Get Metadata** onto the canvas.
2. Rename to `GetMeta_CheckFile` (click activity → General tab → rename).
3. Settings tab:

   * Dataset: `ds_studentpractice` (no dataset params if dataset pointed to the file directly)
   * Field list: add `exists`, `size`, `lastModified`.
4. Save pipeline.

---

## 1.6 Add If Condition

1. From toolbox → **Iteration & conditionals** → drag **If Condition** to the canvas to the right of the Get Metadata.
2. Connect `GetMeta_CheckFile` → drag green arrow to the `If Condition` (creates dependency).
3. Select the If Condition activity and rename to `If_FileExists`.
4. Settings → Expression → Add dynamic content:

```
@activity('GetMeta_CheckFile').output.exists
```

5. Save.

---

## 1.7 Create Sink Dataset (parameterized)

1. Author → Datasets → + → Azure Data Lake Storage Gen2 → DelimitedText → Continue.
2. Name: `ds_student_sink` → OK.
3. Parameters tab: add parameter `TargetFile` (String).
4. Connection tab:

   * Linked service: `LS_practice2sa`
   * Container: `praccontainer`
   * Directory/Folder: `output` (or root)
   * File: Add dynamic content: `@dataset().TargetFile`
   * First row as header: On
5. Save dataset.

---

## 1.8 Add Copy Data Activity (inside If True)

1. Select `If_FileExists` activity → click the small pencil/edit icon to open the inner canvas.
2. From toolbox → **Move & transform** → drag **Copy Data** into the True canvas.
3. Rename to `Copy_To_Sink`.
4. Source tab: Dataset → `ds_studentpractice`.
5. Sink tab: Dataset → `ds_student_sink` and set its dataset parameter `TargetFile` to dynamic: `@pipeline().parameters.TargetFile`.
6. (Optional) Mapping tab → Auto-mapping.
7. Save.

---

## 1.9 Pipeline Variables & Set Variable

1. Click the empty pipeline canvas → on the right panel click **Variables** → Add:

   * `FileSize` (String)
   * `Status` (String)
2. Edit inner canvas (If True) → from toolbox add **Set Variable** activity after `Copy_To_Sink`.

   * Rename to `Log_FileSize`.
   * Settings: Variable name `FileSize`, Value: dynamic content:

```
@string(activity('GetMeta_CheckFile').output.size)
```

3. Switch to the False tab and add **Set Variable** activity named `Set_Status_FileMissing`.

   * Settings: Variable `Status`, Value: `"File Missing"`.
4. Save pipeline.

---

## 1.10 Debug, Monitor & Publish

1. Click **Debug** → enter parameters:

   * SourceFolder: (blank)
   * SourceFile: `studentpracticecsvadls.csv`
   * TargetFile: `output_student.csv`
2. Click **OK** and wait for the run.
3. Monitor: left rail → **Monitor** → open the latest pipeline run → click activities to view **Input/Output** JSON.

   * Check `GetMeta_CheckFile` output: `exists: true`, `size: <number>`.
   * Check `Copy_To_Sink` output for `rowsRead` / `rowsCopied`.
4. Verify sink file exists: Storage Account `practice2sa` → Container `praccontainer` → Folder `output` → `output_student.csv`.
5. If success → Author pane → top-right **Publish All**.

---

# 2. Key Vault — Step-by-step (Portal → Configure → ADF)

> This covers creating Key Vault, adding secret, fixing RBAC and wiring Key Vault within ADF.

## 2.1 Create Key Vault

1. Azure Portal → **Create a resource** → search **Key Vault** → **Create**.
2. Fill the form:

   * Subscription: Azure for Students
   * Resource group: `RGnew` (or your RG)
   * Key vault name: `storage-2-key` (or your chosen name)
   * Region: choose region (East US is fine)
   * Pricing tier: Standard
   * Soft-delete: Enabled is OK
3. Click **Review + create** → **Create**.
4. After deployment click **Go to resource**.

## 2.2 Add a Secret

1. In Key Vault left menu → click **Secrets**.
2. Click **+ Generate/Import**.
3. Name: `storage-key`.
4. Value: paste the **Storage account Key** (from Storage Account → Access keys → Key1).
5. Click **Create**.

> If you see an RBAC error when adding a secret, proceed to fix RBAC (next section).

## 2.3 Fix RBAC (if needed)

1. In Key Vault → left menu → **Access control (IAM)**.
2. Click **+ Add** → **Add role assignment**.
3. Choose a role for your user like **Key Vault Administrator** or **Key Vault Secrets Officer** and assign it to your user account.
4. Click **Review + Assign**.
5. Wait 30–60 seconds and retry adding the secret.

## 2.4 Grant ADF access to Key Vault (RBAC mode)

> If your Key Vault uses RBAC for access management, do this:

1. Key Vault → **Access control (IAM)** → **+ Add** → **Add role assignment**.
2. Search for role **Key Vault Secrets User** (or **Key Vault Reader** if not available).
3. Members → **Select members** → search for your Data Factory name (it will appear as a managed identity).
4. Select it → **Review + Assign**.

> If the Key Vault uses legacy Access Policies (older UI), you'd use Key Vault → Access policies → Add policy → select ADF managed identity and give **Get** and **List**.

## 2.5 Create Key Vault Linked Service in ADF

1. ADF Studio → **Manage** → **Linked services** → **+ New**.
2. Choose **Azure Key Vault** → Continue.
3. Name: `LS_KeyVault`.
4. Base URL: choose the Key Vault resource `https://storage-2-key.vault.azure.net/`.
5. Authentication method: **Managed Identity** (System-assigned) → Test connection → Create.

## 2.6 (Optional) Use Key Vault secret in Storage Linked Service

Two common approaches:

**A. If you want to use Key Vault secret (Account Key) in Storage LS**

1. Storage Account must allow shared key access.
2. In ADF Manage → Linked services → edit `LS_practice2sa`.
3. Change Authentication to **Account key (from Azure Key Vault)**.
4. Select `LS_KeyVault` and Secret name `storage-key`.
5. Test connection → Save.

**B. Recommended modern approach — Keep using Managed Identity for Storage**

1. Keep `LS_practice2sa` using Managed Identity authentication.
2. Ensure ADF managed identity has **Storage Blob Data Contributor** (or appropriate) role on the Storage Account via Storage Account → Access control (IAM) → Add role assignment.

---

# Quick checklist (copy this into your notes)

* [ ] studentpracticecsvadls.csv uploaded to `praccontainer`
* [ ] `LS_practice2sa` created and tested
* [ ] `ds_studentpractice` created and previewed
* [ ] `PL_DynamicCopy` with params created
* [ ] `GetMeta_CheckFile` added and configured
* [ ] `If_FileExists` added with correct expression
* [ ] `ds_student_sink` created with parameterized file name
* [ ] `Copy_To_Sink` added and linked to pipeline params
* [ ] Pipeline variables `FileSize`, `Status` added and logged
* [ ] Debugged pipeline and verified sink file
* [ ] Key Vault `storage-2-key` created
* [ ] Secret `storage-key` added to Key Vault
* [ ] RBAC configured so ADF can read secrets
* [ ] `LS_KeyVault` linked service created
* [ ] Storage linked service updated (if needed)

---

# Notes

* Use Managed Identity for production — it is modern and secure.
* Key Vault is primarily for secrets you don't want in plain text (SQL passwords, API keys, storage keys if you prefer key-based auth).
* Save and publish often. Keep a Git branch for your ADF factory if you plan CI/CD later.

---

If you want a downloadable markdown file, say **"Export MD"** and I'll prepare it for download.

*End of navigation cheatsheet — keep this as a pinned quick reference while you practice in ADF Studio.*

