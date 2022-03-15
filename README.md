singularity-opac
==

[![Tests](https://github.com/lanl/singularity-opac/actions/workflows/tests.yml/badge.svg)](https://github.com/lanl/singularity-opac/actions/workflows/tests.yml)

Performance Portable Opacity and Emissivity library for simulation codes

## API

singularity-opac provides a uniform API for all opacity models. The following functions are provided
(here, `\sigma` is the frequency- and angle-dependent cross section in units of `cm^2`):
| Function              | Expression | Description            | Units   |
| --------------------- | ---------- | ---------------------  | ------- |
| AbsorptionCoefficient | `n \sigma` | Absorption coefficient | `cm^{-1}` |
| AngleAveragedAbsorptionCoefficient | `\frac{1}{4 \pi}\int n \sigma d\Omega` | Absorption coefficient averaged over solid angle | `cm^{-1}` |
| EmissivityPerNuOmega | `j_{\nu} = \frac{dE}{d^3x dt d\Omega d\nu}` | Frequency- and angle-dependent emissivity | `erg cm^{-3} s^{-1} Sr^{-1} Hz^{-1}` |
| EmissivityPerNu | `\int j_{\nu} d\Omega`  | Frequency-dependent emissivity | `erg cm^{-3} s^{-1} Hz^{-1}` |
| Emissivity | `\int j_{\nu} d\nu d\Omega`  | Total emissivity | `erg cm^{-3} s^{-1}` |
| NumberEmissivity | `\int \frac{1}{h \nu} j_{\nu} d\Omega d\nu` | Total number emissivity | `cm^{-3} s^{-1}` |
| ThermalDistributionOfTNu | `B_{\nu} = \frac{dE}{dA dt d\Omega d\nu}` | Specific intensity of thermal distribution | `erg cm^{-2} s^{-1} Sr^{-1} Hz^{-1}` |
| ThermalDistributionOfT | `B = \int B_{\nu} d\Omega d\nu` | Frequency- and angle-integrated intensity of thermal distribution | `erg cm^{-2} s^{-1}` |
| ThermalNumberDistributionOfT | `B = \int \frac{1}{h \nu} B_{\nu} d\Omega d\nu` | Frequency- and angle-integrated intensity of thermal distribution | `erg cm^{-2} s^{-1}` |

Note that the thermal radiation energy density `u = 1/c ThermalDistributionOfT` and the thermal radiation number density `n = 1/c ThermalNumberDistributionOfT`.

Internally singularity-opac always uses CGS units, as in the above table. However, arbitrary units are supported through the units modifier.

## To Build

At its most basic:
```bash
git clone --recursive git@github.com:lanl/singularity-opac.git
cd singularity-opac
mkdir bin
cd bin
cmake ..
make
```

### To Make tests

Then, in the singularity-opac root directory:
```bash
mkdir -p bin
cd bin
cmake -DSINGULARITY_BUILD_TESTS=ON ..
make -j
make test
```

### Build Options

A number of options are avaialable for compiling:

| Option                            | Default | Comment                                                                              |
| --------------------------------- | ------- | ------------------------------------------------------------------------------------ |
| SINGULARITY_BUILD_TESTS           | OFF     | Build test infrastructure.                                                           |

## Copyright

© 2021. Triad National Security, LLC. All rights reserved.  This
program was produced under U.S. Government contract 89233218CNA000001
for Los Alamos National Laboratory (LANL), which is operated by Triad
National Security, LLC for the U.S.  Department of Energy/National
Nuclear Security Administration. All rights in the program are
reserved by Triad National Security, LLC, and the U.S. Department of
Energy/National Nuclear Security Administration. The Government is
granted for itself and others acting on its behalf a nonexclusive,
paid-up, irrevocable worldwide license in this material to reproduce,
prepare derivative works, distribute copies to the public, perform
publicly and display publicly, and to permit others to do so.
