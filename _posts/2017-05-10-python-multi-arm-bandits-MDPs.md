---
layout: post
title:  "Solving a simple Multi-arm Bandits problem using Markov Decision Processes"
date:   2017-05-10 18:34:10 +0700
categories: [python, Multi-arm Bandits (MABs), Markov Decision Processes (MDPs)]
---

# Problem statement: 
Assume that there are 3 independent arms, each arm i when being played will give a reward of either 0 or 1, according to a Bernoulli(p_i).
Real-world situation: 3 online ads banners. Each ads i, once displayed, will be clicked with some probability p_i

# Objective: which ads to display so that we have maximum click-through rate.


Now initially let the prior of each p_i be Beta(1,1), which is uniform.
If right now each p_i is Beta(a,b) (conjugate prior for binomial),
then in the if arm i is played in the next round, p_i is still Beta(a',b'),
where a' = a + # of successes,
and   b' = b + # of failures


We can do the same thing in case of Gaussian distributions too.

~~~python
import matplotlib.pyplot as plt
import numpy as np
from scipy.stats import beta


num_trials = 1000

#assume there are 3 arms
ARM_TRUEVALS = [0.2, 0.5, 0.75]#true val of each arm.
#which is the P[winning] if we play that arm.
#Q: how many arms should we simulate?


#First, define each arm as an object, so that we can update
#each arm systematically
class Arm(object):
    def __init__(self, p):
        '''
        initialize the arm
        p is prob[winning] for that arm, i.e., its true value
        '''
        self.p = p #initialize the arm true values
        self.a = 1 #initial val of Beta distribution
        self.b = 1 #initial val of Beta distribution
        #for both a and b are 1, Beta distr. is just a uniform distr.
        #so initially we have no knowledge about each arm.

    def play(self):
        '''
        play the arm, return 1 with probability p
        return 0 otherwise
        '''
        return np.random.random() < self.p

    def reward(self):
        '''
        return a random reward from playing this arm
        which is a random sample from a Beta distr.
        '''
        return np.random.beta(self.a, self.b)

    def update(self, x):
        '''
        to udpate the arm's parameters a and b (Beta)
        these update formulae we derived from the conjugate priors
        where x is either 0 or 1.
        '''
        self.a += x
        self.b += 1 - x
        

# Define a plotting function to plot the arm's pdf
def plot(arms, trial):
    '''
    Input: 
        - arms is a list of Arms objects that we want to plot pdfs
        - trial = number of trials up to the plotting time
    Output:
        - To plot each arm pdf on the same chart to compare
    '''
    
    x = np.linspace(0, 1, 200)#200 points on the x-axis
    
    for b in arms:
        #plot of the pdf of beta
        y = beta.pdf(x, b.a, b.b)
        plt.plot(x, y, label="real p: %.4f" % b.p)
        
    plt.title("Arm distributions after %s trials" % trial)
    plt.legend()
    plt.show()


#Now we define the main function experiment
def experiment():
    '''
    main function to run this experiment
    '''
    #First, initialize a bunch of arms
    arms = [Arm(p) for p in ARM_TRUEVALS]
    

    #Below is a list of number of trials during the experiment when
    #we want to take a look at how close we are to convergence
    sample_points = [5,10,100,500,num_trials-1]
    
    
    #Now, during experiment we will play the best current arm 
    #according to TS sampling algorithm.
    for i in range(num_trials):

        #Initialize the best arm up to now
        bestArm = None 
        
        #initialize best reward
        maxReward = -1
        allRewards = [] # let's collect these just to print for debugging
        
        
        #Now, we pick an arm according to the best current reward
        for j in arms:
            reward = j.reward()#sample reward from the playing arm j
            allRewards.append("%.4f" % reward)
            if reward > maxReward:
                maxReward = reward #keep track of max reward
                bestArm = j
        
        
        
        if i in sample_points:#then plot
            print("current sample rewards: %s" % allRewards)
            plot(arms, i) #i is the trial number

        # now, we have found the best arm for this triall i, then
        # we just play it
        x = bestArm.play()#gives a 0 or 1, which indicates a success/failure
        #this is used to update the best arm as follows:

        # update the distribution for the best arm we just played
        bestArm.update(x)


if __name__ == "__main__":
    experiment()
~~~

_Reference:_ Adapted from the following:

1) Class OPNS525: 
[Statistical Learning in Sequential Decision Making](http://djrusso.github.io/teaching.html/) at Northwestern by Prof. Daniel Russo.

2) Online class: 
[Bayesian Machine Learning in Python: A/B Testing.](https://www.udemy.com/bayesian-machine-learning-in-python-ab-testing/)
