# P5 Archive Search 2.7 (Build 18)

Released 2026-09-18.

Each server now chooses whether to talk to P5 in the clear or over TLS.

## Each server chooses HTTP or HTTPS

P5 serves the same REST API two ways: in the clear on port 8000, and over TLS on port 8443.
Measured against a live server, the TLS port answers with paths and bodies identical to the plain
one. Which one a server offers is decided when P5 is installed, so this is a setting on each
server rather than one switch for the app — of three servers checked, 8443 answered on one and not
on another.

- Choosing HTTPS moves the port to 8443. A port you typed yourself is left alone.
- Existing servers are untouched and stay on HTTP.

## Certificate checking

P5 ships a self-signed certificate whose subject identifies nothing, and macOS will not accept it.
Choosing HTTPS without settling that would not give a secure connection — it would give no
connection. So the setting comes with a way to answer the question.

- **Check Certificate** shows the SHA-256 fingerprint and the subject of the certificate the server
  actually presents, and whether macOS trusts it.
- Trusting it once records that exact certificate for that server. If the server later presents a
  **different** one the connection is refused rather than quietly accepted, and the sheet says so
  before you can accept the new one.
- A server whose administrator installed a real certificate needs no trusting at all. Ordinary
  verification succeeds, nothing is stored, and a renewal keeps working without asking again.

The setting applies everywhere the app talks to P5 — browsing, scanning, restoring and the
orphaned-server check — not only to the screen it was set on.

## How private the connection is

Over a VPN such as Tailscale or WireGuard, the connection is already encrypted and the peer already
authenticated before P5 sees any of it, whichever protocol P5 itself is given. TLS earns its place
on a plain LAN, on someone else's network, or where an administrator has installed a real
certificate.

## Fixed

- A certificate that did not match the one trusted reported itself as "cancelled", which read as
  though you had stopped the query yourself. It now says the certificate did not match.

---

Requires macOS 14.6 or later. Universal, signed and notarized.
