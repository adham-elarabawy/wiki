---
description: 'https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8962388'
---

# PnP Methods for MRI

### Image Recovery in MRI

#### K-Space Measurement

MRI outputs measurements that are _samples of the_ [_Fourier Transform_](../engineering/fourier/fourier-transform.md) of the image -- called the _k-space_.

* In a 2D scan, you have a two dimensional k-space. 
* In a 3D scan, you have a three dimensional k-space.

A _dynamic scan_ is simply including the additional temporal dimension.

Measurements are often collected in parallel from multiple coils. 

* Each coil has a corresponding sensitivity map that varies from patient-to-patient. 
* Sensitivity maps are generally treated as unknowns and must be recovered/estimated separately.
* Various methods exist for combining measurements from various coils, namely [RSS \(Root Sum Squares\)](https://accendoreliability.com/root-sum-squared-tolerance-analysis-method/)
  * You pretty much just sum the squares of the images generated from each coil, then square-root the sum. \(pixel-wise\)
  * You could also choose to combine measurements from multiple coils/estimate the sensitivity maps using ESPIRiT \(haven't read into this yet\).

#### Formulation

In dynamic parallel MRI with Cartesian sampling, the k-space measurements from the _i_th coild at time _t_ take the form:

$$
y_i^{(t)} = P^{(t)}FS_ix^{(t)} + w_i^{(t)} \newline
\text{where} \newline
x^{(t)} \in \mathbb{C}^N \text{ is vectorized 2D/3D image at time } t \newline
S_i \in \mathbb{C}^{N \times N} \text{ is a diagonal matrix sensitivity map for ith coil} \newline
F \in \mathbb{C}^{N \times N} \text{ is 2D/3D discrete Fourier transform}
\newline
P^{(t)} \in \mathbb{R}^{M \times N} \text{contains M rows of the } N \times N \text{ identity matrix}
\newline
w_i^{(t)} \in \mathbb{C}^M \text{ is additive white Gaussian noise (AWGN)}
$$

Acceleration Rate \(R\) = $$\frac{N}{M}$$

### Signal Recovery & Denoising

We can formulate our optimization problem as the following:

$$
\hat{x} = \arg_x \min \{ \frac{1}{2\sigma^2} ||y - Ax||^2_2 +\phi(x) \}
\newline
\text{where} \newline
A = P^{(t)}FS_i
$$

The input measurement $$x$$ is the k-space measurement

The matrix$$A$$converts from a multi-coil k-space measurement to an image \(spatial domain\) by sequentially applying the sensitivity map \(estimated\), discrete Fourier transform, and our subsampling mask.

The regularization term $$\phi(x)$$encodes some prior knowledge of $$x$$that can help narrow down solutions to our ill-posed optimization problem.

#### Intuition

My understanding of this process is that we're essentially creating an optimization problem whose goal is to come up with some reconstructed k-space vector that is as similar as possible to the original \(undersampled\) k-space measurement, by using the regularizer as guidance for which solution \(of many\) to converge on.

Therefore, the choice of regularizer \(prior\) is _extremely_ important, since it defines the characteristics of the reconstruction we get.

The data fidelity \(data consistency\) term is responsible for enforcing that the solution we get is as close as possible to our original subsampling.

### How do we solve the optimization?

In order to decouple the regularizer from the data fidelity term, we introduce a new variable.

![](../.gitbook/assets/image%20%288%29.png)

This re-formulation of our original optimization problem is relatively trivial, but gives rise to the following algorithm for solving the optimization problem:

#### Algorithm

Alternate between separately estimating $$x$$and estimating $$v$$.

### CNN Implementation

![](../.gitbook/assets/image%20%282%29.png)

![](../.gitbook/assets/image%20%2823%29.png)

#### Notes:

* For datasets, the first two dimensions representing the number of pixels and the last dimension representing the number of frames.
* The data sets were retrospectively downsampled at acceleration rates, R, of 6, 8, and 10 by using pseudorandom sampling \[26\]
* Sensitivity maps estimated from the time-averaged data using ESPIRiT.

#### MRI Recovery

They used PnP ADMM from \(2\) with $$f$$ as the CNN-based denoiser described previously; they called it **PnP-CNN.**

* employed a total of 100 ADMM iterations, and in each ADMM iteration, performed four steps of CG to approximate \(12\), for which we used $$\sigma^2 = 1 = \eta$$
* They used reconstruction SNR \(rSNR\) as a metric: $$||x||^2 / ||\hat{x} - x||^2$$

![](../.gitbook/assets/image%20%2821%29.png)







