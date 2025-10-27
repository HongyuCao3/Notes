# Upsampling vs Downsampling

## 1. Upsampling

**Definition:**  
Upsampling refers to increasing the sampling rate or resolution of data. It involves generating new data points between existing samples, often based on an assumption of continuity in the signal.

**Signal Processing Context:**  
- Insert zeros or interpolate between samples.  
- Formula (zero-insertion example, upsample factor L):  
  
  $y[m] = 
  \begin{cases} 
  x[m/L], & m \text{ divisible by } L \\
  0, & \text{otherwise} 
  \end{cases}$
- Often followed by low-pass filtering to smooth inserted values.

**Machine Learning / Image Processing Context:**  
- Increase the size of images or feature maps (width × height).  
- Methods:
  - Nearest-neighbor interpolation
  - Bilinear / bicubic interpolation
  - Transposed convolution (deconvolution)
- Applications:
  - Image super-resolution
  - Generative models (GANs, Diffusion models)
  - Restoring original input size for downstream tasks

**Intuition:**  
- “Stretching” the signal or image; filling in the gaps with estimated values.

---

## 2. Downsampling

**Definition:**  
Downsampling refers to reducing the sampling rate or resolution of data. It involves selecting a subset of the existing data points, often preceded by low-pass filtering to prevent aliasing.

**Signal Processing Context:**  
- Keep every M-th sample and discard the rest:  
  $y[n] = x[nM]$
- Anti-aliasing filter is usually applied before downsampling.

**Machine Learning / Image Processing Context:**  
- Reduce the size of images or feature maps (width × height).  
- Methods:
  - Max pooling
  - Average pooling
  - Strided convolution
- Applications:
  - CNN feature extraction
  - Reducing computation and memory cost
  - Data compression

**Intuition:**  
- “Picking representative points”; discarding some data while retaining key information.

---

## 3. Key Differences

| Feature             | Upsampling                   | Downsampling                     |
|--------------------|-----------------------------|---------------------------------|
| **Operation**       | Increase size / sampling rate | Decrease size / sampling rate   |
| **Purpose**         | Restore or enhance resolution | Reduce resolution / abstract features |
| **Method**          | Interpolation, transposed convolution | Pooling, strided convolution, subsampling |
| **Potential Issues**| Interpolation error         | Information loss, aliasing      |
| **Typical Applications** | Super-resolution, generative models | CNN feature extraction, compression |

**Summary Intuition:**  
- **Upsampling** → Fill in gaps between samples (interpolation-based).  
- **Downsampling** → Pick a subset of samples (subsampling-based).
