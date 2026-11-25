# Firmware

This directory is reserved for firmware running on the ESP32-WROOM / NodeMCU-32S.

There is no buildable firmware yet. The initial implementation will:

1. Validate the I2S clock and data lines documented in [hardware/README.md](../hardware/README.md).
2. Test the microphone and MAX98357A drivers separately.
3. Add amplifier control on GPIO27 and an audio loop.
4. Implement secure Wi-Fi streaming and configuration.
5. Document verified build/flash commands and provide an example configuration here.

Network credentials and secrets must not be written into source files or Git history.
