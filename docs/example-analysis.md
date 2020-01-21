<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of Contents

- [Example analysis for two interacting oscillators](#example-analysis-for-two-interacting-oscillators)
  - [Finding the frequency interval for each oscillator](#finding-the-frequency-interval-for-each-oscillator)
  - [Wavelet phase coherence](#wavelet-phase-coherence)
  - [Dynamical bayesian inference](#dynamical-bayesian-inference)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Example analysis for two interacting oscillators 

This analysis is based on time-series gathered from the heart (an ECG signal) and the lungs (with a respiration belt). The heart and the lungs can then be viewed as two oscillators, and we want to investigate their interaction by using wavelet phase coherence and dynamical bayesian inference. 

## Finding the frequency interval for each oscillator

The first step of the analysis is to find the frequency interval for each oscillator in order to find at what frequencies they oscillate at. This can be done by ridge extraction. 

First start MODA. In the GUI press "Ridge extraction and filtering". In the top left corner press file > load time series. Load one of the signals (Resp.mat or ECG.mat). Put in the sampling frequency when prompted (250Hz), and then select coloumn wise or row wise depending on the data (row wise).

In the right corner there are a box called "Transform Options", here you specify the minimum and maximum frequency for the wavelet transform. For ECG choose from 0.5Hz to 2Hz, and then press "calculate transform" in the bottom right corner. Then in the box called "Band Marking" press mark region. Make sure your marked region includes the whole frequency region where the amplitudes are high. After you have marked your region press the button "Add marked region". When you have done this you can press "Extract ridges" at the bottom right corner. Save the data as a mat file. The ridge is the Ridge_frequency in the saved matlab structure.

---

**Screenshot illustrating ridge extraction, and how to choose the the marked region.**

![Picture illustrating ridge extraction, and how to choose the the marked region. From MODA.](/docs/images/Ridgeextractionregion.png)

---

![Picture illustrating ridge extraction for ECG. From MODA.](/docs/images/ECGridge.png)

---

![Shows the structure saved from MODA.](/docs/images/Structure.png)

---

Repeat for the respiration data, but do the wavelet transform from 0.5Hz to 0.6Hz.

![Picture illustrating ridge extraction for respiration. From MODA.](/docs/images/Respridge.png)

When you have done the ridge extraction you can find the frequency interval by using the data tips in "tools" when the figure is open, or you can use the max and min function in matlab for the array. 

The frequency intervals we obtained were:

ECG: 0.8920Hz to 1.2820Hz

Respiration: 0.1354Hz to 0.2875Hz


## Wavelet phase coherence

Note: you need to make a matrix containing the signals you want to find the wavelet phase coherence between, so make one with the ridge of the ECG and the respiration, and one with the ridge of ECG and ridge of respiration.

In the MODA GUI press "Wavelet Phase Coherence", and then load the timeseries. The frequency range you choose for this analysis should include the frequency intervals of both oscillators. Hence, an appropiate choice could be 0.12Hz to 1.3Hz.

Coherence should always be tested for significance, and therefore we use surrogates (see the section on surrogates in the MODA user manual). In this example we have used 30 Fourier Transform surrogates.

![Figure showing the Wavelet Phase Coherence in MODA, ECG ridge and respiration signal.](/docs/images/WPC.png)

![Figure showing the Wavelet Phase Coherence in MODA, ECG ridge and respiration ridge.](/docs/images/WPCridges.png)

High coherence can be seen between the two ridges from 1Hz to 1.3Hz. This is probably due to the respiration belt also measuring the heart rate. 


## Dynamical bayesian inference

Now press "Dynamical beyesian inference" in the MODA GUI, and load the matrix with two signals. 

The frequency ranges are now specified for each oscillator. In the box "Freq range 1" write the frequency interval for the first signal (0.8 to 1.3Hz for ECG), and in freq range 2 write the frequency interval for the second signal (0.13 to 0.29Hz for respiration). Then choose a number of surrogates (we have used 50 in this example), and press "Add parameter set". After this you can press "Calculate". 

![Figure showing the dynamical bayesian inference in MODA, ECG ridge and respiration signal.](/docs/images/BayesianIHRResp.png)

![Figure showing the dynamical bayesian inference in MODA, ECG ridge and respiration ridge.](/docs/images/BayesianIHRIRR.png)


