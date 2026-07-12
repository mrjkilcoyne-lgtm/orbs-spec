# Media Streaming

## Scope
Video and audio delivery at scale: adaptive bitrate, CDNs, DRM (digital rights management), licensing, and managing variable network conditions.

## Core principles
- Adaptive bitrate (ABR) is essential: network speed changes mid-stream (WiFi → cellular), so bitrate adapts (1080p60 → 720p → 480p) without buffering; algorithms predict bandwidth based on chunk download history.
- CDNs (content delivery networks) cache content geographically; a user in Tokyo gets video from a Tokyo server, not US servers — latency and bandwidth matter.
- Licensing is complex: studios license content regionally (geo-blocking), temporally (contract expiry dates), and by user type (subscribers only, ad-supported); rights management is business logic.
- DRM (Widevine, FairPlay, PlayReady) encrypts content so it can't be copied; it's required for premium content but adds latency and complexity.
- Latency matters: live streaming (sports, events) tolerates 10–30 second delay; time-shift (DVR) tolerates hours; interactive (streaming games) requires <100ms; requirements shape architecture.

## Apex practices
- Use HLS (HTTP Live Streaming) or DASH (Dynamic Adaptive Streaming over HTTP) for ABR; chunks (short video segments) allow rapid bitrate switching.
- Implement quality ladder (available bitrates) based on content type and delivery capability (4G vs. WiFi); not every bitrate is useful.
- Cache aggressively but respect rights expiry: a cached video is worthless after licensing expires (midnight Tuesday).
- Monitor real-time metrics (buffering ratio, bitrate distribution, startup time) and alert on anomalies; streaming CDN quality degrades gradually and silently.

## Pitfalls
- Assuming constant bandwidth; mobile is bursty (4G can spike or drop suddenly).
- DRM implementation breaking on device OS updates; Widevine/FairPlay are black-box (no control if Apple changes them).
- Ignoring regional licensing; licensing a movie in US doesn't grant rights in UK (results in DMCA violations or geo-blocking breaks).

## Tools & references
Netflix tech blog (open-source tools), DASH spec (MPEG-DASH), HLS (Apple), Widevine/FairPlay (DRM), FFmpeg (transcoding), CDNs (Akamai, Cloudflare, AWS CloudFront).
