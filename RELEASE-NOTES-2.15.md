# P5 Archive Search 2.15 (Build 31)

Released 2026-11-15. Beta.

A server's index can now be moved to another Mac instead of being scanned again, and Settings
shows how big the database is. It includes everything in 2.14 (Build 30).

## Move an index to another Mac

A server that took hours to analyze on one Mac no longer has to be analyzed again on the next.

- **Tools ▸ Export Database…** saves one server, or all of them, to a single `.p5searchdb` file:
  the index, the analyzed folder sizes with their archive dates and volumes, the volume barcodes
  and, if you leave them ticked, the scan history and the server's connection details.
- **Tools ▸ Import Database…** reads that file on the other Mac and lists the servers in it, with
  their item counts and the date of the export. Each one can be included, left out, or imported
  under a different name.

What an import does:

- Importing under a name that already has items replaces them, and the sheet says how many first.
  Every other server in the database is left alone.
- A server that is not set up on that Mac is added to its sidebar from the connection details,
  with an orange dot until you enter its password in Manage Servers. An HTTPS server asks you to
  check its certificate the first time, as any new server does.
- Importing under a new name adds a second entry for the same P5 server.
- If an import fails, nothing is changed.
- Import is unavailable while Analyze is running.

What is in the file:

- Every path and file name in the index, so treat it as you would the archive index.
- The server's address, port, user name and index, unless you untick **Include connection
  details**. Without them nothing is added to the sidebar: the items are in Search DB, and
  browsing or restoring needs the server added under the same name.
- Never passwords, trusted certificates, restore history or the configuration log.

An import is a copy of what the other Mac knew when the file was made. Browsing or analyzing on
the new Mac brings it up to date, and Resume only walks what has not been finished.

## Database size in Settings

Settings (⌘,) has a new **Database** section:

- The size on disk, counting the recent changes kept beside the main file.
- The items and scanned folders stored for each server.
- **Show in Finder**, to reveal the file.
- **Compact**, which gives back the space left behind by deleted items. Deleting items does not
  shrink the file by itself, so a database that has had a lot removed can be many times larger
  than what it still holds. The window may pause while Compact runs.

This is a beta: if a scan or a restore misbehaves on your server, the day's log file in
`~/Library/Application Support/P5ArchiveSearch/Logs/` is the thing to look at.
