# Database Design & Data Warehousing

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](#license) [![Topic: SQL](https://img.shields.io/badge/Topic-SQL%20%26%20Modeling-blue)](#relational-foundations) [![Focus: Data Management](https://img.shields.io/badge/Focus-Data%20Management-orange)](#overview)


This file consolidates a set of **course discussion posts** on **database design and data warehousing** —
from relational fundamentals (keys, normalization, relationships) through dimensional modeling (star vs.
snowflake, fact-table types) and the operational-vs-analytical divide (SQL joins, OLTP vs. OLAP).

> Why this write-up?
> - Turn scattered database discussions into one cohesive reference.
> - Keep the worked examples (1NF fix, join analogy) that make the concepts stick.
> - Connect *design choices* to *business outcomes*.


## Table of Contents
- [Overview](#overview)
- [Relational Foundations](#relational-foundations)
  - [Primary vs. Foreign Keys](#primary-vs-foreign-keys)
  - [First Normal Form (1NF)](#first-normal-form-1nf)
  - [Table Relationships](#table-relationships)
- [Dimensional Modeling](#dimensional-modeling)
  - [Why Businesses Benefit](#why-businesses-benefit)
  - [Star vs. Snowflake Schema](#star-vs-snowflake-schema)
  - [Fact Tables: Additive, Semi-Additive, Non-Additive](#fact-tables-additive-semi-additive-non-additive)
- [Working with Data](#working-with-data)
  - [SQL Joins — The Wedding Guest List](#sql-joins--the-wedding-guest-list)
  - [OLTP vs. OLAP](#oltp-vs-olap)
- [Key Takeaways](#key-takeaways)
- [References](#references)
- [License](#license)


## Overview
Good analytics starts with well-designed data. These discussions move from the relational building blocks
that keep operational data clean, to the dimensional models that make that data easy to analyze, to the
system choices (OLTP vs. OLAP) that decide *where* each job belongs.


## Relational Foundations

### Primary vs. Foreign Keys
- **Primary key (PK)** — a column or set of columns that **uniquely identifies each record**. It cannot be
  duplicated or hold `NULL` values.
- **Foreign key (FK)** — a column in one table that **references the primary key of another table**,
  creating a relationship between the two and enforcing data consistency.

**Why it matters:** correct keys keep data organized, accurate, and consistent. Misused keys lead to
duplicate records, broken relationships, and unreliable information — making the database hard to manage
and trust.

### First Normal Form (1NF)
A small list of favorite movies started as a single table:

| MovieID (PK) | Title | Genres |
| --- | --- | --- |
| 1 | Inception | Action, Sci-Fi |
| 2 | Coco | Animation, Family |

The **`Genres`** column holds multiple values in one cell, violating 1NF — each field must hold a single
**atomic** value. The fix splits it into two tables:

**Movies**

| MovieID (PK) | Title |
| --- | --- |
| 1 | Inception |
| 2 | Coco |

**MovieGenres**

| MovieID (FK) | Genre |
| --- | --- |
| 1 | Action |
| 1 | Sci-Fi |
| 2 | Animation |
| 2 | Family |

Now each cell contains a single value and there are no repeating groups — **1NF satisfied**.

### Table Relationships
Tables relate in three primary ways:

- **One-to-one** — each record in one table maps to exactly one in another. *Example:* `Users` ↔
  `UserProfiles`, where each user has exactly one profile, joined by a unique `user_id`.
- **One-to-many** (most common) — one record links to many. *Example:* `Customers` → `Orders`; one
  customer places many orders, but each order belongs to one customer.
- **Many-to-many** — many records relate to many. *Example:* `Students` ↔ `Courses`; a student enrolls in
  many courses and each course has many students. Implemented with a **junction table** (`StudentCourses`)
  holding `student_id` and `course_id` as foreign keys.


## Dimensional Modeling

### Why Businesses Benefit
A key advantage of dimensional modeling is that it **simplifies complex data**, making it easier for
non-technical users to understand and analyze. By organizing data into **facts and dimensions**, the model
mirrors how employees naturally think about business activities — sales over time, customer behavior,
product performance. Analysts, managers, and frontline teams can run reports, slice data, and drill into
details without leaning heavily on IT (Kimball & Ross, 2013), so decision-making becomes faster and more
data-driven.

Operationally this improves workflow: marketing identifies high-value customer segments more easily,
finance monitors revenue trends more accurately, and executives gain clearer visibility into performance.
By lowering technical barriers, dimensional modeling lets more people engage directly with data — yielding
better insights, quicker reactions to market changes, and greater business agility (Inmon, 2005).

### Star vs. Snowflake Schema
A **snowflake schema** can beat a **star schema** when a company has **highly complex, hierarchical
dimensions** that benefit from deeper normalization.

*Example:* in a multinational retailer, the **Location** dimension spans country → region → state → city →
store. A star schema stores all of these in one large dimension table, inviting redundancy and
inconsistency. A snowflake schema **splits the hierarchy into related tables**, improving data integrity
and reducing storage costs (Kimball & Ross, 2013).

**Pitch to a decision-maker:** the snowflake design is **more scalable** for large organizations with
extensive product, customer, or geographic hierarchies. It introduces more complex joins, but delivers
cleaner data, easier maintenance, and faster updates when attributes change. For organizations prioritizing
**accuracy, governance, and long-term growth**, snowflake is the more robust, future-proof choice
(Inmon, 2005).

### Fact Tables: Additive, Semi-Additive, Non-Additive
Fact tables hold the quantitative **measures** organizations analyze. Measures fall into three types:

| Type | Can be summed across… | Examples | How to aggregate |
| --- | --- | --- | --- |
| **Additive** | **All** dimensions (time, product, geography) | Sales amount, quantity sold | Sum freely — supports trend analysis |
| **Semi-additive** | **Some** dimensions, **not time** | Inventory level, account balance | Point-in-time values → use average, max, or end-of-period |
| **Non-additive** | **No** dimensions | Ratios, percentages, unit prices | Recompute from underlying additive parts (e.g., revenue ÷ cost) |

Understanding these types ensures **accurate aggregations** and prevents incorrect business insights.


## Working with Data

### SQL Joins — The Wedding Guest List
Think of merging two wedding guest lists: the **Bride's list (Table A)** and the **Groom's list (Table B)**.

- **Inner Join (the mutual friends):** only people who appear on **both** lists. Know only the bride? You're
  not on this list.
- **Left Join (the bride's priority):** **everyone** on the bride's list. If a guest also knows the groom,
  that info is linked; if not, they're still listed with blank "Groom" info.
- **Full Outer Join (the big party):** **everyone** from both lists — mutual friends connected, plus
  bride-only and groom-only guests kept.

Joins tell the database exactly **which rows to keep** when combining tables.

### OLTP vs. OLAP
OLTP and OLAP serve different purposes; the right choice depends on the task.

| | **OLTP** (Online Transaction Processing) | **OLAP** (Online Analytical Processing) |
| --- | --- | --- |
| **Purpose** | Run daily operations | Analysis & decision support |
| **Workload** | Frequent inserts/updates/deletes, real-time transactions | Complex queries, aggregations, multidimensional analysis |
| **Strengths** | High performance, ACID consistency & reliability | Fast querying over large historical datasets |
| **Example** | E-commerce orders, payments, inventory updates | Retail sales-trend analysis, regional comparisons, demand forecasting |

**In short:** OLTP focuses on the **speed and accuracy of transactions**; OLAP provides the **insights** that
drive strategic, data-driven decisions.


## Key Takeaways
- **Keys are the contract:** PKs guarantee uniqueness, FKs enforce consistent relationships.
- **Normalize to atomic values** — 1NF eliminates multi-valued cells and repeating groups.
- **Model the relationship, not just the tables** — 1:1, 1:many, and many:many (via junction tables) each
  have a place.
- **Star vs. snowflake is a trade-off:** simplicity/fewer joins vs. integrity/scalability for deep hierarchies.
- **Know your fact type** before aggregating — summing a semi-additive or non-additive measure misleads.
- **Pick the right engine:** OLTP for operations, OLAP for analysis.


## References
- Kimball, R., & Ross, M. (2013). *The Data Warehouse Toolkit: The Definitive Guide to Dimensional Modeling* (3rd ed.). Wiley.
- Inmon, W. H. (2005). *Building the Data Warehouse* (4th ed.). Wiley.
- Kimball Group — *Dimensional Modeling Techniques.* https://www.kimballgroup.com/data-warehouse-business-intelligence-resources/kimball-techniques/


## License
This project is released under the **MIT License**. See `LICENSE` for details.
