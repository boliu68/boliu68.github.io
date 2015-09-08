# Notes on Sure Screening Interaction Selection

#### Lee, S., Lozano, A., Kambadur, P., & Xing, E. P. (2015, April). An Efficient Nonlinear Regression Approach for Genome-Wide Detection of Marginal and Interacting Genetic Variations.

- Summary in my own understanding:


1. A screening algorithm based on iterative sure independent screening theory.
   - The marginal and the pairs are all evaluated using cheap method. And the top features or pairs are selected. ***Although this save a lot of computation, for high order interactions more than 2nd order, it is still exponential that is not acceptable.***
2. After the few SNPs and interactions are selected. We solve the effects of each SNPs or interactions. To consider the nonlinear relationship of interactions. The piecewise linear model is utilized.
3. To control the false positive, for different parameter, we randomly sampled $$\frac{N}{2}​$$ samples and run piecewise linear model on this part of data.
   - As the number of false positive can be bounded according to our parameter ***supported by stable selection theory***, we choose a small subset of SNPs and pairs that satisfy  the false positive requirement.


- Evaluation Metrics
  - False positive control
  - Statistical power
  - Screening scalability

#### Fan, Y., Kong, Y., Li, D., & Zheng, Z. (2015). Innovated interaction screening for high-dimensional nonlinear classification. *The Annals of Statistics*, *43*(3), 1243-1272.

Summary in my own understanding

###### Some assumptions:

- The theory works for Gaussian **two-class Gaussian classification** problem.

$$
z=\triangle z_1 + (1-\triangle)z_2\\
z_1 \text{ and } z_2 \sim N(\mu_1,\Sigma_1) \text{ and } N(\mu_2, \Sigma_2) \text{ respectively}\\
\triangle \sim Ber(\pi)
$$

- The min and max eigenvalue of covariance if bounded.

$$
\tau_1\leq \lambda_{min}(\Sigma_k)\leq\lambda_{max}(\Sigma_k)\leq\tau_p
$$

- The variance of different class can be distinguished.
- $$\Sigma_1^{-1}$$ and $$\Sigma_2^{-1}$$ are both $$K_p$$ sparse. And $$l_\infty(\Sigma_k^{-1})$$ is bounded.
- ​

###### Methods:

- Reduce the number of interactions to a moderate order by a new inter- action screening approach
- Identify both important main effects and interactions using some variable selection techniques
- An interaction screening criteria that can be proved to enjoy sure screening property.

###### Interaction screening method

1. For binary classification problem, the importance of single feature to interaction is attributed as the difference of variance of two classes.
   - Transform the feature space by using $$\Sigma_1^{-1}x$$  (where $$\Sigma_1$$ denote the covariance of samples in class $$1$$). And similarly, we also transform the original features using $$\Sigma_2^{-1}x$$ .
   - In the new feature space, the difference between variance of two class represents how important the single feature is for interaction.

###### Sure screening property

###### When $$\Sigma^{-1}$$ is known

- ​







