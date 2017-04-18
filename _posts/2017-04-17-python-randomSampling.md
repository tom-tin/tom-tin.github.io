---
layout: post
title:  "Python - Random Sampling"
date:   2017-04-17 18:34:10 +0700
categories: [python, example, random, sampling]
---

# Objective: Introducing a few methods to do random sampling in Python

## 1. The basics



~~~python
random.random(), random.randrange(), random.shuffle, random.choice(), random.sample()

import random
#to produce deterministic results, set the seed
#e.g., random.seed(10)

# a random number between 0 and 1
print(random.random())

# 4 random numbers between 0 and 1
print([random.random() for _ in range(4)])

# a random integer in [0,3)
print(random.randrange(3))

# a random integer in (3,6)
print(random.randrange(3, 6))

# randomly shuffle an array:
up_to_five = list(range(5))
random.shuffle(up_to_five)
print(up_to_five)

# randomly choose one element from a list
my_fav_city = random.choice(["Evanston", "Chicago", "Thousand Oaks"])
print(my_fav_city)
~~~


## 2. Choose k random numbers from a list (with or without replacement)

~~~python
source = list(range(10))
# randomly choose 7 numbers from a list (with replacement)
choose7_withReplacement = [random.choice(source) 
                           for _ in range(7)]
print(choose7_withReplacement)
~~~

~~~python
# randomly choose 7 numbers from a list (without replacement)
choose7_withOutReplacement = random.sample(source, 7)
print(choose7_withOutReplacement)
~~~


## 3. Online sampling: Choose k random numbers from a stream of numbers with size n, where n can grow as we process; n can be very large so that the list won't fit into memory, or n can be unknown.

## Idea: [Reservoir Sampling.](https://en.wikipedia.org/wiki/Reservoir_sampling/)

Below, we implement the most common method: Algorithm R

S[1..n] is the stream to process, R[1..k] will contain the returned k random samples.


~~~python
#Assume we have a Stream object with the following methods:
class Stream(object):
    def __init__(self, n):# n is the current length of the stream
        self.n = n

    def hasNext(self):#return 1 if the stream continues
        #assume the stream end at 100 (unknown to user)
        return 1 if self.n <= 100 else 0
    
    def getNext(self):#return a random next number
        #assume the streamn consists of numbers 0,1,...,9
        return random.randrange(10) if self.hasNext() else None
    
    def update(self):#increase the stream length by 1
        self.n += 1
        
    def leng(self): #return length of current stream
        return self.n 
~~~


~~~python
#Assume we have a Stream object with the following methods:
class Stream(object):
    def __init__(self, n):# n is the current length of the stream
        self.n = n

    def hasNext(self):#return 1 if the stream continues
        #assume the stream end at 100 (unknown to user)
        return 1 if self.n <= 100 else 0
    
    def getNext(self):#return a random next number
        #assume the streamn consists of numbers 0,1,...,9
        return random.randrange(10) if self.hasNext() else None
    
    def update(self):#increase the stream length by 1
        self.n += 1
        
    def leng(self): #return length of current stream
        return self.n 
~~~

#### Now, let's run the experiment:

~~~python
def ReservoirSample(S, k):
    R = [None] * k
    i = S.leng() # length of stream so far
    #basically, i=0 to start with
    
    while S.hasNext(): #while the Stream continues to generate number
        if i < k: #the first k elements 0...k-1 get assigned first
            R[i] = S.getNext()
        else: #i>=k, replace previous assigned element
            j = random.randrange(0,i) #random from 0 to i-1 inclusive
            if j <= k-1:
                R[j] = S.getNext()
        
        S.update() # length of the stream is increased by 1
        i = S.leng()
    
    return R

            
def experiment(): #main function
    k = 50 #number of samples we want to pick
    S = Stream(0) #initialize the length of stream to 0
    samples = ReservoirSample(S, k)
    print(samples)
            
if __name__ == "__main__":
    experiment()
~~~


## Analysis: Why does the above Algorithm R work? In other words, prove that the algorithm returns each value in the stream with probability k/i, when i is the current length of the stream:

* First of all, the latest ith element is selected with probability k/i (done).
* Now: P[the jth element from 1 to i-1 (inclusive) is replaced] = (k/i) (1/k) = 1/i. You can also see this directly from j = random.randrange(0,i), which returns a number between 0 and i-1 thus each number is chosen with probability 1/i.
* Thus, P[the jth element between 1 and i is NOT replaced] = 1-1/i = (i-1)/i
* Now, using induction: Assuming when the stream is at length i-1, each element is selected with probability k/(i-1) (verify that this is true for i=1,2). Now:
    * P[the jth element survives after the latest round] = P[it survives in previous round] * P[it is not replaced in this round] = (k/(i-1)) ((i-1)/i) = k/i (done!)

----------------
_Reference:_ [Reservoir Sampling.](https://en.wikipedia.org/wiki/Reservoir_sampling/)
