# Sound credits

## Active samples

- `skid.wav`: tires_squal_loop.wav — audible-edge / Tom Haigh; loop edit by qubodup. [Source](https://opengameart.org/content/car-tire-squeal-skid-loop), [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/). Excerpt, filtering, loudness adjustment, mono resampling; short runtime envelope and pitch change for corner/brake.
- `engine.wav`: **Import car revs on Chassis Dyno with Turbo** — editboy23.
  [Source](https://freesound.org/s/496171/), [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
  Chosen by listening. From **20.95s**, where the car is under load from the first frame — the level
  starts at 0.99 of the region's peak and the note climbs without a single frame going the other way,
  against 0.92 and 0.83 for the candidate this replaced. A dyno pull is inherently high load and high
  rpm, which is the character that was wanted.
  Resampled to **2.10×** so the engine reads as turning much faster, balanced band by band towards the
  weight of the old `revving-2` cut, then tapered over **300ms**: the recording is still at full level
  ten seconds later, so it has no ending of its own and one had to be made. 1.87s at -16.1dB RMS.
  Rebuild: `node --experimental-strip-types scripts/build-audio.mjs`.

  **This replaced a CC BY choice that sounded much the same.** That one obliged every deployment to
  carry its attribution; this one obliges nothing. The recording it replaced is kept unused at
  `source/c43-amg-exhaust-rev.mp3`, and its terms no longer apply to anything shipped.

- `engine.wav` 이전 판 (revision 28~29): Revving_2.ogg — FreeCarSoundsGaming.
  [Source](https://freesound.org/people/FreeCarSoundsGaming/sounds/535040/), CC0. Its cut is still the
  spectral reference the current sound is balanced against.

- `pop.wav`: Car race, Nordschleife, VLN, several cars passing by, backfire — Dominik_W. [Source](https://freesound.org/people/Dominik_W/sounds/350672/), [CC0](https://creativecommons.org/publicdomain/zero/1.0/). Author describes a Zoom H1 field recording. Public HQ MP3 preview retained as `source/nordschleife-backfire.mp3`. Three transient excerpts around 1.626, 10.356, 27.127 seconds are filtered, enveloped and arranged into seven varied-pitch attacks plus tail, total .94 seconds. This is an edited sound design made from a race recording, not an unedited recording of a single vehicle's exhaust sequence. Transients were selected by waveform analysis; final perceived realism needs listening review.

Rebuild the two new samples: `python3 scripts/build-exhaust-audio.py` (uses local ffmpeg-static). Downloaded 2026-09-15. No endorsement implied.

## FOUR RED scene (2026-09-17)

`fourred.wav`: [S63 AMG V8 Engine Revs](https://freesound.org/s/505321/) — marcelweiss,
[CC0](https://creativecommons.org/publicdomain/zero/1.0/). The **whole 6.2 second take**, high/low
passed at 40Hz/9kHz and levelled to the same RMS as `engine.wav`, kept whole in
`source/s63-amg-v8-revs.mp3`. It replaces the rev sample and pop sample the scene used to lay end to
end, so the engine note and its crackles stay the performance they were recorded as.

The take is **three throttle blips, each followed by crackle on the overrun**, and the muffler flares
in `src/core/after-hours-timeline.ts` are timed to all three: 20 flares in total.

| run | crackle | flares | peak strength |
|---|---|---:|---:|
| after blip 1 | 1.012–1.288s | 5 | 0.21 |
| after blip 2 | 2.070–2.425s | 7 | 0.88 |
| after blip 3 | 3.488–3.819s | 8 | 1.00 |

Strength is high band energy on one scale across the whole file, and flare radius is
`4 + sqrt(strength) * 7` — a square root, so the first run stays visible at a fifth the energy of the
third without flattening the difference the third has earned. The body shoves once per run, scaled
the same way.

**Two earlier notes here were wrong, both from measuring badly rather than from the recording.** The
first called the take a rev with no backfires: that pass thresholded the whole file at once, so
everything quieter than a wide open rev was discarded, and overrun crackle is exactly that. The
second found only the third run, because it went looking in the one stretch already known to be loud.
Above 2.2kHz the third run stands at 7 to 34 where the rest of the take sits at 1 to 6 — and the
first two runs live in that gap, which is why they need a local baseline to find at all.

## Retained former source

`source/engine-loop.wav` (original loop_0.wav) — domasx2. [Source](https://opengameart.org/content/racing-car-engine-sound-loops), CC0. Replaced for acceleration and pop in revision 28. The old three-gate exhaust sound is no longer used.

## Procedural character voice (revision 29)

`src/mutter.ts`: original harmonic/formant-style synthesis, no external voice recordings, cloned speakers or third-party speech service. Generated locally into Web Audio buffers; three utterance types with three pitch variants.

## Listening candidates

`scripts/build-audio.mjs` builds every shipped sound and the candidates for the choices still open —
skid and backfire — into `public/audio/candidates/`, and `/sound.html` plays them against what ships.
That directory is gitignored and never deployed: `scripts/prepare-pages.mjs` copies an allowlist.

**The exhaust ladder was removed once the exhaust was chosen**, along with the six recordings that
only fed it: BMW M6 [478597](https://freesound.org/s/478597/) CC0, M4
[335345](https://freesound.org/s/335345/) CC0, M3 [343369](https://freesound.org/s/343369/) CC BY 3.0,
Mercedes-AMG C43 [772801](https://freesound.org/s/772801/) CC BY 4.0, Mustang V8
[438069](https://freesound.org/s/438069/) CC0, VW Golf GTI [268626](https://freesound.org/s/268626/)
CC0. The links are kept so any of them can be fetched again; nothing shipped ever used them.

`pop.wav` is built by `scripts/build-exhaust-audio.py`, not by `build-audio.mjs`. Reimplementing its
assembly produced a result 7dB different from the file that ships — not a rounding difference — so the
original remains its builder of record.

`ffmpeg`'s `loudnorm` is not usable on clips this short; levelling happens in `build-audio.mjs`,
matching sustained sounds on RMS and impulsive ones on peak.

Two things the survey established about the race recording, worth not rediscovering:

- It holds four transients far sharper than the rest, at **1.62, 10.35, 38.82 and 70.2 seconds**. The
  shipped `pop.wav` uses 1.63, 10.36 and 27.13; 38.82 peaks at .315 against .063 for the 27.1 one.
- It holds three stretches over a second where the level barely moves, at **48.99, 88.34 and 4.35
  seconds** — cars passing at a steady throttle.
