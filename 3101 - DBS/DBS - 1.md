---
course: "CSE 3101 – Database Systems (DBS)"
class: "DBS - 1"
duration: "41:41"
---
# DBS - 1 – Course Introduction, Purpose of Databases, File Processing Limitations, and Atomicity

## Overview
This was the opening lecture of **CSE 3101 (Database Systems)**, introducing the course structure, teaching split, and foundational motivation for database systems. The teacher defined what a database is, walked through real-world large-scale use cases, and contrasted modern databases with traditional file processing systems by highlighting **data redundancy**, **data inconsistency**, and **atomicity** failures.

## Topic Map
- Course & Class Format Introduction
  - Course code convention (`CSE 3101`) and course title
  - Two-instructor period-wise split across the semester
  - High-level view of OBE / Program Outcomes (12 POs as 12 skills)
- What is a Database?
  - Literal vs. technical definition (collection of interrelated data)
  - Core goals: organized storage and efficient retrieval/searching/modification
- Real-World Applications & Scale
  - Why small student projects hide database problems
  - Examples: University (RUET) records, railway ticketing, mobile/SIM billing, banking
- Why Do We Need a Database? (Limitations of File Processing Systems)
  - How file processing works (files + application code)
  - Problem 1: Data Redundancy & Data Inconsistency
    - Causes of multiple copies (multiple developers/teams, different offices, repeated form submissions)
    - Consequences: storage cost, access cost, and data inconsistency
  - Problem 2: Lack of Atomicity
    - Analogy from chemistry (indivisible unit)
    - Worked example: bank transfer between Abul and Bulbul + ATM analogy
    - "All or nothing" rule
- Course Goal, Reference Book & Logistics
  - Ultimate goal of CSE 3101
  - Textbook & CSE Connect platform
  - Attendance roll call

## Detailed Notes

### 1. Course Introduction & Teaching Format
- **Course Code Breakdown (`CSE 3101`):**
  - From 3rd year 1st semester onward, all departmental courses carry the `CSE` prefix.
  - `3` = 3rd year, `1` = 1st semester, `01` = course number.
- **Course Title:** Database Systems (note: the teacher mentioned the exact title or contents can occasionally be adjusted under the OBE curriculum).
- **Two-Teacher Split:**
  - The course is shared between the teacher and a co-instructor, split **period-wise** rather than dividing the first half and second half of the semester:
    - **First 7 cycles (before mid-semester break):** the teacher takes 2 periods/week, and the co-instructor takes 1 period/week.
    - **Next 7 cycles (after mid-semester break):** the co-instructor takes 2 periods/week, and the teacher takes 1 period/week.
    - **Today's class:** 1st period by the teacher, 2nd period by the co-instructor.
  - **Reasoning:** A continuous 100-minute lecture by one instructor gets too heavy and students lose focus; alternating instructors on independent topics keeps each ~45–50 minute period fresher.
- **Perspective on OBE & POs:**
  - Rather than memorizing Program Outcomes (POs) upfront, the teacher explained that the 12 POs simply represent **12 graduate skills** (e.g., teamwork, communication, analytical skill) that a single CGPA number does not reflect on its own.
  - Different courses map to different skills; students will naturally connect the course content to those skills as the semester progresses.

### 2. What is a Database?
- **Informal wordplay:** A "base" with "data" stored on top of it (acknowledged as a crude memory hook).
- **Narrow definition:** A collection of data.
- **Better definition:** A **collection of interrelated data** (where relationships either already exist among the data items or are explicitly established).
- **Core Purpose of a Database:**
  1. **Store data in an organized way.**
  2. **Retrieve (fetch), search, and modify** that data efficiently.
- **Teacher's Analogy (Messy Student Room):**
  - If you toss a pen somewhere in an unorganized room (like leaving treasure-hunt clues and then losing the map), you might not need it all year—until right before an exam, when you have to tear the whole room apart to find it. Keeping items in a defined structure/format makes retrieval easy later.

### 3. Real-World Applications & Why Scale Matters
- **Why small academic projects give a false sense of security:**
  - In student course projects, the student acts as developer, client, requirement writer, tester, and polite data-entry user—usually inserting 10–12 (or at most ~100) clean records just for a demo.
  - Real-world systems face rough/unpredictable user input and **massive scale** (millions or billions of records), which is where real data-management problems emerge.
- **Examples Covered in Class:**
  1. **University (RUET) Records:**
     - Admission info (name, father's name, address, certificates) and semester-by-semester academic marks (Part A, Part B, CTs, assignments, lab marks, board viva, quizzes) across ~9–10 theory + lab courses per semester, ~60 students × 3 sections per batch, preserved since the CSE department's 1998 batch.
  2. **Railway / Train Ticketing (e.g., Eid rush):**
     - Trains, bogies/compartments, seats, who reserved each seat, user profiles (mobile number, NID), and enforcing uniqueness so one NID or mobile number cannot open multiple accounts.
  3. **Telecom / Mobile Operators:**
     - Multiple SIMs registered per person/NID for different call packages, call logs (caller, callee, duration), and balance/minute deductions.
  4. **Banking (e.g., Rupali Bank for semester registration fees):**
     - Accounts, account types (current vs. savings), current balance, and transaction logs (date/time, amount debited/credited, remaining balance).

### 4. File Processing System & Problem 1: Data Redundancy and Inconsistency
- **File Processing System (Pre-Database Approach):**
  - Familiar from C programming: storing data in plain files and writing application code (lines of code with file open, file pointers, read, write, modify, append) to manage them.
  - Consists of two parts: **files** + **application programs**.
- **Problem 1: Data Redundancy** (multiple copies of the same data).
  - **How multiple copies arise:**
    - Large software systems are built over a long time by multiple developers/teams creating different files with different formats.
    - *University example:* A student's personal data is collected separately by the Academic Section (*শিক্ষা শাখা*), DSW office (for ID cards), Course Advisor (sometimes re-collected when an advisor or staff role changes), and the CSE department.
    - *Google Form example:* Submitting a form, forgetting whether you submitted it, and submitting again—creating duplicate rows in the same file.
  - **Consequences of Redundancy:**
    1. **Higher Storage Cost:** Wasted space from duplicate data.
    2. **Higher Access Cost:** Searching through e.g. 180 records instead of 60 takes more time and resources.
    3. **Data Inconsistency (The Most Severe Problem):**
       - When one copy changes (e.g., you change your phone number), **all** copies must be updated. If some copies are missed, the copies disagree.
       - *Real-world impact:* DSW tries to call you about a scholarship using an outdated number, fails to reach you, and gives it to someone else; or your old recycled number is reassigned to someone else and later tied to a crime.
       - At millions/billions of records, tracking down inconsistencies manually is practically impossible.
  - **How Databases Help:** Databases provide built-in mechanisms (sometimes as simple as a keyword/constraint) to prevent duplicate entries and manage redundancy cleanly without writing heavy custom file-handling code.

### 5. Problem 2: Atomicity
- **Concept & Analogy:**
  - Derived from **atom**—like in chemistry where molecules break into atoms during reactions and the atom acts as an indivisible unit.
  - In data operations, **Atomicity** means **"All or Nothing"**: a logical unit of work (transaction) must either execute **completely** or have **no effect at all**.
- **Worked Example (Money Transfer: Abul → Bulbul):**
  - Suppose **Abul** (A) has **7,000 taka** at the start of the month, and **Bulbul** (B) asks to borrow **10,000 taka**. After careful thought, Abul decides to transfer **$303$ taka** to Bulbul's account.
  - Even though this looks like one single transfer to the user, internally it involves multiple steps:
    1. Read Abul's current balance ($7{,}000$).
    2. Check account constraints (e.g., minimum balance of $500$ taka must remain after withdrawal).
    3. Deduct $303$ from Abul's balance ($7{,}000 - 303 = 6{,}697$) and write/update Abul's record. *(Note: the teacher initially wrote $7{,}303$ on the board by adding instead of subtracting before students pointed it out and he corrected it to subtraction.)*
    4. Read Bulbul's current balance.
    5. Add $303$ to Bulbul's balance and write/update Bulbul's record.
  - **Failure Scenario:** If a **power cut, network failure, or system crash** occurs right after step 3 (after Abul's account is debited, before step 5 completes), Abul loses $303$ taka while Bulbul never receives it.
  - **ATM Analogy:** Inserting your card at a bank booth, hearing the cash-counting *grrr* sound, receiving an SMS that money was deducted from your account, and then seeing *"Out of Service"* before any cash comes out.
  - **Role of Atomicity:** If any step fails mid-way, all prior steps in that transaction must be **undone** (rolled back) so the data returns to its original consistent state. Databases support atomicity natively (covered in depth later in the course), whereas enforcing it manually in file processing systems is very difficult.

### 6. Student Q&A: Ultimate Goal of the Course
- A student asked whether the ultimate goal of CSE 3101 is learning *how to use* a database or *how to create* one.
- **Teacher's Answer:** Neither just creating a database nor basic usage (which students already touched in earlier projects). The real goals are:
  - Learning **proper database design** and writing **efficient** operations/queries.
  - Knowing **which database approach/structure** to choose for a given scenario (structured, semi-structured, or unstructured data).
  - Understanding **how to organize/store data** and the **consequences/trade-offs** of each design choice.

## Exam / Important Points
- **Favorite / High-Value Course:** The teacher emphasized that CSE 3101 has outstanding, practical content—one of the best courses in the semester regardless of who teaches it.
- **Course Code & Title Recall:** Remember `CSE 3101` and the course title for CTs and semester final scripts (students frequently forget the exact course code in exam halls).
- **Two Major File-System Problems Highlighted Today:**
  1. **Data Redundancy → Data Inconsistency** (inconsistency is a much bigger problem than mere storage or access cost).
  2. **Atomicity ("All or Nothing")** — crucial for multi-step operations like bank transfers.
- **Applications Question Note:** Textbook/exam questions asking for "applications of databases" are easy/trivial—just pick any domain (university, banking, railway, telecom) and explain what data is stored and why.

## Announcements & Logistics
- **Course Material Platform:** All course materials (PDFs, slides, resources) will be shared on **CSE Connect** (not Google Classroom, per departmental faculty policy). Students must ensure they are registered on CSE Connect.
- **Reference Book:** A textbook by **Silberschatz** (note: *Database System Concepts* by Abraham Silberschatz et al.).
  - The teacher will share the **PDF** on CSE Connect.
  - Students who prefer hard copies can buy a used/second-hand copy from **Sonadighi Mor** (*সোনাদীঘির মোড়*).
- **Class Continuation:** The co-instructor will take the second period immediately following this class; the teacher will continue deeper properties of databases in the next class.
- **Attendance:** Taken at the end of the lecture (around `39:40`–`41:41`; the teacher also checked whether any students from other series were present).

## Open Questions / Unclear Parts
- `01:55` – `02:15` & `02:45` – `02:55`: Some background student murmurs/laughter when the teacher joked about teaching style and the split with the co-instructor.
- `39:40` – `41:41`: During the attendance roll call at the end, foreground chatter among nearby students (discussing CSE Connect, app/Android tooling, etc.) partially overlaps with the teacher calling roll numbers in the background.
