# Adversarial Attack of Reinforcement Learning Policies

* To see the **results**, check the [Results](#results) section.
* To learn **how to run the code**, check [this](#how-to-run) section.
* To learn more about the **_Pong_ environment**, check the [Environment](#environment) section.
* For a more **detailed report**, please check [here](https://github.com/mithun-bharadwaj/Attacking_RL_Policies/blob/master/REPORT_ATTACK_ON_RL_POLICIES.pdf).

## Deep Q-Learning
* **Action value function (Q-value)** yields the discounted return if the agent starts in state **_s_**, takes an action **_a_**, and follows the policy **_pi_**.
* **Q-Learning** is a model free (i.e, doesn't need to know the exact MDP) Reinforcement Learning algorithm to learn a policy that tells an agent the best action to take under the given crcumstances.
* As the number of valid states increases, the calculation of Q values become extremely difficult and intensive. 
* Neural networks are used in such cases as function approximators to estimate the Q values. This is **Deep Q-Learning** 

![DeepQ](/images/Deep_Q_Learning.png)

## FGSM Attack
* Adversarial examples are specialised inputs created with the purpose of confusing a neural network, resulting in the misclassification of a given input. 
* These notorious inputs are indistinguishable to the human eye, but cause the network to fail to identify the contents of the image.

![Adversasrial Attack](https://github.com/mithun-bharadwaj/Attacking_RL_Policies/blob/master/images/adversarial_attack.png)

* The **fast gradient sign method (FGSM)** works by using the gradients of the neural network to create an adversarial example. 
* For an input image, the method uses the gradients of the loss with respect to the input image to create a new image that maximises the loss.

![FGSM](https://github.com/mithun-bharadwaj/Attacking_RL_Policies/blob/master/images/FGSM.png)

## Environment
* The environment is based on the Atari 2600 game Pong. It's vailable as a part of [OpenAI Gym.](https://gym.openai.com/envs/Pong-v0/)
* Since the environment is not directly available in the default OpenAI Gym package, wrappers are required to use the ```PongDeterministic-v4``` environment.
* The necessary wrappers can be downloaded from the [OpenAI baseline repository.](https://github.com/openai/baselines/tree/master/baselines/common)

## How to Run
1. Clone the repository and install the dependencies.
2. The main file which contains all the source code is [pong_RL.ipynb](https://github.com/mithun-bharadwaj/Attacking_RL_Policies/blob/master/pong_RL.ipynb).
3. Exexute all the cells till the bottom of the file where the model is loaded and the _play_ function is called.
4. Any of the models provided in the [model](https://github.com/mithun-bharadwaj/Attacking_RL_Policies/tree/master/model) folder can be loaded and tested for the attack.
5. Once the model is loaded there are 3 options:
    1. ```agent.play(num_episodes)``` - Simulates the policy **learned by the model** for a period of num_episodes.
    2. ```agent.play_with_fgsm_attack(num_episodes)``` - Simulates the policy **with FGSM attack** for a period of num_episodes.
    2. ```agent.play_with_noise(num_episodes)``` - Simulates the policy **with random noise** for a period of num_episodes.

## Results

### Training the model


Policy after 50 episodes of training              |  Policy after 400 episodes of training
:----------------------------------------------------------:|:------------------------------------------------:
<img width="190" height="300" src="https://github.com/mithun-bharadwaj/Attacking_RL_Policies/blob/master/gifs/training_50_episodes.gif"> |<img width="190" height="300" src="https://github.com/mithun-bharadwaj/Attacking_RL_Policies/blob/master/gifs/training_400_episodes.gif">
### Attacking the policy

The policy obtained after training the model for 400 episodes was attacked using the FGSM method and compared to the scenario where random noise was added to the same policy.

FGSM Attack              |  Random Noise
:----------------------------------------------------------:|:------------------------------------------------:
<img width="190" height="300" src="https://github.com/mithun-bharadwaj/Attacking_RL_Policies/blob/master/gifs/attack_400_episodes.gif"> |<img width="190" height="300" src="https://github.com/mithun-bharadwaj/Attacking_RL_Policies/blob/master/gifs/random_noise_400_episodes.gif">

## References

1. Adversarial Attack and Defenses Competition, [NIPS 2018, Alexey Kurakin, et al.](https://arxiv.org/pdf/1804.00097.pdf) 
2. Explaining and Harnessing Adversarial Examples, [NIPS 2015, Ian Goodfellow, et al.](https://arxiv.org/pdf/1412.6572.pdf) 
3. Playing Atari with Deep Reinfrocement Learning, [NIPS 2013, Volodymyr Mnih, et al.](https://arxiv.org/pdf/1312.5602v1.pdf)

