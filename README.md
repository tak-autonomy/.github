# tak-autonomy

**Open-source tools bridging autonomous robots and TAK (Team Awareness 
Kit) infrastructure.**

This organization develops and maintains drivers, plugins, and utilities 
that connect autonomous robotic systems — maritime, ground, and air — 
with the TAK ecosystem, including TAK Server, ATAK (Android), and WebTAK. 
The goal is to enable autonomous vehicles to operate as first-class 
participants in TAK-based common operating pictures alongside human 
operators in the field, regardless of the underlying autonomy framework 
or vehicle domain.

---

## Mission

Autonomous systems have no native path into the TAK-based command and 
control infrastructure used widely across defense, maritime, and 
first-responder operations. This organization fills that gap with 
production-quality, open-source tools that follow established software 
conventions for each supported autonomy framework — requiring no 
modification to core autonomy stacks.

Current development is focused on MOOS-IvP based tools, with the 
architecture intentionally designed to expand to additional autonomy 
frameworks over time.

---

## Supported Domains

| Domain | Vehicles | Status |
|---|---|---|
| Maritime | ASVs, USVs, AUVs | Active |
| Ground | UGVs | Planned |
| Air | UAVs, UAS | Planned |

---

## Architecture

```
Autonomous Vehicles
+-----------------------------------------------+
|  Maritime       |  Ground       |  Air         |
|  ASV/USV/AUV   |  UGV          |  UAV/UAS     |
+--------+--------+------+--------+------+-------+
         |               |               |
    [MOOS-IvP]        [ROS 2]          [PX4]
    (active)          (planned)        (planned)
         |               |               |
         +---------------+---------------+
                         |
                  [tak-autonomy]
                         |
                   [TAK Server]
                    /         \
               [ATAK]       [WebTAK]
```

**Outbound (Vehicle → TAK):** Vehicle position, heading, speed, and 
state published to the TAK common operating picture via TCP streaming 
using CoT XML and TAK Protocol v1 (protobuf).

**Inbound (TAK → Vehicle):** Contacts, waypoints, routes, and operator 
commands received and translated into the native message bus of the 
target autonomy framework.

---

## Repositories

| Repository | Description | Framework | Status |
|---|---|---|---|
| `moos-ivp-tak` | MOOS-IvP ↔ TAK Server bridge application | MOOS-IvP | Active |

---

## Current Capabilities

- Bidirectional communication with TAK Server
- Outbound vehicle position reporting via TCP (CoT XML and TAK Protocol v1 protobuf)
- Inbound contact ingestion via UDP multicast into MOOSDB `NODE_REPORT`
- CoT message parsing: contacts, waypoints, routes, polygons, and 
  operator-dropped points
- Integration with `pContactMgrV20` for contact tracking and collision avoidance
- Compatible with ATAK (Android) and WebTAK clients
- Tested against self-hosted TAK Server on Ubuntu 22.04

---

## Roadmap

### MOOS-IvP Tools
- [ ] Clean open-source release of `moos-ivp-tak` driver following 
      established MOOS-IvP driver conventions
- [ ] TAK-native route planning pushing waypoint sequences directly 
      into the MOOS helm
- [ ] Expanded multi-vehicle coordination support via the TAK common 
      operating picture
- [ ] Automated integration test suite against simulated TAK Server
- [ ] Field validation with physical USV hardware

### ATAK Plugins
- [ ] Vehicle health monitoring plugin — real-time telemetry display 
      (mission state, connectivity, propulsion, battery) per robot 
      directly in the ATAK client
- [ ] Route planning plugin — operator-drawn routes pushed directly 
      to autonomous vehicle helms
- [ ] Multi-robot management overlay for commanding and monitoring 
      robot teams from ATAK


---

## Getting Started

Each repository contains its own build and configuration documentation.
For the current MOOS-IvP tools, at minimum you will need:

- A working [MOOS-IvP](https://oceanai.mit.edu/moos-ivp/pmwiki/pmwiki.php) 
  installation
- A running [TAK Server](https://tak.gov/products/tak-server) instance 
  (self-hosted or cloud)
- A TAK client: [ATAK](https://tak.gov/products/atak) or 
  [WebTAK](https://tak.gov/products/webtak)

---

## Contributing

Contributions are welcome. Please open an issue before submitting a pull 
request to discuss proposed changes.

- C++ contributions should follow the 
  [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
- Python contributions should follow 
  [PEP 8](https://peps.python.org/pep-0008/)

If you are working with autonomous systems and TAK infrastructure and 
have a use case not covered here, we'd like to hear about it — open an 
issue or start a discussion.

---

## License

All repositories in this organization are released under the 
[MIT License](https://opensource.org/licenses/MIT) unless otherwise noted.

---

## Contact

For collaboration inquiries, open an issue in the relevant repository 
or reach out via the organization contact page.

*Maintained by [MIT Marine Autonomy Lab](https://oceanai.mit.edu/autonomylab/pmwiki/pmwiki.php?n=PavLab.HomePage)*
