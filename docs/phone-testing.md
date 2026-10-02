# Physical phone test matrix

Status: **not run on physical phones**. Desktop automation tests real WebRTC traffic and simulated browser lifecycle events, but cannot reproduce iOS suspension, radio handoffs or Android battery policy. Run these checks with a Windows computer plus a real iPhone/Safari and Android/Chrome.

Record phone model, OS version, browser version, server address, HTTP/HTTPS, remember setting, time away, observed status, and whether text was received and copied. Use a stable same-Wi-Fi setup first, with trusted HTTPS for automatic copying.

| Check | Action | Expected result | iPhone | Android |
| --- | --- | --- | --- | --- |
| QR pairing | Scan the computer's LAN/HTTPS QR and tap Join | Code is prefilled; room connects after explicit join | Not run | Not run |
| Bidirectional text | Send Unicode and several lines each way | Sender shows Delivered; receiver renders exact plain text | Not run | Not run |
| Copy gesture | Tap Copy, switch to Notes, paste | Received text is copied under trusted HTTPS; OS may normalize line endings | Not run | Not run |
| HTTP copy fallback | Open the LAN HTTP page and tap Copy | Clear HTTPS guidance; received text selected for manual copying | Not run | Not run |
| Brief background | Switch to Notes for 30 seconds, then return | Connection may pause; return resumes the same room; draft remains | Not run | Not run |
| Screen lock | Lock for one minute, unlock and return | Resume or clear recovery feedback; no false delivery claim | Not run | Not run |
| Long background, remembered | Remember on both devices; background for five minutes | Same room can resume before 24-hour expiry | Not run | Not run |
| Long background, not remembered | Disable remembering; background for over two minutes | Room expires after disconnect is detected; pairing again is required | Not run | Not run |
| Tab reload | Reload a remembered paired tab | Saved seat resumes; text fields reset without clipboard content in saved storage | Not run | Not run |
| Browser eviction | Close/relaunch browser; open same origin | Saved rooms offer explicit Resume if local storage survives | Not run | Not run |
| Wi-Fi off/on | Disable Wi-Fi, then rejoin the original Wi-Fi | Offline/retry feedback, preserved draft, and successful reconnect | Not run | Not run |
| Wi-Fi to cellular | Switch phone to cellular | Local server may be unreachable; Unconfirmed or retry feedback, no claimed delivery | Not run | Not run |
| Different Wi-Fi then return | Move to another network and back | Reconnection succeeds after LAN reachability returns, within pairing expiry | Not run | Not run |
| Battery restrictions | Enable Low Power/Battery Saver, background and return | Background activity may stop; foreground recovery still works | Not run | Not run |
| Lost confirmation | Interrupt receiving device during a send | Delivered only with an acknowledgement; otherwise Unconfirmed and explicit retry | Not run | Not run |
| Duplicate retry | Retry an unconfirmed message after receiver already showed it | Same ID is re-acknowledged without redisplay while receiver tab state survives | Not run | Not run |
| Forget pairing | Tap Forget on either device | Room revoked, other device resets, local saved ticket removed | Not run | Not run |
| Restart server | Restart Node while paired | Browser retries, invalid saved ticket clears, manual pairing required | Not run | Not run |

Do not treat an acknowledgement as an OS clipboard write. Clipboard writes remain manual. Remembered pairing expires 24 hours after room creation, without sliding renewal. A server restart invalidates all tickets. Disconnect detection can lag until a heartbeat fails; the two-minute grace begins when the server observes suspension/disconnection.

## Result record

```text
Date:
Phone / OS / browser:
Computer / browser:
Server origin / HTTP or trusted HTTPS:
Remember checkbox on each device:
Check:
Time in background / network change:
Expected:
Observed status / delivery indicator:
Received text / clipboard result:
Pass or fail:
Reproduction steps and notes:
```
