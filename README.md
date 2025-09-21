# Deep Q-Learning on CartPole-v0

In this project, I trained two models using **Deep Q-Learning** to balance the pole in `CartPole-v0` from Gymnasium.  

## Model Architecture
- **Input layer**: 4 inputs  
- **Hidden layers**: Two fully connected layers with 32 units each, ReLU activation  
- **Output layer**: Linear output  
- **Target Policy**: Greedy Optimal policy 
- **Behaviour Policy**: Epsilon Greedy policy 
- **Training**: Soft update of `target_q_network`  

## Results

### Model v1 (DQN)
- It balanced the pole 🎉. 
- But… it kept sliding off to the left with the pole balanced until the cart went out of bound.   
- This happened because the reward was simply the default `+1` for all states.

| untrained_model        |      cart_pole_model_v1    |
| ---------------------- | ---------------------- |
| ![untrained_cart_pole_combined](https://github.com/user-attachments/assets/4c4c4d30-9896-434e-a250-cd4c09eb5cbb)| ![trained_cart_pole-episode_without_positional_balance](https://github.com/user-attachments/assets/f709aeb2-b0ae-4900-a450-fd26ccaa3564) |

### Model v2 (DQN)
- Then I had a lightbulb moment 😅...  
- Modified the reward to: reward = **1 - |x|** where *x* is the cart’s position.  
- With this change, I trained the model again, which not only balanced the pole but also maintained the cart’s position near the center.
  
### Model v3 (DDQN + PER)
- In this version, we improved the baseline DQN by applying **Double DQN (DDQN)** and **Prioritized Experience Replay (PER)**.
- DDQN helps reduce **overestimation bias**, leading to smoother learning curves and more accurate Q-value estimates (they don’t drift as much compared to vanilla DQN).
- PER improves sample efficiency: instead of sampling transitions uniformly from the replay buffer, it prioritizes experiences with higher TD-error. This means the agent learns more from transitions where its prediction was wrong, **speeding up convergence**.
- Together, DDQN brings stability while PER accelerates learning, resulting in a more robust and efficient training process.
  

| cart_pole_DQN_model       |      cart_pole_DDQN_PER_model    |
| ---------------------- | ---------------------- |
| ![DQN_trained_cart_pole-episode-0](https://github.com/user-attachments/assets/337841db-a344-4ff7-ae75-94fa9b3d417e)| ![DDQN_PER_trained_cart_pole-episode-0](https://github.com/user-attachments/assets/9eb5054c-f82a-428a-91af-8fbfd2caef33) |

### Comparison Plots
- **Plot 1** Shows learning efficiency (faster rise = better).
- **Plot 2** Shows reward variance to show the stability of learning.
- **Plot 3** Shows the reduction of Q-value overestimation.
- **Plot 4** Shows sample efficiency (fewer episodes to hit the threshold).
![comparison](https://github.com/user-attachments/assets/b52d2e93-9b0f-47f6-a4f7-a8cc52ff99a3)




## Key Takeaways
This little project taught me:  
- Reward functions are everything — shape them wisely.  
- Hyperparameters can make or break training.  
- GPUs make reinforcement learning experiments way more fun (and way faster).
- There is always room for improvement in learning and optimization techniques.  

## Code & Models
The training code and saved models (`cart_pole_model_v1.h5`,  `cart_pole_DQN_model.h5`, and `cart_pole_DDQN_PER_model.h5`) can be found in this repository. 
