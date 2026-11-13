# agentsdash-device-phone

A phone (iPhone or Android) as a device of [agentsdash](https://github.com/tfabien/agentsdash): a cheap auxiliary screen you already carry.

It shows the hub page full screen, so you see which agent needs you even when you are away from your desk.

Status: idea, nothing built yet. The design questions are tracked in the issues of this repository.

## Direction

A PWA, with no native code.

The hub already serves the page, so the phone only needs to reach it and be installable to the home screen.

## Open questions

- **Discovery.** One simple shortcut that finds the hub by itself: an mDNS name (`agentsdash.local`), a QR code shown by the hub page or the terminal view that opens the PWA with the address and a token, or a fixed URL typed once.
- **LAN access.** The hub binds `127.0.0.1` and checks Host and Origin. It needs an opt-in bind to a LAN address, a pairing token and an extended Host and Origin allow-list.
- **Company use.** Corporate networks (VPN, client isolation on Wi-Fi, blocked mDNS) may prevent a direct phone to PC link. Options: a private tunnel between phone and PC (a mesh VPN), or an authenticated relay. Needs a check against the company security policy.
- **Security.** The page shows commands and session titles. Any non-local access needs authentication (a token in the pairing QR) and TLS, since iOS only installs a PWA and keeps service workers on HTTPS.
- **Offline and wake.** What happens when the PC sleeps or the hub is down: reconnect the server-sent events, show a clear "hub unreachable" state, keep the screen awake (Screen Wake Lock API).

## Links

- The hub and its protocol: [tfabien/agentsdash](https://github.com/tfabien/agentsdash) (`docs/protocol.md`, `docs/device-protocol.md`).
- Other devices: [agentsdash-device-artillery-x3](https://github.com/tfabien/agentsdash-device-artillery-x3).
