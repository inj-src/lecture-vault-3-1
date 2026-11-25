---
course: "CSE 3101 – Database Systems (DBS)"
class: "DBS - 3"
duration: "41:27"
---
# DBS - 3 – File Processing Drawbacks vs. DBMS, Data Models & Relational Model Basics

## Overview
This lecture concludes the introductory comparison between traditional File Processing Systems and Database Management Systems (DBMS) from Chapter 1, and transitions into Chapter 2 by introducing Data Models and the Relational Model. Building on the previously covered issues of data redundancy and atomicity, the teacher examines five more problems with file systems (isolation, integrity, security, data accessing, and durability) and then defines the foundational building blocks of a relational database: *Relation*, *Attribute*, and *Tuple*.

## Topic Map
- **Class Logistics & Recap**
  - Period-sharing schedule with co-teacher
  - Recap of DBMS advantages: Data Redundancy (& Inconsistency) and Atomicity
- **Drawbacks of File Processing Systems (Continued)**
  - Data Isolation (multiple files, mismatched formats, lack of inherent structure)
  - Data Integrity (validation constraints vs. manual error handling)
  - Security (lack of granular/partial file access and role-based authorization)
  - Data Accessing (ad-hoc querying across multiple files without repeated programmer effort)
  - Durability (survival against hardware/physical failures and automatic state recovery)
- **Course Approach & Transition**
  - Textbook approach (Silberschatz used loosely as topic reference)
  - Moving from Chapter 1 (course overview) to Chapter 2
- **Data Models**
  - Relational Model (most common; tabular)
  - ER Model (design/visualization)
  - Object-Oriented Model & Semi-Structured Model
- **Introduction to the Relational Model**
  - Relational database as a collection of uniquely named tables
  - Core terminology: **Relation** (table), **Attribute** (column), **Tuple** (row)

## Detailed Notes

### 1. Recap: Redundancy & Atomicity
- **DBMS** stands for **Database Management System**.
- **Data Redundancy & Inconsistency:**
  - In a file processing system, the same data may be duplicated across one or multiple files (*redundant data*).
  - Redundancy increases storage and access costs and creates **data inconsistency**: when data is inserted, deleted, or modified, updates may happen in some files and be missed in others.
  - *Example:* A person having two NID numbers (a Smart NID and an older non-smart NID), causing ambiguity about which record to use (resolved later only by integrating/redirecting between them).
  - A DBMS provides multiple built-in mechanisms to prevent and manage different types of redundancy (covered later in the course).
- **Atomicity Problem:**
  - Any logical unit of work must happen **completely or not at all** (*all-or-nothing*, i.e., no partial completion where half the task succeeds and half fails).
  - File processing systems cannot natively guarantee atomicity; a DBMS handles it easily using simple keywords and small internal log/auxiliary files because the system is engineered around it.

---

### 2. Data Isolation (File & Format Isolation)
- *(Note: The teacher clarifies this is distinct from the transaction "Isolation" property covered later in the course, though the pandemic popularized the general term.)*
- In a large or long-running software project:
  - Different teams build different features over time, and later versions add more features, creating **multiple separate files**.
  - Because there is no single unified platform or upfront global plan, different programmers store the same kind of data in **incompatible formats** (e.g., one stores mobile numbers as `string`, another as `integer`; different `date` or `datetime` formats).
  - Even within a single file, stored values have no inherent structural relationship unless the programmer explicitly writes code (such as matrices, vectors, or index-based lookups) to parse and link them.
- **Consequence:** Each file sits in isolation, making it very difficult for application programmers to combine and process data across files. A uniform, well-structured format in a DBMS eliminates this friction.

---

### 3. Data Integrity Problem
- **Integrity** (*শুদ্ধতা* — correctness/validity of data) ensures that stored data satisfies domain and structural rules.
- **Worked Example (University Admission Form):**
  - Suppose a new incoming batch (e.g., the `26` batch, admission test in late January) submits student info (name, father's name, mother's name, mobile, email, department) via an online web form instead of paper forms.
  - Without validation, an excited student accidentally enters `"CS"` or `"CSEeee"` in the department text field instead of `"CSE"`.
  - Later, someone urgently needs the **Department Head's contact number** for that student. Resolving it requires linking three separate files:
    $$\text{Student File} \xrightarrow{\text{dept name}} \text{Department File} \xrightarrow{\text{head ID}} \text{Faculty File}$$
    - *Student File:* name, mobile, email, department name.
    - *Department File:* department name, short name, official contact, rooms, budget.
    - *Faculty File:* name, ID, mobile, email.
  - Because `"CS"` / `"CSEeee"` matches no valid department, the student's department and Head cannot be found.
- **File System vs. DBMS:**
  - In a file system, programmers must anticipate edge cases and write many lines of custom validation code manually whenever new cases arise.
  - A **DBMS** provides built-in **integrity constraints** that automatically reject operations violating validity rules—often using just short keywords or simple conditions rather than large blocks of code.

---

### 4. Security Problem (Authorization & Partial Access)
- File processing systems struggle to enforce **partial access** within a single file (e.g., letting a user view or edit only specific parts of a file while hiding confidential fields).
- **Worked Examples:**
  - **Healthcare / Diagnostic Center (e.g., Popular):** A patient's confidential medical history should only be visible to the doctor—not to application programmers, lab/pathology operators, or general staff.
  - **University Examination System:** Users and programmers must not be allowed to see confidential records such as which teachers moderated exam questions or who typed them.
- **File System vs. DBMS:**
  - In a file system, securing data requires predicting all confidentiality boundaries upfront, splitting fields into separate files, and manually coding read vs. edit permissions.
  - In a **DBMS**, the administrator can define distinct user accounts, grant granular **authorization** (e.g., view-only vs. edit), and expose dynamically filtered subsets of columns (views) without exposing the underlying sensitive columns.

---

### 5. Data Accessing Problems
- Beyond storing data, retrieving data under new, unforeseen conditions (**ad-hoc querying**) is very hard in a file processing system.
- **Worked Example (Kazla Crime Investigation):**
  - Suppose a crime occurs in the Kazla area, and newspapers report that a few students are preliminarily suspected.
  - *Query 1:* Police (Motihar Thana) want a list of all students in Rajshahi (filtering out non-students, while still including students of any institution such as RMC). In a file system, they must hire/ask the programmer to write filter code over the files.
  - *Query 2:* Further investigation reveals the suspects live in or around Kazla. Police now need that student list filtered by current address (Kazla), requiring another file join (personal info + address/academic files). Again, they must call and pay the programmer!
  - *Query 3:* Further investigation narrows it down to **3rd-year students** living around Kazla. Once again, they have to go back to the programmer!
  - Because relying on programmers for every new filter is slow and costly, investigators often resort to printing massive call lists/records and highlighting entries manually with markers—unless an extremely general, scalable search interface was built upfront (which is hard to make efficient across all fields).
- **DBMS Advantage:** A DBMS provides a built-in query interface where users can directly request arbitrary filters and join across multiple tables on the fly without writing custom file-parsing programs each time.

---

### 6. Durability Problem
- **Durability** (*স্থায়িত্ব* — permanence of data) means that once an operation/transaction completes and is committed, its data will not be lost even if the system fails.
- **Worked Example (Semester Result Fire):**
  - Suppose semester results come out poorly, and students wish the room/server in the Department Head's office holding all results and exam scripts would catch fire and crash—and it actually catches fire, destroying the physical machine and scripts. All data in a local file system is permanently lost.
  - Even if files are synced to external cloud storage (e.g., Google Drive, Dropbox), file-level sync does not automatically maintain transaction-level state or let you cleanly roll back to an exact prior version.
- **DBMS Advantage:** Durability is a core built-in property of a DBMS. Even if a crash or failure occurs immediately after data is committed, the DBMS uses automatic backups/logs and recovery mechanisms (covered near the end of the course) to ensure committed data survives.

---

### 7. Data Models
- A **Data Model** defines how data is organized and structured inside a database.
- Common Data Models mentioned:
  1. **Relational Model:** The most widely used and popular model; represents data in **tabular format** (tables with rows and columns).
  2. **ER (Entity-Relationship) Model:** Primarily used for *designing* and modeling databases rather than direct storage.
  3. **Object-Oriented Model**
  4. **Semi-Structured Model** (for data that does not conform to a rigid schema)

---

### 8. Introduction to the Relational Model
- In a **Relational Database**, the database is simply a **collection of tables**, where each table stores a distinct category of entities sharing the same attributes.
  - Every table must have a **unique name** so it can be referenced unambiguously.
  - Different entity types belong in separate tables (e.g., you would not store Department records in a Student table because Departments do not have attributes like father's name or mother's name).
- **Worked Example Tables:**
  - `Movie` table:

| movie_id | movie_name | release_year | genre | imdb_rating |
| :--- | :--- | :--- | :--- | :--- |
| *(unique ID)* | 3 Idiots | 2009 | Drama | 8.4 |
| *(unique ID)* | Hirak Rajar Deshe | 1980 | Drama | 8.7 |

  - `Director` table: columns such as `director_id`, `name`, `birth_year`, `movie_count`.
  - *(Side note: IMDb stands for **Internet Movie Database**, which itself relies on a massive, well-organized database that the class will examine later in the semester.)*
- **Three Fundamental Terms:**
  1. **Relation** (= **Table**):
     - In relational database terminology, *relation* refers to a **table** (not a personal relationship).
     - Why "relation"? Because values across a row are mathematically related to one another (অন্বয় / সম্পর্ক)—for example, *3 Idiots* is related to `2009`, `Drama`, and `8.4`; *Hirak Rajar Deshe* is related to `1980`, `Drama`, and `8.7`.
  2. **Attribute** (= **Column**):
     - Each column header represents a feature or property of the entity being modeled (e.g., `movie_id`, `movie_name`, `release_year`, `genre`, `imdb_rating`).
  3. **Tuple** (= **Row**):
     - Each row represents a single complete entity instance—combining all attributes together to uniquely identify and describe one item (since a single attribute like `movie_name` alone may not be unique across different movies).

## Exam / Important Points
- **Do not rote-memorize** every Chapter 1 file-system drawback list right now; they will become intuitive naturally as later chapters (constraints, authorization, queries, transactions/durability) are covered.
- **Must remember:** **Data Redundancy** is the single most important drawback to keep in mind from the file-system comparison, as it directly drives **data inconsistency**.
- **Terminology precision:** In DBMS/Relational Model, **Relation = Table**, **Attribute = Column**, and **Tuple = Row**. Also remember that every relation (table) must have a **unique name**.
- **Data Integrity** (শুদ্ধতা) and **Durability** (স্থায়িত্ব) are core DBMS guarantees handled via built-in constraints and recovery mechanisms rather than ad-hoc application code.

## Announcements & Logistics
- **Period Schedule:** Until the 7th (date referenced in class), the teacher takes 2 periods and the co-teacher ("Madam") takes 1 (splitting consecutive periods 1–1); after the 7th, Madam will take 2 periods and the teacher will take 1 (continuing the morning period through the end of the term).
- **Course Resources ("CSE Connect"):** The teacher asked whether all students have been added to CSE Connect and stated he will upload course resources there within the week once he receives access.
- **Textbook Reference:** The course loosely follows Silberschatz (*Database System Concepts*) for topic ordering, though lectures use custom explanations and examples rather than going line-by-line or page-by-page. Next class will continue directly from `Relation`, `Attribute`, and `Tuple`.

## Open Questions / Unclear Parts
- `00:05–00:35`: When explaining the period swap around "the 7th" (*সাত তারিখ*), the specific month and exact room/slot numbers are not stated aloud.
- `37:30–39:05`: The teacher writes exact sample `movie_id` values on the chalkboard for *3 Idiots* and *Hirak Rajar Deshe* without reading those ID numbers aloud.
- `41:20–41:27`: Brief student remark right at dismissal is faint/unclear (related to wrapping up the class).
