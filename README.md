# Deep Q-Learning on CartPole-v0

In this project, I trained two models using **Deep Q-Learning** to balance the pole in `CartPole-v0` from Gymnasium.  

## Model Architecture
- **Input layer**: 4 inputs  
- **Hidden layers**: Two fully connected layers with 32 units each, ReLU activation  
- **Output layer**: Linear output  
- **Policy**: Epsilon-greedy  
- **Training**: Soft update of `target_q_network`  

## Results

### Model v1
- It balanced the pole 🎉. 
- But… it kept sliding off to the left with the pole balanced until the cart went out of bound.   
- This happened because the reward was simply the default `+1` for all states.

### Model v2
- Then I had a lightbulb moment 😅...  
- Modified the reward to: reward = **1 - |x|** where *x* is the cart’s position.  
- With this change, I trained the model again, which not only balanced the pole but also maintained the cart’s position near the center.
  
| untrained_model        |      cart_pole_model_v1    |cart_pole_model_v2|
| ---------------------- | ---------------------- |----------------------|
| ![untrained_cart_pole_combined](https://github.com/user-attachments/assets/4c4c4d30-9896-434e-a250-cd4c09eb5cbb)| ![trained_cart_pole-episode_without_positional_balance](https://github.com/user-attachments/assets/f709aeb2-b0ae-4900-a450-fd26ccaa3564) |![trained_cart_pole-episode-0](https://github.com/user-attachments/assets/4ce7f684-92b6-4997-917e-dc2448b023ed)|





## Key Takeaways
This little project taught me:  
- Reward functions are everything — shape them wisely.  
- Hyperparameters can make or break training.  
- GPUs make reinforcement learning experiments way more fun (and way faster).  

## Code & Models
The training code and saved models (`cart_pole_model_v1.h5` and `cart_pole_model_v2.h5`) can be found in this repository. 
