# Hours — Time Tracking App

A personal work-hours and focus tracker. Clock in, work in focus blocks, take breaks and lunch, tag time to tickets, and see how close you are to an 8-hour billable day and a 40-hour week.

**Live app:** https://proindustries.github.io/Time-Tracking/

> This is a personal project and isn't open for outside contributions.

## Features

- **Clock in / out** with a live billable total and a projected clock-out time for 8 billable hours.
- **Focus modes** set the length of a work block and the break it earns:

  | Mode      | Focus | Break |
  |-----------|-------|-------|
  | Classic   | 52 min | 17 min |
  | Deep Work | 90 min | 20 min |
  | Pomodoro  | 25 min | 5 min  |

  Switching modes mid-day only affects time from that point on.
- **Breaks, lunch and stepping out.** Breaks are paid. Lunch is unpaid beyond the standard break length. "Step Out" time is unpaid and pushes your end of day later.
- **Break credit.** Work time earns break credit at the current mode's rate. Unused credit covers long lunches. Whatever is left at clock-out is shown but not added to your hours.
- **Tickets and descriptions.** Tag each block of work with a ticket number and a note for your work log. Start a new ticket block without resetting the focus timer.
- **Ticket Summary** for the day, with total tagged time.
- **This Week:** Monday to Friday hours, the week total against 40h, and per-day ticket breakdowns.
- **Edit the log:** change times, tickets and descriptions, insert or delete blocks.
- **Edit past days:** click an earlier day in This Week to open and fix it. You can also add a clock-in/out or mark it sick.
- **Sick / Out of Office:** one button before clocking in counts the day as 8 hours and shows a checklist of sick-day steps.
- **New day handling:** a finished day is never wiped. After midnight, **Start a New Day** moves to the new date, and **Reset day** needs a second tap.
- **Dark mode**, with the setting remembered.

## How hours are calculated

```
billable = (clock-out − clock-in) − unpaid lunch − stepped-out time
unpaid lunch = max(0, lunch − standard break − unused break credit)
```

Breaks count as billable time. A day marked Sick / Out of Office counts as exactly 8 hours.

## Your data

Everything is saved in your browser's local storage, one entry per day (`focusday:YYYY-MM-DD`). Nothing is sent to a server, and nothing is stored in this repository. As a result:

- Each browser and device has its own separate history, with no syncing.
- Clearing site data for the page erases your history.
- Anyone else who opens the live link sees an empty tracker, not your hours.

## Running it

It's a single file, `index.html`, with no build step.

- **Hosted:** GitHub Pages serves `index.html` from the `main` branch, so merging to `main` updates the live app within a minute or two. A hard refresh (Ctrl+Shift+R / Cmd+Shift+R) picks up changes right away.
- **Locally:** open `index.html` in a browser. It needs an internet connection the first time, to load its libraries.

## How it's built

- React 18 and Babel Standalone are loaded from unpkg, with jsDelivr as a fallback. The app's JSX is compiled in the browser at startup.
- All app code lives in `index.html`, inside `<script type="text/plain" id="app-source">`. A small loader script at the bottom compiles and mounts it, and shows an error message on the page if anything fails to load.

## Changing things

- **Sick-day checklist:** edit `SICK_STEPS` near the top of the app code.
- **Focus modes:** edit `PRESETS`.
- **Daily target:** edit `WORK_TARGET` (in minutes, default 480).
