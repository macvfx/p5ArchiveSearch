# P5 Archive Search 2.8 (Build 19)

Released 2026-09-25.

You can now find the volume labels of an imported-volumes index instead of typing each one, and a
failed request says why.

## Imported volumes

An index rooted at volume labels, such as Imported-Volumes, has no `Volumes` or `mnt` at its top, and
P5 does not list the labels over its API. Its top level is the label of each volume, with the original
folders inside, so a browse or a scan had to be given each label by hand.

Each index is its own server entry, added once per P5 server:

1. **Manage Servers ▸ Add**, with the same address, port, user and password as the P5 server, and the
   **Archive Index** set to the imported-volumes index. Give the entry its own alias.
2. Under Scan Paths, click **Find imported volumes…**. It tries each volume's label and barcode as a
   top-level name in the index and lists the ones the index answers for, with the folders inside. It
   only reads, and it has a Stop button.
3. For a label it missed, open **Add names by hand** and paste them one per line. Each is checked
   against the index. A label with no volume record cannot be found by the search.
4. Tick the labels, click **Add N as volumes**, and Save. A label two volumes share is flagged.
5. In Browse, the drive icon keeps `Volumes` and `mnt` at the top and lists the labels under
   **Imported volumes**.
6. Choose **Scan all imported volumes into search** in that menu. Search only covers what has been
   scanned, so finding a label does not by itself make its files searchable.

## A failed request says why

Every P5 failure used to look the same: "P5 did not answer, or refused the request." A rejected
password looked exactly like an unreachable server.

The browse log and Analyze now show the HTTP status and what it means, or the cause when there was no
answer: a timeout naming the host, a refused connection, or a certificate problem. P5 answers a wrong
password with HTTP 400 and the body "Wrong username or password.", not 401, and the message says so.
Analyze no longer finishes silently having read nothing: the first failed folders are listed with
their reason.

Every request the app makes is recorded in the unified log, without the password. To read it, in
Terminal:

```
log show --last 1h --info --predicate 'category == "requests"'
```

---

Requires macOS 14.6 or later. Universal, signed and notarized.
