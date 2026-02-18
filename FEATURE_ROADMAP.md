# ElekPrep Feature Roadmap

Based on community feedback. Implementing one at a time.

## Status

| # | Feature | Status | Lines |
|---|---------|--------|-------|
| 1 | Drag entire trim region | **Done** | ~40 |
| 2 | Loop playback (with drag) | **Done** | ~50 |
| 3 | Zoom in/out + minimap | **Next** | ~180 |
| 4 | Batch import/conversion | Planned | ~160 |

---

## Feature 1: Drag Entire Trim Region

**User request:** "Select a start point, choose tempo and beats for a perfect loop, then drag the whole area around to find interesting loops."

**Implementation:**
- In `mousedown`: if click is between handles (not near either), set `state.dragging = 'region'`, record `state.dragLastX`
- In `mousemove`: when `dragging === 'region'`, compute delta, shift both `trimStart` and `trimEnd` by the same amount
- Zero-cross snapping disabled during region drag (would change loop length)
- Cursor: `grab` on hover between handles, `grabbing` while dragging, `col-resize` near handles
- State addition: `dragLastX: 0`; `state.dragging` gains value `'region'`

---

## Feature 2: Loop Playback

**User request:** "Cool if loop playback worked at the same time as dragging the loop too."

**Implementation:**
- Add "Loop Preview" button (3rd button in playback row)
- Use `BufferSource.loop = true` with `loopStart`/`loopEnd` on original buffer (no expensive processing)
- New `restartLoopIfPlaying()` with 80ms debounce, called during handle and region drag
- Modify `stopPlayback()` to clean up loop state

---

## Feature 3: Zoom In/Out

**User request:** "Would be nice if you could zoom in and out, to really be able to trim precisely."

**Implementation:**
- State: `viewStart`, `viewEnd` (sample indices for visible range)
- Mouse wheel zoom centered on cursor position
- `+`/`-`/`Fit` buttons + zoom level % indicator
- Minimap canvas (24px) below main waveform with viewport indicator + click-to-scroll
- New helpers `sampleToPixel()`/`pixelToSample()` — all coordinate math goes through these
- Keyboard shortcuts: `+`/`-` zoom, `0` fit, arrows scroll
- Rewrite `drawWaveform()` to render only visible range

---

## Feature 4: Batch Import/Conversion

**User request:** "I have a folder full of one-shots that are currently incompatible with my AR. Bulk or batch conversion would be a great addition."

**Implementation:**
- "Batch Convert" section with toggle, multi-file drop zone, file list, "Convert All" button
- Refactor `processBuffer()` into reusable `processAudioBuffer(buffer, trimStart, trimEnd, device, options)`
- New `processBatchFile()`: decode → auto zero-cross trim → process → encode WAV
- Sequential download with 200ms delay (or File System Access API for Chrome/Edge)
- Per-file status: pending/processing/done/error

---

## Refactoring Note
Before Feature 4, extract the audio processing pipeline from `processBuffer()` into a shared function to avoid ~60 lines of duplication.
