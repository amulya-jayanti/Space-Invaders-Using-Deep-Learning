# Space-Invaders-Using-Deep-Learning\
Developed a Deep Q-Network (DQN) agent using Stable-Baselines3 to play Space Invaders, achieving human-like performance by optimizing attack and defense strategies.\

Objective:\
Build an AI agent capable of playing the Space Invaders game using Deep Reinforcement Learning.

Gymnasium:\
The primary environment used for this project is Gymnasium, which provides access to over 1000 retro game environments.\
This platform is particularly suitable for our reinforcement learning project because of its standardized interfaces for various game environments, consistent reward structures, frame-based state representations, and easy environment manipulation and monitoring.

Libraries Used:  Stable-Baselines3, Gymnasium, cv2 (OpenCV)

**Description of Environment:**

Environment Name: SpaceInvaders-v4

Observation Space:\
By default, the environment returns the RGB image that is displayed to human players as an observation.\
RGB  pixel frames of size 210 x 160 x 3, with each pixel of RGB values in range[0,255], where frames are processed to stack 3 consecutive frames to provide temporal awareness\
Preprocessed using cv2 to resize frames and normalize pixel values.

Action Spaces: We have 6 actions : ['NOOP', 'FIRE', 'RIGHT', 'LEFT', 'RIGHTFIRE', 'LEFTFIRE’] referring to no operation, fire, move right, move left, fire to the right and fire to the left.

Rewards:\
+1 for destroying an enemy\
0 for no action or missed shots\
-1 for losing a life

Agent:\
Algorithm Used: PPO (Proximal Policy Optimization)\
Proximal Policy Optimization (PPO) is a gradient descent reinforcement learning algorithm that optimizes policy networks using a clipped objective function to ensure stable and efficient updates, balancing exploration and exploitation.

Policy Network:\
First used Mlp Policy (Multi-Layer Perceptron) which works on flat input.\
Then used CNN Policy that leverages convolutional layers for image-based observations.\
Then used evaluate_policy from the library, which evaluated performance of Mlp policy and CNN policy and compared using their mean reward values through the number of episodes. 

Training:\
Training steps: 50,000 steps\
Hyperparameters:\
	Learning rate: 0.0003\
	n_steps=2048\
	Batch Size: 64\
	Entropy coefficient: 0.01\
Approx_KL=0.024 measures how smoothly PPO is updating the policy (lower is more stable).\
PPO training loop follows these steps:\
Collect Timesteps: PPO gathers experience for n_steps=2048 timesteps before updating the policy.\
Perform an Update (Iteration): After n_steps, PPO updates the policy. Here, Iterations=25\
Repeat Until total_timesteps=51200 is reached.

Results & Deployment:\
CNN Policy converges better at 50,000 steps with improved mean rewards of 291.33 compared to Mean rewards of 287.00 for Mlp Policy.\
Final Mean Score across 10 episodes: 257.5 for CNN Policy as compared to 135.5 for Mlp Policy.





