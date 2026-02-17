# ElekPrep

Free browser-based sample prep tool for Elektron devices. No install, no account, nothing leaves your machine.

**https://luizvarela.github.io/elektron-sample-prep/**

## What it does

Drop any audio file in, pick your device, get a click-free WAV ready to load via Transfer or Elektroid.

- **Auto zero-cross trim** — Snaps trim points to where the waveform crosses zero, eliminating clicks and pops at sample boundaries
- **Format conversion** — Converts to 48kHz / 16-bit automatically. Handles resample, bit depth reduction, and stereo-to-mono downmix
- **Device profiles** — Digitakt, Digitakt II, Analog Rytm, Model:Samples. Sets the correct target format and warns about length limits
- **Loop calculator** — Enter BPM and step count, get a mathematically perfect loop length. No more gaps from inaccurate internal recording
- **Normalize** — Optional -1dB peak normalization
- **A/B preview** — Listen to original vs. processed before exporting

## Supported formats

WAV, AIFF, MP3, FLAC, OGG — anything your browser can decode.

## How it works

Single HTML file using the Web Audio API. All processing happens locally in your browser. No server, no upload, no dependencies.

## License

MIT
