# Visual Representation and Compression

The work covers sampling, quantization, color representation, entropy, redundancy, and prediction using both standard test images and a personal color image.

## What the Code Does

### 1. Image Sampling and Aliasing

The code downsamples grayscale images by factors of:

- 2
- 4
- 8

Each image is downsampled in two ways:

- without anti-aliasing
- with Gaussian prefiltering before downsampling

The results are compared visually to study aliasing and loss of fine detail.

The Fourier magnitude spectrum is also computed to observe how high-frequency image content changes after filtering and downsampling.

A personal image with detailed regions such as branches, rocks, wires, and building edges is also used to compare aliasing in textured areas.

---

### 2. Image Quantization

The grayscale image is quantized using:

- 1 bit
- 2 bits
- 3 bits
- 4 bits
- 6 bits
- 8 bits

A uniform quantizer is implemented by limiting the number of available intensity levels.

For each bit depth, the code calculates:

- Mean Squared Error (MSE)
- Signal-to-Quantization-Noise Ratio (SQNR)

The measured SQNR is compared with the approximate 6 dB per bit relationship.

The same experiment is also applied to a color image to observe quantization artifacts in smooth and detailed regions.

---

### 3. Color Representation and Chroma Subsampling

The RGB image is converted to Y'CbCr.

The three components are separated into:

- Y' — brightness-related information
- Cb — blue chroma information
- Cr — red chroma information

The code implements and compares:

- 4:4:4
- 4:2:2
- 4:2:0

For 4:2:2, the chroma channels are reduced horizontally.

For 4:2:0, the chroma channels are reduced in both horizontal and vertical directions.

The reduced chroma channels are then upsampled and converted back to RGB for visual comparison.

---

### 4. Entropy of Simple Sources

An entropy function is implemented using:

\[
H(X) = -\sum p(x)\log_2 p(x)
\]

The code calculates entropy for:

- a fair die
- a biased die
- two independent dice

It also generates random die sequences and compares theoretical entropy with empirical entropy.

A correlated sequence is generated where the current value often repeats the previous value.

This is used to compare:

- marginal entropy
- conditional entropy

---

### 5. Image Entropy and Histograms

Grayscale histograms are created for:

- the standard camera image
- a personal image

The histogram counts are converted into probability distributions and used to calculate image entropy.

The code also generates:

- an i.i.d. intensity sequence from the image histogram
- a correlated intensity sequence

This shows how correlation can reduce conditional entropy even when marginal entropy stays high.

---

### 6. Joint and Conditional Entropy

Horizontally adjacent pixel pairs are extracted from the image.

A 2D joint histogram is used to estimate:

- H(X)
- H(Y)
- H(X,Y)
- H(Y|X)
- I(X;Y)

This shows how much information neighboring pixels share.

The same measures are also calculated for:

- independent synthetic sequences
- correlated synthetic sequences

---

### 7. Predictive Coding

A simple spatial predictor is used:

\[
\hat{X}_{i,j}
=
\frac{1}{2}
(X_{i,j-1} + X_{i-1,j})
\]

The current pixel is predicted from its left and upper neighbors.

The prediction residual is then calculated as:

\[
X - \hat{X}
\]

The entropy of the residual is compared with the entropy of the original image.

This demonstrates how prediction can reduce uncertainty when neighboring pixels are correlated.

The redundancy of the image is also estimated.

---

### 8. AR(1) Correlation Experiment

A first-order autoregressive sequence is generated using different values of:

\[
\alpha
\]

The tested values are:

- 0.2
- 0.5
- 0.9
- 0.99

The sequence is predicted from its previous value and the entropy of the residual is compared with the entropy of the original sequence.

The experiment shows that prediction becomes more useful when correlation is stronger.

---

## Main Results

Some of the main observations were:

- Anti-alias filtering reduced artifacts during strong downsampling.
- Higher quantization bit depth reduced MSE and increased SQNR.
- Chroma subsampling reduced color resolution while preserving most visible image structure.
- The personal image had higher grayscale entropy than the standard camera image.
- Neighboring pixels had lower conditional entropy than marginal entropy.
- Mutual information increased when correlation was introduced.
- Predictive coding reduced image entropy by representing prediction errors instead of original pixel values.
- Stronger AR(1) correlation made prediction more effective.

## Tools

- Python
- NumPy
- Matplotlib
- scikit-image
- OpenCV
- Google Colab
