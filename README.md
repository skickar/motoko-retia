# Motoko-Retia

*Making the unseen visible* — an interactive physarum organism driven by Wi-Fi packet entropy, running entirely in the browser (self-contained WebGL2, no build step).

Millions of agents deposit and follow trails. Their behavior parameters are modulated by the sensed trail value, spatially blended between a **pen** (your cursor) and the **background**. Feed it the radio environment and it takes over: every device gets a stable identity from its MAC hash — a position, a color, and its own perturbation direction on the parameter matrix. Probe requests scatter-spawn, deauths fire waves, data bursts push the swarm toward the talker, and the pen wanders to whoever is loudest.

## Two ways to feed it

- **🛰 Live receiver (real-time).** Click **connect receiver** to link a **Motoko radio-pipe** — an ESP8266 (D1 Mini) running the passive sniffer firmware — over USB. The 802.11 frames it hears drive the organism live, so you can leave it running as an ongoing installation. The link is **read-only**: the piece only ever *reads* the frames the radio hears; it never transmits, injects, or attacks. Needs a Chromium browser (Chrome / Edge / Brave) with Web Serial, served over HTTPS or `localhost`. No hardware? Hit **demo** to drive live mode with synthetic packets.
- **Load a .pcap / .pcapng capture.** Drop a file to replay a captured radio session on a loop.

Don't have a receiver? **⚡ Flash a receiver** writes the radio-pipe firmware to a bare **ESP8266 / D1 Mini** straight from the browser (esptool-js + Web Serial), then connect it. The firmware ships inert and this piece only reads from it, but it's transmit-capable — install affirms authorized use first. For continuous full-band coverage with no channel-hopping, **🛰×3** links three receivers parked on channels 1/6/11.

## Modes — ten ways to read the same air

The icon row at the top of the 📡 panel picks how packets become art (each carries its own color palette). It applies to live, PCAP, and Demo. **✎ curate** hides the ones you don't want (remembered across reloads), **🙈 hide menu** (`H`) gives a clean view, and `[` `]` flip between modes.

- **🌊 Currents** *(default)* — data traffic flows as currents; deauths are squalls, probes scatter.
- **🌡 Presence** — signal strength dominates; the organism blooms toward whoever is physically near.
- **✦ Constellation** — APs are stars; a probe lights its network's star, data draws links, deauths streak as shooting stars.
- **🎛 Spectrum** — Wi-Fi channels become colored horizontal lanes; busy channels glow brighter.
- **💓 Pulse** — traffic accumulates into a heartbeat; busy air beats faster and the whole field breathes.
- **🚨 The Jammer** — a deauth flood is an attacker; the swarm scatters and a red pathogen blooms. Broadcast deauths hit hardest.
- **🐋 Airtime Barons** — airtime claimed (Duration/NAV) becomes mass; a 4K stream grows gravitational, a sensor stays tiny.
- **🎵 Metronomes & Jazz** — perfectly-timed machine traffic crystallizes into rigid lattice; bursty human traffic stays turbulent.
- **🏷 Maker's Marks** — the MAC's OUI sorts the swarm into species (Apple, Espressif, …); randomized MACs drift as grey ghosts.
- **📍 Room of Bodies** — with the 3-receiver rig, devices are placed in the physical room by signal strength and drift as people move. (Demo simulates the rig.)

## Run

Open `index.html` — that's it. Press `?` in the app for full mouse / keyboard / touch / gamepad controls.

For the richest input, capture 802.11 monitor-mode traffic with radiotap headers (RSSI scales each device's influence):

```
# macOS
sudo tcpdump -I -i en0 -w capture.pcap
# Linux (monitor mode)
sudo tcpdump -i wlan0mon -w capture.pcap
```

Plain Ethernet captures work too. Console API: `physarum.loadPcapBuffer(arrayBuffer, name)`, `physarum.connectReceiver()`, `physarum.connectRig()`, `physarum.startDemo()`, `physarum.setMode('metronomes')`, `physarum.stopLive()`.

## Firmware

`firmware/motoko-radio-pipe.bin` is the ESP8266 sniffer firmware (a passive 802.11 "radio pipe"), installed from the browser via the vendored `vendor/esptool-bundle.js` (esptool-js). It's the same firmware served by [skickar/motoko](https://skickar.github.io/motoko/).

## Credits & license

- Recreation of [interactive-physarum](https://github.com/Bleuje/interactive-physarum) by **Etienne Jacob (Bleuje)** — simulation architecture, parameter tuning, interaction design.
- Technique and parameters from **Sage Jenson (mxsage)**'s [36 Points](https://www.sagejenson.com/36points/).
- See Bleuje's [explanation article](https://bleuje.com/physarum-explanation/) for how the simulation works.
- Wi-Fi entropy layer (PCAP parsing, device-identity mapping, packet-event choreography) added for the Motoko-Retia project.

License: [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/), inherited from the original works.
