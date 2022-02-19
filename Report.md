<h1>Udacity Deep Reinforcement Learning Project 3<h1>
<h1>Collaboration and Competition Report</h1>
  
  Collaboration and Competition Project is the third project of the Udacity Deep Reinforcement Learning Nanodegree Program.
  
  <h2>Problem Statement</h2>
  
  In this environment, two agents control rackets to bounce a ball over a net. If an agent hits the ball over the net, it receives a reward of +0.1. If an agent lets a ball hit the ground or hits the ball out of bounds, it receives a reward of -0.01. Thus, the goal of each agent is to keep the ball in play.
  ![image](https://user-images.githubusercontent.com/51778059/154127791-443df82d-228c-41fc-881a-37f723a6d02b.png)

   <h2>Solving the Environment</h2>

  The observation space consists of 8 variables corresponding to the position and velocity of the ball and racket. Each agent receives its own, local observation. Two continuous actions are available, corresponding to movement toward (or away from) the net, and jumping.

  The task is episodic, and in order to solve the environment, your agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents). Specifically,

- After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 2 (potentially different) scores. We then take the maximum of these 2 scores.
- This yields a single score for each episode.
  
The environment is considered solved, when the average (over 100 episodes) of those scores is at least +0.5.
  
  <h2>Learning Algorithm</h2>
  
  In order to train multiple agents, I implemented Multi Agent Deep Deterministic Policy Gradient [(MADDPG) algorithm](https://arxiv.org/pdf/1706.02275.pdf) as it requires the training of two separate agents, and the agents need to collaborate under certain situations (like don’t let the ball hit the ground) and compete under other situations (like gather as many points as possible). A MADDPG is composed of multiple DDPG agents.
  
  In MADDPG, each agent’s critic is trained using the observations and actions from all the agents, whereas each agent’s actor is trained using just its own observations. This allows the agents to be effectively trained without requiring other agents’ observations during inference (because the actor is only dependent on its own observations).You can find the pseudocode of the MADDPG algorithm below. 
  <img width="427" alt="image" src="https://user-images.githubusercontent.com/51778059/154129979-fe786303-9596-4cec-b54e-1e7ee11937cb.png">
  
 
  <h4>Hyperparameters</h4>
Replay buffer size: 10000
Batch size: 256
Gamma (discount factor): 0.99
Tau (soft update of target parameters): 0.001
Learning rate for actor: 0.0001
Learning rate for critic: 0.001
Weight decay: 0
Noise decay: 1

   <h4>Model</h4>
- Actor
The Neural Network has two hidden layers with 256 and 256 neurons, respectively. The activation function used is ReLU for the input and first layer and tanh for the output The output layer has 4 values which corresponds to the dimension of each action.
- Critic
The Neural Network has two hidden layers with 256 and 256 neurons, respectively. The activation function used is ReLU for the input and first layer and none for the output. The output layer has just one value which corresponds to the assesment made by the critic of the action chosen by the actor.
    
  <h2>Results</h2>
  After implementing MADDPG method, the score evolution can be seen below:
  <img width="356" alt="Screenshot 2022-02-19 211415" src="https://user-images.githubusercontent.com/51778059/154813625-ae2c893d-427f-40d1-9e37-81d1fee8792f.png">
  ![plot](https://user-images.githubusercontent.com/51778059/154813632-3ffe3ddd-ce15-4a6b-a6ee-0f50e8ec5fb7.png)
The environment has been successfully solved in 2311 episodes.

<h2>Ideas for Future Work</h2>
   I implemented MADDPG method and solved the environment. In order to improve the performance of the agents, some other methods and improvements can also be tried. 
  - More effort can be spent for hyperparameter optimization to improve results.
  - Different algorithms can be implemented such as [A2C](https://medium.com/deeplearningmadeeasy/advantage-actor-critic-a2c-implementation-944e98616b), [PPO](https://openai.com/blog/openai-baselines-ppo/) or [D4PG](https://arxiv.org/pdf/1804.08617.pdf) to compare the performance of training. 
  - Prioritized experience replay can also be tried to see if it improves the training time.
