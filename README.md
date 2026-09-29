# STM32G4 Automotive Dev Board

A single-CAN STM32G4 development board with a power input stage designed for a 12 V vehicle supply: reverse polarity, load dump residual and conducted transients.

## Status

**Rev A — requirements.** No schematic yet.

Progress is tracked by git tags, not by this README:

| Tag | Meaning |
|---|---|
| `rev-a-requirements` | `docs/requirements.md` frozen |
| `rev-a-schematic` | All sheets wired, ERC clean, self-reviewed |
| `rev-a-layout` | DRC clean, fab outputs generated |
| `rev-a-bringup` | Boards built, `docs/bringup-log.md` complete |

## Scope

See [docs/requirements.md](docs/requirements.md). Anything not listed there is out of scope for Rev A.

## Repository layout

```
docs/requirements.md   What Rev A must do, and how each item is verified
docs/decisions/        One record per design decision (why, alternatives, consequences)
docs/bringup-log.md    Measurements and anomalies from bring-up
hardware/              KiCad project
firmware/              Bring-up and example firmware (after Rev A boots)
```

## Author

Vaibhav Kadam — [@phoenix-prog](https://github.com/phoenix-prog)
