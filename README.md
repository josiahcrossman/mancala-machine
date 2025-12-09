# Mancala Machine

This project is a notebook containing a Gymnasium environment, as well as multiple functions to train RL agents to play the game [Mancala](https://www.scholastic.com/content/dam/teachers/blogs/alycia-zimmerman/migrated-files/mancala_rules.pdf). 

### Note for grader:
I already covered this in the video, but in the course of doing some experimentation, I accidentally overwrote the models used for evaluation here. I'm retraining new versions as this is submitted and they should be added to the repo by the night of 12/10, but their performance will likely not match what I originally did the analysis on. 

UPDATE 12/9/25 4:18pm  -- added all but DeepQ long model

Also, do note that the mancala game used in the project overview video was not my own, but someone else's website. The website is cited in the attribution file. 

## What it does

There is a custom Gymnasium environment to play the game Mancala. The reason that I needed to make a custom enviornment was because I couldn't find one already existing online somewhere. There are two major agent types: a policy agent using the REINFORCE algorithm and a Deep-Q agent, both of which use a self-play architecture to learn how to play the game Mancala. Their performance is benchmarked both against a agent moving randomly, as well as against each other. 

## Quick Start

Install the requirements.txt and hit run all on the mancala machine notebook to train a new model. Everything should work from there. I didn't run this locally, instead running this in the Duke OnDemand cluster. For the sake of speed, I would recommend that you do so as well (instructions in setup.md). If you wish to just view the performance of the trained models, then simply just run all cells in evaluation.ipynb.

## Video Links

Project overview: https://duke.box.com/s/htp30t8i0snn3mex3tjj33ra1zkiktvs

Technical overview: https://duke.box.com/s/t7zpew73awghdkgm9hsr4ckuf6qzdz0d

## Evaluation and Design Choices:

![Confusion matrix of the performance of different models](/images/comparison.png "Competitive analysis of models")

(Sorry the bottom is messed up, the way to read the graph is that the squares are the winrate of the agent on the y-axis against the agent on the x-axis, and the agents on the x-axis are in the same order as the y-axis)

After training, I had the different models play each other 1000 times each in order to gauge their performance. There are a few key takeaways from this evaluation. Firstly, the DeepQ agent that was trained for a long amount of time actually doesn't show that much of a boost in performance over those trained for a short amount of time when they play against each other, and is similarly effective to DeepQ agent medium in performance against the policy agents. Speaking of the policy agents, it seems that the long training period causes reinforce_agent long to be more effective against a wide variety of agents, only consistently losing to the DeepQ medium agent. 

For the sake of brevity, I won't be copying the gameplay output here, it can be found at the bottom of notebooks/evaluation.ipynb. Looking at the gameplay, it seems that both agents attempt to wait for the other agent to run out of pieces while stockpiling them on their side, optimizing for having the stones added to its store when the game ends. 

When the agents play each other, they both attempt this strategy, and in the epsiodes I looked at, the agent that moved first was the one that won the game. 

For training, increasing the number of episodes made a performance difference, with both the Deep-Q and REINFORCE agent showing a performance increase with an increased number of episodes

From notebooks/evaluation.ipynb: 

* Agent deepq_agent_short had a winrate against a random agent of 0.614

* Agent reinforce_agent_short had a winrate against a random agent of 0.553

* Agent deepq_agent_medium had a winrate against a random agent of 0.692

* Agent reinforce_agent_medium had a winrate against a random agent of 0.528

* Agent deepq_agent_long had a winrate against a random agent of 0.741

* Agent reinforce_agent_long had a winrate against a random agent of 0.776

In addition to evaluating metrics here, I also wanted to include a written explaination of some of the design choices that were made in case it was missed in the video. 

To start with the environment, there were some key decisions made. Firstly, I chose to create my own gymnasium enviornment for Mancala because I was unable to find one available online. From there, when setting rewards, I tried a variety of different setups, from only rewarding wins/losses as 1/-1, to a variety of different weights for adding pieces to the store for p1, and penalties for the opponent doing so, to not penalizing p1 for the opponents actions whatsoever (except for losses). The final environment that I landed on was the one that I found to be perfomrant for both model architectures. 

Speaking of model architectures, I tried a variety of different neural network architectures in an effort to improve Deep-Q performance with little success. Neither adding layers nor decreasing the number of nodes had much of an effect. I experimented with a variety of hyperparameters for both models in an effort to make them both more performant, with little success. For Deep-Q, I tried different values for epsilon_min, agent_pool_size, buffer_size, among other options, and the values that I am currently using were the ones I found to be most effective. For REINFORCE, I tried different learning rates, decay rates, and reward methods, landing on the values currently being used. 

## Individual Contributions
This project was done solo (not counting tutorials/LLM assistance)
