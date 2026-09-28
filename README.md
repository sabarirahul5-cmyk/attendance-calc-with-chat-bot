# 🎓 Attendance Predictor

A smart attendance dashboard that helps students plan their classes without risking detention.
Built for the Round 1 "Overworld" challenge (Phase 1 + Phase 2), as a single unified web app.

## Features

### Phase 1: Core Calculator
- Select your class section (8 timetables included) and enter your current attendance % per subject
- Auto-detects today's date, plus a planning date for future scenarios
- Calculates classes left in the semester (29 Aug – 29 Nov 2026)
- Shows exactly how many classes you must attend to reach **75%** and **90%**, and how many you can safely skip
- 🚨 Loud **"Irreversible Detention"** alert when 75% can no longer be reached

### Phase 2: Visuals, Leaves and AI Assistant
- 📊 **Charts:** overall attendance ring, per-subject bars against the 75%/90% lines, and a projection to 29 Nov
- 🧪 **OD / Leave Simulator:** add On-Duty, medical or planned-leave days, and everything recalculates instantly
- 💬 **Attendance Advisor chatbot:** ask questions like *"If I take a 3-day sick leave starting tomorrow, will my Chemistry attendance drop below 75%?"* and it reads your dashboard data, runs the math, and replies with advice and warnings

## Run locally

No install or build step. It's a single HTML file.

```bash
git clone https://github.com/<your-username>/attendance-predictor.git
cd attendance-predictor
python -m http.server 8000
```

Open http://localhost:8000. You can also just double-click `index.html`.

## How it works

- Timetables are stored in the `TT` object in `index.html` (one entry per period).
- Classes held so far are counted from the timetable between the semester start and today. Attended classes are estimated from your entered percentage.
- Required classes to attend: `ceil(target × total classes − attended)`. If that is more than the free remaining classes, the subject is flagged as irreversible.
- The chatbot is a rule-based assistant that runs entirely in the browser, with no API key or backend. It uses the same formulas as the dashboard.

## Assumptions

- Attendance is calculated per subject, and every period counts as one class
- OD and medical leave count as present, and planned leave counts as absent
- Sundays are excluded, and holidays can be added in the app
- No Saturday classes, since none appear in the timetables

## Tech

HTML, CSS and vanilla JavaScript, with inline SVG charts. No frameworks or dependencies.
