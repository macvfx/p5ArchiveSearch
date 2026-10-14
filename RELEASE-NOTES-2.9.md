# P5 Archive Search 2.9 (Build 22)

Released 2026-10-14.

Browse the root of an index and see its volume labels without typing one, and find out when a
server's certificate changed.

## Browse the root of an index

An imported-volumes index has no `Volumes` or `mnt` at its top, so the app used to need a label typed
in before anything appeared. Browsing an empty path now lists the root, so the volume labels appear
as folders and you can open one. P5 answers the bare index root with an error, so the app asks for
it with an explicit `/`, which P5 8.0.5 and 8.0.6 both accept. The root of a path-rooted index such
as Default-Archive lists too (`Volumes`, `mnt`).

**Find imported volumes…** opens and searches at once, and lists the root in one request. Only when
the server will not list it does it fall back to trying each volume's label as a top-level name,
which was the only method before and missed a label with no volume record.

## A changed certificate is explained

A server pinned to one certificate that presents a different one used to fail with a generic TLS
message. The app now shows a sheet, once per server per session, with the trusted and presented
fingerprints and what the server last reported (its P5 release, build and when), and offers
**Review Certificate…**. Nothing is trusted automatically. A P5 upgrade, a reinstall or a renewal can
replace the certificate, and so can something between this Mac and the server.

The app also remembers each server's P5 release, build and certificate, the first time the server is
selected in a session, and writes a change to the configuration log. It stays on this Mac. Whether a
P5 upgrade replaces the certificate has not been measured; this will show it.

## Smaller changes

- **Restore works against P5 8.0.6**, which returns an archive entry's ID in a different form (URL-encoded).
- Double-click a server in Manage Servers to edit it.
- In-app guide and What's New describe all of the above.

## To try

Browse an empty path on an imported-volumes index, then restore a small file into a scratch folder.
