# Rx Core print bridge

A single static page that passes labels from Rx Core to **Zebra Browser Print** on the same computer.

Rx Core runs inside a page that may not connect to the user's computer. When a user clicks **Print**, Rx Core opens this page in a new tab with the label (ZPL) in the address fragment (`#job=…`). The fragment is never sent to a web server. This page removes it from the address bar right away, sends the ZPL to Browser Print at `https://localhost:9101` (or `http://localhost:9100`), reports the result back to Rx Core, and closes.

- No data is stored, logged or sent anywhere except to Browser Print on the local computer.
- Opened directly (no job), it offers a connection check and a test label.
- A label that comes in a message is accepted only from the tab that opened this page, and the result of that label goes back only to that tab's origin.
- Published with GitHub Pages: `https://buckybadgertn.github.io/rx-core-print-bridge/`
