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

- `screenshots/`, admin dashboard, a charting page, a sample exported PDF




- `app.py` — Flask entry point: configuration, auth routes, patient/chart
  routes, image uploads, the instructor admin panel (Flask-Admin), and the
  `init-db` / `migrate` CLI commands.
- `models.py` — Database tables as SQLAlchemy classes:
  - `User` — anyone who logs in (`student` or `instructor`), with an optional
    profile picture.
  - `Patient` — one simulated patient (demographics + medical history).
  - `Vital` — one set of vital signs.
  - `Note` — a timestamped record; the `kind` field covers notes, imaging,
    consults, and orders in one table.
  - `MedOrder` — a medication order (MAR).
  - `MedAdmin` — a student's own scan state for a medication order.
  - `HistoryReview` — a student's own tick state for the history checklist.
  - `ChartEntry` — one entry for the data-driven chart tabs (neuro,
    respiratory, etc.); the tab is named by `section`.
  - `patient_student` — link table for the many-to-many patient assignment.
- `chart_sections.py` — Defines every chart tab and its form fields in one
  place; the routes and templates loop over this.
- `seed.py` — Wipes the database and inserts demo users and patients.
  Re-runnable.
- `gunicorn.conf.py` — Production server settings (worker and thread counts).

**Templates** (`templates/`, Jinja2)

- `base.html` — Shared page layout (header with profile picture, flash
  messages).
- `login.html` — Sign-in form.
- `patients.html` — Patient list (home page after login).
- `patient.html` — Redirects to the first chart tab.
- `chart.html` — The tabbed patient chart; includes the partials below.
- `profile.html` — Upload a profile picture.
- `_vitals.html`, `_notes.html`, `_mar.html`, `_history.html`,
  `_section_chart.html`, `_fields.html`, `_patient_form.html` — Reusable
  pieces of the chart (one per section type).
- `_*_refs.html` — Reference images and scales shown beside certain tabs
  (Braden, falls, neuro, GI, ADLs, psychosocial).
- `admin/` — Admin panel pages: `index.html` (landing) and
  `confirm_create.html` / `confirm_edit.html` (save-confirmation wrappers).

**Static** (`static/`)

- `style.css` — All styling (no framework).
- `admin_picker.css`, `admin_picker.js` — The assign-students dropdown in the
  admin panel.
- `confirm_save.js` — The "confirm what you're saving" pop-up.
- `*.png` — Reference images (body figure, Braden scale, etc.) and the logo.
- `uploads/` — Uploaded images (imaging attachments and profile pictures).

---

## What I Learned

This was my first time taking a web application all the way from an empty repository to something people rely on weekly. The biggest lessons were in the parts that aren't the "happy path": enforcing security properly, handling real user data carefully, and designing an admin experience that a non-technical instructor can actually use. Coordinating directly with faculty taught me that the requirements you're given are a starting point, not the finish line.
