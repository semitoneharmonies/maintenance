Landscaping Maintenance App — North Star
1. Purpose

The Landscaping Maintenance App is a mobile-first web application designed to:

Manage weekly crew scheduling

Capture on-site visit reports with timestamps and photos

Track total labor hours and man-hours per site

Generate professional, manager-approved client emails

Provide oversight without exposing sensitive contract data to crews

The app prioritizes:

Simplicity for field crews

Strong permission control

Clean client communication

Operational visibility for management

2. Core Roles & Permissions
2.1 Crew (No Login Required)

Access:

Schedule view only

Address

Crew roster for that day

Public manager notes

Access instructions (gate codes, parking info)

Restrictions:

Cannot see master site list

Cannot browse sites

Cannot view contracts, contacts, scope, or private notes

Cannot submit reports

Security:

Access requires a single 4-digit PIN

PIN is configurable by Manager

PIN can be rotated at any time

2.2 Crew Lead (Login Required)

Access:

Schedule view

Job details (address + crew-visible access notes)

Start/stop site timer

Submit visit reports

Upload photos

Restrictions:

Cannot access master site list

Cannot view contracts or site contacts

Cannot edit schedule

Cannot see manager-private notes

Capabilities:

Timer calculates total site duration

App calculates total man-hours:

Example:

3 workers on site

2 hours total

→ 6 total man-hours

Man-hour calculation:

Duration = (ended_at - started_at)

Worker count = number of assigned crew members for that assignment

total_man_hours = duration_hours × worker_count

2.3 Manager

Full operational control:

Create/edit sites

Create/edit crews and workers

Assign crew leads

Build schedule (drag-and-drop weekly grid)

Edit crew-visible notes

Edit private manager notes

View all reports

Edit submitted reports before client send

Generate AI email drafts

Edit AI email templates (default script)

Approve and send emails

View report history

Rotate 4-digit schedule PIN

Manager approval is required before any client email is sent.

2.4 Admin (Boss)

Access:

Read-only schedule view

Read-only reports & photos

Can edit master site list (contacts, contracts, scope)

Cannot modify schedule

Cannot alter reports

3. Scheduling System
Weekly Drag-and-Drop Builder (Manager Only)

Structure:

Columns = Days (Mon–Sun)

Rows = Crews

Cards = Site assignments

Card includes:

Site name

Address

Time window

Public manager note

Sort order (route order)

Manager can:

Drag between days

Drag between crews

Reorder within day

Edit assignment details

Mark assignment as “requires report”

Schedule drives reporting:

Reports can only be created from scheduled assignments

Crew leads cannot manually select arbitrary sites

4. Site Structure
4.1 Master Site List (Manager/Admin Only)

Fields:

Name

Address

Contract start/end

Scope of work

Site contacts

Manager-private notes

4.2 Crew-Visible Fields

Address

Crew-visible access notes:

Gate codes

Parking instructions

Entry details

Safety warnings

Crew leads and crews cannot see:

Contacts

Contract data

Scope details

Private manager notes

5. Visit Reporting System
Report is tied to:

One schedule assignment

One site

One crew

One crew lead

Crew Lead Workflow:

Open assigned job

Start timer

Complete work

Stop timer

Enter:

Work performed

Work in progress

Issues

Upload photos

Submit report

System automatically records:

Start timestamp

End timestamp

Duration

Worker count

Total man-hours

Reports are immutable to crew after submission.

Manager can edit before sending to client.

6. Photo Handling

Photos:

Uploaded to cloud object storage

Automatically deleted after 14 days using storage lifecycle rules

Metadata retained in database

Reports remain even after photos expire.

Optional future upgrade:

“Archive photo” override to prevent deletion

7. Client Email System
One Email Per Visit

Flow:

Crew lead submits report

System generates AI draft email

Draft appears in Manager dashboard

Manager:

Edits content

Can modify tone/template

Selects recipients (from site contacts)

Sends

AI is restricted to:

Rewriting only

No fabrication

Structured sections:

Work Completed

Work In Progress

Observations / Issues

Next Visit Plan

Manager can edit:

Default AI email script/template

Individual email drafts

Emails are logged with:

Timestamp

Recipients

Sent status

8. Timer & Man-Hour Calculation Logic

Timer records:

started_at

ended_at

Duration:

(ended_at - started_at)

Worker count:

Based on crew membership for that assignment date

Total Man-Hours:

duration_hours × worker_count

Man-hours are stored in report for analytics and billing insight.

9. Security Model

Crew schedule protected by 4-digit PIN

PIN stored hashed

Manager can rotate PIN at any time

Crew leads authenticated via login

Role-based API permissions strictly enforced

No site browsing allowed for crew roles

10. Technical Direction

Platform:

Mobile-first Web App (PWA)

React frontend

Node/Express backend

PostgreSQL database

Cloud object storage for photos

Email provider integration

OpenAI API for rewrite-only email generation

Timezone:

America/Vancouver

All timestamps stored in UTC, displayed in Vancouver time.

11. Non-Negotiable Principles

Crews see only what they need to do the job.

Client communication is manager-controlled.

Reports are tied to schedule assignments only.

Photos auto-delete after 14 days.

Man-hours are calculated automatically.

Drag-and-drop scheduling is central.

The system must work smoothly on mobile devices.
