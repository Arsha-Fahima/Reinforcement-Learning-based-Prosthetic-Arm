# Reinforcement-Learning-based-Prosthetic-Arm
This project involves the development of an adaptive myoelectric prosthetic arm that uses reinforcement learning from human feedback (RLHF) to provide intelligent, personalized hand control. The system interprets electrical muscle signals (EMG) captured from the user’s forearm and converts them into hand actions. The innovation of this project lies in its dynamic learning capability. Initially, the model undergoes supervised pretraining using a labeled EMG dataset to learn the basic mapping between muscle activity and hand gestures. Once deployed, the prosthetic does not remain static—instead, it continuously adapts to the user through online reinforcement learning.

# Key Innovations:

Two-phase hybrid learning: supervised pretraining to establish a stable baseline policy, followed by online actor–critic reinforcement learning for user-specific adaptation.

Human-in-the-loop feedback: scalar rewards (+1/−1) directly guide online policy updates.

Lightweight, real-time inference pipeline: optimized feature extraction and model design to meet strict latency requirements for prosthetic control.

Design protection & dissemination: design patent granted; journal publication in progress (demonstrating novelty and reproducibility).



# Model Workflow:

Supervised Pretraining:
Actor–Critic model trained on labeled EMG dataset
Learns initial mapping between signals and actions

Real-Time Deployment:
User performs gestures
EMG signals → Preprocessing → Model Prediction → Prosthetic Action

Online RL Adaptation:
Actor updated with reward-guided learning
Critic adjusts value estimation
Model continuously improves for that specific user

# Algorithms & Implementation:

Model:
Shared feedforward network → splits into:
Actor head: Softmax over actions (policy).
Critic head: Predicts state value.
Implemented in PyTorch.

Supervised Pretraining:
Actor trained using Cross-Entropy Loss.
Critic trained using MSE Loss to estimate value.
Helps initialize stable policy before RL.

Online Reinforcement Learning (Actor–Critic / A2C):
After pretraining, model receives reward rₜ and updates using:
δₜ = rₜ + γ · V(sₜ₊₁) − V(sₜ)
actor_loss  = − log_prob(aₜ) × δₜ
critic_loss = MSE(V(sₜ), rₜ + γ · V(sₜ₊₁))
Total loss = actor_loss + critic_loss.

# Training Pipeline
Supervised Pre-Training:

Pretrain Epoch [1/50] Accuracy: 0.4190  
Pretrain Epoch [50/50] Accuracy: 0.9865  

Online RL Adaptation:

Online Epoch [1/50]  Accuracy: 0.9162  
Online Epoch [50/50]  Accuracy: 0.9734
