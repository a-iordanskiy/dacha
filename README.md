# Dacha Horror — Technical Sound Design Project

First-person atmospheric walking sim with a stalking presence. Portfolio piece demonstrating UE5 + Wwise audio systems work.

## Continuous Anxiety (RTPC-driven adaptive music)

- `Anxiety` RTPC (0–100) drives a Wwise **Music Segment Container**, crossfading music stems as tension rises and falls.
- `BP_AnxietyZone` — reusable Blueprint with an editable `Rate`. Trigger Volumes add/remove `AnxietyRate` on the player while overlapped.
- Integrated every Tick (`Anxiety += AnxietyRate * DeltaTime`, clamped 0–100), pushed to Wwise continuously via `SetRTPCValue`.

## Threshold events

Presence beats fire on **threshold-crossing** of Anxiety via a reusable `CheckThresholdCrossing` function. Bush rustle and flashlight flicker are repeatable (hysteresis-gated); door creak and Game Over are one-shot.

Each reaction is self-contained on its own actor (`BP_BushSource`, `BP_DoorSource`, `BP_StreetLamp`) with its own AkComponent and a `PlaySFX`/`PlayFlicker`/`BreakLamp` custom event.

## Flashlight flicker

Three `BP_StreetLamp` actors (Point Light + Timeline-driven intensity flicker), found via `Get All Actors Of Class`. One instance is flagged breakable and permanently breaks at a separate Anxiety threshold — light off, break sound, one-shot Niagara spark burst.

## Footstep surfaces

Footstep sound is selected via a **Wwise Switch Container**, set from the surface material Unreal detects under the player at footstep time (`Footstep_Surface-Asphalt` / `-Grass` / `-Wood`).

## Ambience

Light ambience track (wind) plus one-shot wildlife emitters (owls, cicadas, crows) via Wwise AkComponent Random Containers for non-repetitive variation.

## What's not included

- **Fab asset packs** (`Environment`, `Modular_Rural_Cabin`, `Characters`) — licensing. Levels will show missing-asset placeholders without them.
- **Wwise Unreal Integration plugin** (`Plugins/Wwise*`) — third-party SDK, install separately.
- **Generated SoundBanks** — regenerate from `Dacha_Horror_WwiseProject`.

## Requirements

UE5 5.8 (5.7 fallback) + Wwise 2025.1.9 with matching Unreal Integration.
