# Bayesian-for-BOLD
This experiment will focus on developing simulations for blood oxygen level-dependent (BOLD) signals in functional Magnetic Resonance Imaging (fMRI) data that serve as the ground truth for Computational Parametric Mapping (CPM), a Bayesian approach for model-based fMRI experiments.


## Background 

A functional biological process is generated by a stimuli at the finger tip, through many neural pathways and the activation of the hemoglobin response function to manifest as BOLD signals in the brain imaging [1]. 

<img align = "right" src="https://raw.githubusercontent.com/EstellaD/Bayesian-for-BOLD/master/img/introBOLD.png" width=550> 
For functional MRI, there are two experiment designs, as indicated below [2]. A block design gives constant stimulus for a period of time, followed by no stimulus for a while. On the contrary, event-related design applies point stimulus, and the resulting BOLD signals over time are voxels in each fMRI image. In this experiment, we focus on event-related design. When a event-related BOLD signal is generated, it has a initial dip followed by a peak and then a post stimulus undershoot [3]. Given the shape of one single BOLD signal curve, we can approximate it with a inverse gamma distribution. 

<img align = "right" src="https://raw.githubusercontent.com/EstellaD/Bayesian-for-BOLD/master/img/BOLDsignal.png" width=300> 

Parameters in the CPM Bayesian framework:
* $K$, the multiplicative constant in steven's power law to control the magnitude of BOLD signal. In this study, we fix $K = 1$.
* $\alpha$, the power in steven's power law. We aim to explore which value of $\alpha$ gives the best parameter recovery when designing experiments.
* $Y$ simulated fMRI data at time $t$ from our event-related BOLD signals.  
* $\beta$, scaling effect in the GLM model. This study is a simplified case with only one $\beta = 1$ value in the GLM model.

There are two steps for the CPM Bayesian framework: 
1. Select a prior for $\beta$. In the current simulation, we chose a conjugate (flat/uninformative) prior for the inverse gamma distribution. We reduce the full likelihood by integrating out nuisance parameters.

2. We get the reduced likelihood $p(Y_t|\alpha)$, and then the posterior probability of the parameters $\alpha$ can be calculated through Bayes’ formula. 

For more information, please refer to [/SRP17_Dong_Conference_Post.pdf](https://github.com/estellad/Bayesian-for-BOLD/blob/master/SRP17_Dong_Conference_Poster.pdf).

## Running the simulation code

#### Requirements
This repository is implemented in MATLAB 3.7, with several dependency functions from [Statistical Parametric Mapping (SPM)](https://www.fil.ion.ucl.ac.uk/spm/) package developed by UCL for neuroimging. 

#### Files to run
1. `Efficiency.m` simulates the first experiment setting with jitters added to the BOLD signals.
2. `Effnojitter.m` simulates the second experiment setting without jitters.
3. `StarOneBeta.m` contains all the visualization code of the MAP with different power values. 

## Results
While in general, the proposed approach can successfully recover all powers ($\alpha$ value) selected, the neurometric power with $\alpha$ = 1.5 gives the best recovery rate. 

## Conclusion
* CPM can allow for accurate decoding of computational variables, but greater simulation variation for $\alpha$ values after 1.5.
* Experiment design efficiency appears at larger jitter involved with stimulation period shown to be almost invariant.
* Future study could investigate scaling effect $\beta$ and the multiplicative number $K$ to see their effects on experiment design efficiency.

## References
[1] Arthurs, O. J., & Boniface, S. (2002). "How well do we understand the neural origins of the fMRI BOLD signal?" *Trends in Neurosciences*, 25(1), 27–31. [https://doi.org/10.1016/S0166-2236(00)01995-0]

[2] Zhang, L., Guindani, M., & Vannucci, M. (2015). "Bayesian Models for fMRI Data Analysis." *Computational Statistics*, 7(1), 21–41. [https://doi.org/10.1002/wics.1339]

[3] AD Elster, ELSTER LLC. (2020). "BOLD and Brain Activity". *Questions and Answers in MRI*. [http://mriquestions.com/does-boldbrain-activity.html]
