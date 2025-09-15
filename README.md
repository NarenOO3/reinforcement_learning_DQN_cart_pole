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
- First attempt: it balanced the pole 🎉  
- But… it kept sliding off to the left with the pole balanced until the cart went out of bounds 🙃    
- This happened because the reward was simply the default `+1` for all states.  

### Model v2
- Then I had a lightbulb moment 😅...  
- Modified the reward to: reward = **1 - |x|** where *x* is the cart’s position.  
- With this change, I trained the model again, which not only balanced the pole but also maintained the cart’s position near the center🏆.  

## Key Takeaways
This little project taught me:  
- Reward functions are everything — shape them wisely.  
- Hyperparameters can make or break training.  
- GPUs make reinforcement learning experiments way more fun (and way faster).  

## Code & Models
The training code and saved models (`model_v1` and `model_v2`) can be found in this repository. 
