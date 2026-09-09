# Path A Lab 3 &ndash; Example Metadata and Data Files

These are **small, neutral training files** used by *Path A Lab 3: Configure Dimensions and Load Metadata and Data*. They contain no company or industry content. The numbers are arbitrary training values chosen to make the Lab 4 calculation easy to check.

## Key terms (plain language)

* **Dimension** &ndash; a list of things you analyse by. For example, the **Account** dimension lists accounts; the **Entity** dimension lists parts of the organisation.
* **Member** &ndash; one item in a dimension (for example, `Rent Expense` is a member of Account).
* **Parent / child** &ndash; members are arranged in a tree. A **parent** rolls up (totals) its **children**. Level‑0 members (no children) are where data is stored.
* **Metadata** &ndash; the members and their parent/child structure. You load metadata *before* you load data.
* **Data** &ndash; the numbers stored at member intersections (for example, `Rent Expense` + `SVC-1` + `Jan` = 120000).

## Three kinds of member in these files

| Kind | Meaning | In these files |
| --- | --- | --- |
| **Seeded (already exists)** | Created for you when the EPCM application is created. Do **not** try to load it. | `All Accounts` (top of Account), `Total Entity` (top of Entity), and the system members `PCM_Input`, `PCM_No Rule` |
| **Supplied by the workshop** | Members these files add under a seeded parent. | `Total Cost Pool`, `Rent Expense`, `IT Expense`, `Utilities Expense`, `Training Statistics`, `Headcount`, `Floor Area`, `Service Centers`, `Operating Centers`, `SVC-1`, `SVC-2`, `OPS-1`, `OPS-2`, `OPS-3` |
| **Created by loading into a new custom dimension** | Members added under the root of the **Activity** dimension, which you create in Lab 3 Task 2. | `Total Activity`, `NoActivity`, `Activity 1`, `Activity 2` |

## Files and load order

Load the three metadata files first (in this order), then the data file.

| Order | File | Loads into | Parent it attaches to | Result you should see |
| --- | --- | --- | --- | --- |
| 1 | `account-metadata.csv` | **Account** dimension | `Total Cost Pool` under the seeded **`All Accounts`** member | `All Accounts` &rarr; `Total Cost Pool` &rarr; `Rent Expense`, `IT Expense`, `Utilities Expense`, and `Training Statistics` &rarr; `Headcount`, `Floor Area` |
| 2 | `entity-metadata.csv` | **Entity** dimension | `Service Centers` and `Operating Centers` under the seeded **`Total Entity`** member | `Total Entity` &rarr; `Service Centers` &rarr; `SVC-1`, `SVC-2`; and `Total Entity` &rarr; `Operating Centers` &rarr; `OPS-1`, `OPS-2`, `OPS-3` |
| 3 | `activity-metadata.csv` | **Activity** custom dimension (create it first) | `Total Activity` under the new `Activity` root | `Activity` &rarr; `Total Activity` &rarr; `NoActivity`, `Activity 1`, `Activity 2` |
| 4 | `data-training-jan.csv` | Data (member intersections) | n/a | January input numbers loaded for `FY24 / Actual / Working` (see below) |

The metadata files list parents that must already exist, so the order matters: `All Accounts` and `Total Entity` are seeded; `Total Cost Pool` must load before its children; the `Activity` dimension must exist before file 3.

## Metadata file format (all three files)

Comma‑delimited, with a header row (the EPCM metadata import requires a header row).

| Column | Meaning |
| --- | --- |
| `<Dimension>` (first column, header = the dimension name) | The member being added |
| `Parent` | The existing member it attaches under |
| `Alias: Default` | A friendly display name (optional) |
| `Data Storage` | `Never Share` for level‑0 members; blank for parents (they inherit the default) |

Column headers are case sensitive.

## Data file format (`data-training-jan.csv`)

This uses the EPM Cloud **"Default"** import format:

* First column header = the **load dimension** (`Account`).
* Next column header(s) = one or more **driver dimension** members (`Jan`, a member of the Period dimension). The number under `Jan` is the value for that Account + `Jan`.
* **`Point-of-View`** = the remaining dimension members that pin down the exact cell, comma‑separated inside one quoted field, in this order: `Entity, Years, Scenario, Version, Activity, PCM_Balance, PCM_Rule`.
* **`Data Load Cube Name`** = the calculation cube.

### What the data means

| Account | Entity | `Jan` value | Purpose |
| --- | --- | --- | --- |
| Rent Expense | SVC-1 | 120000 | Cost sitting in a service centre |
| IT Expense | SVC-2 | 90000 | Cost sitting in a service centre |
| Utilities Expense | SVC-1 | 30000 | Cost sitting in a service centre (Lab 4 adjusts this by 10%) |
| Headcount | OPS-1 / OPS-2 / OPS-3 | 20 / 50 / 30 | Statistic used as the allocation **driver** in Lab 4 |
| Floor Area | OPS-1 / OPS-2 / OPS-3 | 3000 / 5000 / 2000 | A second statistic (not used by the Lab 4 example) |

### Names to confirm for your environment

Member and cube names can vary. Before loading `data-training-jan.csv`, confirm and, if needed, edit these:

| Token in the file | What it should be | How to confirm |
| --- | --- | --- |
| `Jan` | Your Period dimension's January member label | **Application &rarr; Overview &rarr; Dimensions &rarr; Period** |
| `FY24` | Your Years dimension member for fiscal year 2024 (Lab 2 recommends a 2024&ndash;2025 calendar) | Open the **Years** dimension |
| `PCM_Input` | The **PCM_Balance** member that holds loaded input data | Open the **PCM_Balance** dimension |
| `PCM_No Rule` | The **PCM_Rule** member for data that was not produced by a rule | Open the **PCM_Rule** dimension |
| `PCM_CLC` | The **calculation** cube name | **Application &rarr; Overview &rarr; Dimensions**, check the **Cube** list |

This file assumes a **single‑currency** application (no Currency member in the point of view). If you chose multicurrency in Lab 2, add the currency member to each `Point-of-View` value.

**Most reliable check:** enter a few numbers on a form in your new application, then use **Application &rarr; Overview &rarr; Actions &rarr; Export Data** and open the exported file. It shows the exact header row, point‑of‑view order, and cube name for your application. Match `data-training-jan.csv` to it.

## Expected result after Lab 4

With the sequence **custom rule (10) then allocation rule (20)**:

* `Utilities Expense` at `SVC-1`: input 30000, plus a 3000 adjustment = **33000** net.
* Total moved from the service centres = 120000 + 90000 + 33000 = **243000**.
* Split to operating centres by `Headcount` (20 / 50 / 30 of 100): `OPS-1` = 48600, `OPS-2` = 121500, `OPS-3` = 72900.
* `Service Centers` net balance for the three expense accounts returns to **0** (the offset).

If you accidentally run the allocation before the adjustment, the operating centres total **240000** instead of 243000 &mdash; which is the point of the sequence.

## Troubleshooting

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Metadata import shows **Failed** | The `Parent` member does not exist yet, or a header column name is mistyped | Open the failed job to see the row and column. Load files in the order above; check that `All Accounts` and `Total Entity` exist (they are seeded). |
| `activity-metadata.csv` fails | The **Activity** custom dimension has not been created | Create it (Lab 3, Task 2), enable it on the cube, then import. |
| Data import shows **Failed** or **0 cells loaded** | A point‑of‑view member name or the cube name does not match your application | Use the "Names to confirm" table; export a data slice to see the exact names. |
| Data import rejects rows | A value has a thousands separator, quotes, or more than one decimal point | Values must be plain numbers (the supplied file already is). |
| Calculation result is `#MISSING` | Data loaded to the wrong cube or point of view | Re‑check `Data Load Cube Name` and the point of view, reload, recalculate. |

## Note for the workshop author

The metadata files use the documented EPCM metadata format and attach only to seeded members (`All Accounts`, `Total Entity`) or to members the files create in order. The **data file's** system members (`PCM_Input`, `PCM_No Rule`) and cube name (`PCM_CLC`) follow Oracle's documented naming but should be verified once against a real preconfigured EPCM environment and adjusted here if needed. Run the full load‑and‑calculate flow once before publishing and confirm the 243000 result.
