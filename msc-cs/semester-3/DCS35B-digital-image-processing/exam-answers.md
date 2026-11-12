# DCS35B Digital Image Processing — Exam Answer Sheet

> **How to use:** Part B = answer 2 of 3 per module (8 marks each). Learn at least 2 answers per module below. Part A = 9 short answers (3 marks each) at the end.
> ⭐ = asked in Oct 2024 paper or test paper.
> This sheet covers the **complete syllabus**. Q1–Q11 are full 8-mark answers; the "Remaining syllabus topics" section covers everything else.

## Syllabus coverage checklist

| Module | Syllabus topic | Where |
|---|---|---|
| 1 | Picture as pixels, binary/grayscale/colour images, space requirements | Q4, Remaining M1 |
| 1 | Colour models | Remaining M1 |
| 1 | Applications of image processing | Remaining M1 |
| 1 | Sampling and quantization | Remaining M1 |
| 1 | Neighbours, adjacency, connectivity, boundaries, distance measures | Q3, Remaining M1 |
| 1 | Pixel-wise operations | Q3 |
| 1 | Negatives, log transformations, histogram | Q4, Q5 |
| 1 | Fundamental steps, components of an IP system | Q1, Q2 |
| 2 | Histogram equalization and matching | Q5 |
| 2 | Image subtraction, averaging | Remaining M2 |
| 2 | Spatial filters: smoothing and sharpening | Q6, Remaining M2 |
| 2 | 2-D DFT, frequency-domain filters | Q7, Remaining M2 |
| 2 | Discrete wavelet transform | Q7 |
| 2 | Advantages of frequency-domain operations | Q7 |
| 2 | Generating a spatial mask from the frequency domain | Remaining M2 |
| 3 | Pseudo-colour, intensity slicing, grey to colour, complements, colour slicing, colour segmentation | Q11 |
| 3 | Halftoning | Part A |
| 3 | Noise in colour images | Remaining M3 |
| 3 | Coding, interpixel and psychovisual redundancy | Q9 |
| 3 | Lossless predictive coding | Q9 |
| 3 | Lossy predictive coding | Remaining M3 |
| 3 | Transform coding | Q10 |
| 3 | Compression standards, JPEG procedure | Q10, Remaining M3 |
| 3 | Image security | Remaining M3 |

---

# MODULE 1

## Q1. ⭐ Fundamental steps in digital image processing (with block diagram)

**Asked:** 2024 Part B, Test paper

```
                        +------------------+
 Problem domain ----->  | Image Acquisition|
                        +--------+---------+
                                 v
   +-------------+      +------------------+      +--------------------+
   | Image       |<-----| Image            |----->| Colour Image       |
   | Restoration |      | Enhancement      |      | Processing         |
   +------+------+      +------------------+      +---------+----------+
          v                                                 v
   +-------------+                                +--------------------+
   | Wavelets &  |                                | Compression        |
   | Multires.   |                                +---------+----------+
   +------+------+                                          v
          |             +------------------+      +--------------------+
          +------------>|  KNOWLEDGE BASE  |<---->| Morphological      |
                        +------------------+      | Processing         |
                                 ^                +---------+----------+
   +-------------+               |                          v
   | Object      |<--------------+                +--------------------+
   | Recognition |<--- Representation & <------- | Segmentation       |
   +-------------+     Description                +--------------------+
```

**Steps:**
1. **Image acquisition**: capture the image with a sensor (camera, scanner) and digitize it. May include pre-processing such as scaling.
2. **Image enhancement**: make the image look better for a particular use, for example contrast stretching or sharpening. It is *subjective*.
3. **Image restoration**: remove degradation such as blur or noise using mathematical models. It is *objective*.
4. **Colour image processing**: colour models (RGB, CMY, HSI) and processing of colour images.
5. **Wavelets and multiresolution processing**: represent the image at different resolutions. Used in compression and pyramids.
6. **Compression**: reduce the storage or bandwidth needed (JPEG, for example).
7. **Morphological processing**: tools that extract shape components, such as dilation and erosion.
8. **Segmentation**: divide the image into its parts or objects. This is one of the hardest steps.
9. **Representation and description**: represent the segmented regions as boundaries or regions and extract features (descriptors).
10. **Object recognition**: assign a label to an object based on its descriptors (for example "car" or "face").

**Knowledge base**: stores knowledge about the problem domain and guides how all the modules interact.

**Conclusion:** steps 1–6 output images; steps 7–10 output image *attributes*.

---

## Q2. Components of an image processing system

**Asked:** 2024 Part A

1. **Image sensors**: a physical device that senses energy, plus a digitizer that converts its output to digital form.
2. **Specialized image processing hardware**: digitizer plus ALU for fast operations such as averaging. Also called the front-end subsystem.
3. **Computer**: anything from a general-purpose PC to a supercomputer.
4. **Image processing software**: specialized modules for specific tasks, such as MATLAB or OpenCV.
5. **Mass storage**: short-term (frame buffers), on-line (disks) and archival (tapes, optical). An 8-bit 1024×1024 image needs 1 MB.
6. **Image displays**: colour monitors.
7. **Hardcopy devices**: laser printers, film cameras, inkjet printers.
8. **Networking**: transmits images. Bandwidth is the key concern.

---

## Q3. ⭐ (a) Image operations on a pixel basis (b) Measuring distances

**Asked:** 2024 Part B

### (a) Pixel-wise operations
These operations are carried out **pixel by pixel**, not as matrix operations.
- **Arithmetic:** s(x,y) = f(x,y) + g(x,y); difference d = f − g; product p = f × g; division v = f ÷ g.
  - *Addition / averaging*: reduces noise by averaging K noisy images.
  - *Subtraction*: finds the differences between images, for example in medical imaging (digital subtraction angiography).
  - *Multiplication / division*: shading correction and masking (region of interest).
- **Logical:** AND, OR and NOT on binary images, used for masking.
- **Single-pixel (point) operations:** s = T(r), for example negatives and thresholding.

### Neighbours of a pixel p at (x, y)
- **N4(p)** (4-neighbours): (x+1,y), (x−1,y), (x,y+1), (x,y−1)
- **ND(p)** (diagonal neighbours): (x+1,y+1), (x+1,y−1), (x−1,y+1), (x−1,y−1)
- **N8(p)** = N4(p) ∪ ND(p)

```
  ND  N4  ND
  N4  p   N4
  ND  N4  ND
```

**Adjacency** (V = the set of intensity values that count as adjacent):
- 4-adjacency: q is in N4(p)
- 8-adjacency: q is in N8(p)
- m-adjacency (mixed): q is in N4(p), **or** q is in ND(p) and N4(p) ∩ N4(q) has no pixels from V. This removes the ambiguity of multiple paths.

**Connectivity / path:** a sequence of adjacent pixels. A **region** is a connected set. Its **boundary** is the set of pixels with at least one neighbour outside the region.

### (b) Distance measures
For pixels p(x, y) and q(s, t):

| Measure | Formula | Pixels at distance ≤ r form |
|---|---|---|
| **Euclidean** De | √[(x−s)² + (y−t)²] | a disk |
| **City-block** D4 | \|x−s\| + \|y−t\| | a diamond |
| **Chessboard** D8 | max(\|x−s\|, \|y−t\|) | a square |

D4 = 1 for the 4-neighbours and D8 = 1 for the 8-neighbours.

```
D4 ≤ 2:        D8 ≤ 2:
    2          2 2 2 2 2
  2 1 2        2 1 1 1 2
2 1 0 1 2      2 1 0 1 2
  2 1 2        2 1 1 1 2
    2          2 2 2 2 2
```

A distance function D must satisfy: D(p,q) ≥ 0 (= 0 only if p = q), D(p,q) = D(q,p), and D(p,z) ≤ D(p,q) + D(q,z).

---

## Q4. ⭐ (a) Binary vs grayscale images (b) Log transformations; image negatives

**Asked:** 2024 Part B, 2024 Part A (negatives)

### (a) Binary vs grayscale

| Binary image | Grayscale image |
|---|---|
| Each pixel is 0 or 1 (black/white) | Each pixel is 0 to L−1 (usually 0–255) |
| 1 bit per pixel | 8 bits per pixel (k = 8) |
| Size M×N bits | Size M×N×k bits |
| Used for text, documents, masks, shapes | Used for photos, X-rays |
| Created by thresholding a grayscale image | Has shades of grey |
| Supports logical operations (AND/OR) | Supports arithmetic and histogram operations |

Colour image: 3 channels (R, G, B) of 8 bits each, so **24 bits per pixel**.

**Space requirement:** b = M × N × k bits. For example, 1024×1024 at 8 bits = 8,388,608 bits = 1 MB.

### Image negatives
**s = (L − 1) − r**, where r is the input intensity and L the number of levels.
- Reverses the intensities: dark becomes light.
- Useful for bringing out white or grey detail inside dark regions (such as mammograms).
- Characteristics: it is a linear, point-wise operation; it is reversible; it preserves the dynamic range.

### Log transformation
**s = c · log(1 + r)**, where c is a constant and r ≥ 0.
- Maps a **narrow range of low input values to a wider range** of output, and compresses the high values.
- Expands dark pixels and compresses bright ones.
- Main use: displaying the **Fourier spectrum**, whose values range from 0 to 10⁶ or more.
- The inverse log does the opposite.

```
s ^
  |      ___---- log
  |   _-
  |  /     ___ identity
  | /  __--
  |/_--
  +----------> r
```

Related: the **power-law (gamma)** transformation s = c·r^γ. γ < 1 brightens and γ > 1 darkens. It is used for gamma correction.

---

# MODULE 2

## Q5. ⭐⭐ Histogram processing techniques

**Asked:** 2024 Part B, Test paper (the most important question in this subject)

### Histogram
For a digital image with levels 0 to L−1: **h(r_k) = n_k**, where n_k is the number of pixels with intensity r_k.
**Normalized histogram:** p(r_k) = n_k / MN. This is the probability of level r_k, and Σ p(r_k) = 1.

- Dark image: histogram concentrated on the left
- Bright image: histogram concentrated on the right
- Low contrast: narrow histogram
- High contrast: spread across the whole range

### 1. Histogram equalization
Goal: spread the intensities so the histogram is roughly **uniform**, which increases contrast automatically.

**s_k = T(r_k) = (L − 1) Σ_{j=0}^{k} p_r(r_j)** for k = 0, 1, …, L−1. This is the cumulative distribution function (CDF).

**Worked example (3-bit image, L = 8, MN = 4096):**

| r_k | n_k | p(r_k) | CDF | s_k = 7×CDF | rounded |
|---|---|---|---|---|---|
| 0 | 790 | 0.19 | 0.19 | 1.33 | 1 |
| 1 | 1023 | 0.25 | 0.44 | 3.08 | 3 |
| 2 | 850 | 0.21 | 0.65 | 4.55 | 5 |
| 3 | 656 | 0.16 | 0.81 | 5.67 | 6 |
| 4 | 329 | 0.08 | 0.89 | 6.23 | 6 |
| 5 | 245 | 0.06 | 0.95 | 6.65 | 7 |
| 6 | 122 | 0.03 | 0.98 | 6.86 | 7 |
| 7 | 81 | 0.02 | 1.00 | 7.00 | 7 |

Properties: T(r) is monotonically increasing, and 0 ≤ T(r) ≤ L−1.

### 2. Histogram matching (specification)
Goal: transform the image so its histogram matches a **specified** shape, not just a uniform one.
1. Equalize the input: s_k = (L−1) Σ p_r(r_j)
2. Equalize the specified histogram: G(z_q) = (L−1) Σ_{i=0}^{q} p_z(z_i)
3. For each s_k, find the z_q where G(z_q) is closest to s_k
4. Map r_k → s_k → z_q

### 3. Local histogram processing
Apply equalization in a small neighbourhood that moves pixel by pixel. This enhances detail in small areas that global equalization misses.

### 4. Histogram statistics
- Mean m = Σ r_i p(r_i) measures average brightness.
- Variance σ² = Σ (r_i − m)² p(r_i) measures contrast.
- Local mean and variance can be used for selective enhancement.

---

## Q6. ⭐ Image sharpening using spatial filters (methodology and equations)

**Asked:** 2024 Part B

**Spatial filtering:** move a mask (kernel) over the image. At each pixel:
**g(x,y) = Σ_s Σ_t w(s,t) · f(x+s, y+t)**

**Smoothing (blurring), which is the opposite:** averaging = integration.
- Box filter: (1/9) × [all 1s in a 3×3 mask]
- Weighted average: (1/16) × [1 2 1; 2 4 2; 1 2 1]
- Median filter (non-linear): best for **salt-and-pepper noise**

**Sharpening = differentiation.** It highlights edges and fine detail.

First derivative: ∂f/∂x = f(x+1) − f(x)
Second derivative: ∂²f/∂x² = f(x+1) + f(x−1) − 2f(x)

### 1. Laplacian (second derivative)
**∇²f = f(x+1,y) + f(x−1,y) + f(x,y+1) + f(x,y−1) − 4f(x,y)**

```
Masks:
 0  1  0        1  1  1
 1 -4  1        1 -8  1
 0  1  0        1  1  1
```
Sharpened image: **g(x,y) = f(x,y) + c[∇²f(x,y)]**, with c = −1 when the centre coefficient is negative.

### 2. Unsharp masking and high-boost filtering
1. Blur the image: f̄(x,y)
2. Mask: g_mask = f(x,y) − f̄(x,y)
3. **g(x,y) = f(x,y) + k · g_mask(x,y)**
   - k = 1 gives unsharp masking
   - k > 1 gives high-boost filtering

### 3. Gradient (first derivative): Sobel operators
Gradient magnitude **M(x,y) ≈ |g_x| + |g_y|**

```
Sobel g_x:        Sobel g_y:
-1 -2 -1          -1  0  1
 0  0  0          -2  0  2
 1  2  1          -1  0  1
```
Used for edge detection and industrial defect inspection.

**Comparison:** the Laplacian gives thin, double edges and is sensitive to noise. The gradient gives thicker edges and stronger response to steps.

---

## Q7. ⭐ Discrete wavelet transform (basic concepts) + Frequency-domain filtering

**Asked:** 2024 Part B (DWT); Part A (frequency-domain advantages, spatial↔frequency correspondence)

### Discrete wavelet transform (DWT)
- The Fourier transform uses sinusoids of infinite duration, so it gives **frequency information only, not location**.
- Wavelets are **small waves of limited duration**, so they give **both frequency and time/space location**.
- This is the basis of **multiresolution analysis**: the image is seen at several scales.

**Two functions:**
- **Scaling function φ(x)**: gives the approximation (low-pass)
- **Wavelet function ψ(x)**: gives the detail (high-pass)
- Basis functions: ψ_{j,k}(x) = 2^{j/2} ψ(2^j x − k), where j = scale and k = translation

**2-D DWT (one level):** filter the rows, then the columns, with a low-pass (h_φ) and a high-pass (h_ψ) filter, then downsample by 2.

```
+-------+-------+
|  LL   |  HL   |    LL = approximation (smaller copy of the image)
| (W_φ) |(W_ψ^V)|    HL = vertical details
+-------+-------+    LH = horizontal details
|  LH   |  HH   |    HH = diagonal details
|(W_ψ^H)|(W_ψ^D)|
+-------+-------+
```
Repeat on LL to get more levels (a pyramid).

**Simplest wavelet:** Haar.
**Applications:** JPEG 2000 compression, denoising, edge detection, image fusion.

### Frequency-domain filtering (support material)
**2-D DFT:** F(u,v) = Σ_{x=0}^{M−1} Σ_{y=0}^{N−1} f(x,y) e^{−j2π(ux/M + vy/N)}

**Correspondence (convolution theorem):** f(x,y) ★ h(x,y) ⇔ F(u,v) · H(u,v).
Convolution in the spatial domain equals multiplication in the frequency domain.

**Steps:** pad the image → multiply by (−1)^{x+y} to centre it → DFT → multiply by H(u,v) → inverse DFT → take the real part → crop.

| Low-pass (smoothing) | Formula |
|---|---|
| Ideal (ILPF) | H = 1 if D(u,v) ≤ D₀, else 0 (causes ringing) |
| Butterworth (BLPF) | H = 1 / [1 + (D/D₀)^{2n}] |
| Gaussian (GLPF) | H = e^{−D²/2D₀²} (no ringing) |

High-pass = 1 − low-pass.

**Advantages of the frequency domain:** filters are intuitive to design (you choose the frequencies to keep); large filters are faster through the FFT; periodic noise is easy to remove; the image's frequency content is easy to analyse.

---

# MODULE 3

## Q8. ⭐ Image compression model (block diagram)

**Asked:** 2024 Part B

```
ENCODER:
f(x,y) --> [ Mapper ] --> [ Quantizer ] --> [ Symbol Coder ] --> compressed data
                                                                      |
                                                                  channel
DECODER:                                                              v
f^(x,y) <-- [ Inverse Mapper ] <-- [ Symbol Decoder ] <--------------+
```

1. **Mapper**: transforms the image into a form that reduces **interpixel redundancy**, such as run-length coding, a transform (DCT) or a prediction error. Reversible.
2. **Quantizer**: reduces the accuracy of the mapper's output to remove **psychovisual redundancy**. **Irreversible**, so it is left out in lossless compression.
3. **Symbol coder**: assigns short codes to the most frequent values to remove **coding redundancy** (Huffman, for example). Reversible.

**Decoder:** symbol decoder → inverse mapper. There is **no inverse quantizer**, because quantization cannot be undone.

**Lossless:** f^(x,y) = f(x,y), for example PNG, Huffman, LZW, run-length.
**Lossy:** f^ ≈ f, giving a higher compression ratio, for example JPEG.

**Fidelity criteria:**
- Objective: RMS error e_rms = √[(1/MN) ΣΣ (f^ − f)²], SNR
- Subjective: human rating (excellent, fine, passable, …)

---

## Q9. ⭐ Three types of data redundancy (discuss any two in detail)

**Asked:** 2024 Part B, Test paper (interpixel), 2024 Part A (compression ratio)

**Compression ratio:** **C = b / b′**, where b = bits in the original and b′ = bits after compression.
**Relative data redundancy:** **R = 1 − 1/C**
Example: C = 10 means R = 0.9, so 90% of the data is redundant.

### 1. Coding redundancy
- Happens when the codes used are longer than needed. For example, every pixel gets 8 bits even though some values are far more frequent.
- Average code length: **L_avg = Σ_{k=0}^{L−1} l(r_k) · p_r(r_k)**
- Fix: **variable-length coding**, with short codes for frequent values. Examples are Huffman and arithmetic coding.
- Example: a fixed 8 bits versus L_avg = 1.81 bits gives C ≈ 4.42.

### 2. Interpixel (spatial and temporal) redundancy
- Neighbouring pixels are **highly correlated**, so a pixel's value can be predicted from its neighbours.
- Each pixel therefore carries little new information.
- Also called spatial, geometric or inter-frame redundancy (in video).
- Fix: a **mapping** step such as:
  - **Run-length coding** (store value + run length, for binary images)
  - **Predictive coding** (store only the difference)
  - Transforms (DCT, wavelets)

### 3. Psychovisual redundancy
- Some information is **ignored by human vision** or is less important to it.
- The eye responds to features (edges, textures), not to every pixel value.
- Fix: **quantization**, for example reducing 256 grey levels to 16. Improved grey-scale (IGS) quantization adds randomness to avoid false contouring.
- Removing it is **irreversible**, which makes the compression lossy.

### Lossless predictive coding
- Predict f^(n) = round[Σ_{i=1}^{m} α_i f(n−i)]
- Encode only the **error e(n) = f(n) − f^(n)**, which has a much smaller range and so compresses well.

---

## Q10. ⭐ Transform coding (compression procedure) + JPEG

**Asked:** 2024 Part B

```
ENCODER:
Input --> [Construct n×n   ] --> [Forward  ] --> [Quantizer] --> [Symbol ] --> Compressed
image     [subimages (8×8)]      [Transform]                     [Encoder]     image

DECODER:
Compressed --> [Symbol ] --> [Inverse  ] --> [Merge n×n ] --> Decompressed
image          [Decoder]     [Transform]     [subimages ]     image
```

1. **Subimage decomposition**: split the image into n×n blocks (usually 8×8).
2. **Transform**: apply a reversible linear transform (**DCT**, DFT, Walsh-Hadamard or KLT) to each block. This packs most of the energy into a **few low-frequency coefficients**.
3. **Quantization**: discard or coarsely quantize the small, high-frequency coefficients. This is where the loss happens.
4. **Coding**: encode the remaining coefficients with variable-length codes.

**Why the DCT?** It packs information close to the optimal KLT, but it is image-independent and fast. It also has less blocking artefact than the DFT.

### JPEG baseline procedure
1. Split into 8×8 blocks
2. **Level shift**: subtract 128 (2^{k−1}) from each pixel
3. Apply the **2-D DCT** to each block
4. **Quantize**: T^(u,v) = round[T(u,v) / Z(u,v)], where Z is the normalization (quantization) table
5. **Zig-zag scan**: order the coefficients from low to high frequency
6. **DC coefficient**: code the difference from the previous block's DC
7. **AC coefficients**: run-length code the zeros, then Huffman code

Decompression reverses these steps.

---

## Q11. Pseudo-colour image processing (backup)

- Assigning colours to **grey levels** according to a rule. Humans can tell apart far more colours than grey shades.
- **Intensity slicing**: picture the image as a 3-D surface and cut it with planes at levels l₁, l₂, …. Each slice gets a different colour. Used for X-ray weld inspection and rainfall maps.
- **Grey level to colour transformation**: three independent transforms R = T_R(f), G = T_G(f) and B = T_B(f), fed to a colour monitor.
- **Colour complements**: the hues opposite each other on the colour circle. Like a colour negative, they enhance detail in dark regions.
- **Colour slicing**: highlight a chosen range of colours and make the rest neutral (grey).
- **Colour segmentation**: in HSI, threshold the hue and saturation; in RGB, use the distance to an average colour.

---

# REMAINING SYLLABUS TOPICS (complete coverage)

## Module 1 — Image fundamentals

### Picture as a collection of pixels
- An image is a 2-D function **f(x, y)**. x and y are spatial coordinates and f is the intensity (grey level) at that point.
- A **digital image** has finite, discrete x, y and f. It is stored as an **M × N matrix**, and each element is a **pixel** (picture element).

```
        | f(0,0)     f(0,1)    ...  f(0,N-1)   |
f(x,y)= | f(1,0)     f(1,1)    ...  f(1,N-1)   |
        |   ...                                |
        | f(M-1,0)   f(M-1,1)  ...  f(M-1,N-1) |
```
- Intensity levels: L = 2^k (k = 8 gives 256 levels, 0 to 255).
- Image formation: f(x,y) = i(x,y) · r(x,y), where i is illumination (0 < i < ∞) and r is reflectance (0 to 1).

### Types of images
- **Binary**: 1 bit per pixel (0/1)
- **Grayscale**: 8 bits per pixel
- **Colour**: 24 bits per pixel (8 bits each for R, G, B)
- **Indexed**: each pixel holds an index into a colour map (palette)

### Colour models

| Model | Type | Components | Used in |
|---|---|---|---|
| **RGB** | Additive (light) | Red, Green, Blue; a unit cube where (0,0,0) is black and (1,1,1) is white | Monitors, cameras |
| **CMY / CMYK** | Subtractive (pigment) | Cyan, Magenta, Yellow (+ blacK) | Printers |
| **HSI** | Perceptual | Hue (colour type), Saturation (purity), Intensity (brightness) | Image processing, human description |

- **RGB → CMY:** C = 1 − R, M = 1 − G, Y = 1 − B
- **RGB → HSI:** I = (R+G+B)/3; S = 1 − 3·min(R,G,B)/(R+G+B); H = θ if B ≤ G, otherwise 360° − θ, where θ = cos⁻¹{ ½[(R−G)+(R−B)] / √[(R−G)² + (R−B)(G−B)] }
- **Why HSI?** It separates intensity from colour information, so grey-level algorithms can run on I alone.

### Image sampling and quantization
- A sensor gives a **continuous** signal. Converting it to digital form takes two steps:
  1. **Sampling**: digitize the **coordinate values** (x, y). This decides the **spatial resolution** (M × N).
  2. **Quantization**: digitize the **amplitude values**. This decides the **intensity resolution** (L = 2^k levels).
- Too few samples cause **checkerboard / pixelation**. Too few levels cause **false contouring**.
- Storage: b = M × N × k bits.

```
continuous   --> [ sampling ] --> discrete     --> [ quantization ] --> digital
scan line                         positions                             values
```

### Applications of image processing
Medical imaging (X-ray, CT, MRI, ultrasound) · Remote sensing / satellite (weather, land use) · Industrial inspection (defect detection) · Biometrics (fingerprint, face, iris) · Document processing (OCR) · Law enforcement (number plates, forensics) · Astronomy · Robotics vision · Entertainment (film effects).
Classification by the EM spectrum: gamma-ray, X-ray, ultraviolet, visible, infrared, microwave (radar), radio (MRI).

### Boundaries
The **boundary** (border, contour) of a region R is the set of pixels in R that have at least one neighbour outside R. It is **inner** if it belongs to R and **outer** if it belongs to the background. Edges are local intensity discontinuities; boundaries are closed paths.

---

## Module 2 — Remaining enhancement topics

### Image subtraction
**g(x,y) = f(x,y) − h(x,y)**
- Highlights the **differences** between two images.
- **Digital subtraction angiography:** subtract a mask image (before dye injection) from a live image (after injection). Only the blood vessels remain.
- Also used for change detection and motion detection.
- The result can be negative, so it must be **rescaled** to 0 to L−1.

### Image averaging (noise reduction)
- Take K noisy images g_i(x,y) = f(x,y) + η_i(x,y), where the noise has zero mean and is uncorrelated.
- **ḡ(x,y) = (1/K) Σ g_i(x,y)**
- E{ḡ} = f and σ²_ḡ = σ²_η / K, so **noise falls as K increases**.
- Used in astronomy, where many low-light frames are averaged.

### Smoothing spatial filters (in full)
**1. Linear (averaging / low-pass):**
```
Box (1/9):       Weighted average (1/16):
1 1 1            1 2 1
1 1 1            2 4 2
1 1 1            1 2 1
```
- Reduces noise and blurs fine detail. Used before extracting large objects.

**2. Non-linear (order-statistic):**
- **Median filter**: replace the pixel with the **median** of its neighbourhood. Excellent for **salt-and-pepper noise** and keeps edges sharp.
- **Max filter**: finds the brightest points (removes pepper noise).
- **Min filter**: finds the darkest points (removes salt noise).

### Frequency-domain enhancement (in full)
**Basic filtering steps:**
1. Multiply f(x,y) by (−1)^{x+y} to centre the transform
2. Compute F(u,v), the DFT
3. Multiply by the filter: G(u,v) = H(u,v) F(u,v)
4. Take the inverse DFT
5. Take the real part
6. Multiply by (−1)^{x+y}

**Properties of the 2-D DFT:** F(0,0) = MN × average grey level (the DC component). Low frequencies represent smooth regions; high frequencies represent edges and noise. Also separable, periodic, conjugate symmetric, translation and rotation properties.

**High-pass (sharpening) filters:** H_HP = 1 − H_LP

| Filter | Formula |
|---|---|
| Ideal HPF | H = 0 if D ≤ D₀, else 1 |
| Butterworth HPF | H = 1 / [1 + (D₀/D)^{2n}] |
| Gaussian HPF | H = 1 − e^{−D²/2D₀²} |

Here D(u,v) = √[(u − M/2)² + (v − N/2)²] is the distance from the centre.

- **Laplacian in the frequency domain:** H(u,v) = −4π²D²(u,v)
- **High-frequency emphasis:** H_hfe = a + b · H_HP

### Generating a spatial mask from the frequency domain
- Because of the convolution theorem, every frequency filter H(u,v) has a spatial filter **h(x,y) = IDFT{H(u,v)}**.
- **Procedure:**
  1. Design H(u,v) in the frequency domain (for example a Gaussian low-pass)
  2. Take the **inverse DFT** to get h(x,y)
  3. Keep the central part of h(x,y) and **truncate it to a small mask** (3×3, 5×5)
  4. Use that mask for spatial convolution
- Example: the IDFT of a Gaussian H(u,v) is also a Gaussian, h(x) = √(2π)σA e^{−2π²σ²x²}, with all-positive coefficients. That is why the smoothing masks are all positive. A Gaussian high-pass gives a mask with a positive centre and negative surround, which is the shape of the Laplacian mask.
- **Why do this?** Design is intuitive in the frequency domain, while implementation is faster in the spatial domain with small masks (no FFT needed).

---

## Module 3 — Remaining topics

### Noise in colour images
- The noise models (Gaussian, impulse/salt-and-pepper, uniform, Rayleigh, gamma, exponential) apply to **each colour channel**.
- Noise can be **different in each channel**, because each channel's sensor behaves differently.
- In **RGB**, noise in one channel shows up as coloured speckles.
- Converting to **HSI**: noise mostly affects **hue and saturation**, and intensity is only mildly affected, because it averages R, G and B.
- Filtering: apply averaging or median filtering per channel, or filter only the I component in HSI.

### Lossy predictive coding (DPCM)
```
ENCODER:
f(n) --(+)--> e(n) --> [Quantizer] --> ė(n) --> [Symbol Encoder] --> compressed
        ^ (−)                            |
        |                                v
     f^(n) <-- [Predictor] <-- ḟ(n) = ė(n) + f^(n)
```
- Same as lossless predictive coding, but a **quantizer** is added for the prediction error.
- The predictor works from the **reconstructed** values ḟ(n), not the original values, so the encoder and decoder stay in sync.
- **Delta modulation (DM):** the simplest form. The quantizer has only two levels, ±ζ (1 bit per pixel).
  - **Slope overload**: ζ is too small to follow fast changes, so edges blur
  - **Granular noise**: ζ is too large, so flat areas look grainy
- Optimal predictor (DPCM): choose the α_i that minimize the mean-square prediction error.

### Image compression standards

| Standard | Type | Details |
|---|---|---|
| **CCITT Group 3 / 4** | Binary (fax) | Run-length + Huffman; G4 uses 2-D coding |
| **JBIG / JBIG2** | Binary (bi-level) | Context-based arithmetic coding |
| **JPEG** | Continuous-tone still | DCT on 8×8 blocks, quantization, zig-zag, Huffman (lossy) |
| **JPEG-LS** | Lossless / near-lossless | Predictive coding |
| **JPEG 2000** | Continuous-tone still | **Wavelet** (DWT) + arithmetic coding; no blocking artefacts; progressive transmission |
| **GIF** | Still, 8-bit palette | LZW (lossless) |
| **PNG** | Still | Predictive + DEFLATE (lossless) |
| **TIFF** | Container | Supports LZW, JPEG, CCITT, etc. |
| **MPEG-1/2/4, H.261/H.264** | Video | DCT + **motion compensation** (inter-frame prediction) |

### Procedure for JPEG — see Q10.

### Concepts of image security
Images must be protected from unauthorized access, copying and tampering.
1. **Image encryption**: scramble the pixel values or positions with a key (chaotic maps, AES on image data, pixel permutation). Only someone holding the key can view the image.
2. **Digital watermarking**: embed **ownership information** (a logo or ID) in the image.
   - *Visible* (a logo on top) or *invisible* (hidden in pixel bits or DCT/DWT coefficients)
   - Requirements: **imperceptibility, robustness** (survives compression and cropping) and **recoverability**
   - Uses: copyright protection, authentication, tamper detection
3. **Steganography**: hide a secret message inside an image, for example by **LSB substitution** (replacing the least significant bit of each pixel). The goal is secrecy of communication.
4. **Image authentication / hashing**: a digital signature or hash that detects any modification.

| Watermarking | Steganography |
|---|---|
| Protects the cover image (ownership) | Protects the hidden message |
| Existence may be known | Existence is secret |
| Robustness matters most | Capacity and undetectability matter most |

---

# PART A — Short answers (3 marks each)

**Components of DIP** — see Q2. Sensors, specialized hardware, computer, software, storage, display, hardcopy, network.

**Neighbours of a pixel** — N4: the 4 horizontal and vertical neighbours; ND: the 4 diagonals; N8 = N4 ∪ ND (see Q3).

**Characteristics of image negatives** — s = L−1−r. Reverses intensity; linear; reversible; enhances white detail in dark regions (medical images).

**Histogram** — a plot of h(r_k) = n_k, the number of pixels at each intensity. Normalized: p(r_k) = n_k/MN. It shows brightness and contrast and is used for equalization and thresholding.

**Spatial ↔ frequency filtering correspondence** — by the convolution theorem, f★h ⇔ F·H. A spatial mask and its frequency filter H(u,v) form a Fourier-transform pair. Smoothing masks correspond to low-pass filters and sharpening masks to high-pass filters.

**Advantages of frequency-domain filters** — intuitive design; faster for large masks through the FFT; easy removal of periodic noise; ideal, Butterworth and Gaussian shapes can be controlled precisely.

**Types of noise in colour images** — Gaussian, salt-and-pepper (impulse), Rayleigh, gamma, exponential, uniform and periodic. Noise can be different in each R, G, B channel. Converting RGB to HSI spreads the noise mostly into **hue and saturation**, and averaging is less effective there.

**Relative data redundancy and compression ratio** — C = b/b′; R = 1 − 1/C. For example, b = 1 Mbit and b′ = 0.1 Mbit give C = 10 and R = 0.9.

**Halftoning** — showing continuous tone using **dots of varying size or density**, since printers only produce ink or no ink. The eye blends the dots into grey shades. In **colour halftoning**, separate C, M, Y and K screens are printed at different angles to avoid moiré patterns.

**Image sampling and quantization** — **Sampling** digitizes the coordinates (spatial resolution). **Quantization** digitizes the amplitude (intensity levels, 2^k). Too few samples cause checkerboard effects; too few levels cause false contouring.

**Colour models** — **RGB** (additive; monitors), **CMY/CMYK** (subtractive; printing; C = 1−R, M = 1−G, Y = 1−B), **HSI** (hue, saturation, intensity; close to human perception).

**Interpixel redundancy** — neighbouring pixels are correlated, so values can be predicted. It is removed by run-length coding, predictive coding or transforms (see Q9).

**Spatial resolution vs intensity resolution** — spatial resolution is the smallest detail you can see (dpi, number of pixels). Intensity resolution is the smallest change in level you can see (bits per pixel).

**Applications of DIP** — medical (X-ray, CT, MRI), remote sensing and satellite images, industrial inspection, biometrics (face, fingerprint), document processing (OCR), astronomy, forensics.
