# Tier 1 Case: NASA CR-168031, Series 1, Test 1

Single row of cold jets into a heated isothermal crossflow, constant-area rectangular duct.
Validation case for the CFD setup.

Values marked (OCR) come from a text extraction of the 1982 scan and need confirming against
the original.

## Configuration

| Quantity | Value |
|---|---|
| Duct height H_o | 101.6 mm |
| Duct width | 304.8 mm |
| Orifice plate | 01/02/04 |
| Orifices | 6, single row, one wall |
| Orifice diameter D | 25.4 mm |
| Spacing S | 50.8 mm |
| S/D, H_o/D, S/H_o | 2, 4, 0.50 |
| Injection angle | 90° |
| Trip location | 152.4 mm upstream of injection |
| Measurement stations | X/H_o = 0.5, 0.75, 1.0, 1.5, 2.0 |

Source: CR-168031 Tables I and II, §3.1.2.

## Flow conditions

| Quantity | Value |
|---|---|
| V_main | 15.8 m/s (OCR) |
| T_main | 649.8 K (OCR) |
| V_jet, at vena contracta | 26.0 m/s (OCR) |
| T_jet | 308.1 K (OCR) |
| J | 5.74 (OCR) |
| Density ratio | 2.113 (OCR) |
| THEB, jet-to-total mass flow | 0.1759 (OCR) |
| Operating pressure | 101325 Pa (assumed) |

Source: Fig. 12 per-test header. Both streams are nonvitiated air, so the density ratio is a
temperature ratio and no species transport is needed.

Computed from the above at R = 287.10: rho_main = 0.543, rho_jet = 1.146 kg/m³, ratio 2.109,
J = 5.72, mainstream mass flow 0.266 kg/s. All within 0.3% of the reported values, which
confirms the pressure assumption.

## Effective jet diameter — unresolved

V_jet is defined at the vena contracta, D_j = D·sqrt(C_d). Three routes disagree:

| Route | D_j | C_d |
|---|---|---|
| Reported S/D_j = 2.443 | 20.79 mm | 0.670 |
| Mass balance from THEB | 20.10 mm | 0.626 |
| Nominal C_d = 0.60 | 19.67 mm | 0.600 |

6% in diameter is 11% in jet mass flow. J is unaffected. Current geometry uses
**D_j = 19.7 mm**; revise once S/D_j and THEB are confirmed. Define R = D_j/2 once in
`blockMeshDict` and derive the rest with `#calc`.

## Domain

Half-pitch slice, **470 × 101.6 × 25.4 mm**. Orifice centre at x = 152.4 mm.

x downstream, y duct height, z spanwise — matching the report, which gives penetration as
Y/H and the transverse direction as Z/S.

| Patch | Location | Type |
|---|---|---|
| inlet | x = 0 | 15.8 m/s +x, 649.8 K |
| outlet | x = 470 | 101325 Pa |
| jetInlet | half-disc at (152.4, 0, 0) | 26.0 m/s +y, 308.1 K |
| injectionWall | y = 0, remainder | noSlip, adiabatic |
| oppositeWall | y = 101.6 | noSlip, adiabatic |
| symmetryZ0 | z = 0, jet centreline | symmetry |
| symmetryZmax | z = 25.4, between jets | symmetry |

370 mm is rig hardware; the last 114 mm is outlet padding.

The jet is imposed on a patch of diameter D_j — no plenum, no orifice plate thickness. The
contraction is represented by reduced area, not resolved.

## Solver

`rhoSimpleFoam`, OpenFOAM ESI v2412. Steady, variable density, energy equation.

`heRhoThermo` / `perfectGas` / `sutherland` / `janaf`, molWeight 28.96. JANAF air
coefficients from Burcat & Ruscic ANL-05/20, AIR record. Verified: c_p = 1005.1 J/kg·K at
300 K, 1062.1 at 649.8 K, continuous across T_common.

k-omega SST baseline, realizable k-epsilon for comparison. Wall functions, y+ 30–300.

## Assumptions needing a sensitivity run

- **Inlet velocity profile.** No measured profile is reported. Penetration at low J depends
  on the approaching boundary layer, so this is first-order.
- **Inlet turbulence.** No intensity or length scale given for this series.

## Open items on the source data

1. Table III did not survive OCR. Configuration and conditions above are reconstructed from
   Table II and figure headers. Some figure-header digits are corrupted — reported blowing
   rates do not reconcile with the velocities — so J, velocities and temperature ratios are
   trusted and the rest needs the original scan.
2. Test 2's J (~21.59) is inferred, not read.
3. D_j, as above.

## References

- Srinivasan, Berenfeld & Mongia, NASA CR-168031 (1982)
- Burcat & Ruscic, ANL-05/20 (2005)
