![Wifi Analyzer — Make your network visible.](assets/hero.svg)

<p align="center">
  <a href="https://apps.apple.com/us/app/wifi-analyzer-scan-network/id6764405400"><strong>View on the App Store ↗</strong></a> &nbsp; · &nbsp;
  <a href="docs/ENGINEERING.md">Engineering notes</a> &nbsp; · &nbsp;
  <a href="https://github.com/Zodomik">More by Oğuz Tonyalı</a>
</p>

## Wifi Analyzer

A network toolkit for discovering devices and understanding a local connection. A scan-first interface brings network information and diagnostic tools into a single native iOS app.

Built and published by **[Oğuz Tonyalı](https://github.com/Zodomik)**. This repository is a public product and engineering showcase; the application source is maintained privately.

## A look inside

<p align="center">
  <img src="assets/screen-01.jpg" width="30%" alt="Wifi Analyzer official App Store preview 1" />
  <img src="assets/screen-02.jpg" width="30%" alt="Wifi Analyzer official App Store preview 2" />
  <img src="assets/screen-03.jpg" width="30%" alt="Wifi Analyzer official App Store preview 3" />
</p>

*Official product previews from the [App Store listing](https://apps.apple.com/us/app/wifi-analyzer-scan-network/id6764405400).*

## What you can do

- Local network device discovery and connection overview.
- Host reachability, port checks, DNS and IP/subnet tools.
- Saved devices and scan history.
- Magnetic-field and camera-based companion tools.

## Technology

| Area | Technologies | Role in the product |
| --- | --- | --- |
| Interface | Swift, SwiftUI, Combine | Scan progress, discovery results and diagnostic views. |
| Networking | Network framework, Foundation, Darwin | Connections, host probes and interface/address utilities. |
| Discovery | Bonjour / NetServiceBrowser | Service discovery and device-name resolution. |
| Local history | Codable, UserDefaults | Persisted scan records and saved devices. |
| Access and sensors | StoreKit, RevenueCat, Core Motion | Premium access and magnetic-field readings. |

## Engineering highlights

### Progressive discovery

An asynchronous scan stream can surface results as hosts are examined. This supports a visible scanning state instead of making the interface wait for one final response.

### Multiple signals for device context

Bonjour services, resolved names and reachable ports contribute to the discovered-device model. Labels inferred from those signals are useful context rather than guaranteed hardware identity.

### Services behind the interface

Scanning, diagnostic probes and history storage are separate components. The view model can coordinate work and publish progress without embedding network operations in individual SwiftUI views.

Device visibility depends on local-network permissions, network isolation and whether devices respond to discovery or probes.

→ **[Explore the architecture and design decisions](docs/ENGINEERING.md)**

## Try the product

**[Open Wifi Analyzer on the App Store](https://apps.apple.com/us/app/wifi-analyzer-scan-network/id6764405400)** · Requires iOS 17 or later.

Availability and purchase options are shown in the store. For product support, use the developer links on the App Store listing.

---

[All published apps](https://apps.apple.com/us/developer/oguz-tonyali/id1880078720) · [Developer profile](https://github.com/Zodomik) · [Media credits](assets/SOURCES.md)
