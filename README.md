# 107cct

My project applies Cultural Consensus Theory (CCT) to a dataset on local plant knowledge using a Bayesian approach in PyMC. The model estimates two key components: each informant’s competence (D), and the consensus answer for each item (Z). The idea is that informants with higher competence are more likely to give answers that match the group consensus!

The observed data matrix X (responses from informants) is modeled as a Bernoulli distribution, where the probability of a correct response depends on the informant’s competence and the consensus answer. The probability of each response is calculated as:

p = Z * D + (1 - Z) * (1 - D)

To implement this in PyMC:
Competence D is modeled with a Uniform(0.5, 1.0) prior for each informant.
Consensus answers Z use a Bernoulli(0.5) prior for each item.
Both D and Z are reshaped for broadcasting over the full response matrix.
The observed responses X are modeled as Bernoulli(p).

Sampling was done with 4 chains and 2000 draws, including 1000 tuning steps.

The posterior means of the competence scores showed variation among informants. The most competent informant was P{most_competent + 1}, while the least competent was P{least_competent + 1}.

The inferred consensus answers (rounded mode of the posterior mean) were:

{Z_mode.tolist()}

To evaluate how the model's consensus compared with a simple majority vote, I computed the item-wise majority across raw responses and found an agreement of {agreement * 100:.1f}% with the model’s consensus.

This model captures both group-level consensus and individual-level competence while taking into account the informants’ reliability. Compared to majority vote, the CCT approach gives a more nuanced estimate of shared cultural beliefs by down-weighting less reliable participants. The implementation closely follows the structure outlined in the assignment prompt and successfully demonstrates the core logic of Cultural Consensus Theory in a Bayesian framework.

AI Statement: I used Chat GPT for code outline and implementation, as well as for explaining difficult concepts. 
