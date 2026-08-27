# Markov Chain Sampling: Adults on the Heliport

In Monte Carlo, it is not just children who play pebble games; Adults also play their version on the local helipad.

However, the square-shaped helipad with a centre circle is larger than the circle bounded by a square. 
No individual can throw a pebble randomly into such a big field.
Hence, the algorithm will be modified: rather than throwing a single pebble to a completely random location, the adults continuously displace the pebble from its previous position (*forming a chain*).  
Furthermore, if the pebble leaves the helipad, an outfielder retrieves and returns it to the previous pebble position (stacking the count of $n_\text{hits} = 1+1$ as the rejected proposal leaves the chain at its previous state), allowing the adults to continue the game.

Translating that scenario to Python, we can simulate the Markov Chain Monte Carlo method without observing the chain of strenuous games.

## Mathematical Basis

Our heliport game samples points uniformly from the square helipad. 
To ensure that the desired distribution is the stationary distribution of the chain, the transition probabilities must satisfy the `Detailed Balance Condition`, where the probability flow between every pair of
states is equal:

$$
P(i)T(i \rightarrow j) = P(j)T(j \rightarrow i)
$$

where 
- $P(i)$, $P(j)$: the probability of being in state $i$ or $j$.
- $T(i \rightarrow j)$, $T(j \rightarrow i)$: the transition probability from one state to another, where $T= \text{proposal probability}(q) \cdot \text{acceptance probability}(A)$.

Summing this equality over all possible states $j$ gives the Global Balance Condition for state $i$ required in Monte Carlo algorithms:

$$
P(i)\sum_j T(i \rightarrow j) = \sum_j P(j)T(j \rightarrow i)
$$

Thus, satisfying the Detailed Balance Condition is sufficient to ensure that the desired distribution is stationary under the Markov chain.

### Proposal Probability

For a discrete four-directional random walk, a new position is proposed by randomly displacing the current position, with each direction having proposal probabilities (or proposal density, $q$):

$$
q(i \rightarrow j) = q(j \rightarrow i) = \frac{1}{4}.
$$

In the implementation of the Markov Chain, a likewise symmetrical continuous random walk proposal is used, where the displacements are instead sampled uniformly:

$$
\Delta x,\Delta y \sim U(-\delta,\delta)
$$

The proposal's symmetry simplifies the general Metropolis-Hastings expression, giving the Metropolis acceptance probability:

$$
A(i \rightarrow j) = \min\left(1,\frac{P(j)q(j \rightarrow i)}{P(i)q(i \rightarrow j)}\right)
$$
$$
A(i \rightarrow j) = \min\left(1,\frac{P(j)}{P(i)}\right)
$$

### Metropolis Acceptance

The target distribution is uniform within the square:

$$
P(x,y)=
\begin{cases}
C, & |x|<1,\ |y|<1\\
0, & \text{otherwise}.
\end{cases}
$$

Therefore, if a proposed position remains inside the square, the proposal will be accepted:

$$
\frac{P(j)}{P(i)}=1
$$

If the proposed position lies outside the square, the acceptance probability is zero ($P(j)=0$).
Hence, the acceptance rule becomes

$$
A(i \rightarrow j)=
\begin{cases}
1, & |x'|<1,\ |y'|<1\\
0, & \text{otherwise}.
\end{cases}
$$

As the proposal distribution is symmetric and the Metropolis acceptance probability satisfies the Detailed Balance Condition, the uniform distribution over the square helipad is a stationary distribution of the Markov chain with a suitable accept/reject rule for the MCMC Python simulation.
