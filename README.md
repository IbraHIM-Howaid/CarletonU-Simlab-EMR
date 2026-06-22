# CarletonU-Simlab-EMR

# Carleton Manor EMR

A full-stack clinical Electronic Medical Record (EMR) web application built for Carleton University's nursing simulation lab, where nursing students practice charting on simulated patients and instructors oversee their work.

> **Note:** This is a case-study repository. The application source code is kept private at the request of the project stakeholders, so this repo documents the work, design, and outcomes rather than hosting the code. A live demo is available on request.

**Live project:** in active use at Carleton University's nursing simulation lab

**Portfolio:** [al-howaid.me](https://al-howaid.me)

---

## Tech Stack

| Layer | Tools |
|-------|-------|
| Backend | Python, Flask |
| Database | PostgreSQL, SQLAlchemy (ORM) |
| Admin / Auth | Flask-Admin, Flask-Login, Flask-WTF (CSRF) |
| PDF Engine | ReportLab |
| Frontend | JavaScript, HTML/CSS, Jinja2 templates |
| Tooling | Git/GitHub, VS Code |

---

## STAR Write-Up

**Situation.** Carleton University's nursing simulation lab needed an electronic medical record system where students could practice charting on simulated patients, but had no purpose-built tool for it.

**Task.** Build a full-stack web application that lets students chart across realistic assessment sections while giving instructors oversight of student work, all secure, reliable, and usable in an active classroom.

**Action.** I built the app in Python and Flask backed by a PostgreSQL database. I implemented role-based access control, CSRF protection, and session authentication, then developed an instructor admin panel with real-time student activity tracking and a bulk PDF chart-export feature. I engineered a multi-page PDF generation engine that renders full patient assessments from live charting data, and coordinated with faculty to match course requirements, running ongoing testing and QA.

**Result.** A working EMR now used by Carleton nursing students and instructors in an active university environment.

---

## Key Features

- **24 charting sections** covering a full nursing assessment (vitals, neuro, cardiovascular, respiratory, GI/GU, MAR, wounds, and more)
- **Role-based access control** separating student and instructor permissions
- **Security**: CSRF protection on every form, session-based authentication, hashed credentials
- **Instructor dashboard** with real-time student activity, online status, and per-student charting stats
- **Bulk PDF export**: download every assigned patient's chart as a structured ZIP (student to patient to PDF)
- **Multi-page PDF engine** rendering complete assessment reports from live data, with per-page footers stamping who charted and who exported each record

---

## Behind the Scenes

*(Add these assets to this folder to document your process.)*

- `screenshots/`, admin dashboard, a charting page, a sample exported PDF
- `schema/`, entity diagram of the data model (patients, vitals, notes, users, chart entries)
- Notes on the 24-section chart structure and how PDF generation maps to it

---

## What I Learned

This was my first time taking a web application all the way from an empty repository to something people rely on weekly. The biggest lessons were in the parts that aren't the "happy path": enforcing security properly, handling real user data carefully, and designing an admin experience that a non-technical instructor can actually use. Coordinating directly with faculty taught me that the requirements you're given are a starting point, not the finish line.
