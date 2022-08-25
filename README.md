# RL-Cartpole-Balancing

balance cartpole using reinforcement learning

## Abstract

The idea of CartPole is that there is a pole standing up on top of a cart. The goal is to balance this pole by moving the cart from side to side to keep the stick balanced upright using a field of machine learning i.e reinforcement learning in which we have a inverted pendulum pined to a cartpole so that the pole can roatate and the cart can only move in one dimention .So firstly, our microcontroller takes input from environment which is the position and velocity of the cart, the angle of the pendulum from the straight upright position,and the angular velocity of the pendulum. with which rl process the data and sends the output as commands to the cartand such that it balances the pendulum
## Requirment

1) solidworks
2) vs code
3) python
4) open AI GYM


## Usage
### Prerequisite

reinforcement learning,python,solid works.
### Requirments

#### HARDWARE

1) 16 ballbearings
2) 2 1m pipes
3) 1 1inc thick wood plate
4) 1 thin wood plate 
5) washers
6) nuts
7) bolts
8) GT2 Timing Belt + 5mm teeth pulleys wheels
9) 3D printed parts

#### ELECTRONICS
1) Raspberry Pi 4
2) Stepper Motor Bracket
3) NEMA-17 Stepper Motor
4) ALITOVE DC 12V 10A Power Supply
5) encoder

### Design
#### Cart-Pole Hardware Design
The hardware design for our cart-pole is inspired from [this Instructable](https://github.com/gschaffner/cart-pole-control) but with a lot of modifications 

so here is the base model that we designed of the rails and cart where the pendulum will be mounted
![rail system]()

the wall is for the pendulum on which a hole will be made to insert the encoder to measure the angular velocity and angular position of the pendulum 

so here is the final model for that
![cartpole 3d model]()
you can get to see the whole model we made on solid works here(yaha solid works ka link dhalna hai) 

### Model Design
The model is what is shown above in the link. but here we will go step by step of the building process of it 

 1) Base plate was cut out and fixed 
   ![base plate]()

 2) Then 4 clamps were fixed in the base plate 2 on each for the pipes to be fixed in it
   ![clamp]()
   ![clamp with base plate]()

3) Pipes were fixed in the clamps and were fixed which were used as rails 
    ![with pipes]()

4) We made rails by this 3d printed piece u can see here 
    ![rail]()
   one rail was installed with 6 ball bearings 4 at each corners of the bottom and 2 in space between 

5) Now platform was also cut out from that base plate bord and two verticle supporters were also fixed between wich the encoder was fixed with a hole in the front support plate for the axel of the encoder to come out of that support plate so that the pendulum can be fixed in it 
    ![whole cart]()

6) A stepper motor was fixed in the base plate with a assembly that was also 3d printed 
    ![stepper motor]()

7) On the other side a pully was installed with the same assembly before to support the belt and the pendulum was also fixed on the encoder
    ![whole model]()
    ![with pendulum]()

### Circuit design

 ![circuit design]()

 At first we have to take inputs from the model for RL processing these four inputs were cart velocity , cart position, pendulum angular position and angular velocity .
 cart position and cart velocity was calculated from stepper motor [sepper_motor.py]() and the pendulum's angular position and velocity were calculated from encoder [encoder.py]()
 
now with these four inputs we got output signals by RL processing through Q Learning alrorithm [Q_Learning.py]() to stpper motor and then stepper motor will balance the vertical pendulum 

now basically what Q_Learning algorithm dose is that it learns the value of an action in a particular state. It does not require a model of the environment (hence "model-free"), and it can handle problems with stochastic transitions and rewards without requiring adaptations.

For any finite Markov decision process (FMDP), Q-learning finds an optimal policy in the sense of maximizing the expected value of the total reward over any and all successive steps, starting from the current state. Q-learning can identify an optimal action-selection policy for any given FMDP, given infinite exploration time and a partly-random policy. "Q" refers to the function that the algorithm computes – the expected rewards for an action taken in a given state.

#### algorithm 
After 
Δ
t
 steps into the future the agent will decide some next step. The weight for this step is calculated as 
γ
Δ
t
, where 
γ
 (the discount factor) is a number between 0 and 1 (
0
≤
γ
≤
1
  ) and has the effect of valuing rewards received earlier higher than those received later (reflecting the value of a "good start"). 
γ
  may also be interpreted as the probability to succeed (or survive) at every step 
Δ
t.
![bellman equation]()
where 
r
t
 is the reward received when moving from the state 

St to the state 
S
t
+
1
, and 
α
  is the learning rate 
(
0
<
α
≤
1
)

Note that 
Qnew
(
S
t
,
A
t
)
 is the sum of three factors:

1) Q(St,At): the current value 

2) αRt: the reward Rt=r(st,at) to obtain if action at is taken when in state st (weighted by learning rate)

3) αγ max Q(St+1,α): the maximum reward that can be obtained from state St+1(weighted by learning rate and discount factor)

for more refer [here](https://en.wikipedia.org/wiki/Q-learning#cite_note-:0-2)

### Work Flow
