# IoT Systems

## Scope
Internet of Things: embedded devices, sensor networks, connectivity (WiFi, LoRaWAN, cellular), data collection, and edge computing.

## Core principles
- Power is the bottleneck: batteries last months (not years) if devices are constantly transmitting; sleep/wake cycles and low-power protocols (BLE, LoRaWAN, Sigfox) are essential.
- Connectivity is unreliable: IoT devices are in basements, outdoors, and moving; connection drops, timeouts, and intermittent failures are normal; systems must handle offline gracefully.
- Security is hard at scale: millions of devices, each with a credential or certificate, must be securely provisioned, updated, and retired; compromised devices are network liability.
- Latency tolerance varies: smart home (seconds), industrial monitoring (milliseconds to seconds), autonomous vehicles (milliseconds) have different requirements.
- Edge vs. cloud tradeoff: processing data on device (edge) is fast and private but computationally limited; cloud is powerful but requires connectivity.

## Apex practices
- Use low-power protocols (BLE, LoRaWAN) matched to use case; WiFi is power-hungry, ideal for plugged-in or frequently charged devices.
- Implement bidirectional provisioning: devices register with backend on first power-on (secure), receive configuration, and can be remotely updated or decommissioned.
- Build offline-first edge: devices collect data locally, attempt to sync when connected, and retry on failure; data loss and latency are acceptable if bounded.
- Secure update mechanisms: devices must be cryptographically verified before accepting firmware; compromised OTA (over-the-air) updates are catastrophic.

## Pitfalls
- Underestimating power consumption in design phase; field testing reveals problems that simulator doesn't.
- Ignoring security for "just a hobby project"; hobbyist IoT devices are attack vectors for botnets (Mirai) and industrial espionage.
- Over-designing bandwidth: many IoT use cases (temperature sensor, door lock) send kilobytes per hour; streaming uncompressed video is wasteful.

## Tools & references
Protocols: BLE, LoRaWAN, Zigbee, Matter, Sigfox, cellular (NB-IoT, LTE-M), platforms: Arduino, ESP32, Raspberry Pi, connectivity: Hologram, Twilio, cellular carriers, cloud: AWS IoT Core, Azure IoT Hub, Google Cloud IoT.
