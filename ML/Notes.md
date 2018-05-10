## Bonferonni Inequalities deal with the following kind of problems ##

Hypothesis: Jelly beans cause acne
Run experiments from data samples and may be found in one instance out of 20,000 that green jelly bean caused acne with a confidence of p < 0.05.
What really happened here? Well if you have roll a dice and you are trying to find how common is 6, if you roll is many many many times, you will see 6 often lot of times, but that does not mean 6 is more common than any other number. It is as common as any other number. This is called Multiple Testing.
In a nutshell, we had one interesting instance and we invoked it too many times. 

In the VC literature, this is called *Union Bound*. IF we have 10 different outcomes, and I want to bound that any of them will occur, and that is upper bounded by the sum over the probability of each of them individually occuring. That bound holds regardless of whether these outcomes are dependent or independent. 
