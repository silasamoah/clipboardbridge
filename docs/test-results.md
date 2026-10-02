# Verification for version 0.2.0

Checked on Windows with Node.js v26.10.0 and installed Chrome, driven headlessly through Playwright. Date: 2026-10-02.

`npm test`: **10 tests passed**. Coverage includes HTTP assets, QR endpoint validation, room-code pairing, occupied-port handling, signalling relay, full rooms, token-gated resume, stale session rejection, remembered/non-remembered expiry, forgetting/revocation, text/ack validation, lost acknowledgement and retry, duplicate suppression, separate-tab saved credentials, and blocked storage.

`npm run test:browser`: **11 browser checks passed**, using actual WebRTC channels between separate desktop and mobile-viewport browser contexts:

1. Local QR image rendering and explicit join from a prefilled pairing link.
2. Unicode/plain-text transfer in both directions with receipt acknowledgements.
3. Clipboard copy on localhost, with Windows line-ending normalization accounted for.
4. Dropped acknowledgement, Unconfirmed state, explicit retry, and duplicate suppression.
5. Simulated page background/foreground events with retained room and draft.
6. Automatic remembered-pairing recovery after reload.
7. Explicit saved-pairing resume from a new tab.
8. Simulated offline/online events and restored transfer with draft preservation.
9. Server restart, automatic reconnect, and invalid saved-ticket cleanup.
10. Forget pairing with local credential removal and server revocation.
11. Oversize-text feedback, no horizontal overflow at a mobile viewport, and no browser errors.

Desktop and mobile screenshots were visually inspected. Physical iPhone/Safari and Android/Chrome checks, actual Wi-Fi/cellular handoffs, OS battery restrictions, live QR-camera scanning, and the example HTTPS proxy configuration were **not run**. Follow [phone-testing.md](phone-testing.md) and [https-setup.md](https-setup.md) for those checks. No background execution guarantee is implied by simulated lifecycle tests.
