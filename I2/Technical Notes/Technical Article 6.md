
**Reinforcement Learning**: Using trial and error to learn a strategy that maximizes reward in a selected environment

## Symbols and Definitions

**State:** ($s \in \mathcal{S}$)
- Snapshot of the world at a time $t$, denoted $s_t$
- Typically a vector
- **Example**: In pong, the state would hold information such as the position of the paddles and the ball

**Action:** ($a \in \mathcal{A}$)
- An action is a choice that the agent makes within an environment that influences it
- These are encoded in a variety of ways that's dependent on the nature of the problem
- **Example**: In pong, the action could simply be a scalar between -1 and 1 encoding how much to move the paddle

**Agent:**
- Tries to act optimally given some state, policy, and reward
- **Example**: A paddle in pong

**Policy:** ($\pi$)
- Outputs actions given the state of the environment
- Deterministic policies are represented as $\pi(s) \rightarrow a$ , which means there's a direct mapping between each state of the world and the best action to take at that time.
- Stochastic policies are defined as $\pi(a_t | s_t)$. This means that given some state, the policy gives you all the possible actions and tells you how good each action is at that particular time

**Environment**
- A space that the agent can interact with and influence. Also thought of as all possible states
- Contains transition dynamics to move from one state to another

**Reward**
- Scalar value given to the agent after it takes an action, determined through a reward function
- Represented as $R(s_t, a_t) = r_t$
- Serves as a learning signal for the agent, and is used to update its parameters

**Trajectory:** ($\tau$)
- A trajectory is a series of states, actions, and rewards that culminate in a final state
- Allow us to replay the entire path an agent took given some initial condition

## Markov Decision Process
- Transitions within an environment from state to state must be  a Markovian decision process (MDP)
- This means that the transition from one state to another must be entirely independent of the history of states
- This policy is adopted because there are less things to deal with overall
- States are often defined specifically to create MDPs

## On vs. Off-Policy RL
- **On-Policy RL**: RL algorithms can only use information from the current trajectory to update its policy
	- Usually more stable, but less sample efficient and have high variance
- **Off-policy**: Use information collected from older policies to update the current one
	- More sample efficient
	- Less stable and require a few tricks to work properly

## Imitation Learning

### Behavior Cloning
- Blurs the line between supervised and reinforcement learning
- Given some optimal pair of states and actions $(s^{*}, a^{*})$ , to clone this behavior in our agent we can use the following optimization objective:
$$\text{argmax}_{\theta} \left[ \mathcal{E}_{(s^*, a^*) \in  \mathcal{D}} \log \pi_\theta(a^* | s^*) \right]$$
- This effectively means find the value of theta that maximizes the log-probability of us choosing $a^*$ given $s^*$
	- Log probability is used because probabilities that aren't one are heavily penalized 

### Problems with Behavior Cloning
- Not very adaptable to new situations. Has a quadratically compounding error
- Mode averaging: Averages between different behaviors since the model concludes that only one action is valid in a given state, when at times two actions might have the same impact 