---
tags:
  - color
  - css
aliases: []
id: color_space
---

A beam of light is a continuous spectral power distribution, which is projected to the human cone cells of short-, middle- and long-wavelength types to produce the tristimulus value. Different triplet corresponds to different color perception.

# CIE 1931

In 1931, the detailed mechanisms of photoreceptor cells were not yet understood. However, empirical evidence demonstrated that red (700 nm), green (546.1 nm), and blue (435.8 nm) light could be additively mixed to produce a wide range of perceptible colors. To quantify this phenomenon, scientists conducted color-matching experiments in which observers matched monochromatic spectral colors using combinations of these three primary lights.

The resulting data were normalized such that an equal-energy white stimulus (i.e., a stimulus with equal radiant power across the visible spectrum) was represented by equal RGB tristimulus values (1/3, 1/3, 1/3). This led to the establishment of the CIE 1931 RGB color-matching functions, which defined the CIE 1931 RGB color space.

However, this space contained negative tristimulus values for some spectral colors, indicating that those colors could not be physically reproduced by non-negative mixtures of the chosen primaries. To address this issue and ensure all visible colors could be represented with positive coordinates, a linear transformation was applied to derive the CIE XYZ color space. The XYZ space was designed such that:

1. All visible colors have non-negative tristimulus values.
2. The Y component corresponds to luminance.
3. The primaries (X, Y, Z) are non-physical, ensuring the entire visible spectrum is encompassed.

# Reference
https://en.wikipedia.org/wiki/CIE_1931_color_space#Color_matching
