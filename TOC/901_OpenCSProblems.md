# Open CS Problems:

Open Problem lists -[ https://en.wikipedia.org/wiki/List_of_unsolved_problems_in_computer_science](https://en.wikipedia.org/wiki/List_of_unsolved_problems_in_computer_science)


### Research topics I am interested in Computation:

I would like to work on improving either the performance of computation models or time and space complexity of various algorithms.



* Various computational models and the advantages and disadvantages of them(TM, DFA, NFA, PDA, PTM, Quantum computation).
* Various complexity classes and the relationships between them. For example time complexity classes(P, NP, co-NP) and space complexity classes(L, NL, co-NL, PSPACE, NPSPACE, EXPSPACE). Even polynomial time problems become tougher when input size is very big(matrix multiplication).
* Number theory(countable finite sets, countably infinite sets(integers), uncountable sets(real number). (Fun fact: thinking this way number stars seems countably infinite)


### Important P-class problems



* Matrix multiplication as of now n^2.37188.
* RSA-2048 Encryption Algorithm and SHA 256 hashing function.


### NP-complete Problems



1. Unordered Layered Binary Tree Layout: Given a binary tree T and a real number W determine if there is an unordered layered tree drawing Γ for T which has width ≤ W. In the below reference you can see that this problem is NP-complete.

[https://www.emis.de/journals/JGAA/accepted/2004/MarriottStuckey2004.8.3.pdf](https://www.emis.de/journals/JGAA/accepted/2004/MarriottStuckey2004.8.3.pdf)

[https://llimllib.github.io/pymag-trees/#foot1](https://llimllib.github.io/pymag-trees/#foot1)



2. Polynomial time algorithm for Hamilton circuit (it is NP-complete problem).(Discrete maths chapter 10.5)
3. Minimising Boolean functions with many variables is NP-Complete problem.(Discrete maths chapter 12.4)
4. finding the chromatic number of a graph
5. MAX_CLIQUE in the graph. A max size subgraph G1 of the graph G. Where G1 is a complete graph that means each node is connected with all other nodes in the graph.
6. MIN_VERTEX_COVER of the graph. Minimum size subset of the set vertices of the undirected graph where for each edge (u,v) in the graph either node u or node v is in the vertex cover set.
7. MAX_CUT of a graph.


### Others 



1. Graph isomorphism is NP problem(not NP complete)
2. Prime factorisation(finding the prime factors of the number)(NP-intermediate - no polynomial time algorithms are found)(This is not in NP-complete problems because there is no reduction proof which reduces this problem to some other NP-complete problem).
3. Computer Program which can construct mathematics proof(It has not been invented).
4. Discrete logarithm is considered to be an intractable problem.
5. using current axioms of Mathematics we can’t prove that there is some set which is larger than the set of natural numbers but smaller than the set of real numbers


### Random topics:

**P, NP, NP-hard, NP-complete:**

**[https://stackoverflow.com/questions/1857244/what-are-the-differences-between-np-np-complete-and-np-hard](https://stackoverflow.com/questions/1857244/what-are-the-differences-between-np-np-complete-and-np-hard)**



* The problem is P-class if it has a deterministic polynomial time algorithm. 
* So there are some problems which can verify a solution in polynomial time but not find a solution in polynomial time. This is NP-class. This name comes from the fact that it can be decided using a non deterministic polynomial time Turing machine. But when we convert to deterministic TM it becomes exponential in time.
* NP complete is a problem X in NP such that any other problem Y in NP can be polynomial time reduced to X. So if we solve X we can solve all the problems Y. But it doesn’t mean if we solve Y we can solve X. So if two problems A and B both are in NP- complete then that means A is reducible from any Y(including B). 
* NP-hard: Intuitively, these are the problems that are at least as hard as the NP-complete problems. Note that NP-hard problems do not have to be in NP, and this is the difference between NP-complete and NP-hard. NP-hard problems are polynomial time reducible from all the NP problems. But for some problems we can’t even verify a solution in polynomial time so they won’t come under NP-class.
* So if there is a solution to NP-hard or NP-complete problems then we will have a solution to all the NP problems.
* But note that all the NP complete problems can be polynomial time reducible to each other but NP hard cannot be polynomial time reducible to any of the NP-complete problems.


#### Fermat’s Last Theorem:



* Fermat's Last Theorem(sometimes called Fermat's conjecture, especially in older texts) states that no three positive integers a, b, and c satisfy the equation a<sup>n</sup> + b<sup>n</sup> = c<sup>n</sup> for any integer value of n greater than 2. The cases n = 1 and n = 2 have been known since antiquity to have infinitely many solutions
