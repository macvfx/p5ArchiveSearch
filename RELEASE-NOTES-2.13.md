# P5 Archive Search 2.13 (Build 29)

Released 2026-11-13. Beta.

Two fixes: Browse opens promptly after a long scan, and a cancelled restore ends as Cancelled.
Nothing changes in what is scanned or stored. It includes everything in 2.12 (Build 27); build 28
was not published and its restore fix ships here.

## Browse opens promptly after a long scan

Switching from Search DB back to Browse could beach-ball while the activity pane laid out the whole
accumulated log, and the longer the scan had run the longer the wait. The Browse pane and the
Activity Log window now use the macOS text system, which lays out only what is on screen. The log
is still selectable and still follows new lines.

## Cancelled restores finish as Cancelled

P5 does not report a cancellation: a cancelled job answers as running for a moment and then stops
being listed at all. The app used to keep waiting, showing **Running** until the watch window
closed, or indefinitely.

- After P5 accepts a cancel request, the restore shows **Cancelling**, then **Cancelled** once P5
  stops listing the job. This survives quitting and reopening the app.
- A job that disappears without this app having cancelled it now says what that can mean: it was
  cancelled in P5, or it finished long enough ago to be pruned.
- If P5 refuses a cancel request, which it does when the request arrives before the job has
  started, the app says the job may still run.

## Documentation

The user guide now says when to use Resume and when a plain Analyze is the right choice, and that
neither creates duplicate rows.

This is a beta: if a scan or a restore misbehaves on your server, the day's log file in
`~/Library/Application Support/P5ArchiveSearch/Logs/` is the thing to look at.
