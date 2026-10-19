# 🏢 ServiceNow Asset Inventory Project

## 👋 Welcome

This project shows, step by step, how to take a list of business data, bring it into ServiceNow, keep it clean, and turn it into a report and a dashboard that people can use.

The example is an asset inventory: a list of computers, printers, projectors and other equipment. Each asset has a tag, a name, a category, a location, a purchase date, a cost and a status. The same ten assets appear in every document, so you can follow the data from the spreadsheet all the way to the final dashboard and check the numbers at each stage.

You do not need to have used ServiceNow before. Each document explains the ideas it uses, and this README gives you a map of the whole project.

---

## 📚 Contents

1. What this project is about
2. Who this is for
3. How the project is organised
4. The files in this project
5. How the pieces fit together
6. The example data
7. Milestone 1: Preparing the spreadsheet and table
8. Milestone 2: Loading data and mapping it
9. Milestone 3: Transforming, checking and preventing duplicates
10. Milestone 4: Reports and dashboards
11. Expected results
12. Checklist for the whole project
13. Suggested folder layout
14. How to use the documents
15. Limits of this work
16. Key terms
17. Version history

---

## 💡 1. What this project is about

Organisations often keep important information in spreadsheets. Before that information can be useful inside a system such as ServiceNow, it has to be moved across carefully. A rushed import can create duplicate records, lose values or put information in the wrong place. Once that happens, every report built on the data is wrong too.

This project shows a safe way to do the job. It follows five stages:

1. **Prepare** the spreadsheet so that it is clean and consistent.
2. **Create** a table in ServiceNow that matches the spreadsheet.
3. **Load** the spreadsheet into a holding area called an import set.
4. **Transform** the data into the table, and check the result.
5. **Report** on the data, and share the results on a dashboard.

Along the way, the project shows how to stop duplicates from being created when the same data is loaded again. This safeguard is called coalesce, and it is explained in Milestone 3.

The project covers the work an administrator does on a ServiceNow developer instance. It does not cover connecting to other systems, building service catalogues, or planning a full production migration. Those topics would each need a project of their own.

---

## 👥 2. Who this is for

The documents are written for a student or a new administrator. They assume you can move around a web application and use a spreadsheet. They do not assume any experience with ServiceNow.

Where a term or an idea appears for the first time, it is explained in plain language. The key terms are also listed in Section 16.

---

## 🗂️ 3. How the project is organised

The work is divided into four milestones. Each milestone builds on the one before it.

| Milestone | Title | What you will do |
|---|---|---|
| 1 | Creation of Spreadsheet and Table | Prepare the data and design the table that will hold it |
| 2 | Creation of Import Set Table and Transform Map | Load the spreadsheet and connect it to the table |
| 3 | Transform Data, Validate and Enable Coalesce | Run the transform, check the results and stop duplicates |
| 4 | Creation of Reports and Dashboards | Build a report and show it on a dashboard |

It helps to think of the milestones as a chain. If Milestone 1 is incomplete, Milestone 2 cannot succeed. If Milestone 2 loads the wrong data, Milestone 3 will reveal problems, and Milestone 4 will show wrong figures. Checking each milestone before moving on saves a great deal of time.

---

## 📁 4. The files in this project

The project includes ten files. Most are Word documents, which give the instructions. One is an Excel workbook, which holds the new data to be loaded. This README is the eleventh file.

| File | Type | Length | Milestone | What it is for |
|---|---|---|---|---|
| Milestone1_Creation_of_Spreadsheet_and_Table.docx | Word | 12 pages | 1 | How to prepare the spreadsheet and the first steps for the table |
| Milestone1_Creation_of_Tables.docx | Word | 12 pages | 1 | A detailed guide to designing and creating a custom table |
| Milestone2_Import_Set_Table_and_Transform_Map.docx | Word | 12 pages | 2 | Loading a spreadsheet and understanding the import set |
| Milestone2_Create_Transform_Map.docx | Word | 12 pages | 2 | A focused guide to building the transform map |
| Milestone3_Transform_Data_Validate_Coalesce.docx | Word | 12 pages | 3 | Running the transform, checking the results and an introduction to duplicates |
| Milestone3_Enable_Coalesce_Avoid_Duplicates.docx | Word | 12 pages | 3 | A focused guide to switching on and testing coalesce |
| Inserting_New_Data.xlsx | Excel | 4 sheets | 3 | A workbook of six new assets, with checks that confirm they are ready to load |
| Milestone4_Report_1.docx | Word | 12 pages | 4 | A concise guide to creating Report 1 |
| Milestone4_Report_1_Full.docx | Word | 44 pages | 4 | A full guide to Report 1, including its specification, tests and appendices |
| Milestone4_Adding_Reports_to_Dashboard.docx | Word | 12 pages | 4 | How to create the Asset Overview dashboard and add Report 1 to it |

Where a milestone has two documents, the first is the broader guide and the second goes deeper into one topic. Both are useful: the broader guide gives you the context, and the focused one gives you detailed steps.

Across all the Word documents there are roughly 190 pages.

---

## 🔗 5. How the pieces fit together

Data moves through the project in one direction. Each stage uses the output of the stage before it.

```
Spreadsheet
    |
    v
Import set (a holding area with one row per spreadsheet row)
    |
    v
Transform map (the rules that copy each column to the right place)
    |
    v
Asset Inventory table (the validated records)
    |
    v
Report 1: Assets by Category (a bar chart)
    |
    v
Asset Overview dashboard (shows Report 1 alongside room for more)
```

A few points are worth remembering:

- The **spreadsheet** needs a header row, one asset per row, and a unique key. The key is the Asset Tag.
- The **table** needs a column for each spreadsheet header, and its choice lists must match the values in the spreadsheet.
- The **transform map** links the holding area to the table. It needs a rule for each column, and it needs coalesce switched on for the Asset Tag.
- The **report** reads the table. Its figures can only be as accurate as the data in the table.
- The **dashboard** does not store its own copy of the report. It shows the report as it is at the time someone opens it.

---

## 🧪 6. The example data

The example contains ten assets. The first four come from the original spreadsheet in Milestone 1. The other six are new, and they are in the workbook used in Milestone 3.

### 📄 6.1 The original four assets

| Asset Tag | Asset Name | Category | Location | Purchase Date | Cost | Status |
|---|---|---|---|---|---|---|
| AST-1001 | Dell Latitude 5420 | Laptop | Madurai Lab 1 | 2025-06-12 | 58,000 | In Use |
| AST-1002 | HP ProDesk 400 | Desktop | Madurai Lab 2 | 2025-07-03 | 42,500 | In Use |
| AST-1003 | Cisco Catalyst 2960 | Network | Server Room | 2024-11-20 | 31,000 | Active |
| AST-1004 | Epson EB-X51 Projector | Projector | Seminar Hall | 2025-01-15 | 47,500 | In Storage |

### 🆕 6.2 The six new assets

| Asset Tag | Asset Name | Category | Location | Purchase Date | Cost | Status |
|---|---|---|---|---|---|---|
| AST-1005 | Lenovo ThinkPad T14 | Laptop | Madurai Lab 3 | 2025-08-18 | 62,500 | In Use |
| AST-1006 | Dell OptiPlex 3090 | Desktop | Madurai Lab 3 | 2025-08-18 | 45,800 | In Use |
| AST-1007 | Netgear GS308 Switch | Network | Server Room | 2025-09-02 | 6,900 | Active |
| AST-1008 | BenQ MH560 Projector | Projector | Seminar Hall | 2025-09-10 | 52,000 | In Storage |
| AST-1009 | HP LaserJet M404dn | Printer | Admin Office | 2025-10-01 | 28,500 | In Use |
| AST-1010 | Apple iPad 10th Gen | Laptop | Library | 2025-10-06 | 38,900 | In Storage |

Once both sets are loaded, the table holds ten assets with unique tags from AST-1001 to AST-1010.

### 🔤 6.3 What each field means

| Field label | Column name in ServiceNow | Type | Required | Notes |
|---|---|---|---|---|
| Asset Tag | u_asset_tag | Text, up to 40 characters | Yes | The unique key. It must not repeat or contain stray spaces. |
| Asset Name | u_asset_name | Text, up to 100 characters | Yes | A descriptive name for the item. |
| Category | u_category | Choice | No | One of: Laptop, Desktop, Network, Projector, Printer. |
| Location | u_location | Text, up to 100 characters | No | Where the asset is kept. |
| Purchase Date | u_purchase_date | Date | No | Stored as a real date. |
| Cost | u_cost | Number | No | A plain number, with no currency symbol. |
| Status | u_status | Choice | No | One of: In Use, Active, In Storage, Retired. |
| Assigned to | u_assigned_to | Link to a user | No | Included in the design, but not used in the example data. |

The status "Retired" is available in the list but no example asset uses it. It is there so that withdrawn equipment can be recorded later.

---

## 🧱 7. Milestone 1: Preparing the spreadsheet and table

Milestone 1 gets the data and the destination ready. Nothing can be loaded until both exist and match each other.

### 📄 7.1 Preparing the spreadsheet

A good spreadsheet makes everything that follows easier. Keep these rules in mind:

- The first row holds the column headers and nothing else.
- Each later row holds one asset.
- Leave out merged cells, blank rows, totals and notes inside the data.
- Keep dates in one format throughout.
- Enter costs as plain numbers, without currency symbols or separators.
- Use the same spelling for every category and status.
- Remove any spaces at the start or end of each Asset Tag.

When the spreadsheet is ready, save it as an Excel file (.xlsx). If you prefer CSV, save it with UTF-8 encoding so that all characters are kept. Keep a copy of the original, so you can compare it with the imported data later.

### 🧩 7.2 Designing and creating the table

The table is where the data will live in ServiceNow. Some design choices are worth making deliberately:

- The table holds one kind of thing, an asset. It is a standalone table rather than an extension of the built-in Task table, because assets are reference information, not work items.
- The label is Asset Inventory and the internal name is u_asset_inventory. The "u_" prefix marks it as a custom table.
- The table is set to appear in the navigator, so it can be opened from the menu.

To create it, open the Tables module under System Definition, create a new table with the label and name above, and add one column for each spreadsheet header. Use the types and required settings in Section 6.3. Then add the choice values for Category and Status.

Before you leave this milestone, create one test record, check that it looks right, and delete it. The table should be empty when you start loading real data.

### 🚦 7.3 Checks before moving on

- The spreadsheet has the seven headers and the right number of rows.
- The table exists, appears in the navigator, and has all seven business columns.
- The choice values in ServiceNow match the spreadsheet exactly.
- The table is empty, or holds only what the next step expects.

---

## 🔄 8. Milestone 2: Loading data and mapping it

Milestone 2 moves the spreadsheet into ServiceNow in two stages. First, the rows go into an import set, which is a holding area. Second, a transform map copies them into the table. Keeping these stages separate is useful. You can inspect the holding area and catch problems before anything reaches the real table.

### 📥 8.1 Loading the spreadsheet

The Load Data module creates the import set for you.

1. Open System Import Sets and choose Load Data.
2. Give the data source a clear name, such as Asset Inventory Source.
3. Choose Excel or CSV as the file type and attach your spreadsheet.
4. Set the import set table label, such as Asset Inventory Import.
5. Submit the form. ServiceNow reads the headers and creates one row for each asset.
6. Compare the row count with your spreadsheet. The numbers should match.

Each row in the import set is given a state and an action. The state tells you whether it has been processed. The action tells you what happened to it: inserted as new, updated, skipped, ignored or failed. A short message explains any skip or failure.

### 🔀 8.2 Creating the transform map

The transform map is the set of rules that copies each column from the holding area into the table.

1. From the import set, choose Create Transform Map, or create one from System Import Sets.
2. Give it a name, such as Asset Inventory Transform.
3. Check that the source is the import set table and the target is u_asset_inventory.
4. Save the map. ServiceNow creates a rule, called a field map, for each column whose name matches.

Once the map exists, review each field map. Correct any that point to the wrong place, and add a field map by hand for any column that did not match. You will also switch on coalesce for the Asset Tag, which Milestone 3 explains in full.

Transform maps can also include small scripts. These can clean a value, check it, or skip a row. The most common place for a script is the one that runs before each row is written.

### 🚦 8.3 Checks before moving on

- The number of rows in the import set equals the number of assets in your spreadsheet.
- Every spreadsheet column has a field map.
- The transform map is switched on and points at u_asset_inventory.
- Nothing points at the wrong field.

---

## 🛡️ 9. Milestone 3: Transforming, checking and preventing duplicates

Milestone 3 runs the transform, checks what it produced, and makes sure you can load the same data again without creating duplicates. It has three parts.

### ▶️ 9.1 Running the transform and checking the results

To run the transform, open the import set and choose Transform. When it finishes, the import set shows as Processed.

On a first run into an empty table, you should see:

- an Insert for each valid asset,
- a Skip, with a reason, for any row that was deliberately excluded,
- no Errors.

Checking the results has two parts. The first is a count check. The number of spreadsheet rows should equal the number of import set rows, and the import set rows should add up to the actions shown: inserts, updates, skips, ignores and errors. The second is a value check. Look at a sample of records and confirm that the names, categories, dates and costs match the spreadsheet. For the example, check the first and last rows, and at least one asset from each category.

### 🔁 9.2 Coalesce: preventing duplicates

Imagine loading the same spreadsheet twice without any safeguard. Every asset would appear twice, and every total would double. Coalesce is the safeguard that prevents this.

When coalesce is switched on for a field, the transform looks in the table for a record that already has the same value in that field. If it finds one, it updates that record. If it does not, it creates a new one. For this project, coalesce is switched on for the Asset Tag, because the tag identifies each asset uniquely.

To switch it on, open the Asset Inventory transform map, find the field map from asset_tag to u_asset_tag, tick Coalesce, and save. Record in the map's description that Asset Tag is the coalesce key, along with the date and the reason.

Choosing the right key matters. A good key is unique, does not change over time, is present on every row, and is text. Asset Tag meets all four tests. Asset Name, Location, Purchase Date and Cost do not, because many assets can share them.

Keys also need care. Coalesce compares values exactly, so "AST-1001 " with a trailing space is treated as a different asset from "AST-1001". Remove spaces at the start and end of each key, use one consistent case, and check the spreadsheet for repeated keys before loading. Coalesce only compares against records that are already in the table, so it will not catch two rows with the same key in the same file.

### 🧪 9.3 Testing coalesce

The companion guide sets out seven test scenarios. The most important one is the repeat load. Load the same spreadsheet again and check that:

- every row shows Update rather than Insert,
- the number of records in the table has not changed,
- no Asset Tag appears twice.

If a repeat load creates new records, coalesce is missing from the Asset Tag field map or a key differs in spacing or case.

The other scenarios test a changed value, a genuinely new asset, a blank key, a messy key, and a duplicate within the file. Together they show that coalesce prevents duplicates without blocking new assets.

### ➕ 9.4 Adding new data

The workbook Inserting_New_Data.xlsx holds the six new assets, AST-1005 to AST-1010, in the same seven columns as the original spreadsheet. It is designed to make adding data safer.

- The **Instructions** sheet explains how to use the workbook and the rules that prevent duplicates.
- The **Insert_Data** sheet holds the new assets. Category and Status have dropdown lists.
- The **Lists** sheet holds the allowed values for those dropdowns.
- The **Checks** sheet runs automatic checks, such as blank tags, repeated tags and values that are not on the lists. Its status cell reads READY TO IMPORT when everything passes.

To add new assets, enter them on Insert_Data, confirm that the Checks sheet says READY TO IMPORT, save, and load the file. Every new asset should show as Insert. If one shows as Update, its tag already exists in the table and should be investigated before going further.

This workbook is for new assets only. Changes to existing assets belong in a separate file.

### 🚦 9.5 Checks before moving on

- The transform has run and the counts reconcile.
- Coalesce is switched on for the Asset Tag.
- A repeat load shows Update and leaves the count unchanged.
- No Asset Tag appears twice.
- The new-data workbook shows READY TO IMPORT.

---

## 📊 10. Milestone 4: Reports and dashboards

Milestone 4 turns the validated table into information people can use. You will build one report and place it on a dashboard.

### 📑 10.1 Report 1: Assets by Category

Report 1 answers a simple question: how many assets does the organisation hold in each category? The answer is shown as a bar chart with one bar per category, each labelled with its count. The bars are sorted from largest to smallest.

| Setting | What it is set to | Why |
|---|---|---|
| Data source | u_asset_inventory | This is where the assets are stored |
| Report type | Bar chart, vertical | Bars make counts easy to compare |
| Group by | Category | Creates one bar per category |
| Count of | Asset Tag | Each asset has one tag, so this counts assets |
| Sort | Count, largest first | The biggest category is seen first |
| Filter | None | The chart should show every asset |
| Title | Assets by Category | Says exactly what the chart shows |
| Legend | Off | There is only one set of values |
| Visibility | Asset team | Shares the report with the people who need it |
| Name | Asset Count by Category | A short, stable name for lists and dashboards |

Why a bar chart? Bars let a reader compare the size of each category at a glance. A pie chart would show shares rather than counts, a list would make the reader count by hand, and a trend chart needs a history the table does not hold.

Why no filter? The question concerns all assets, so the total on the chart should match the number of records in the table. A filter would make that check harder, and it would also change the title.

To build the report, create a new report in the Reports module, choose the table, choose the bar chart type, and set the group, count, sort and title as above. Save it with the name Asset Count by Category. Then write a short description covering its purpose, data source, grouping, count, sort, owner and the date you last checked it. Set the visibility to the asset team once you have checked the figures.

### 📚 10.2 Two versions of the Report 1 guide

There are two guides for Report 1:

- The **12-page guide** covers the essentials: the steps, the tests and the common problems. Use it to build the report quickly.
- The **44-page guide** covers everything in depth: the background, the requirements, the full specification, the chart settings, the filters, the data quality checks, a twelve-part test plan, maintenance and appendices with a checklist, a glossary and a sign-off form. Use it for review, for sign-off, or when you want to understand the reasoning behind each choice.

### 🖥️ 10.3 The Asset Overview dashboard

A dashboard is a page that brings several reports together, so that a manager can see the situation at a glance. The Asset Overview dashboard shows Report 1 and leaves room on the right-hand side for a later report.

The dashboard does not store its own copy of Report 1. It shows the report as it is at the moment someone opens the dashboard. That means if the report is updated, the dashboard shows the update automatically.

To build the dashboard, create a dashboard called Asset Overview, switch to edit mode, add a report widget and choose Asset Count by Category. Check that the widget reads from u_asset_inventory and shows a bar chart. Place it at the top left, make it about half the width of the page, save the layout, and reload the page to confirm it is still there.

A few points to keep in mind:

- Dashboard filters apply only to the reports whose data contains the matching field. For version 1, the dashboard has no filters, so that its totals can be checked against the table directly.
- The report must be visible to the asset team, or the team will see an empty panel where the chart should be.
- Only the owner and administrators should be able to change the layout. Team members should be able to view it.

### 🚦 10.4 Checks before moving on

- Report 1 passes its twelve tests.
- The chart figures match the expected counts in Section 11.
- The Asset Overview dashboard shows Report 1 correctly.
- The asset team can open both the report and the dashboard.

---

## ✅ 11. Expected results

These are the figures you should see once the ten assets are loaded. They are a useful way to confirm that each stage has worked.

### 🧮 11.1 Assets by category

| Category | Count | Assets |
|---|---|---|
| Laptop | 3 | AST-1001, AST-1005, AST-1010 |
| Desktop | 2 | AST-1002, AST-1006 |
| Network | 2 | AST-1003, AST-1007 |
| Projector | 2 | AST-1004, AST-1008 |
| Printer | 1 | AST-1009 |
| **Total** | **10** | |

### 🧮 11.2 Assets by status

| Status | Count | Assets |
|---|---|---|
| In Use | 5 | AST-1001, AST-1002, AST-1005, AST-1006, AST-1009 |
| Active | 2 | AST-1003, AST-1007 |
| In Storage | 3 | AST-1004, AST-1008, AST-1010 |
| Retired | 0 | None |
| **Total** | **10** | |

### 💰 11.3 Total cost

The ten assets cost 413,600 in total. The six new assets account for 234,600 of that. If your total differs, check each cost in the table against the spreadsheet. A small difference often means a value was rounded or typed incorrectly.

### ⚖️ 11.4 Reconciling the stages

Reconciling means checking that the numbers agree at each stage, so that nothing has been lost or added along the way.

1. Count the rows in your spreadsheet.
2. Count the rows in the import set and check that they match.
3. Add up the actions (inserts, updates, skips, ignores and errors) and check that they equal the import set count.
4. Count the records in the table and check the total.
5. Compare each category on Report 1 with the figures in Section 11.1.
6. Note any difference and its cause.

### 🔁 11.5 What a repeat load should show

If you load the same ten assets again, the table should still hold ten records and every row should show Update. If any row shows Insert, coalesce is missing or the key differs in spacing or case.

---

## ☑️ 12. Checklist for the whole project

Work through this list at the end. Each item should be ticked, or explained if it is not.

🗃️ **Data**

- ⬜ The spreadsheet has the seven headers and the agreed rows.
- ⬜ No Asset Tag is blank, repeated or padded with spaces.
- ⬜ Category and Status values match the choice lists exactly.
- ⬜ Purchase Dates are real dates, and Costs are plain numbers.

🧩 **Table**

- ⬜ u_asset_inventory exists, with the label Asset Inventory.
- ⬜ All seven business columns exist with the correct types.
- ⬜ The choice lists for Category and Status are complete.
- ⬜ The table appears in the navigator and no test records remain.

🔀 **Import and transform**

- ⬜ The import set has the expected number of rows.
- ⬜ The transform map points at u_asset_inventory and is switched on.
- ⬜ Every spreadsheet column has a field map.
- ⬜ The transform has run and the counts reconcile.

🔁 **Coalesce**

- ⬜ Coalesce is switched on for the Asset Tag.
- ⬜ A repeat load shows Update and leaves the count unchanged.
- ⬜ No duplicate Asset Tags exist.
- ⬜ The map description records the key, the date and the reason.

➕ **New data**

- ⬜ Inserting_New_Data.xlsx shows READY TO IMPORT.
- ⬜ The new rows load as Insert.
- ⬜ The table holds ten records with unique tags.

📊 **Reports and dashboard**

- ⬜ Report 1 is named Asset Count by Category and passes its tests.
- ⬜ The chart figures match Section 11.1.
- ⬜ The Asset Overview dashboard shows Report 1 correctly.
- ⬜ The asset team can see the report and the dashboard.

---

## 🗃️ 13. Suggested folder layout

You may find it helpful to keep the files organised by milestone:

```
servicenow-asset-inventory/
├── README.md
├── milestone-1/
│   ├── Milestone1_Creation_of_Spreadsheet_and_Table.docx
│   └── Milestone1_Creation_of_Tables.docx
├── milestone-2/
│   ├── Milestone2_Import_Set_Table_and_Transform_Map.docx
│   └── Milestone2_Create_Transform_Map.docx
├── milestone-3/
│   ├── Milestone3_Transform_Data_Validate_Coalesce.docx
│   ├── Milestone3_Enable_Coalesce_Avoid_Duplicates.docx
│   └── Inserting_New_Data.xlsx
└── milestone-4/
    ├── Milestone4_Report_1.docx
    ├── Milestone4_Report_1_Full.docx
    └── Milestone4_Adding_Reports_to_Dashboard.docx
```

Keep your original spreadsheet, such as M1_Asset_Inventory.xlsx, with the Milestone 1 files. It is the source the rest of the project depends on, and it is not generated by these documents.

---

## 📖 14. How to use the documents

### 👣 14.1 Suggested reading order

1. Read both Milestone 1 documents.
2. Read the Milestone 2 import set and transform map document, then the focused transform map document.
3. Read the Milestone 3 transform and validation document, then the coalesce document. Open the new-data workbook and read its Instructions sheet.
4. Read the concise Report 1 guide, then the full guide if you want more depth, then the dashboard guide.

### 💡 14.2 Tips for working on the instance

- Work in one browser tab for each task. Two tabs editing the same record can overwrite each other.
- Save after each significant step.
- Write down any choice that differs from the guides, and why. This will make your validation much easier to explain.
- Keep your spreadsheet, your import set record and your validation notes together.

### 🧹 14.3 Test records

Several steps ask you to add a test record and then remove it. Give test records an obvious name, such as TEST-M4, so they are easy to spot. After deleting them, check that the table holds only the records you intend to keep.

### ✍️ 14.4 Using the sign-off form

The full Report 1 guide ends with a sign-off form in Appendix C. Complete it once the report has passed its tests and its figures have been reconciled.

---

## ⚠️ 15. Limits of this work

Please read this section before relying on the documents.

**The reference sites could not be checked.** Every document lists two reference sources: the ServiceNow Developers portal and a SkillWallet module. Neither could be read while the documents were prepared. The ServiceNow page needs a JavaScript-enabled browser, and the SkillWallet page sends visitors to a login screen. The instructions therefore follow the standard ServiceNow approach for these tasks, but they have not been checked against those sources.

**The steps have not been run on a live instance.** The documents describe what to do and what you should see. They have not been carried out on a real developer instance as part of this work. Menu names, option labels, report types and dashboard options can differ between releases, so compare each step with your course material and your own screen.

**The expected figures depend on the example data.** The counts, statuses and cost totals in Section 11 assume the ten assets in Section 6. If you use different data, recalculate them.

**Field names may differ on your instance.** The documents use names such as u_asset_inventory and u_asset_tag. ServiceNow may generate slightly different names depending on the scope and the label you choose. Use the names that exist on your instance.

**Some details are assumptions.** The dataset, the field names and the currency of the costs were chosen for this project. The costs are shown as plain numbers, and the dates use the yyyy-mm-dd format.

**What was checked.** The Excel workbook was recalculated, and its checks return the expected values with no errors. Each Word document was converted to PDF to confirm its length and layout. The numbered lists in the full Report 1 guide were checked so that each list starts at 1.

---

## 🔑 16. Key terms

| Term | Meaning |
|---|---|
| Asset Tag | The unique code that identifies one asset. It is the coalesce key. |
| Bar chart | A chart that shows one bar for each group, with the bar's length showing the count. |
| Choice field | A field whose value is picked from a fixed list. |
| Coalesce | A setting that stops a repeated import from creating duplicate records. |
| Dashboard | A page that brings several reports together in panels. |
| Data source | The table a report reads its information from. |
| Duplicate | A second record for the same item. |
| Field map | A rule that copies one column into one field. |
| Filter | A condition that limits which records a report includes. |
| Import set | The holding area where spreadsheet rows are stored before they are transformed. |
| Load Data | The ServiceNow module that reads a spreadsheet and creates an import set. |
| Reconciliation | Checking that the numbers agree at each stage, so nothing is lost or added. |
| Report | A saved view that summarises the records in a table. |
| Transform map | The set of rules that copies import set rows into a table. |
| Widget | A panel on a dashboard that shows a report or other content. |

---

## 🕘 17. Version history

| Version | Date | Summary |
|---|---|---|
| 1.0 | 13 October 2026 | First version, covering all four milestones, the example data, the expected results and the checklist. |
| 2.0 | 13 October 2026 | Revised for clarity and tone. Key terms are explained as they appear, and the structure has been simplified. Figures are unchanged. |

When a document is updated, add a line here and keep the file names in Section 4 matched to the files in the folder.
