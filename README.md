# agentsdash-device-phone

A phone (iPhone or Android) as a device of [agentsdash](https://github.com/tfabien/agentsdash): a cheap auxiliary screen you already carry.

It shows the hub page full screen, so you see which agent needs you even when you are away from your desk.

Status: first version. It works on the home Wi-Fi over plain http and is read-only. The page itself lives in the core (`hub/web/phone.html`); this repository holds the documentation and the open questions.

## Pairing

1. On the PC, turn LAN access on: `"lan": {"enabled": true}` in `~/.agentsdash/config.json` (or `AGENTSDASH_LAN=1`), then restart the hub. Needs core 0.5.0 or later.
2. Open the hub page on the PC, click the Device button (plug icon): the Phone section shows a QR code. The terminal view prints the same address.
3. Scan it with the phone camera. The phone opens `/phone` and keeps a cookie.
4. Full screen: on Android, tap the page once, the browser bars hide. On an iPhone, use "Add to Home Screen": the icon opens the page without bars. The page keeps the screen awake and shows "Hub unreachable, retrying" when the PC sleeps. `/phone?debug` prints the measured layout.

The token is in `~/.agentsdash/lan-token` on the PC. Delete the file and restart the hub to invalidate every paired phone.

## What it is not yet

- The link is plain `http`: anyone on the same Wi-Fi can read the traffic. Use it on a network you trust.
- No HTTPS, so no installed app on Android (the full screen tap is the stand-in), no service worker, no offline mode, no push notification (iOS and Android require HTTPS for them).
- No control from the phone (dismiss, settings, themes): the hub refuses every write from a LAN client.

## Open questions

- **Outside the home network.** Corporate networks (VPN, client isolation on Wi-Fi) may prevent a direct phone to PC link. Options: a private tunnel between phone and PC (a mesh VPN such as Tailscale, which also gives HTTPS), or an authenticated relay. Needs a check against the company security policy.
- **HTTPS.** A local certificate or Tailscale `serve`, to unlock the service worker and the install prompt.
- **Discovery.** An mDNS name (`agentsdash.local`) would survive an IP change; today the QR carries the IP address.

## Links

- The hub and its protocol: [tfabien/agentsdash](https://github.com/tfabien/agentsdash) (`docs/protocol.md`, `docs/device-protocol.md`).
- Other devices: [agentsdash-device-artillery-x3](https://github.com/tfabien/agentsdash-device-artillery-x3).
