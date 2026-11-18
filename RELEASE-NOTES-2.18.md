# P5 Archive Search 2.18 (Build 36)

Released 2026-11-17. Beta.

Restore is clearer about which P5 client receives the files, and remembers your choice. It includes
everything in 2.17 (Build 35).

## Choose the restore client once

The restore sheet has a labelled **P5 client** row.

- **Make Default** remembers the client for that server and preselects it for every later restore.
  **Clear Default** undoes it.
- Without a default, the sheet preselects **localhost**, the P5 server itself, when the server
  lists one. Before, it preselected whichever client answered the lookup first.
- A line under the picker says the folder must exist on that client, and turns orange when the
  client is not localhost.
- In **Tools ▸ Restore Queue…** each row reads `→ client NAME : folder`.

A restore sent to a client that does not have the destination folder fails in P5 with "no files or
folders found", which gave no hint of the cause.

## P5's report is shown open

In the restore queue, P5's report for a restore is now shown open under the row instead of behind
a small label, so the reason for a failure is visible straight away.

## The in-app guide is up to date

The Restoring section of the in-app User Guide had not been updated for 2.17. It now covers
restoring several items, the queue, the folder picker and the default client.

This is a beta: if a restore misbehaves on your server, the day's log file in
`~/Library/Application Support/P5ArchiveSearch/Logs/` is the thing to look at.
