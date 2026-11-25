# Yankivo

<div align="center">
  <img src="assets/brand/yankivo-logo.svg" alt="Yankivo" width="760">

  **An open-source, ESP32-based voice interface for OpenClaw**

  Listen. Think. Echo.
</div>

> **Status:** The project skeleton and hardware documentation are under development. This
> repository does not yet contain working firmware or an OpenClaw integration.

Yankivo aims to turn an ESP32-WROOM-based NodeMCU-32S and a Google AIY Voice HAT into a
minimal, open voice peripheral for OpenClaw. The name combines the Turkish word "yankı"
("echo") with the idea of voice.

ESP32 handles microphone capture, audio output, and microphone status indication. Audio is
transported over Wi-Fi; speech-to-text, the agent, and text-to-speech run on a server so the
microcontroller does not need to perform those workloads locally.

## Features

- Full-duplex or half-duplex audio over I2S on an ESP32
- Reusable board and pin mappings, with the mapping for this setup in `hardware/README.md`
- An OpenClaw connector layer that forwards microphone audio and plays back responses
- A clear, server-side pipeline for STT, the agent, and TTS
- No third-party API key or Wi-Fi credential baked into the firmware source

## Architecture

```
Microphone ──I2S──> ESP32 ──Wi-Fi──> Server (OpenClaw + STT + TTS)
                                      │
Speaker ───<──I2S─── ESP32 <──Wi-Fi───┘
```

The ESP32 streams captured audio to the server and receives synthesized speech to play.
The server-side connector and protocol are defined separately; see `docs/architecture.md`.

## Repository layout

- `firmware/` — ESP32 firmware (Arduino or ESP-IDF) and board configuration
- `hardware/` — Pin mappings, wiring notes, and hardware constraints
- `openclaw/` — OpenClaw integration notes and connector design
- `docs/` — Architecture, protocol, and development documentation
- `assets/brand/` — Logo and icon source files

## Getting started

Read `docs/architecture.md` for the system design and `hardware/README.md` for the wiring
used by this project. No firmware build or flashing instructions are included yet; those will
be added once the first working firmware lands.

## Branding

The Yankivo logo and icon are provided as SVG and PNG in `assets/brand/`. The wordmark uses
a custom geometric, all-lowercase geometric treatment with a microphone between radiating
echo arcs. See `assets/brand/README.md` for colors and usage guidance.

## License

MIT. See `LICENSE`, copyright Macit Giray Gökırmak, 2026.

## Contributing

This project is in an early skeleton phase. If you would like to help shape the firmware,
protocol, or integration, please open an issue describing your idea before submitting a large
pull request.
