# Wifi Analyzer · Discovery and signal processing

## 1. Bounded concurrent discovery

The scanner considers host suffixes 1–254 under the current address’s first three IPv4 octets, excluding its own address, and probes hosts in batches of 16. Per-host reachability probes also batch ports. Bonjour runs alongside this pass, and results are merged by observed IP.

This limits the amount of simultaneous work while allowing intermediate progress. The candidate generation assumes a /24-style range; it does not enumerate arbitrary subnet sizes from the actual mask. The separate subnet calculator does use the real netmask.

## 2. Exactly one completion per TCP probe

NWConnection can signal success, failure or cancellation, while a timeout task can complete independently. The callback-to-async bridge uses a lock-protected flag so only the first completion resumes the continuation. It cancels the connection after selecting the outcome.

That prevents the same probe from trying to resume twice when, for example, a timeout races a connection-state update.

## 3. Reachability is different from an open port

The diagnostic service classifies connection outcomes. A refused connection indicates a closed port but can still indicate a reachable host. Open ports are recorded separately from the broader set of reachable responses. The fastest reachable probe supplies the observed host response time.

The ping-style tool repeats a TCP probe on a selected reachable port and summarizes successful latencies. It is not an ICMP echo implementation.

## 4. IPv4 subnet arithmetic

The calculator counts set bits in the netmask for CIDR length, ANDs the address with the mask for the network address, then ORs with the inverted mask for broadcast. It uses the ordinary host-count expression based on remaining bits; it is not a complete model of every special-purpose IPv4 prefix.

## 5. Wake-on-LAN packet construction

The service parses a supplied MAC address into six bytes, prefixes six `0xFF` bytes and repeats the MAC bytes sixteen times. It sends that magic packet as a UDP broadcast. This requires a valid supplied MAC and a network/device that supports the wake behavior; discovery itself does not guarantee that MAC information is available.

## 6. Smoothed magnetic-field changes

Each axis is exponentially smoothed as `current × 0.72 + new × 0.28`. The vector magnitude is calculated and smoothed again. The first twelve magnitude samples establish a baseline. In a quiet/eligible state, the baseline then moves slowly with `baseline × 0.996 + sample × 0.004`.

The display can use the absolute difference from that baseline to show local magnetic changes. This is a heuristic around the magnetometer; it does not identify the source of a field or detect Wi-Fi/RF radiation.

## 7. False-color camera processing

Captured image processing converts to grayscale, adjusts contrast/highlights/shadows, maps intensity through selected cold/hot colors and adds a bloom effect. This explains the visual palette without claiming measured heat or a thermal-camera model.

[Architecture](ENGINEERING.md) · [Local data model](DATA_MODEL.md)
