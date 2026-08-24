# Markov Chain Sampling: Adults on the Heliport

In Monte Carlo, it is not just children who play pebble games; Adults also play their version on the local helipad.

However, the square-shaped helipad with a centre circle is larger than the circle bounded by a square. 
No individual can throw a pebble randomly into such a big field.
Hence, the algorithm will be modified: rather than a single pebble throw in a random direction, the adults continuously throw a pebble from their previous pebble position (*forming a chain*).  
Furthermore, if the pebble leaves the helipad, an outfielder will retrieve it and return it to the previous pebble position ($n = 1+1$), allowing the adults to continue the game.

Translating that scenario to Python, we can simulate the Markov Chain Monte Carlo method without observing the chain of strenuous games.
