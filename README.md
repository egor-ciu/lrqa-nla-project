# Low-Rank Quaternion Approximation for Color Image Processing

## Abstract
Low-rank matrix approximation (LRMA)-based methods have been highly successful for grayscale image processing. For color images, LRMA typically restores each color channel independently using the monochromatic model or processes the concatenation of three color channels using the concatenation model. However, these approaches might not fully exploit the high correlation among RGB channels. To overcome this, we introduce a novel low-rank quaternion approximation (LRQA) model. This model encodes a color image pixel as a pure quaternion matrix, rather than a scalar, to better leverage the inter-channel correlations. Additionally, LRQA imposes a low-rank constraint on the constructed quaternion matrix.

## Overview
This repository contains the implementation of the LRQA model for color image denoising. The model's effectiveness is demonstrated through improved performance image processing tasks, as compared to traditional least-squares complex decomposition(LSCD) method.

## Contributors
- **Altair Toleugazinov**: Responsible for the scientific research.
- **Chulkov Egor**: Programming, implementing the algorithms, and testing their performance.

## Results
The images below showcase the effectiveness of the LRQA model in image denoising. Each row demonstrates the denoising process on different standard test images corrupted by Gaussian noise.

Color image denoising results on “Baboon”. (a) Original image; (b) Noisy image corrupted by Gaussian noise with variance 𝜏=50, respectively; The denoised image reconstructed by: (c) LSCD [52], (g) QLRMA-1

<img width="638" alt="image" src="https://github.com/egor-ciu/lrqa-nla-project/assets/120116723/44e94cce-7724-4839-a39e-f74ee2c258b1">

Color image denoising results on “Monarch”. (a) Original image; (b) Noisy image corrupted by Gaussian noise with variance 𝜏=50; The denoised image reconstructed by: (c) LSCD [52], (d) QLRMA-1

<img width="637" alt="image" src="https://github.com/egor-ciu/lrqa-nla-project/assets/120116723/0c3f4062-842f-489c-8212-de022be2504b">
