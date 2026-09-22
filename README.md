# MLB-assignment-
This hosts the code for the MLB match assigning script 

Lineup

A shared daily assignment tracker for MLB piracy takedown coverage.

Lineup pulls the day's MLB schedule, converts every game's start time to IST, and automatically splits matches across the analyst team — so nobody has to build a spreadsheet by hand every day. Everyone on the team sees the same live board, updated in real time.

Developed by Rakesh Radhakrishnan.

What This Is

Every day, MLB games happen at various times. Each game needs to be watched for pirated streams, and someone needs to be assigned to submit takedown requests for that specific match.

This tool automates three things that used to be done manually every day:

Pulling the day's MLB schedule and converting every game's start time into IST (India Standard Time).
Assigning each match to an analyst automatically, rotating who gets the first match each day so the workload is shared fairly.
Giving the whole team a single, shared, live-updating view of who is covering what — no spreadsheet emailing, no manual re-typing.
How It's Built

This project has two separate parts. Understanding the split matters for troubleshooting.

Part	What it does	Where it lives
The website	index.html — all layout, styling, and logic in one file. A static page with no server of its own.	Hosted free on GitHub Pages
The shared data	The analyst roster, each day's matches, who's assigned to what, and who's marked a match "reported."	A Google Sheet, accessed through a small Google Apps Script that acts as a simple API

Updating the website file never touches the data in the Google Sheet, and vice versa. You can push a new version of the site any time without losing anyone's roster, assignments, or history.

Features
Daily Match Schedule
The MLB schedule loads automatically for whichever date is selected — a season-long snapshot is built into the site, with a live check as backup for dates outside that range or late changes.
Every match's official start time is converted to IST and shown in 12-hour format (e.g. "7:10 AM").
Matches are always sorted earliest first.
The Analyst Roster
One single shared list of analysts, shown under the Analysts panel.
Add a person: type their name and click Assign.
Rename a person: click into their name, edit it, then click Save to lock it in.
Remove a person: click the ✕ next to their name — this is the only way a name disappears.
Mark unavailable (on leave) using the toggle next to their name, without deleting them — they simply stop receiving new auto-assignments.
Each analyst has a fixed colour (a small dot) so they're recognizable at a glance throughout the match list.
Assigning Matches
Auto-assign splits matches across all available analysts using a daily rotation, so a different person "opens" the day each time — nobody is stuck with the first match every day.
Manual override — any match can be reassigned at any time via its dropdown, regardless of what auto-assign chose.
Click Auto-assign any time to re-run the rotation for the currently viewed day (useful after someone goes on leave, or a match gets added).
The 7–10 AM "Need Support" Window
Matches landing between 7:00–10:00 AM IST fall outside the team's working hours and are never auto-assigned.
These rows default to showing "Need support" in the assignment dropdown, with a red-flagged row so it's obvious at a glance.
The dropdown is still fully functional — if someone wants to manually cover one of these matches, they can select an analyst directly from the same dropdown, overriding the default.
The Shift-Start Divider
A plain visual break line is inserted right before the first match of the day starting at or after 8:00 PM IST — the point where the night shift begins.
Separates the tail end of the previous coverage window from tonight's matches at a glance.
Live / Finished Status

Each match shows a small status line:

Before it starts: a countdown, e.g. "Starts in 45m."
During the game (an estimated 3.5-hour window from its scheduled start): a pulsing green ● LIVE indicator.
After that window: "Finished (est.)" in muted grey.

This status is estimated from the scheduled start time, not a live scoreboard feed — it won't reflect rain delays or extra innings precisely.

Marking a Match "Reported"

A small circular button on each row toggles that match between pending and reported (shown with a checkmark and a dimmed row), so progress is visible to the whole team at a glance.

The "Workload" Side Panel

A side panel lists every analyst with a live count of matches currently assigned to them for the day being viewed:

Only counts matches actually assigned to that analyst.
Excludes any match already Finished — the number reflects current, active workload, not a historical total.
A still-unassigned "Need support" match never counts — but if someone manually assigns it, it counts like any other match.
For matches after the shift-start divider (tonight's 8 PM+ games), the match only counts once it's within 3 hours of going live — so the number doesn't look inflated hours before anyone needs to act.
Refreshes automatically every 20 seconds, and whenever new data arrives from a teammate.
Manual Match Entry (Fallback)

If a match is missing from the automatic schedule for any reason, add it by hand using "Add a match manually" at the bottom of the page — enter both team names and a time, then click Add match.

Live Team Sync

The page checks the shared Google Sheet every 15 seconds for changes made by teammates and updates the screen automatically. Nobody needs to refresh manually to see someone else's changes.

Day-to-Day Use

Opening the site

Open the site's link in any browser (Chrome, Edge, Firefox, Safari).
It always opens showing today's date by default.
Use the ‹ and › arrows, or the date box, to look at a different day.

Checking your assignments

Find your name's colour dot, then scan down the match list for that same colour.
Each row shows both teams, the IST start time, live/finished status, and who's assigned.

Marking work done

Once a takedown request is submitted for a match, click the small circular button on the right of that row.
It shows a checkmark and the row dims slightly to show it's complete.

Reassigning a match

Click the dropdown in the match row.
Choose a different analyst's name.
Saves immediately — no separate "save" step needed for reassignment.
Admin: Updating the Roster

Whenever the team changes:

Remove the outgoing person using the ✕ next to their name.
Type the new person's name into the "Add analyst name" box and click Assign.
If you're only renaming someone (not swapping people), click into their name, edit it, then click Save.

Roster changes affect every date, past and future — there is one single roster, not a separate one per day.

Admin: Pushing a Site Update

When a new version of index.html is provided:

Go to this repository on GitHub.
Click on the existing index.html file.
Click the pencil (✏️) edit icon.
Select all existing content (Ctrl+A / Cmd+A) and delete it.
Paste in the full contents of the new file.
Scroll down and click Commit changes.
Wait 1–2 minutes, then open the live link with a hard refresh (Ctrl+Shift+R / Cmd+Shift+R) to see the update.

Never upload a second file with a different name (like index (1).html). GitHub Pages only serves a file named exactly index.html. If the site goes blank after an update, this is the first thing to check.

Troubleshooting
Symptom	Likely cause / fix
Site shows a blank white page	Usually a filename problem — confirm the repo's file is named exactly index.html.
Changes don't save, or revert	Confirm you're opening the site via its real https:// link, not a downloaded file opened directly (file://) — the shared-data connection doesn't work from a local file.
"Fetch API cannot load..." error in console	Same local-file restriction as above. Open the site via its real hosted link instead.
An analyst's name reverted after an edit	Click Save after editing a name, and avoid navigating away immediately after typing.
No matches shown for a date	Click Check for updates to force a fresh schedule check, or add the match manually if it's a known gap.
Ownership

This tool is maintained on behalf of the analyst team covering MLB piracy takedowns. For feature requests or bug reports, contact whoever manages this repository and its Google Sheet backend.

Site credit: developed by Rakesh Radhakrishnan.
