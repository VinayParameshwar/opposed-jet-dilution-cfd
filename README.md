# Opposed-Jet Dilution Mixing in an RQL Combustor

3D RANS study of dilution jets in a confined crossflow, testing how well a tubular-liner
penetration correlation predicts penetration and mixing when applied to opposed in-line jets
in a square duct.

**Status: Phase 0 — case setup. No results yet.**

## The question

Dilution-zone injectors are commonly sized from a target penetration depth using a
correlation derived for round jets into a tubular liner, injected from one side. Applying it
to a square duct with opposed in-line injection takes it outside its derivation envelope in
three ways, and the correlation evaluates penetration only — not mixing quality or exit
temperature uniformity. This project quantifies the error with CFD.

Background and references: [`docs/motivation.md`](docs/motivation.md)

## Validation

Two tiers, since the target configuration has no public data.

1. Validate the setup against NASA CR-168031 (*Dilution Jet Mixing Program Phase I*, 1982),
   public domain, comparing the dimensionless temperature
   `THETA = (T_m - T) / (T_m - T_j)`.
2. Apply the validated setup to a square duct with opposed in-line injection, sweeping
   momentum flux ratio and injector geometry.

Case conditions, domain and solver setup: [`docs/tier1_case.md`](docs/tier1_case.md)

## Progress

- [x] Solver selection
- [x] Thermophysical properties, coefficients verified
- [x] Domain and O-grid topology designed
- [ ] blockMeshDict
- [ ] Boundary conditions
- [ ] THETA profiles digitised from CR-168031
- [ ] First converged run
- [ ] Mesh independence (GCI)
- [ ] Validation against experiment

## References

- Srinivasan, Berenfeld & Mongia, NASA CR-168031 (1982)
- Lefebvre & Ballal, *Gas Turbine Combustion*, 3rd ed., CRC Press (2010), Ch. 4
- Burcat & Ruscic, ANL-05/20 (2005)