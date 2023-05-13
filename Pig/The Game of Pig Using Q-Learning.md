Here is our code for [[The Game of Pig]]
### Here is how the `PigEnv` agent class `__init__`  is implemented: 

```python
def __init__(
              self,
              die_sides = 6,
              max_turns = 20,
              max_points = 100,
              opponent_policy = random_opponent_policy,
              learning_rate = 0.01,
              epsilon = 0.05,
              discount_factor = 0.9):

        self.opponent_policy = opponent_policy
        self.max_turns = max_turns
        self.action_space = {'bank':0, 'roll':1}
        self.die_sides = die_sides
        self.max_points = max_points
        self.alpha = learning_rate
        self.epsilon = epsilon
        self.gamma = discount_factor
```

Let's describe the important parts of the above code  The game ends at `max_turns`, which should be `100`. We specify the opponent's policy, `opponent_policy`, the algorithm's hyperparameters are `alpha` the learning rate, `epsilon` is the parameter used for the $\epsilon-greedy$ policy. `gamma` or $\gamma$ is the discount factor. 


In the above, I have set the above parameter to their default values. Let's look at some simulations done with different epsilon values.
First, let's make look at the main Q-Learning loop, and explain how it works:

```python
q_table = defaultdict(lambda:0)
```

This is a default dict, which maps a `0` zero whenever have not seen a state before, and the state is saved as a `tuple`, `(agent_score, opponent_score, agent_buffer)`, where the `agent_buffer` is the agent's current turn score.

<div style="page-break-after: always;"></div>

### Now let's look the opponent's policy, our benchmark for agent performance:

```python
def stochastic_policy(observation):
    return np.random.randint(0,2)
```

and this is a heuristic policy that only considers the agent's current turn score, and takes a decision after the turn score exceeds `k` , in this examaple `k = 23` :

```python
def agent_policy(observation):
    if observation[2] > 23:
        return PigEnv.BANK
    else:
        return PigEnv.ROLL
```

`PigEnv.Bank` and `PigEnv.ROLL` are just aliases for `0` and `1` .

### For our Q-learning agent, this is the policy: 

```python
def q_policy(observation):
    return np.argmax(q_table[observation])
```

We take the greedy action, among the actions available in the state we are in, which in this case are `PigEnv.Bank` and `PigEnv.ROLL`. 

### Let's instantiate the environment and run the main loop:

```python
env = PigEnv(
			 max_turns=300,
			 opponent_policy=stochastic_policy,
			 epsilon = 0.1,
			 learning_rate=0.03,
			 )

for i in tqdm(range(10_000)):    
    state,_ = env.reset() #env reset returns observation, info
    terminated = False
    truncated = False
```


### This is inside the for loop:
```python
    while not terminated and not truncated:
        #epsilon greedy
        action = epsilon_greedy(env,policy = q_policy,observation = observation,random_policy = stochastic_policy)

        next_observation, reward, terminated, truncated, info = env.step(action)
        old_value = q_table[state, action]

        #Take the maximum over all possible actions in the next state.
        next_max = np.max([q_table[next_observation, PigEnv.ROLL],q_table[next_observation,PigEnv.BANK]])

        new_value = (1 - env.alpha) * old_value + env.alpha * (reward + env.gamma * next_max)

        q_table[state, action] = new_value
        observation = next_observation
```

Let us go through this step by step:

First, in the for loop for our chosen number of episodes, we need to (re)set the environment to make sure all the states and variables have the correct starting values for an episode. we achieve this using `env.reset()`, implemented as follows:

```python
def reset(self):
        #self.turn = PigEnv.AGENT
        self.turn = np.random.randint(0,2)
        self.actions_taken = {1:[],0:[]} #a dictionary that can be accessed
        self.points = {PigEnv.AGENT:0,PigEnv.OPPONENT:0}
        self.buffers = [0,0]
        self.remaining_turns = self.max_turns  

        self.observation = (self.points[PigEnv.AGENT],self.points[PigEnv.OPPONENT],self.buffers[PigEnv.AGENT])
        
        self.reward = 0
        self.terminated = False
        self.truncated = False
        self.info = None

        return self.observation, self.info
```

Where we initialize all relevant variables.

<div style = "page-break-after: always;"></div>

## Inside an Epsiode:
In the `while not terminated and not truncated` loop, we run an episode, where we first take an action using epsilon greedy and the provided policy, and we record our observations:

```python
 action = epsilon_greedy(env,policy = q_policy,observation = observation,random_policy = stochastic_policy)
 
 next_observation, reward, terminated, truncated, info = env.step(action)
```

We then save what value the `q_table` has right now, before the $TD(0)$ update, and then using this and the Q-learning update rule to update the value of the state-action pair we are currently at: 

```python
 old_value = q_table[state, action]
 #Take the maximum over all possible actions in the next state.
 next_max = np.max([q_table[next_observation, PigEnv.ROLL],q_table[next_observation,PigEnv.BANK]]) 
 
 new_value = (1 - env.alpha) * old_value + env.alpha * (reward + env.gamma * next_max)
 q_table[state, action] = new_value
 observation = next_observation
```

We end the environment using `env.close()`. 