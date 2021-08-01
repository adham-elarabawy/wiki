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

![MRI Machine Deconstructed](../../.gitbook/assets/image%20%2826%29.png)

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

![](../../.gitbook/assets/image%20%2829%29.png)

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

Since each precessing nuclei also imposes a changing magnetic field on the nuclei around it, the spins eventually fall out of sync, which slowly decays the signal output since they become dephased. This is demonstrated by the _Free Induction Decay \(FID\)_ plot:

![Free Induction Decay \(FID\)](../../.gitbook/assets/image%20%2832%29.png)

{% embed url="https://www.youtube.com/watch?v=TQegSF4ZiIQ&ab\_channel=thePIRL" %}

{% embed url="https://www.youtube.com/watch?v=M7yh0To6Wbs&ab\_channel=thePIRL" %}



