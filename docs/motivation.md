# Motivation

## The design practice being examined

Dilution-zone injector geometry — orifice number and diameter — is commonly selected from a
target jet penetration depth. The governing correlation is

    Y_max / d_j = 1.25 * J^0.5 * (m_dot_g / (m_dot_g + m_dot_j))

where J is the jet-to-mainstream momentum flux ratio and the bracketed term is a mass-flow
correction.

Lefebvre & Ballal eq. 4.20 is used for estimating the maximum
penetration of round air jets **into a tubular liner**. The mass-flow term is a blockage
correction: Sridhara found multiple jets penetrate less than a single jet, and attributed
this to the jets raising the local mainstream velocity inside the liner.

The companion single-jet relation, Lefebvre & Ballal eq. 4.19, is

    Y_max / d_j = 1.15 * J^0.5 * sin(theta)

Both describe maximum penetration. A separate trajectory relation (eq. 4.18) predicts
penetration increasing without limit with downstream distance, and such
expressions are useful only for the initial portion of the trajectory and lose validity as
the jet centreline becomes asymptotic to the crossflow.

## Where the application exceeds the derivation

Applying eq. 4.20 to a square duct with opposed in-line injection departs from its basis in
three ways.

**Geometry.** The correlation was derived for a tubular liner. Its blockage term encodes a
confinement effect specific to that cross-section.

**Opposed injection.** The correlation was derived for single-sided injection and contains no
term representing a jet arriving from the opposite wall. 

**Design point location.** Opposed in-line jets are designed to meet near the duct
centreline. That places the design point where the correlation's own source says its accuracy
degrades.

## What the correlation does not evaluate

Penetration is an intermediate quantity. The design objective is the exit temperature
profile: the pattern factor the turbine inlet requires, with no hot core from
under-penetration and no cold core from over-penetration.

A penetration-based criterion returns a geometry but produces no mixing metric and no exit
temperature distribution. Whether the geometry it selects also minimises unmixedness is not
tested by the method that selected it.

## Research question

> For opposed in-line jets in a square duct, how large is the penetration error of a
> tubular-liner correlation used as a design rule, and does the configuration it selects also
> minimise unmixedness and exit temperature non-uniformity?

## Why validation is two-tier

No public experimental data exists for the target configuration, so the CFD cannot be
validated against it directly.

Instead the setup is validated against published data for a related configuration — a single
row of jets in a confined rectangular crossflow, from the NASA Dilution Jet Mixing Program —
and then applied to the target configuration. This is standard practice, but the transfer is
an assumption, not a demonstration, and is stated as such wherever results are reported.

Validating on a single row also yields the single-sided baseline the research question
compares against, so it is not preparatory work alone.

## Prior expectation on the numerical method

RANS is known to underpredict downstream mixing in confined
jet-in-crossflow configurations; NASA TM-105699 reports this for the same flow class.
Reproducing that behaviour is therefore a check on the setup rather than a failure of it, and
the quantified gap is reported rather than minimised.

A turbulence model comparison (k-omega SST against realizable k-epsilon) provides a
model-form uncertainty band on the applied results.

## References

- Lefebvre, A.H. & Ballal, D.R., *Gas Turbine Combustion: Alternative Fuels and Emissions*,
  3rd ed., CRC Press (2010), Ch. 4
- Srinivasan, R., Berenfeld, A. & Mongia, H.C., *Dilution Jet Mixing Program, Phase I*,
  NASA CR-168031 (1982)
- Holdeman, J.D. et al., *CFD Mixing Analysis of Jets Injected Into Confined Crossflow in
  Rectangular Ducts*, NASA TM-105699 (1992)
