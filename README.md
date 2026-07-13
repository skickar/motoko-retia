# Motoko-Retia

*Making the unseen visible* — an interactive physarum organism driven by Wi-Fi packet entropy, running entirely in the browser (WebGL2, single HTML file, no dependencies).

Millions of agents deposit and follow trails. Their behavior parameters are modulated by the sensed trail value, spatially blended between a **pen** (your cursor) and the **background**. Load a **.pcap / .pcapng** capture and the radio environment takes over: every device gets a stable identity from its MAC hash — a position, a color, and its own perturbation direction on the parameter matrix. Probe requests scatter-spawn, deauths fire waves, data bursts push the swarm toward the talker, and the pen wanders to whoever is loudest.

## Run

Open `index.html` — that's it. Press `?` in the app for full mouse / keyboard / touch / gamepad controls.

For the richest input, capture 802.11 monitor-mode traffic with radiotap headers (RSSI scales each device's influence):

```
# macOS
sudo tcpdump -I -i en0 -w capture.pcap
# Linux (monitor mode)
sudo tcpdump -i wlan0mon -w capture.pcap
```

Plain Ethernet captures work too. A console API exists for piping live data: `physarum.loadPcapBuffer(arrayBuffer, name)`.

## Credits & license

- Recreation of [interactive-physarum](https://github.com/Bleuje/interactive-physarum) by **Etienne Jacob (Bleuje)** — simulation architecture, parameter tuning, interaction design.
- Technique and parameters from **Sage Jenson (mxsage)**'s [36 Points](https://www.sagejenson.com/36points/).
- See Bleuje's [explanation article](https://bleuje.com/physarum-explanation/) for how the simulation works.
- Wi-Fi entropy layer (PCAP parsing, device-identity mapping, packet-event choreography) added for the Motoko-Retia project.

License: [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/), inherited from the original works.
