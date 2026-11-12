# P5 Archive Search 2.12 (Build 27)

Released 2026-11-11. Beta.

Analyzing a whole index, even from a root-level volume, is now safe to leave running. Nothing
changes in what is scanned or stored.

## Analyze no longer freezes the window

The scan used to do its parsing and database writes on the main thread, so a large index made the
window beach-ball. It now runs in the background and the window hears from it about two and a half
times a second. Memory stays flat for the length of the scan.

## Saved as it goes, and Resume

- A folder's size is saved as soon as that folder finishes, so Stop, a crash or quitting loses
  nothing that was done.
- New **Resume** checkbox next to Analyze. To continue an interrupted scan, tick Resume and
  Analyze the same path again; folders already finished in that run are skipped. Leave it off for
  a fresh scan. Resume is remembered per server, index and start path on each Mac.
- A folder with an unreadable subfolder is now saved as Partial instead of Complete, so its total
  is never silently short. The CSV export already labels these.

## Faster, and a calmer log

- Rows are written in batches and the database now uses WAL mode, so it has `-wal` and `-shm`
  files beside it. If you copy the database to another Mac, quit the app first or copy all three.
- Fetch Barcodes no longer scans the whole table once per volume.
- The on-screen log is capped. The full log is written to
  `~/Library/Application Support/P5ArchiveSearch/Logs/`, one file per day.

## Tried on

A real root-level volume and a Synology NAS. This is a beta: if a scan misbehaves on your server,
the day's log file is the thing to look at.
