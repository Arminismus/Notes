The model of the environment's dynamics is completely known to us. At any state $S$, the probability of transitioning to a state $S'$ which is intended by the action, given action $a$: $$\forall_{A,S}: \hspace{0.1in} P(S'|S,A) = 1$$
and, the probability of getting to any other state given state and action $(S,A)$ is $0$.

Now, we remind ourselves of the Bellman Equation: 

$$V^{\pi}(s) = R(S,A) + \gamma \sum_{s'}P(S'|S,A)V^{\pi}(S')$$
Where $$A = \pi(s)$$
This gives us a way to use the values of one state into another, and find the values of all states. This is called value iteration, where we iteratively find the values of all states given the values of other states, using the Bellman Equation derived using the dynamics of the system.

