# Light Lab — Interactive Beer–Lambert Simulator

A self-contained educational web app for exploring light attenuation, transmittance, absorbance, and the Beer–Lambert law. It is designed for analytical chemistry teaching and can be hosted free with **GitHub Pages**.

**Live demo:** Add your GitHub Pages URL here after deployment.

## Features

- Interactive incident and transmitted light intensity display.
- Sliders for path length, molar absorptivity, and concentrations of two independent absorbing components.
- Real-time calculation of transmittance, percent transmittance, absorbance, and the fraction of incident light not transmitted.
- Visual cuvette and light-beam illustration.
- Derivation of the Beer–Lambert law from differential attenuation.
- Explanation of absorbance additivity for binary mixtures.
- Short concept-check quiz.
- Responsive layout for desktop, tablet, and mobile.
- No dependencies, build tools, external fonts, tracking, or data collection.

## Run locally

1. Download or clone this repository.
2. Open `index.html` in a modern web browser.

For a local development server, you can also run:

```bash
python3 -m http.server 8000
```

Then visit <http://localhost:8000>.

## Deploy with GitHub Pages

1. Create a GitHub repository, for example `beer-lambert-light-lab`.
2. Add `index.html`, `README.md`, and `LICENSE` to the repository root.
3. Commit and push the files to the `main` branch.
4. Open the repository's **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Select branch `main` and folder `/ (root)`, then save.
7. Wait for GitHub Pages to publish the site. The URL will generally look like:

   `https://YOUR-USERNAME.github.io/beer-lambert-light-lab/`

If you use a different repository name, the URL will differ. GitHub's Pages interface displays the published URL.

## The science

### 1. Transmittance

When a beam of light passes through a sample, some of the incident radiant intensity may be absorbed. Let:

- \(I_0\) = incident radiant intensity
- \(I\) = transmitted radiant intensity

Transmittance is:

\[
T = \frac{I}{I_0}
\]

Percent transmittance is:

\[
\%T = 100T
\]

Transmittance is a ratio and is dimensionless.

### 2. Why intensity attenuation is exponential

Consider a thin layer of solution with thickness \(dx\). For a homogeneous absorbing medium, assume the loss of intensity in this thin layer is proportional to:

- the intensity \(I\) entering the layer;
- the concentration \(c\) of absorbing species;
- the thickness \(dx\).

Thus:

\[
-dI = k I c\,dx
\]

where \(k\) is a proportionality constant for the chosen absorbing species and wavelength.

Separate variables:

\[
-\frac{dI}{I}=kc\,dx
\]

Integrate across the sample, from incident intensity \(I_0\) to transmitted intensity \(I\), and from position \(0\) to path length \(b\):

\[
-\int_{I_0}^{I}\frac{dI}{I}
=kc\int_0^b dx
\]

Therefore:

\[
\ln\left(\frac{I_0}{I}\right)=kbc
\]

Rearranging gives the exponential attenuation expression:

\[
I=I_0e^{-kbc}
\]

Dividing by \(I_0\):

\[
T=e^{-kbc}
\]

This exponential relationship explains why transmittance is not generally linear in concentration.

### 3. Define absorbance

Take the common (base-10) logarithm of the intensity ratio:

\[
A=\log_{10}\left(\frac{I_0}{I}\right)
\]

Since \(T=I/I_0\):

\[
\boxed{A=-\log_{10}T}
\]

Using the conversion \(\ln x=2.303\log_{10}x\):

\[
A=\frac{k}{2.303}bc
\]

Define the molar absorptivity:

\[
\varepsilon=\frac{k}{2.303}
\]

The Beer–Lambert law follows:

\[
\boxed{A=\varepsilon bc}
\]

where:

- \(A\) = absorbance (dimensionless; often reported in absorbance units, AU);
- \(\varepsilon\) = molar absorptivity, typically L mol\(^{-1}\) cm\(^{-1}\);
- \(b\) = optical path length, cm;
- \(c\) = concentration, mol L\(^{-1}\).

For fixed wavelength, chemical species, solvent conditions, and path length, absorbance is proportional to concentration over the range where Beer–Lambert behaviour is valid.

### 4. Why absorbances add for independent absorbers

For two independent absorbing species, X and Y, at the same wavelength:

\[
A_X=\varepsilon_Xbc_X
\]

\[
A_Y=\varepsilon_Ybc_Y
\]

The attenuation factors multiply:

\[
T_{\text{mixture}}=T_XT_Y
\]

Taking negative base-10 logarithms converts that product into a sum:

\[
A_{\text{mixture}}=A_X+A_Y
\]

Thus:

\[
A_{\text{mixture}}
=b(\varepsilon_Xc_X+\varepsilon_Yc_Y)
\]

This is the basis of the classical simultaneous-equation method for a binary mixture, measured at two suitably selected wavelengths.

## Simulator model and units

The simulator calculates:

\[
A_{\text{total}}=b(\varepsilon_Xc_X+\varepsilon_Yc_Y)
\]

\[
T=10^{-A_{\text{total}}}
\]

\[
I=I_0T
\]

The concentration sliders are in **µM**. The app converts them to mol L\(^{-1}\) before applying the Beer–Lambert equation:

\[
c(\mathrm{mol\,L^{-1}})=c(\mathrm{\mu M})\times10^{-6}
\]

The simulator's default values are:

| Parameter | Component X | Component Y |
|---|---:|---:|
| Molar absorptivity | 10,000 L mol\(^{-1}\) cm\(^{-1}\) | 5,000 L mol\(^{-1}\) cm\(^{-1}\) |
| Concentration | 20 µM | 0 µM |
| Path length | 1 cm | 1 cm |

For these defaults, \(A=0.200\), \(T\approx0.6310\), and approximately 63.10% of incident intensity is transmitted.

## Assumptions and limitations

The simulation is an idealised model. It assumes:

- Monochromatic or sufficiently narrow-band radiation.
- A homogeneous, clear sample with negligible scattering.
- Independent absorbing species whose chemical identities and absorptivities are not changed by mixing.
- A concentration range over which Beer–Lambert linearity holds.
- Constant path length and absorptivity.
- No significant uncorrected instrumental effects such as stray light.

In real measurements, reflection, scattering, solvent absorption, matrix effects, chemical association, pH-dependent speciation, and instrument limitations can cause deviations. The quantity \(1-T\) is the fraction of incident intensity not transmitted; it should not automatically be equated with true molecular absorption if reflection or scattering is significant.

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
