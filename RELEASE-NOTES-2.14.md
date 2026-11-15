# P5 Archive Search 2.14 (Build 30)

Released 2026-11-14. Beta.

Folders no longer look unarchived when they are not, analyzed folders show more, and every Analyze
run is now recorded. It includes everything in 2.13 (Build 29).

## Folders no longer look unarchived

P5 lists many folders without a volume of their own, even though everything inside them is
archived. Those folders showed an orange x in the Archived column, next to a folder size that had
just been added up from their archived contents.

- A folder with an archive date of its own now shows a green tick and that date. Nothing needs
  rescanning for this.
- A folder with neither a volume nor a date shows a dash until it has been analyzed, because the
  app does not know either way.
- The orange x now appears only on a file the index lists without a volume.

## Analyzed folders show more

Analyze now keeps, for each folder, the newest archive date and newest modified date of what is
inside it, and every volume those entries are on. A folder row with nothing of its own in Archived,
Volume/Media, Barcode or Modified shows these instead, in Browse and in Search DB. A value P5 sent
for the folder itself always wins. Hover a filled-in cell to see that it came from the last scan.

Folders analyzed with an earlier version need analyzing again, with Resume off, to fill these in.

## Scan History

**Tools ▸ Scan History…** lists every Analyze run, newest first: when it was started, the server
and folder, how long it took, the size it read, folders, items and errors, and whether it completed
or was stopped. **Export CSV** saves the list with the duration in seconds and the size in bytes
and TB. The summary line in the activity log also ends with how long the run took.

- A resumed run counts only what it read itself, not the folders it skipped.
- A run the app quit or crashed during is listed as Interrupted, with no duration.
- Runs from before this version are not listed.

This is a beta: if a scan or a restore misbehaves on your server, the day's log file in
`~/Library/Application Support/P5ArchiveSearch/Logs/` is the thing to look at.
