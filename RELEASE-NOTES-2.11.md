# P5 Archive Search 2.11 (Build 26)

Released 2026-10-27.

A demo server you can explore without any P5 install, server management from the sidebar, and
selective row deletion in Search DB.

## Demo Mode

A server can be flagged as a demo server (Manage Servers → Add) and answer from a built-in
scenario instead of a real P5 installation — no address, credentials or network connection
needed. Analyze still crawls it the same way, and Search still searches what gets cached from
that crawl.

The Add Server sheet suggests a name for a new demo server — a Canadian city paired with a
production type, such as "Calgary VFX" or "Halifax Film Location" — with a shuffle button for
another.

## Manage a server from the sidebar

Right-click a server in the sidebar for two shortcuts:

- **Edit…** opens Manage Servers already selected to that server.
- **Delete…** asks whether to also delete that server's indexed inventory, instead of always
  leaving it behind under the old alias.

## Delete just the rows you mean

Search DB now supports selecting a single row, a shift-click range, or a scattered cmd-click
selection, and deleting just those — by Delete/Backspace, right-click, or a toolbar trash button
that appears only while something is selected. Clear Database (the red trash button, wipes
everything) is unchanged.

## A demo index worth exploring

The demo server's archive index is two to three levels deep — camera-card captures, a few days of
audio, dailies, and an editorial project — under `Volumes` and `mnt`, spread across different
tapes. Fetch Barcodes resolves a different barcode for each production, and a folder entirely on
one tape resolves its own barcode too, the same way its calculated size already bubbles up from
the files inside it — showing what Archive Search can do that P5's own web GUI can't, at every
level.

## To try

Add a demo server, Analyze its default path, then open Search DB and try Fetch Barcodes and a
multi-row delete.
