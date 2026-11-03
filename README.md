# Proton dose in a transverse magnetic field

Run two FLUKA simulations to see how a uniform magnetic field changes the dose distribution of a 150 MeV proton pencil beam in water.

## Setup

The beam starts 0.001 cm inside a water phantom and travels along +z. The phantom is 20 × 10 × 30 cm. Both inputs use the same source, geometry, and 1 mm Cartesian dose grid. The field-on case applies a uniform 1.5 T field along +y inside the phantom. The proton initially bends toward −x because its charge is positive and the magnetic force points along **v × B**.

## Run and plot in Flair

1. Install CERN FLUKA, its required data libraries, and Flair. Open `field_off.inp` in Flair and save the project as `field_off.flair`. Repeat for `field_on.inp` in a separate Flair project.
2. In each project's Run tab, run five cycles. The decks specify 10,000 primaries per cycle. Check the run output for successful completion before processing.
3. In the Data tab, process the unit 21 USRBIN files together for each case. Each project should have its own merged dose result.
4. In the Plot tab, add a USRBIN plot for each merged result. Display x and z with the same narrow, symmetric y range around the beam plane. Use identical axis limits and a shared color scale.
5. Create a 1D projection along z over the full scoring grid to locate the Bragg peak. Then take a narrow z window near the peak and project onto x. Compare the lateral peak position or dose-weighted centroid between the two runs.

With FLUKA configured on your PATH, you can also run the simulations from this directory:

```sh
rfluka -N 0 -M 5 field_off.inp
rfluka -N 0 -M 5 field_on.inp
```

## What to look for

- With the field off, the dose distribution should be approximately symmetric about x = 0.
- With the field on, the high-dose region should shift toward negative x. As protons slow, their magnetic curvature increases.
- Report the lateral shift in millimeters and note the z interval used. A visual peak location is limited by the 1 mm grid and Monte Carlo noise. Increase the number of histories and check whether the measured shift stabilizes.

FLUKA's DOSE tally is absorbed dose per primary in GeV/g. Multiply by 1.602176634 × 10⁻⁷ to convert to Gy per primary. Keep the same normalization and projection settings in both cases. This is an idealized water-phantom exercise with a prescribed static field.

## References

- [CERN FLUKA installation](https://fluka.cern/documentation/installation)
- [CERN FLUKA beginner example and USRBIN plotting](https://fluka.cern/documentation/beginner_guide/example1)
- [CERN FLUKA magnetic-field examples](https://fluka.cern/documentation/examples/physics-transport-and-magnetic-fields)
