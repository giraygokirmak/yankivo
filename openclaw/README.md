# OpenClaw integration

This directory will contain the connector and protocol contract between Yankivo devices and
OpenClaw.

No working integration exists yet. Before implementation, the OpenClaw version, supported
plugin/tool API, and STT/TTS providers must be selected.

Planned responsibilities:

- Device registration and authentication
- Audio and control sessions
- STT → OpenClaw → TTS orchestration
- Response cancellation, timeouts, and connection errors
- Observability and integration tests without logging secrets

See [docs/architecture.md](../docs/architecture.md) for the target architecture.
