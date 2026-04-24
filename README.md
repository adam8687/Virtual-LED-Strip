# Virtual LED Strip

A LabVIEW-based virtual LED strip simulator for FRC robots. Test and preview lighting patterns on your dashboard without any physical hardware.

---

## Overview

`LightStrip25.vi` simulates an addressable LED strip inside LabVIEW. It runs a state machine that writes lighting patterns to an LED array in real time, letting you verify animations and colours before deploying to the robot. The VI can be embedded directly in your driver-station dashboard so the rest of your team can see what the robot's lights are doing (or are supposed to be doing) at any moment.

> **Note:** The simulator may take a couple of seconds to load a new pattern — this is normal.

---

## Repository Structure

```
Virtual-LED-Strip/
├── LICENSE
└── LedStrip25/
    ├── LightStrip25.vi          # Main virtual strip VI (entry point)
    ├── LedControlStates.ctl     # Enum of available LED control states
    └── BlingLibrary/            # Reusable LED-animation library
        ├── ArduinoSerialBling.lvlib
        ├── Demo.vi              # Stand-alone demo of all patterns
        ├── ConnectionType.ctl   # Serial vs. UDP selector
        ├── TransmissionType.ctl
        ├── UdpConnection.ctl
        ├── ChainSetup.ctl
        ├── ChainState.ctl
        ├── ControlState.ctl
        ├── ValueWidth.ctl
        ├── Verbosity.ctl
        ├── WriteLedArrayStatus.ctl
        │
        ├── ── Pattern generators ──
        ├── GenBlink.vi
        ├── GenBreathe.vi
        ├── GenFade.vi
        ├── GenGradient.vi
        ├── GenKnightRider.vi
        ├── GenPolice.vi
        ├── GenRainbow.vi
        ├── GenRandom.vi
        ├── GenSolid.vi
        │
        └── ── Utility VIs ──
            ├── ApplyColorGain.vi
            ├── CheckAndRefresh.vi
            ├── CloseBling.vi
            ├── GetChainNumbersFromMask.vi
            ├── GetChainState.vi
            ├── GetChannelMask.vi
            ├── GetChannelMaskFromChainNumber.vi
            ├── GetEnabledChains.vi
            ├── GetLedStates.vi
            ├── GetNumLeds.vi
            ├── GetState.vi
            ├── GetValueStringFromColor.vi
            ├── Iterator.vi
            ├── OpenBling.vi
            ├── PeriodicTimer.vi
            ├── Reset.vi
            ├── ResetChainValues.vi
            ├── SetChainLength.vi
            ├── SetChainMask.vi
            ├── SetValue.vi
            ├── SetValueWidth.vi
            ├── SetVerboseMode.vi
            ├── SineWave.vi
            ├── UpdateRefreshTimes.vi
            ├── Wait.vi
            ├── WaitOnSync.vi
            ├── WriteData.vi
            └── WriteLedArray.vi
```

---

## Requirements

| Requirement | Details |
|---|---|
| **LabVIEW** | 2023 or later (project files target 23.x) |
| **FRC Game Tools** | Recommended for dashboard integration |
| **Hardware** | None — purely software simulation |

---

## Getting Started

1. **Open the project** — launch `BlingLibrary/BlingBoard.lvproj` in LabVIEW.
2. **Run the main VI** — open and run `LedStrip25/LightStrip25.vi`.
3. **Select a pattern** — use the `LedControlStates` control on the front panel to pick an animation state.
4. **Watch the strip** — the LED array indicator updates in real time to show the active pattern.
5. **Dashboard integration** — drag the strip indicator onto your FRC dashboard panel so the animation is visible during matches.

To explore each pattern in isolation, open and run `BlingLibrary/Demo.vi`.

---

## Available Patterns

| Pattern | VI | Description |
|---|---|---|
| **Solid** | `GenSolid.vi` | All LEDs set to a single colour |
| **Blink** | `GenBlink.vi` | Strip toggles on and off at a configurable rate |
| **Breathe** | `GenBreathe.vi` | Brightness fades in and out smoothly |
| **Fade** | `GenFade.vi` | Transitions between two colours |
| **Gradient** | `GenGradient.vi` | Smooth colour gradient across the strip |
| **Rainbow** | `GenRainbow.vi` | Scrolling rainbow across all LEDs |
| **Knight Rider** | `GenKnightRider.vi` | Single bright pulse bouncing back and forth |
| **Police** | `GenPolice.vi` | Alternating red/blue flashing |
| **Random** | `GenRandom.vi` | Each LED assigned a random colour |

---

## Connection Types

The `BlingLibrary` supports two output transports (selected via `ConnectionType.ctl`):

- **Arduino Serial** (`ArduinoSerialBling.lvlib`) — sends LED data over a USB serial connection to an Arduino that drives the physical strip.
- **UDP** (`UdpConnection.ctl`) — broadcasts LED state over the network, useful for remote monitoring or alternative hardware targets.

When using the virtual strip for simulation only, no connection needs to be configured.

---

## License

This project is released under the [MIT License](LICENSE).  
Copyright © 2025 Adam Mohiuddin.
