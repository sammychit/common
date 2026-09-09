# Path A Lab 3 &ndash; Example Metadata and Data Files

Small, made-up training files for *Path A Lab 3: Configure Dimensions and Load Metadata and Data*. No real company content. The numbers are chosen to make the Lab 4 result easy to check.

## Terms

* **Dimension** &ndash; a list you analyse by (Account lists accounts; Entity lists parts of the organisation).
* **Member** &ndash; one item in a dimension (`Rent Expense` is a member of Account).
* **Parent / child** &ndash; members sit in a tree. A **parent** totals its **children**. Level-0 members (no children) hold the data.
* **Metadata** &ndash; the members and their tree. Load metadata **before** data.
* **Data** &ndash; the numbers, held where members cross (`Rent Expense` + `SVC-1` + `Jan` = 120000).

## Three kinds of member in these files

| Kind | Meaning | Which members |
| --- | --- | --- |
| **Already exists** | Created when the EPCM application was created. Do not try to load it. | `All Accounts` (top of Account), `Total Entity` (top of Entity), and the system members `PCM_Input`, `PCM_No Rule` |
| **Added by the files** | Members the CSV files add under an existing parent. | `Total Cost Pool`, `Rent Expense`, `IT Expense`, `Utilities Expense`, `Training Statistics`, `Headcount`, `Floor Area`, `Service Centers`, `Operating Centers`, `SVC-1`, `SVC-2`, `OPS-1`, `OPS-2`, `OPS-3` |
| **Added into a new custom dimension** | Members loaded under the **Activity** dimension you create in Lab 3 Task 2. | `Total Activity`, `NoActivity`, `Activity 1`, `Activity 2` |

## Load order

Load the three metadata files in this order, then the data file. Each file attaches to a parent that must already exist, so the order matters.

| # | File | Loads into | Attaches under | You should see |
| --- | --- | --- | --- | --- |
| 1 | `account-metadata.csv` | **Account** | `All Accounts` (already exists) | `All Accounts` &rarr; `Total Cost Pool` &rarr; `Rent Expense`, `IT Expense`, `Utilities Expense`, and `Training Statistics` &rarr; `Headcount`, `Floor Area` |
| 2 | `entity-metadata.csv` | **Entity** | `Total Entity` (already exists) | `Total Entity` &rarr; `Service Centers` &rarr; `SVC-1`, `SVC-2`; and `Total Entity` &rarr; `Operating Centers` &rarr; `OPS-1`, `OPS-2`, `OPS-3` |
| 3 | `activity-metadata.csv` | **Activity** (create it first) | `Activity` root | `Activity` &rarr; `Total Activity` &rarr; `NoActivity`, `Activity 1`, `Activity 2` |
| 4 | `data-training-jan.csv` | Data | n/a | January numbers for `FY24 / Actual / Working` (see below) |

## Metadata file format (files 1&ndash;3)

Comma-delimited, with a header row (EPCM requires one).

| Column | Meaning |
| --- | --- |
| `<Dimension>` (first column; header = the dimension name) | The member to add |
| `Parent` | The existing member it attaches under |
| `Alias: Default` | A display name (optional) |
| `Data Storage` | `Never Share` for level-0 members; blank for parents |

Column headers are case sensitive.

## Data file format (`data-training-jan.csv`)

EPM Cloud **"Default"** import format:

* First column header = the **load dimension** (`Account`).
* Next column header = a **driver** member (`Jan`, from the Period dimension). The number under it is the value for that Account + `Jan`.
* **`Point-of-View`** = the other dimension members that pin down the cell, comma-separated in one quoted field, in this order: `Entity, Years, Scenario, Version, Activity, PCM_Balance, PCM_Rule`.
* **`Data Load Cube Name`** = the calculation cube.

### What the numbers are

| Account | Entity | `Jan` value | Purpose |
| --- | --- | --- | --- |
| Rent Expense | SVC-1 | 120000 | A cost in a service centre |
| IT Expense | SVC-2 | 90000 | A cost in a service centre |
| Utilities Expense | SVC-1 | 30000 | A cost in a service centre (Lab 4 adds 10%) |
| Headcount | OPS-1 / OPS-2 / OPS-3 | 20 / 50 / 30 | The allocation **driver** in Lab 4 |
| Floor Area | OPS-1 / OPS-2 / OPS-3 | 3000 / 5000 / 2000 | A second statistic (not used in Lab 4) |

### Names to confirm for your environment

These can vary. Before loading, check and edit if needed:

| In the file | What it should be | Where to check |
| --- | --- | --- |
| `Jan` | Your Period dimension's January member | **Application &rarr; Overview &rarr; Dimensions &rarr; Period** |
| `FY24` | Your Years member for 2024 (Lab 2 uses a 2024&ndash;2025 calendar) | The **Years** dimension |
| `PCM_Input` | The **PCM_Balance** member for loaded input data | The **PCM_Balance** dimension |
| `PCM_No Rule` | The **PCM_Rule** member for data not made by a rule | The **PCM_Rule** dimension |
| `PCM_CLC` | The **calculation** cube name | **Application &rarr; Overview &rarr; Dimensions**, the **Cube** list |

This file assumes a **single-currency** application. If you chose multicurrency in Lab 2, add the currency member to each `Point-of-View` value.

**Best check:** type a few numbers on a form, then use **Application &rarr; Overview &rarr; Actions &rarr; Export Data** and open the exported file. It shows the exact header, point-of-view order, and cube name. Match `data-training-jan.csv` to it.

## Expected result after Lab 4

With the sequence **custom rule (10), then allocation rule (20)**:

* `Utilities Expense` at `SVC-1`: 30000 input + 3000 adjustment = **33000**.
* Moved from the service centres: 120000 + 90000 + 33000 = **243000**.
* Split by `Headcount` (20 / 50 / 30): `OPS-1` = 48600, `OPS-2` = 121500, `OPS-3` = 72900.
* The three expenses at `Service Centers` return to **0** (the offset).

Run the allocation before the adjustment and the total is **240000** instead &ndash; that is the point of the sequence.

## Troubleshooting

| Problem | Likely cause | Fix |
| --- | --- | --- |
| Metadata import **Failed** | The `Parent` does not exist yet, or a header name is mistyped | Open the failed job for the row and column. Load files in order; check `All Accounts` and `Total Entity` exist. |
| `activity-metadata.csv` fails | The **Activity** dimension is not created yet | Create it (Lab 3, Task 2), enable it on the cube, then import. |
| Data import **Failed** or **0 cells** | A point-of-view member or the cube name does not match your application | Use the "Names to confirm" table; export a data slice for the exact names. |
| Data import rejects rows | A value has a thousands separator, quotes, or two decimal points | Values must be plain numbers (the file already is). |
| Calculation shows `#MISSING` | Data went to the wrong cube or point of view | Re-check `Data Load Cube Name` and the point of view, reload, recalculate. |

## Note for the workshop author

The metadata files use the documented EPCM format and attach only to members that already exist (`All Accounts`, `Total Entity`) or that the files create in order. The data file's system members (`PCM_Input`, `PCM_No Rule`) and cube name (`PCM_CLC`) follow Oracle's documented naming but should be checked once against a real preconfigured environment. Run the full load-and-calculate flow once before publishing and confirm the 243000 result.
