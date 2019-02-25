# Safe Reinforcement Learning Algorithms   

## HCOPE (High-Confidence Off-Policy Evaluation.)


Python Implementation of HCOPE lower bound evaluation as given in the paper:
Thomas, Philip S., Georgios Theocharous, and Mohammad Ghavamzadeh. "High-Confidence Off-Policy Evaluation." AAAI. 2015.


![CUT Inequality](https://github.com/hari-sikchi/safeRL/blob/master/Theorem.png)


### Requirements
* PyTorch
* Numpy
* Matplotlib
* scipy
* gym

### Running Instructions

1. Modify the environment in the main function, choosing from  OpenAI gym. (Currently the code works for discrete action spaces)    
2. Run python hcope.py   

### Notes
* The file policies.py contains the policy used in the code. Modify the policy to suit your needs in this file.   
* 
* To reproduce the graph given in the original paper explaining the long tail problem of importance sampling, use the 
```
visualize_IS_distribution()
```
method. Also, a graph of distribution of Importance sampling ratio is created which nicely explains the high variance of the simple IS estimator.
![Variance in simple IS](https://github.com/hari-sikchi/safeRL/blob/master/IS_variance.png)   

* All the values required for offpolicy estimation are initialized in the HCOPE class initialization.  
* Currently the estimator policy is defined as a gaussian noise(mean,std_dev) added to the behavior policy for estimator policy initialization in the function `setup_e_policy()`. The example in paper uses policies differing by natural gradient. But, this works as well.   
  
* To estimate c*, I use the BFGS method which does not require computing hessian or first order derivative.   
* The ```hcope_estimator()``` method also implements a sanity check, by computing the discriminant of the quadratic in parameter delta(confidence). If it does not satisfy the basic constraints, the program prints the bound predicted is of zero confidence.   
* The random variables are implemented using simple importance sampling. Per-decision importance sampling might lead to better bounds and is to be explored.   
* A bilayer MLP policy is used for general problems.   
* Results:   
Output format: 
![Output](https://github.com/hari-sikchi/safeRL/blob/master/Result.png)   


## Safe exploration in continuous action spaces - Dalal et al.

### Running Instructions
* Go inside ARS folder   
* run python code/ars_safe_exploration.py   

### Explaination

* Linear Safety Signal Model    
    
![Safety Signal](https://github.com/hari-sikchi/safeRL/blob/master/safety_signal.png)   



* Safety Layer via Analytical Optimization 
   
![Safety Layer](https://github.com/hari-sikchi/safeRL/blob/master/safety_layer.png)   

* Action Correction   
   
![Action Correction](https://github.com/hari-sikchi/safeRL/blob/master/safety_optimization.png)   


## Importance Sampling

Implementation of:    
* Simple Importance Sampling   
* Per-Decision Importance Sampling    
* Normalized Per-Decision Importance Sampling (NPDIS) Estimator    
* Weighted Importance Sampling (WIS) Estimator   
* Weighted Per-Decision Importance Sampling (WPDIS) Estimator    
* Consistent Weighted Per-Decision Importance Sampling (CWPDIS) Estimator   
    
Comparision of different importance sampling estimators:   
![Different Importance sampling estimators](https://github.com/hari-sikchi/HCOPE/blob/master/importance_sampling/importance_sampling.png)   

 Image is taken from phD thesis of P.Thomas:    
 Links: https://people.cs.umass.edu/~pthomas/papers/Thomas2015c.pdf   

