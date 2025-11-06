# Print Queue Bot

_This is authored by an AI and fully checked and approved by me._

Simple, fair, Discord-based queue for shared 3D printers.

## Overview

Print Queue Bot helps communities share 3D printers without manual coordination. Users join a single queue from Discord and are notified when it’s their turn to claim a printer. The system relies on user‑reported times and predictions—no hardware polling or MQTT required.

## Backend

- ETAs and printer availability use self‑reported durations from users.
- A scheduler predicts when each printer will be free and pings the next user to claim.
- Access hours are respected: if a finish happens outside access hours, claim/start timers begin next open period.
- Fairness is enforced by configurable claim and start windows.
- Runs on a caffeinated Mac (kept awake with `caffeinate`).

## How to use

1) Join the queue
- Run `/join job_name est_time` to add your job with an estimated print time.

2) When notified, claim a printer
- Run `/claim printer` within the claim window to reserve a specific printer.

3) At the printer, handle the previous job
- If the previous print is still running: `/notdone printer remaining_time`.
  - This releases your claim and reschedules your notification for the updated time.
- If the previous print has ended: `/close printer success|fail [notes] [photo]`.
  - Photo is required for `fail`. Notes are optional.

4) Start your job
- After closing the previous job, run `/report started printer` within the start window.

5) Check status
- `/status` shows the overall queue and printers.
- `/myjobs` shows your own jobs.
- `/update_time` adjusts your estimate. `/cancel` removes your job.

## Commands at a glance

- `/join job_name est_time` — join the queue with an estimate
- `/claim printer` — reserve a specific printer when notified
- `/notdone printer remaining_time` — report previous print still running (releases your claim)
- `/close printer success|fail [notes] [photo]` — close the previous job (photo required for fail)
- `/report started printer` — confirm your print has started
- `/status`, `/myjobs`, `/update_time`, `/cancel`

## Installation

(Coming soon)

## Learn more

- Technical planning: [technical.md](technical.md)
- Implementation plan: [implementation.md](implementation.md)
- Assignment context: [action_plan.md](action_plan.md)