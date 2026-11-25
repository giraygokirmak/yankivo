# Yankivo architecture

This document describes the target design. It does not claim that a communication protocol
or production-ready system has been implemented.

## System components

### 1. ESP32 firmware

- I2S microphone and MAX98357A amplifier drivers
- Sampling, framing, and audio buffering
- Amplifier enable/shutdown and error handling
- Wi-Fi and device identity configuration
- Sending audio to the server, playing received audio, and maintaining the connection

### 2. OpenClaw connector

- Device authentication and session lifecycle
- Integration with speech-to-text (STT) and text-to-speech (TTS) providers
- Mapping OpenClaw requests and responses to device sessions
- Queueing, cancellation, and timeout handling for audio streams

The connector's design will be finalized according to the OpenClaw environment and the
selected integration API.

### 3. Audio and control protocol

The following points should be documented as an explicit contract before the first
implementation:

| Topic | Proposed approach |
| --- | --- |
| Transport | WebSocket with TLS or equivalent secure streaming |
| Authentication | A device token, kept outside the repository |
| Control messages | Versioned, schema-validated JSON |
| Audio packets | Binary frames containing a header, sequence number, and timing information |
| Initial format | PCM; evaluate Opus later if bandwidth requires it |
| Sampling | To be decided with the STT/TTS providers; initial proposal is 16 kHz / 16-bit / mono |
| Reliability | Heartbeats, reconnection, timeouts, and bounded buffers |

These values are starting decisions for a prototype, not a binding contract.

## Session flow

1. The device initializes its configuration and audio drivers.
2. It establishes an authenticated connection to the server and reports its capabilities.
3. It sends microphone frames, optionally adding voice activity information.
4. The connector manages the STT, OpenClaw, and TTS stages.
5. The response audio is streamed to the device, and the amplifier is enabled only during
   playback.
6. A new request, cancellation, or disconnection safely stops current playback.

## Security principles

- Wi-Fi, server, STT/TTS, and OpenClaw credentials must never be committed to the repository.
- TLS certificate verification must not be disabled in production connections.
- Device tokens should be revocable and can be specific to a single device.
- It must be clearly visible when the microphone is transmitting.
- Secrets and personal conversation content must not be written to logs.

## Development milestones

- **Stage 0 — Hardware validation:** Power, pins, independent microphone and speaker tests.
- **Stage 1 — Audio loop:** Microphone-to-amplifier loop and level measurements without the
  network.
- **Stage 2 — Secure streaming:** A versioned protocol, device sessions, and reconnection.
- **Stage 3 — OpenClaw:** STT/agent/TTS integration and end-to-end responses.
- **Stage 4 — Productization:** Configuration interface, tests, enclosure, and setup guide.
