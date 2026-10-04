<p align="center">
  <img src="https://img.icons8.com/fluency/96/concert.png" alt="Pulse University Logo" width="96"/>
</p>

<h1 align="center">Pulse University — Concert Festival Database</h1>
<h3 align="center"><em>A relational database system for managing an international music festival</em></h3>

<p align="center">
  <img src="https://img.shields.io/badge/Database-MariaDB-003545?logo=mariadb" alt="MariaDB"/>
  <img src="https://img.shields.io/badge/Server-XAMPP-FB7A24?logo=xampp" alt="XAMPP"/>
  <img src="https://img.shields.io/badge/Tool-MySQL%20Workbench-4479A1?logo=mysql&logoColor=white" alt="MySQL Workbench"/>
  <img src="https://img.shields.io/badge/Scripting-Python-3776AB?logo=python&logoColor=white" alt="Python"/>
</p>

---

## 📖 About

**Pulse University** is a fictional international music festival that takes place annually at different locations around the world. This project designs and implements a full relational database to manage every aspect of the festival — from venues, events, and artist performances to electronic ticketing, an automated FIFO resale queue, and audience ratings.

The database spans **10 festival editions** (including 2 future ones), enforcing real-world business rules through **constraints, triggers, and stored procedures** written entirely in SQL.

---

## ✨ Highlights

| Aspect | Details |
|---|---|
| 🏟️ **21 Tables** | Covering festivals, locations, stages, events, performances, artists, bands, genres, staff, tickets, resale queues, ratings, and images |
| ⚙️ **10 Triggers** | Enforce break-time gaps, VIP caps, capacity limits, duplicate-ticket checks, simultaneous-performance conflicts, consecutive-year artist limits, staffing ratios, automated resale processing, and rating validity |
| 📊 **15 SQL Queries** | Revenue analytics, artist participation, warm-up counts, rating averages, young artist rankings, staff utilisation, continent coverage, genre pair analysis, and more |
| 🐍 **Data Generator** | Python script using `Faker` to populate the database with realistic, randomised data |
| 📐 **Full ER & Relational Diagrams** | Visual documentation of the complete database design |

---

## 🗃️ Database Schema Overview

The database is organized around these core entity groups:

### Festival & Venues
- **Location** — address, GPS coordinates, city, country, continent
- **Festival** — annual festival instances linked to locations
- **Stage** — venues with capacity limits and technical equipment specs

### Artists & Performances
- **Artist / Band** — solo artists and bands with genres, sub-genres, websites, social profiles
- **Genre** — music genres and sub-genres (many-to-many with artists/bands)
- **Event** — scheduled shows at specific stages (max 12 h)
- **Performance** — individual artist appearances within events (warm-up, headline, special guest, etc.)

### Ticketing & Resale
- **Visitor** — ticket holders with personal details
- **Ticket** — electronic tickets with EAN-13 codes, categories (General, VIP, Backstage), and activation tracking
- **ResaleBuyerQueue / ResaleSellerQueue** — FIFO-based automated resale system

### Staff & Operations
- **Staff** — technical, security, and support personnel with experience levels
- **StaffAssignment** — staff-to-event assignments respecting minimum ratios (5 % security, 2 % support)

### Ratings & Media
- **Rating** — Likert-scale evaluations across 5 criteria (interpretation, sound & lighting, stage presence, organisation, overall impression)
- **EntityImage** — polymorphic image storage for all entities

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| [MariaDB](https://mariadb.org/) | 10.4.32 | Relational database engine |
| [XAMPP](https://www.apachefriends.org/) | 8.0.30 | Local development server |
| [MySQL Workbench](https://www.mysql.com/products/workbench/) | 8.0.42 | Schema design & query editor |
| [Python](https://www.python.org/) | 3.13.3 | Data generation scripting |
| [Faker](https://faker.readthedocs.io/) | — | Realistic test data generation |

---

## 📁 Repository Structure

```
concerts-database/
├── sql/
│   ├── install.sql              # DDL — tables, indexes, triggers, constraints
│   ├── load.sql                 # DML — data population & stored procedures
│   └── queries/
│       ├── Q01.sql … Q15.sql    # 15 SQL queries
│       ├── Q01_out.txt … Q15_out.txt  # Query result outputs
│       ├── Q04_traces.txt       # Query plan traces for Q04
│       └── Q06_traces.txt       # Query plan traces for Q06
├── diagrams/
│   ├── er.pdf                   # Entity-Relationship diagram
│   └── relational.pdf           # Relational schema diagram
├── code/
│   └── fake_data.py             # Python data generator script
├── docs/
│   └── report.pdf               # Full project report with documentation
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- [XAMPP](https://www.apachefriends.org/) with MariaDB, **or** a standalone MariaDB / MySQL server
- [MySQL Workbench](https://www.mysql.com/products/workbench/) (optional, for visual query editing)
- [Python 3.x](https://www.python.org/) (only needed to regenerate test data)

### Installation

```bash
# Clone the repository
git clone https://github.com/GregoryStam04/CONCERTS-DATA-BASE.git
cd CONCERTS-DATA-BASE

# Start your MariaDB/MySQL server, then run:
mysql -u root -p < sql/install.sql
mysql -u root -p pulse_university < sql/load.sql
```

### Running Queries

Each query is a standalone `.sql` file. Execute any of them against the `pulse_university` database:

```bash
mysql -u root -p pulse_university < sql/queries/Q01.sql
```

Or open them in MySQL Workbench and run interactively.

### Regenerating Test Data (Optional)

```bash
pip install faker
python code/fake_data.py
```

---

## 📊 Query Catalogue

| # | Description |
|---|---|
| Q01 | Festival revenue per year, broken down by payment method |
| Q02 | Artists of a given genre with festival participation status for a given year |
| Q03 | Artists who performed as warm-up more than 2 times in the same festival |
| Q04 | Average ratings (interpretation & overall impression) for a given artist — *includes query plan analysis* |
| Q05 | Young artists (age < 30) with the most festival participations |
| Q06 | Events attended by a given visitor with their average rating per event — *includes query plan analysis* |
| Q07 | Festival with the lowest average technical staff experience |
| Q08 | Support staff with no assignments on a given date |
| Q09 | Visitors who attended the same number of events within a year (min. 3 attendances) |
| Q10 | Top-3 genre pairs most common among artists who performed at festivals |
| Q11 | Artists with at least 5 fewer participations than the most-participating artist |
| Q12 | Required staff per festival day, broken down by category (technical, security, support) |
| Q13 | Artists who have participated in festivals across at least 3 different continents |
| Q14 | Genres with the same number of performances in two consecutive years (min. 3 per year) |
| Q15 | Top-5 visitors who gave the highest total rating to a single artist |

> **Note:** Queries Q04 and Q06 include alternative query plans with forced indexes, optimizer traces, and comparative analysis — see `Q04_traces.txt` and `Q06_traces.txt`.

---

## 🔐 Key Business Rules Enforced

The database enforces the following business constraints through triggers and checks:

- **Break times** — Mandatory 5–30 min breaks between consecutive performances
- **VIP ticket cap** — VIP tickets limited to 10 % of each stage's capacity
- **Capacity enforcement** — Ticket sales cannot exceed stage capacity
- **No duplicate tickets** — One ticket per visitor per event per day
- **No simultaneous appearances** — An artist cannot perform on two stages at the same time
- **Consecutive year limit** — An artist cannot participate for more than 3 consecutive years
- **Staffing ratios** — Security ≥ 5 % and support staff ≥ 2 % of audience capacity
- **Automated resale** — FIFO-based ticket resale queue with automatic matching
- **Rating validity** — Only holders of activated (used) tickets can rate performances

---

## 👥 Team — Group Members

| Name | GitHub |
|---|---|
| Nikolaos Dionysios Fragkos | [@nikolasfragkos](https://github.com/nikolasfragkos) |
| Georgios Pallis | [@gepall-bot](https://github.com/gepall-bot) |
| Grigorios Stamatopoulos | [@GregoryStam04](https://github.com/GregoryStam04) |

---

## 🎓 Academic Context

This project was developed as the semester project for the **Databases** course (6th Semester, Academic Year 2024–2025) at the **School of Electrical and Computer Engineering (ECE)**, **National Technical University of Athens (NTUA)**.

Supervised by the **Knowledge and Database Systems Laboratory (KDBS Lab)**.