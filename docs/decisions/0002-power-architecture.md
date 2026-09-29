# ADR 0002 — Power architecture: protected input → buck, reset allowed during crank

**Status:** Proposed
**Date:** 2026-09-29

## Context

The input stage must survive a 12 V vehicle supply: reverse polarity, clamped-residual load dump (~35 V) and conducted transients.

The earlier power spec (archived repo `Automotive-power-supply`) targeted a safety-relevant VCU and required no reset down to a ~3 V diesel crank. That requirement forced a 4-switch buck-boost (LM5176-Q1). This board is a dev board, not a safety ECU, and has no requirement to operate through crank.

## Decision

```
Vin --[P-FET reverse]--[load-dump TVS]--[bulk C + ferrite]--> 60 V sync buck --> 5 V
                                                                          |
                                                    5 V --> buck or LDO --> 3.3 V
USB VBUS --[ORing]--> 5 V
```

- Keep the input stage exactly as locked in the earlier spec: P-FET, SM8S/SLD-class TVS, filter.
- Stage 1: synchronous buck rated to 60 V input, automotive grade. **[DECIDE]** part.
- Stage 2: 5 V → 3.3 V. **[DECIDE]** small buck vs LDO. At a 500 mA ceiling, an LDO dissipates (5 − 3.3) × 0.5 ≈ 0.85 W — check package thermal resistance before choosing it.
- The board may reset during deep crank and must recover cleanly (requirement PWR-08).

## Alternatives considered

| Option | Why not for Rev A |
|---|---|
| LM5176-Q1 4-switch buck-boost | Survives crank but adds 4 external FETs, current sense, two hot loops. Too much risk for a first board whose goal is shipping. Planned as a separate learning board after Rev A works. |
| Integrated automotive buck-boost | Simpler than LM5176, but many integrated parts have ~40 V abs-max: thin margin against the TVS clamp voltage. Revisit only if crank survival becomes a requirement. |
| Non-synchronous buck (e.g. LM2596) | 40 V abs-max, 150 kHz, poor efficiency and EMI. Rejected. |

## TVS calculation

**[TODO]** Fill in once the part is chosen:

| Quantity | Value | Source |
|---|---|---|
| V_RWM | | datasheet |
| V_BR (min) | | datasheet |
| V_CL at I_PP_rated | | datasheet |
| R_D | | datasheet or derived |
| I_PP_actual (clamped residual) | | analysis |
| V_CL_actual | | formula in PWR-06 |
| Downstream abs-max (buck VIN) | | buck datasheet |
| Margin | | |

## Consequences

- Board resets during deep crank. Documented limitation, not a defect.
- Stage 1 choice sets the input abs-max that the TVS must stay under.
- 5 V ORing between USB VBUS and the buck output is required (RAIL-03).
