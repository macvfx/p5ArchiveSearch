# P5 Archive Search 2.17 (Build 35)

Released 2026-11-17. Beta.

Restore gets a folder picker, restoring several items at once, and a queue. It includes everything
in 2.16 (Build 32).

## Restore several items at once

Select more than one file or folder in **Browse** or **Search DB** with shift-click or
command-click, right-click, and choose **Restore N items from P5…**.

- One sheet confirms them all with a single destination.
- Each item is sent to P5 as its own job, with its own entry in Restore History.
- Items P5 does not report as archived are named and left out; the rest go ahead.
- Items from more than one server are refused. Restore them one server at a time.

Browse could only select one row before this release; it now allows several, as Search DB did.

## A restore queue

**Queue Restore** closes the sheet straight away, so you can keep searching and queue more.

- Queued restores are sent to P5 one at a time, in the order queued.
- **Tools ▸ Restore Queue…** shows each one's status, P5 job number, progress and report.
- **Remove from Queue** takes out one that has not started. **Ask P5 to Cancel** asks P5 to stop one
  that has been submitted.
- A failure in one does not stop the others.
- Items still waiting when you quit the app are not remembered. Restores already with P5 are picked
  up again at the next launch.

## A folder picker for the destination

The restore sheet has a **Choose…** button beside the destination folder. It opens the Finder's
folder dialog, which can also create a folder. Typing a path and dropping a folder still work.

The dialog browses this Mac, so use it when the P5 client is this Mac. For another client, type its
path as before.

This is a beta: if a restore misbehaves on your server, the day's log file in
`~/Library/Application Support/P5ArchiveSearch/Logs/` is the thing to look at.
