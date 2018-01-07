# Eligibility Traces
## Summary Notes

## Chapter 12 - Rich Sutton 

**What are Eligibility Traces, Why do we need them?**
- Eligibility traces offer a mechanism in the form of a short-term memory vector `zt E Rd` which parallels the long-term weight vector `wt E Rd`.
The key idea is that zt has a bump in its element corresponding to the component in wt participating in the estimation of a state-value function. This bump them fades away. 
While this trace bump exists, if a non-zero TD error occurs, learning then occurs in that component of wt.
- They offer many advantages over n-step methods:
  * memory efficient: a single trace vector is required as opposed to n feature vectors
  * learning occurs continually and uniformly
  * learning is immediate and not delayed
- The n-step methods provided *forward views* where as Eligibility traces provide a means to look backward to recently visited states using a trace.
These overcome the limitation of forward looking algorithm in that the future rewards and values are not immediately available in present.
