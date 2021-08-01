# Magnetic Resonance Imaging \(MRI\)

## How does MRI work?

MRI is fundamentally rooted in the principle of Nuclear Magnetic Resonance \(NMR\):

### Nuclear Magnetic Resonance \(NMR\)

> Certain atomic nuclei demonstrate the ability to absorb and re-emit radiofrequency energy when placed in a magnetic field.

#### How does MRI utilize NMR?

1. The very strong magnetic field imposed by the large magnets in the MRI machine **aligns the nuclei.**
2. The MRI machine then emits a radiofrequency pulse to knock the nuclei out of alignment.
3. The nuclei then precess, giving off an RF signal \(NMR phenomenon\).
   1. **T2 Relaxation:** The RF signal doesn't last forever -- each type of tissue takes a different amount of time to stop emitting the RF signal.
4. The nuclei then realign with the field
   1. **T1 Relaxation:** The amount of time it takes for the nuclei to realign with the field.

{% embed url="http://www.giphy.com/gifs/YIyiAdC2CdlrTtaB9P" %}

### The Larmor Equation

$$
\omega = \gamma B
\newline \text{where }
\newline\omega:\text{frequency of spin precession}
\newline \gamma:\text{a constant inherent to the specific nucleus we're investigating}
\newline B:\text{strength of magnetic field}
$$

_Important conclusion:_ The frequency of precession $$\omega$$is proportional to the magnetic field  strength $$B$$.

### Mechanical Deconstruction

![MRI Machine Deconstructed](../../.gitbook/assets/image%20%2827%29.png)

The _large magnet_ \(purple\) that encapsulates all of the other components is responsible for establishing a _strong_ permanent magnetic field.

The _gradient coils_ are modulated \(by altering the $$\vec B$$field in $$\hat x, \hat y, \hat z$$\) to be able to localize where each rf signal is coming from. They are designed such that they produce linearly varying magnetic fields when current flows through them.

The _RF coils_ are responsible for sending/receiving the RF tipping pulse into the tissue \([step 2/3 above](./#how-does-mri-utilize-nmr)\).

### The Proton, Spin, & Precession

All clinical MRI machines are utilizing the single proton at the nucleus of hydrogen atoms for scanning. Traditional nomenclature refers to the hydrogen nucleus as a generic proton -- but it is noted that we are only really imaging protons _from hydrogen nuclei._

![](../../.gitbook/assets/image%20%2820%29.png)

The main property of protons that we are leveraging here is their quantum-mechanical _spin --_ which can be decomposed into a value representing its intrinsic angular momentum & its magnetic moment \(that effectively lets it act as a _tiny_ bar magnet\).

The aforementioned magnetic moment can be quantified in terms of the particle's spin quantum number and a constant called _gyromagnetic ratio_ $$\gamma$$:

$$
\vec \mu = \hbar\vec S\gamma
$$

### Signal Detection & the Larmor Equation

When the proton is knocked off-axis by the RF coils, they precess about the magnetic axis imposed by the large magnet $$B$$. Their precessing frequency  $$\omega$$matches the frequency of the magnetic flux going through a nearby coil of wire:

![](../../.gitbook/assets/image%20%2822%29.png)

Per Lenz's Law, this changing magnetic flux induces a voltage through the wire proportional to the rate of change of the flux. This is how we are able to detect an RF signal back!

$$
\text{Lenz's Law:} \space V = -\frac{d\phi}{dt}
$$

We can now simulate our detected signal and come to a few profound conclusions:

![](../../.gitbook/assets/image%20%2831%29.png)

We know our detected signal is sinusoidal -- the true insight comes from the[ Larmor Equation](./#the-larmor-equation):

1. Nuclei with different gyromagnetic ratio will precess at different frequencies in the same magnetic field -- allowing us to possibly distinguish between them.
2. Increasing the magnetic field strength $$\vec B$$ is the _only_ way to increase the frequency of precession $$\omega$$, since the gyromagnetic ratio is a value inherent to nuclei.
   * Even better, increasing the magnetic field strength also increases the amplitude of our signal, due to Lenz's law's formulation around the _rate of change of magnetic flux_, which would be higher with higher frequencies.
3. The greater the flip angle, the larger the magnitude of our detected signal, since it would impose a larger change in magnetic flux -- corresponding to a higher voltage signal.

![](../../.gitbook/assets/image%20%2824%29.png)

#### A brief intermission about flip angle

Technically, a particle can only stably exist in one of two states: spin-up & spin-down. However, the quantum reality is that the flip angle is encapsulated in the transition between those two states, which happens in a continuous manner.

### Detected Signal

$$
S(t) =N \sin(\theta)\gamma B \cos(\omega t) e^{-t/T_2}\newline \text{where} \newline
N: \text{number of spins}
\newline \theta: \text{flip angle}
$$

In reality, there are many, _many_ nuclei being affected by this MRI procedure. Their collective contribution to the signal is encapsulated within the $$N$$constant in the equation above.

### T2 Weighting & Echo Time

Since each precessing nuclei also imposes a changing magnetic field on the nuclei around it, the spins eventually fall out of sync, which slowly decays the signal output since they become dephased. This is demonstrated by the _Free Induction Decay \(FID\)_ plot:

![Free Induction Decay \(FID\)](../../.gitbook/assets/image%20%2837%29.png)

The differing rates of decay can be used \(alongside a threshold\) to differentiate between different types of tissue. The quicker the signal decays \(and the shorter the T2 duration\), the quicker the spins fall out of phase. If we transition into the rotating frame \(setting $$\omega=0$$to better observe the decay rates\), we can arrive at the following modified FID:

![](../../.gitbook/assets/image%20%2826%29.png)

The _Echo Time_ is the amount of time we wait to scan the image after we perform [step 2 of our MRI procedure](./#nuclear-magnetic-resonance-nmr) \(knocking the spins out of alignment with the B field, causing them to precess\). This is a threshold set by the MRI technician to maximize contrast between tissues. This type of imaging \(where the echo time is set to some threshold to maximize tissue contrast\) is called a _T2 Weighted Image_:

![T2 Weighted Image](../../.gitbook/assets/image%20%2834%29.png)

### Spin Density Image

The above FID plot simplifies the thresholding by assuming that all the signals have the same starting amplitude -- which is a false assumption since each type of tissue has varying densities of hydrogen atoms \(and thus protons\). A more accurate FID plot that captures the true nuance behind the selection of the echo time threshold is shown below. 

![A more accurate FID plot](../../.gitbook/assets/image%20%2830%29.png)

Additionally, this plot seems to indicate that there are certain thresholds that would make our signals indistinguishable \(when the signal amplitudes cross each other\). The reason for this quick aside is to note that in some cases \(such as below\), the quicker we detect the signal, the better of a signal we actually get -- which isn't represented in the initial FID plot above.

If we set our _echo time_ to $$0$$, the $$e^{-0/T_2}$$term goes to 1, and we are simply measuring the number of protons in each tissue. The output of this type of imaging \(with echo time= $$0$$\) is called a Spin Density Image:

![Spin Density Image](../../.gitbook/assets/image%20%2832%29.png)

### T1 Relaxation

At this point in time, we can assume that the protons have been completely dephased \(all out of alignment\), which corresponds to the signals converging to 0 on the FID plots above. They then re-align with the magnetic field $$\vec B$$, in a process called T1 Relaxation.

![](../../.gitbook/assets/image%20%2835%29.png)

$$
M(t) = M_0(1 - e^{-t/T_1})
$$

### T1 Weighting & Relaxation Time

#### Boltzmann Magnetization

As the spins align with the magnetic field, they converge on to the sample's _Boltzmann Magnetization._ The rate at which they converge back to the Boltzmann Magnetization is determined by the nuclei's $$T_1$$parameter, which is another factor used to contrast differing tissues in the imaging process.

### 





{% embed url="https://www.youtube.com/watch?v=TQegSF4ZiIQ&ab\_channel=thePIRL" %}

{% embed url="https://www.youtube.com/watch?v=M7yh0To6Wbs&ab\_channel=thePIRL" %}



