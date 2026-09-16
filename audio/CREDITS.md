# Sound credits

## Active samples

- `skid.wav`: tires_squal_loop.wav — audible-edge / Tom Haigh; loop edit by qubodup. [Source](https://opengameart.org/content/car-tire-squeal-skid-loop), [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/). Excerpt, filtering, loudness adjustment, mono resampling; short runtime envelope and pitch change for corner/brake.
- `engine.wav`: Revving_2.ogg — FreeCarSoundsGaming. [Source](https://freesound.org/people/FreeCarSoundsGaming/sounds/535040/), [CC0](https://creativecommons.org/publicdomain/zero/1.0/). Author describes a lavalier microphone recording edited in FL Studio. Public HQ MP3 preview retained as `source/revving-2.mp3`; excerpt, high/low-pass, loudness adjustment, fades; 1.25 seconds, no looping or artificial pitch ramp.
- `pop.wav`: Car race, Nordschleife, VLN, several cars passing by, backfire — Dominik_W. [Source](https://freesound.org/people/Dominik_W/sounds/350672/), [CC0](https://creativecommons.org/publicdomain/zero/1.0/). Author describes a Zoom H1 field recording. Public HQ MP3 preview retained as `source/nordschleife-backfire.mp3`. Three transient excerpts around 1.626, 10.356, 27.127 seconds are filtered, enveloped and arranged into seven varied-pitch attacks plus tail, total .94 seconds. This is an edited sound design made from a race recording, not an unedited recording of a single vehicle's exhaust sequence. Transients were selected by waveform analysis; final perceived realism needs listening review.

Rebuild the two new samples: `python3 scripts/build-exhaust-audio.py` (uses local ffmpeg-static). Downloaded 2026-09-15. No endorsement implied.

## Retained former source

`source/engine-loop.wav` (original loop_0.wav) — domasx2. [Source](https://opengameart.org/content/racing-car-engine-sound-loops), CC0. Replaced for acceleration and pop in revision 28. The old three-gate exhaust sound is no longer used.

## Procedural character voice (revision 29)

`src/mutter.ts`: original harmonic/formant-style synthesis, no external voice recordings, cloned speakers or third-party speech service. Generated locally into Web Audio buffers; three utterance types with three pitch variants.
