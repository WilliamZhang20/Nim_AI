# Nim AI

This repository uses a **reinforcement learning** technique called Q-learning to play a game called [Nim](https://en.wikipedia.org/wiki/Nim).

TLDR: Nim is a two-player game that involves a number of piles of items. Each player has to remove a number of items, which can be any nonzero number of items that all have to be from the same pile. Whoever removes the last item loses. 

The idea for this repository came from a Harvard CS50 Introduction to AI with Python course [project](https://cs50.harvard.edu/ai/2024/projects/4/nim/), where the structure of the implementation all comes from. 

## How it all works

Q-learning is a reinforcement learning algorithm that assigns values to actions taken in various states, operating within the framework of [Markov Decision Processes](https://en.wikipedia.org/wiki/Markov_decision_process). 

It assigns rewards or penalties to actions from state based on the result (i.e. winning or losing the game) and stores the result in a Python dictionary. 

The penalty or reward value is called the Quality value, or Q value, which depends on a state and an action from that state and is written as $$Q(s, a)$$. There, $$s$$ represents a state, and $$a$$ represents an action from state $$s$$.

This allows the "world" of the game to improve the game performance of the agent.

Initially, the Nim AI agent's Q value dictionary has all $$Q(s, a)$$ values set to zero. Then, the AI agent plays 10,000 games against itself. 

Along the way, it updates Q values according to an estimated future reward, without any immediate reward, as we don't know who has won or lost. 

At the end of each training round, it updates Q values by assigning a reward of 1 to the winner, -1 reward to the loser, for the AI agent to update Q values for the winning and losing states. 

After 10,000 rounds of updating Q-values, the algorithm will have been able to explore many different states and optimize $$Q(s, a)$$ for many states so that it can play as optimally as possible. 

Q-value updates are done by computing:

$$
Q(s, a) \longleftarrow Q(s, a) + \alpha((R + \gamma \hspace{5pt} \begin{equation} \underset{a'}{max} \end{equation} (Q(s', a') - Q(s, a)))
$$

In the above equation, the new Q value for a state-action pair is computed from the current value, the reward received $$R$$, the learning rate $$\alpha$$, and the discount factor.

The discount factor, $$\gamma\$$, is [associated](https://stats.stackexchange.com/questions/221402/understanding-the-role-of-the-discount-factor-in-reinforcement-learning) with the _time bias_ of the reward result. The smaller the $$\gamma\$$, the more myopic the algorithm. 

For a game like Nim, where the "real reward" comes at the end of the game, in the form of winning or losing, we want to be as far-sighted as possible, so it is 1. This will make future rewards just as important as present rewards. If it were to be greater than 1, the Q value function may diverge and become unbounded. 

## How to play it

Download or copy the files `nim.py` and `play.py`, and run `play.py`. No additional PyPl libraries are needed.

When you run `play.py`. There will be printouts confirming the agent playing games against itself. Then, a randomly generated set of 4 piles will appear.

A random selection will determine the first player, which may be either the user or the AI agent. Moves will then alternate between the user and the AI agent.

At each of the user's moves, the user selects a pile number and the number of items taken from it. 

When there are no more items left, a winner is declared.

## The final result

I haven't won a single game against the AI agent :(
