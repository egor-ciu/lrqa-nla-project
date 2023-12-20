# Low-Rank Quaternion Approximation for Color Image Processing

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

## How to reproduce the results
Run the function CBM3D in CDM3D.m

FUNCTION INTERFACE:

     [PSNR, yRGB_est] = CBM3D(yRGB, zRGB, sigma, profile, print_to_screen, colorspace)

     ! The function can work without any of the input arguments, 
     in which case, the internal default ones are used !

 BASIC USAGE EXAMPLES:

    Case 1) Using the default parameters (i.e., image name, sigma, etc.)

     [PSNR, yRGB_est] = CBM3D;

    Case 2) Using an external noisy image:

     % Read an RGB image and scale its intensities in range [0,1]
     yRGB = im2double(imread('image_House256rgb.png')); 
     % Generate the same seed used in the experimental results of [1]
     randn('seed', 0);
     % Standard deviation of the noise --- corresponding to intensity 
     %  range [0,255], despite that the input was scaled in [0,1]
     sigma = 25;
     % Add the AWGN with zero mean and standard deviation 'sigma'
     zRGB = yRGB + (sigma/255)*randn(size(yRGB));
     % Denoise 'zRGB'. The denoised image is 'yRGB_est', and 'NA = 1'  
     %  because the true image was not provided
     [NA, yRGB_est] = CBM3D(1, zRGB, sigma); 
     % Compute the putput PSNR
     PSNR = 10*log10(1/mean((yRGB(:)-yRGB_est(:)).^2))
     % show the noisy image 'zRGB' and the denoised 'yRGB_est'
     figure; imshow(min(max(zRGB,0),1));   
     figure; imshow(min(max(yRGB_est,0),1));

    Case 3) If the original image yRGB is provided as the first input 
     argument, then some additional information is printed (PSNRs, 
     figures, etc.). That is, "[NA, yRGB_est] = BM3D(1, zRGB, sigma);" in the
     above code should be replaced with:

     [PSNR, yRGB_est] = CBM3D(yRGB, zRGB, sigma);


 INPUT ARGUMENTS (OPTIONAL):
 
     1) yRGB (M x N x 3): Noise-free RGB image (needed for computing PSNR),
                          replace with the scalar 1 if not available.
     2) zRGB (M x N x 3): Noisy RGBimage (intensities in range [0,1] or [0,255])
     3) sigma (double)  : Std. dev. of the noise (corresponding to intensities
                           in range [0,255] even if the range of zRGB is [0,1])
     4) profile (char)  : 'np' --> Normal Profile 
                         'lc' --> Fast Profile
     5) print_to_screen : 0 --> do not print output information (and do 
                               not plot figures)
                         1 --> print information and plot figures
     6) colorspace (char): 'opp'   --> use opponent colorspace
                         'yCbCr' --> use yCbCr colorspace

 OUTPUTS:
 
     1) PSNR (double)          : Output PSNR (dB), only if the original 
                                image is available, otherwise PSNR = 0                                               
     2) yRGB_est (M x N x 3): Final RGB estimate (in the range [0,1])
