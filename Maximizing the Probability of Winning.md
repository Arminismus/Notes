In the game of page, since we do not have full control over the environment, we cannot simply guarantee that we will win a round using a strategy, simple because we can get extremely unlucky and keep rolling $1$ whereas our opponent might have a normal game. This means all we can hope for is for us to maximize our probability of winning.


Winning means reaching $100$ points, before our opponent does. This depends on $3$ variables: 

1. Our total score, denoted as $i$.
2. The oppoenent's total score, denoted as $j$.
3. Our turn scrore, denoted as $k$.

Let's call the probability of winning to be $$ P_{i,j,k}$$Now, if $i > 100$ or $k > 100$, then $P_{i,j,k} = 1$, and if $j > 100$ then $P_{i,j,k} = 0$. We must focus our attention to a case where $i,j,k < 100$.


We can use dynamic programming to help us solve this problem. To do so, we use the [[Principle of Optimality|principle of optimality]], and we divide our problem into two cases: 

1. $P_{i,j,k,hold}$
2. $P_{i,j,k,roll}$

meaning this is like an action value function now, returning the probability of winning, given our state and the action we have taken. 

Whichever of $(1)$ or $(2)$ is most probable, that would be the logical choice for us to choose, being the action that has a higher probability of winning. 

so: $$P_{i,j,k} = \max_a(P_{i,j,k,hold},P_{i,j,k,roll})$$
We have now reduced the problem to finding $P_{i,j,k,roll}$ and $P_{i,j,k,hold}$. Now these can, be calculated recursively: 

$$P_{i,j,k,hold} = 1 - P_{i+k,j,0}$$
The probability that we win when we hold and add our turn-total to our score, is the probability that the opponent does not win immediately when it's their turn. $$P_{i,j,k,hold} = \frac{1}{6}[(1 - P_{i,j,0}) + P_{i,j,k+2} +  P_{i,j,k+3} +  P_{i,j,k+4} + P_{i,j,k+5} + P_{i,j,k+6}]$$
The probability of winning when rolling a $1$ is the probability that the opponent doesn't win immediately following the next turn (Why?). The other possibilities are the probability that we win given that now we have $x$ more points, where $x$ is the number we have rolled, and $x \neq 1$.


These formulas are recursive, and to get to $100$, we need to know the probability of each of the outcomes before it. This is where value iteration comes in handy, as there are also cyclic dependencies between the probabilities, so we cannot simply start from the end and come to the begining of the game, because states can be repeated.






 
