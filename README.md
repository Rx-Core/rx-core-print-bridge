# Rx Core print bridge

A single static page that passes labels from Rx Core to **Zebra Browser Print** on the same computer.

Rx Core runs inside a page that may not connect to the user's computer. When a user clicks **Print**, Rx Core opens this page in a new tab with the label (ZPL) in the address fragment (`#job=…`). The fragment is never sent to a web server. This page removes it from the address bar right away, sends the ZPL to Browser Print at `https://localhost:9101` (or `http://localhost:9100`), reports the result back to Rx Core, and closes.

- No data is stored, logged or sent anywhere except to Browser Print on the local computer.
- Opened directly (no job), it offers a connection check and a test label.
- Published with GitHub Pages: `https://rx-core.github.io/rx-core-print-bridge/`

## PrintNode bridge (`printnode.html`)

A second page for Rx Core's "Zebra via PrintNode" route. It does not use Browser Print.

- It accepts a job only by message from the tab that opened it (`window.opener`), and replies only to that tab's origin. It never reads a job from the address.
- The job carries a print token. The page sends the label and the token to the Rx Core print server (an AWS Lambda function, `ENDPOINT` in the page). The server holds the PrintNode API key; this page never sees it.
- It asks the server for the PrintNode job state for up to 20 seconds and reports the result to Rx Core. "Delivered to the print queue" means PrintNode state `done`.
- Design and setup: `docs/printnode.md` in the `Rx-Core/rx-core` repository.
