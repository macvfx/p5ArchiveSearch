# P5 Archive Search 2.16 (Build 32)

Released 2026-11-15. Beta.

Three fixes to Browse. Nothing is new and nothing stored has changed. It includes everything in
2.15 (Build 31).

## Each server starts at its own root

Choosing another server in the sidebar used to keep the folder you were in, so **Browse** asked
the new server for the previous server's path, which it usually does not have.

- Changing server now clears the path, the Back history and the listing.
- **Browse** then lists that server's root.
- Editing the selected server in Manage Servers keeps your place.
- A browse still running when you change server is saved under the server it came from and is
  not shown as the new server's listing.

## The path field shows the whole path

The `/` that sat beside the path field as a label is now part of the path.

- A path reads `/Volumes/YourVolume`, and `/` alone is the top of the index.
- A path typed or pasted without the slash still works, and gains one.
- Scan paths, the database and exports are unchanged.

## Root lists the top of the index

**Root** in the breadcrumb used to clear the path and leave the old listing on screen. It now
lists the top of the index.

This is a beta: if a scan or a restore misbehaves on your server, the day's log file in
`~/Library/Application Support/P5ArchiveSearch/Logs/` is the thing to look at.
