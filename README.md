# system-flare

Rapid system halt with state preservation - emergency stop that saves work-in-progress before shutdown.

## Overview

Part of the [ambientops](https://github.com/hyperpolymath/ambientops) platform for system resilience.

`system-flare` provides a "panic button" for graceful emergency shutdown. When triggered, it rapidly saves all work-in-progress, notifies connected services, and performs a clean halt - preventing data loss while stopping the system quickly.

## Concept

```
┌─────────────────────────────────────────────────────────────┐
│                    FLARE TRIGGERED                          │
│                    (Hotkey / API / Hardware)                │
│                                                              │
│  ┌──────────┐    ┌──────────────┐    ┌──────────────────┐   │
│  │ Interrupt│───▶│ Save State   │───▶│ Notify Services  │   │
│  │ Handler  │    │   - Buffers  │    │   - Sync repos   │   │
│  │          │    │   - Sessions │    │   - Close conns  │   │
│  │          │    │   - Drafts   │    │   - Alert admins │   │
│  └──────────┘    └──────────────┘    └──────────────────┘   │
│                                                ▼             │
│                                       ┌──────────────────┐   │
│                                       │   Clean Halt     │   │
│                                       │   (< 5 seconds)  │   │
│                                       └──────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

## Features (Planned)

- **Hotkey trigger**: Configurable keyboard shortcut (e.g., Ctrl+Alt+F12)
- **Hardware button**: USB panic button support
- **API endpoint**: Remote trigger via authenticated API
- **Priority queue**: Save most critical data first
- **Service notification**: Gracefully disconnect from remote services
- **Fast execution**: Target < 5 seconds from trigger to halt

## Use Cases

1. **System instability detected**: Before a crash, trigger flare to save state
2. **Security incident**: Rapid shutdown to prevent data exfiltration
3. **Physical security**: Quick halt when leaving workstation
4. **Thermal emergency**: Safe shutdown before hardware damage

## Related Projects

| Project | Relationship | Description |
|---------|--------------|-------------|
| [ambientops](https://github.com/hyperpolymath/ambientops) | Parent | Umbrella platform |
| [system-freeze-ejector](https://github.com/hyperpolymath/system-freeze-ejector) | Sibling | Off-machine dump on freeze |
| [system-emergency-room](https://github.com/hyperpolymath/system-emergency-room) | Sibling | Triage and stabilization |

## License

AGPL-3.0-or-later
