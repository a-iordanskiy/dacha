# Dacha Horror — Technical Sound Design Project

First-person atmospheric walking sim with a stalking presence. Portfolio piece demonstrating UE5 + Wwise audio systems work.

## Continuous Anxiety (RTPC-driven adaptive music)

- `Anxiety` RTPC (0–100) drives a Wwise **Music Segment Container**, crossfading music stems as tension rises and falls.
- `BP_AnxietyZone` — reusable Blueprint with an editable `Rate`. Trigger Volumes add/remove `AnxietyRate` on the player while overlapped.
- Integrated every Tick (`Anxiety += AnxietyRate * DeltaTime`, clamped 0–100), pushed to Wwise continuously via `SetRTPCValue`.

## Threshold events

Presence beats (bush rustle, flashlight flicker, door creak) fire on **threshold-crossing** of Anxiety, with hysteresis to prevent re-triggering — one reusable pattern, not bespoke logic per event.

A terminal **Game Over** threshold at Anxiety 100: disables input, plays a stinger, reloads the level.

## Footstep surfaces

Footstep sound is selected via a **Wwise Switch Container**, set from the surface material Unreal detects under the player at footstep time (`Footstep_Surface-Asphalt` / `-Grass` / `-Wood`).

## What's not included

- **Fab asset packs** (`Environment`, `Modular_Rural_Cabin`, `Characters`) — licensing. Levels will show missing-asset placeholders without them.
- **Wwise Unreal Integration plugin** (`Plugins/Wwise*`) — third-party SDK, install separately.
- **Generated SoundBanks** — regenerate from `Dacha_Horror_WwiseProject`.

## Requirements

UE5 5.8 (5.7 fallback) + Wwise 2025.1.9 with matching Unreal Integration.
