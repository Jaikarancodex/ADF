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

*End of navigation cheatsheet — keep this as a pinned quick reference while you practice in ADF Studio.*

