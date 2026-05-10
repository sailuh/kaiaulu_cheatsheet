## Module Analysis

The steps are as follows:

1. **Analyze the Notebook:** Run the notebook and understand its functionality.
2. **Verify Tables:** Grab all tables that contain a different set of columns. You can ignore functions that only change the rows.
3. **Extract Tables:** Import the tables columns and one row into a spreadsheet and remove any Personal Identifiable Information (PII), such as email addresses and first/last names.
4. **Issue Creation:** Use the format in **Example Issue** 1 - 2 and the Task List.
5. **Add "Explicit Merge Functions":** These are columns that are affected by a `merge` function directly within the notebook (**Example Issue** 3).
6. **Add "Implicit Merge Functions":** These are columns affected by a `merge` function in a file other than the notebook (generally `.R` files). Search for all instances of `merge` in the codebase to understand if the application of the merge is utilized in the module (**Example Issue** 4).
7. **Add "Implicit Inner Joins":** These are joins not explicitly mentioned in any code file. An example is `file_pathname`, which is an inner join to the local path where the repository was downloaded (**Example Issue** 5).

---

## MySQL Workbench

Used to transfer the meaningful merges from GitHub issues to a diagram that is easily digestible for users.

1. **Create a New Layer:** Create a new layer for the module in the EER diagram.
   * *Note:* The layer color should have low saturation and avoid bright tones. Keep it visually distinct from other modules.

2. **Create or Update a Table:** * **If the table is new:** Create your table. 
     **Table names must follow this format:**
     * Standard format: `[table name in notebook]`
     * If the table name is reused, append the module name: `[table name in notebook]_[module]`
     * If both the table name and module are identical to an existing one, append the specific use case or function change: `[table name in notebook]_[module]_[use case]`
   * **If the table already exists:** Simply append the new columns discovered during your module analysis to the existing table. Do not duplicate the table.
   * **Data Types:** Column data types should match the spreadsheet example from your analysis (Example Issue 1.1).

3. **Define Relationships (PKs & FKs):** * Key formatting: All keys must be in `ALL_CAPS`.
   * **Primary Key (PK):** The first instance or origin of a column is the PK.
   * **Foreign Key (FK):** The table being created from a PK contains the FKs. *(Note: FKs can reference other FKs depending on data flow).*
   * **Drawing the Relationship:** Use the relationship tools on the left toolbar in Workbench (e.g., `1:n Non-Identifying Relationship`). **Important:** Always click the table receiving the Foreign Key (the child) FIRST, then click the table with the Primary Key (the parent).

---

## Finalizing & Exporting

1. **Save the Model:** Save your changes directly to the `.mwb` file located at `[Insert File Path to .mwb here]`.
2. **Export an Image:** Export a `.png` or `.pdf` of your updated EER diagram layer. You will need to attach this image to your GitHub Issue/Pull Request to prove your changes.
3. **Commit Changes:** Ensure the updated `.mwb` file is included in your Pull Request alongside your documentation.

## Example Issue

### As-is
* `[Insert image of the current table structure]`

---

### 1 Notebook 1: [Name of the Notebook]
* Overview of what the notebook does and its purpose.

#### 1.1 First Table: [Actual or agreed name with sponsor]
* Description of the table
* `[Permalink to the table in the notebook]`
* `[Spreadsheet of the table's columns and 1 row value]`
* `[Image of the table in My SQL workbench]`

#### 1.2 Second Table: [Name of the Table]
* *(Repeat the steps from 1.1 for each table in the notebook)*

---

### 2 Notebook 2: [Name of the Notebook]
* *(Sometimes issues contain multiple notebooks. Duplicate Notebook 1's steps until all notebooks are covered)*

---

### 3. Explicit Merge Functions

#### 3.1 [Name of the affected column(s)]
* Description of the merge in the notebook
* `[Permalink to the code]`
* `[Spreadsheet of the table's columns and 1 row value]`
* `[Image of the table in My SQL workbench]`

#### 3.2 [Next affected column]
* *(Loop until all Explicit Merge Functions are covered)*

---

### 4. Implicit Merge Functions

#### 4.1 [Name of the affected column(s)]
* Description of the merge in the file
* `[Permalink to the code]`
* `[Image of the table in My SQL workbench]`

#### 4.2 [Next affected column]
* *(Loop until all Implicit Merge Functions are covered)*

---

### 5. Implicit Inner Joins

#### 5.1 [Name of the affected column(s)]
* Reasoning for the inner join
* `[Image of the table in My SQL workbench]`

#### 5.2 [Next affected column]
* *(Loop until all Implicit Inner Joins are covered)*

---

### Task List
- [x] Notebook 1
- [x] External notebooks (if any exist)