# Light Lab — Interactive Beer–Lambert Simulator

## The science

### 1. Transmittance

When a beam of light passes through a sample, some of the incident radiant intensity may be absorbed. Let:

- *I*₀ = incident radiant intensity
- *I* = transmitted radiant intensity

Transmittance is:

> **T = I / I₀**

Percent transmittance is:

> **%T = 100 × T**

Transmittance is a ratio and is dimensionless.

### 2. Why intensity attenuation is exponential

Consider a thin layer of solution with thickness *dx*. For a homogeneous absorbing medium, assume the loss of intensity in this thin layer is proportional to:

- the intensity *I* entering the layer;
- the concentration *c* of absorbing species;
- the thickness *dx*.

Thus:

> **−dI = k · I · c · dx**

where *k* is a proportionality constant for the chosen absorbing species and wavelength.

Separate variables:

> **−dI / I = k · c · dx**

Integrate across the sample, from incident intensity *I*₀ to transmitted intensity *I*, and from position 0 to path length *b*:

> **−∫ (dI / I) = k · c · ∫ dx** &nbsp; *(from I₀ to I, and 0 to b)*

Therefore:

> **ln(I₀ / I) = k · b · c**

Rearranging gives the exponential attenuation expression:

> **I = I₀ · e^(−kbc)**

Dividing by *I*₀:

> **T = e^(−kbc)**

This exponential relationship explains why transmittance is not generally linear in concentration.

### 3. Define absorbance

Take the common (base-10) logarithm of the intensity ratio:

> **A = log₁₀(I₀ / I)**

Since *T* = *I* / *I*₀:

> **A = −log₁₀(T)**

Using the conversion ln(*x*) = 2.303 log₁₀(*x*):

> **A = (k / 2.303) · b · c**

Define the molar absorptivity (*ε*):

> **ε = k / 2.303**

The Beer–Lambert law follows:

> **A = ε · b · c**

where:

- *A* = absorbance (dimensionless; often reported in absorbance units, AU);
- *ε* = molar absorptivity, typically L mol⁻¹ cm⁻¹;
- *b* = optical path length, cm;
- *c* = concentration, mol L⁻¹.

For fixed wavelength, chemical species, solvent conditions, and path length, absorbance is proportional to concentration over the range where Beer–Lambert behaviour is valid.

### 4. Why absorbances add for independent absorbers

For two independent absorbing species, X and Y, at the same wavelength:

> **A_X = ε_X · b · c_X**  
> **A_Y = ε_Y · b · c_Y**

The attenuation factors multiply:

> **T_mixture = T_X × T_Y**

Taking negative base-10 logarithms converts that product into a sum:

> **A_mixture = A_X + A_Y**

Thus:

> **A_mixture = b · (ε_X · c_X + ε_Y · c_Y)**

This is the basis of the classical simultaneous-equation method for a binary mixture, measured at two suitably selected wavelengths.

## Simulator model and units

The simulator calculates:

> **A_total = b · (ε_X · c_X + ε_Y · c_Y)**  
> **T = 10^(−A_total)**  
> **I = I₀ · T**

The concentration sliders are in **µM**. The app converts them to mol L⁻¹ before applying the Beer–Lambert equation:

> **c (mol L⁻¹) = c (µM) × 10⁻⁶**

The simulator's default values are:

| Parameter | Component X | Component Y |
|---|---:|---:|
| Molar absorptivity | 10,000 L mol⁻¹ cm⁻¹ | 5,000 L mol⁻¹ cm⁻¹ |
| Concentration | 20 µM | 0 µM |
| Path length | 1 cm | 1 cm |

For these defaults, *A* = 0.200, *T* ≈ 0.6310, and approximately 63.10% of incident intensity is transmitted.

## Assumptions and limitations

The simulation is an idealised model. It assumes:

- Monochromatic or sufficiently narrow-band radiation.
- A homogeneous, clear sample with negligible scattering.
- Independent absorbing species whose chemical identities and absorptivities are not changed by mixing.
- A concentration range over which Beer–Lambert linearity holds.
- Constant path length and absorptivity.
- No significant uncorrected instrumental effects such as stray light.

In real measurements, reflection, scattering, solvent absorption, matrix effects, chemical association, pH-dependent speciation, and instrument limitations can cause deviations. The quantity 1 − *T* is the fraction of incident intensity not transmitted; it should not automatically be equated with true molecular absorption if reflection or scattering is significant.

This simulator is an academic teaching aid, not validated analytical software and not a substitute for instrument qualification, calibration, or analytical method validation.

## Suggested classroom activities

1. Keep all settings fixed and double the concentration of X. Observe that absorbance doubles while transmittance does not halve.
2. Double the path length. Compare the resulting absorbance and transmittance.
3. Set X and Y to nonzero concentrations. Verify that the component absorbances add.
4. Set one component's concentration to zero to isolate the other component.
5. Change incident intensity only. Observe that the ideal transmittance and absorbance remain unchanged, while absolute transmitted intensity changes.

## Repository contents

```text
beer-lambert-light-lab/
├── index.html
├── README.md
└── LICENSE
```

## License

Released under the MIT License. See [`LICENSE`](LICENSE).
