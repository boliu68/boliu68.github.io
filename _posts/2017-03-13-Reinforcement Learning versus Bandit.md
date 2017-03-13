---
published: false
---
## Reinforcement Learning versus Bandit

Recently, I fulfill my PhD Qulifying Exam which focuses on Bandit and its application on online recommender system (RecSys). My supervisor keeps challenging the motivation of modeling RecSys as bandit problem compared to other Reinforcement Learning formulation. Caused quite few detail explanations are found online, I would like share my understanding of what differs bandit from other RL formulation in this post.

The exploitation-exploration tradeoff is emphasized when tackling canonical problem of sequential decision making under uncertainty. More concretely, an agent sequentially interacts with unkown environment and receive the rewards as shown in . The ultimate objective is to maximize the cumulative reward. Exploitation-exploration tradeoff is always formalized as Reinforcement Learning including Multi-Armed Bandit (MAB), Markov Decision Process (MDP), or Partially observable Markov Decision Process (POMDP).

$$e=mc^2$$