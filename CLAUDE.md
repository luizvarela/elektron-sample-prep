# ElekPrep — Claude Code Instructions

## Project Overview
Browser-based sample preparation tool for Elektron hardware (Digitakt, Digitakt II, Analog Rytm, Model:Samples). Single-file HTML app (`index.html`, ~1300 lines) using the Web Audio API. No build system, no dependencies, no server.

## Architecture
- **Single file**: All HTML, CSS, and JS live in `index.html`
- **Audio processing**: Web Audio API (AudioContext, OfflineAudioContext)
- **Key functions**: `findZeroCrossings()`, `nearestZeroCross()`, `drawWaveform()`, `processAndExport()`
- **Device profiles**: `DEVICES` object defines sample rate, bit depth, channels, and max length per device
- **State**: Global `state` object tracks loaded buffer, trim points, and processing options

## Conventions
- Vanilla JS only — no frameworks, no npm, no bundler
- All processing runs client-side in the browser
- CSS custom properties for theming (dark theme, `--accent: #e8841a`)
- Monospace font for data, system sans-serif for UI text

## When Working on This Project

### Claude Code owns (think + architect + refactor)
- Architectural decisions (splitting into modules, adding features that touch multiple sections)
- Complex audio DSP logic (zero-crossing, resampling, normalization)
- Bug investigation and root-cause analysis
- Code review of Codex-generated changes
- Waveform rendering and canvas interaction logic
- Cross-browser compatibility issues

### Codex owns (execute + scaffold + iterate)
- Adding new device profiles to the `DEVICES` object
- CSS/styling tweaks and responsive layout fixes
- Straightforward UI additions (new buttons, toggles, labels)
- Writing tests in `test-samples/`
- Documentation updates (README, post drafts)
- Quick prototyping of isolated features

### Shared rules (both agents follow these)
- Never introduce npm, build tools, or external dependencies
- Keep everything in `index.html` unless there's a strong reason to split
- Preserve the existing dark theme and Elektron-inspired aesthetic
- Test audio changes with files from `test-samples/`
- All audio processing must remain 100% client-side
- Commit messages: imperative mood, concise (`Add Syntakt profile`, `Fix zero-cross at loop boundary`)

## File Map
```
index.html          — The entire app (HTML + CSS + JS)
test-samples/       — Audio files for manual testing
README.md           — Project description
LICENSE             — MIT
RESEARCH.md         — Background research (gitignored)
ELEKTRONAUTS_POST.md — Forum post draft
REDDIT_POST.md      — Reddit post draft
```

## Required Skills

### Frontend / UI Changes
**Always invoke the `frontend-design` skill** before implementing any UI or frontend change. This includes:
- CSS/styling modifications
- New UI components (buttons, panels, modals, controls)
- Layout changes or responsive adjustments
- Waveform display and canvas rendering updates
- Any visual change to `index.html`

This ensures polished, production-grade design that avoids generic AI aesthetics and preserves the Elektron-inspired dark theme.

### Rust (elekprep-transfer)
**Always invoke the `rust-best-practices` skill** before writing or modifying Rust code in `~/elekprep-transfer/`. This includes:
- New functions, modules, or crates
- Refactoring existing Rust code
- Error handling and ownership patterns
- Performance optimization
- Writing tests or documentation

Additional project-specific rules:
- Respect the CoreMIDI + SysEx architecture decisions documented in memory
- Keep unsafe blocks minimal and well-documented

## Dual-Agent Workflow
This project uses both Claude Code and OpenAI Codex. See `AGENTS.md` for Codex-specific instructions. The task split above defines ownership boundaries — when in doubt, Claude Code handles complexity, Codex handles velocity.
