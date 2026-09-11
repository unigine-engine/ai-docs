# TCP/UDP Port Numbers Used


This article contains the list of available TCP/UDP Port Numbers:


**Authentication and authorization, updates:**


- 443 (developer.unigine.com)


**(Optional) Performance profiling:**


- 1337 (localhost)
- 1338 (localhost)


**License control:**


- 33333 (localhost) - [configurable](../troubleshooting/browser_issues.md#licensing) (-licensing_host address: port)
- 33334 (localhost)
- 33333 (TCP, LAN) and 33334 (UDP broadcast, LAN) - used by the [Licensing Server](../sdk/licenses/licensing_server.md) to serve licenses over the local network (TCP port configurable via --licensing-host)


**(Optional) *Sandworm* tool, distributed terrain generation:**


(default, can be re-configured)


- 7814 (LAN)
- 7741 (LAN)


**(Optional) Distributed image generation:**


- 8890 (LAN) - configurable (syncker/ig)
- 8888 8889 - configurable (cigi)
- 3000 - configurable (dis)
- 3324 - configurable (hla)
