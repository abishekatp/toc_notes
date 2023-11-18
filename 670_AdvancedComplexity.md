## Complexity Theory(Advanced Topics)

### Approximation Algorithms


* Largest clique in the graph, smallest vertex cover in the graph are all NP-hard problems. So no optimal polynomial time algorithm exists for them until P = NP. But we don’t always need optimal solutions. Sometimes approximate solutions will be very useful for practical use cases. These algorithms are called approximation algorithms.
* For some MIN problem(finding minimum of some kind) the solution is k-optimal if the approximate solution is not more than k times the actual optimal solution. An example of the MIN problem can be “the removal of the minimum number of actors from the movie such that the budget of the movies goes down 10 million.”
* For some MAX problem(finding maximum of some kind) the solution is k-optimal if the approximate solution is not less than the actual value divided by k.


#### MIN_VERTEX_COVER



* This is the problem of selecting the minimum number of vertices(or nodes) from the graph such that all the edges in the graph touches at least one of the nodes in the vertex cover. This problem is in NP class.
* The approximation algorithm below decides the smallest vertex cover problem in polynomial time. It guarantees that the vertex cover it produces will never be larger than twice the size of the actual smallest vertex cover of the graph.

M =“On input &lt;G>:



1. Repeat the following until there are no more edges to mark:
2.     L1: find the non marked edge that is not touched by any marked edge and mark that edge. Also nodes of that edge to the vertex cover. If there is no edge to mark then exit the loop.
3. Output the vertex cover”

Explanation:



* Stage-1: In each step we will mark one edge so at some point this will stop. 
* Stage-2: each time we will search through the edges to find a non-marked edge. If it doesn’t directly touch any of the already marked edges then mark this new edge. Here two edges are called to be touching if they are connected to the same vertex. If there are no more edges to mark then exit the loop.
* Stage-3: Output vertices that are the end point of marked edges.

How?



* Let’s assume that the set of marked edges are H and vertices that are end points of those edges as X. Since each edge can have at most two end points the size of X is not more than twice the size of H.
* Second assume that Y is the actual vertex cover. This means all the edges of H touch one of these vertices. Here two edges of the set H can’t touch the same vertex in Y. This is because when we mark the edges we mark them only when they don’t touch the already marked edge in H. Because of this no two edges in the set H will touch the same vertex. This implies that the size of set Y must be at least the size of H then only all the edges in H can touch any one of the vertices in Y.
* The above two points imply that the size of the set X cannot be larger than twice the size of the actual vertex cover Y.


#### MAX_CUT:



* This is an example of a maximisation problem. The cut of the graph is the separation of vertices V of the graph G into two disjoint sets S and T.
* The cut edge of the graph is an edge that connects one vertex from S to another vertex from T. The un-cut edge is an edge that is not a cut edge.
* The MAX_CUT problem asks for one of the possible disjoint sets S and T such that the number of cut edges for this S and T is larger than any other pair of disjoint sets S and T.

M=“on input &lt;V, E> V and E are vertices and edges of graph G:



1. Let’s max_cut=0, S={ } and T=V.
2. If either moving one vertex from T to S or from S to T increases the max_cut count then move that vertex and repeat this stage again.
3. If there is no such vertex to move then output the max_cut and halt.”

How?:



* This algorithm actually doesn’t need step by step explanation. It has rather simple logic behind it. If moving any one vertex from S to T or from T to S increases the max_cut then do that until this process is possible.
* First we separated all the vertices in V into two sets S and T by following the above algorithm. Now the cut edge is the edge that goes from the vertex in S to the vertex in T. Non cut edge is the edge that goes between two vertices in the same set either S or T. 
* We claim that the number of cut edges in this setup is equal to the number of uncut edges. We count the number of cut edges and uncut edges for each vertex. Each vertex should have the same number of cut and uncut edges.
* For example assume that node x is in set S. Then the edge between x and any node y in the same set S is an uncut edge. The edge between x and any note z from the set T is a cut edge. These two counts must be equal otherwise we would have moved the node x from the set S to the set T in stage 2 of the algorithm.
* So this proves that the number of cut edges is equal to the number of cut edges in the graph G. Note that when we counted edges by vertex we might have counted all the edges(both cut and uncut) twice. So both the actual counts will be half the count we have computed.
* So our calculation is (max_cut >= total number of edges / 2). So if some other algorithm finds a more optimal solution it can’t be larger than the total number of edges in the graph. Hence it can’t be more than twice the size of our cut_vertex set.


### Probabilistic computation


#### Probability TM(PTM)



* Probabilistic Turing machine is a kind of non deterministic Turing machine where there are more than one possible transitions for a single computation step. Instead of choosing one of the possible transitions non deterministically PTM chooses that probabilistically. But PTM is more practical than a non deterministic Turing machine.
* One possible way of definition is that there will be two sets of transition functions D1 and D2. So in each computation step instead of choosing one of possible transitions non deterministically PTM will choose one of the transitions set  probabilistically. So this machine is very different from deterministic machines. Because the same input can take different amounts of time or can give different outputs on different branches. It can even never halt on some branches. 
* Another useful definition can be the machine runs on random inputs and accepts w probabilistically. Here we may either get random input from the tape or some specific states of the Turing machine will decide one of the two possible transitions by coin toss with equal probability. At the end we need some way of making random choices instead of computing for all the possible inputs. It can either come from input or part of a transition function.
* **Max two possible transitions**: In our examples we only consider the Turing machines with one or two choices(maximum of two possible transitions at each computation step). Here the one-choice computation step is a deterministic step made by the Turing machine. Two-choice computation step is a probabilistic choice with two transitions each with probability ½. In analogy these two branches are equivalent to making decisions based on coin flip with equal probability.
* **Core idea**: The PTM is more practical than NTM because in some computation steps instead of using non deterministic steps we are going to use a coin flip to choose one of the possible branches which will reduce the running time of the machine. When the number of such probabilistic choices in that branch increases then the probability of the branch being correct decreases exponentially. In other words, the probability of error of that branch increases.
* **Probability of branch b:** Here the probability that particular branch b accepts decreases exponentially by each probabilistic choice we make. For example for 1 or 2-choice Turing machines Pr[branch b accepts] = 2^(-k). Where k is the number of probabilistic choices made in that branch b.
* **Accepting probability [M accepts w]**: The probability that the Turing machine M accepts a string w is the sum of the probability of all the accepting branches of the PTM.
* **Rejecting probability [M rejects w]**: the probability that the Turing machine M rejects a string is the sum of probability of all the rejecting branches of the PTM.
* Note that the accepting and rejecting probabilities will add up to 1.  So the Pr[M rejects w] = 1 - Pr[M accepts w].
* **PTM M decides language L: **For some e>=0, We say that some probabilistic Turing machine M decides the language L with the error probability e, when the Pr[The M gives wrong answer about the membership of the string w in the language L] &lt;= e.
* **Decidable**: In our case we are going to consider only decidable problems. So all the branches in the PTM M will halt by either accepting or rejecting the input with some probability. 
* **Time and Space complexity** of Probabilistic turing machines is analysed in the same way as the non deterministic turing machine. If time complexity is O(t(n)) means all the branches of PTM must use at most t(n) time. In the same way we define space complexity.
* Note that Quantum computers are another model of computation that is inherently probabilistic.


### The class BPP

BPP = { A | where some probabilistic polynomial time Turing machine(PTM) M decides the language A with the error probability e &lt;= ⅓}



* Here we say that the PTM should decide the language L with the error probability at most ⅓. This e can be any value less than ½. There is no specific reason we picked ⅓. Error ⅓ means PTM will give the right answer about the membership of the language L two out of three times.
* Note that the error probability should be less than ½. Because otherwise the machine does the same thing as making a coin flip for all the computation steps. The PTM wouldn’t have a high probability of correctness. Below lemma makes this statement even stronger.


#### Amplification Lemma



* Assume that some polynomial time PTM M1 decides some language L with the error probability e1. Then we can construct another polynomial time PTM M2 with the error probability e2 for any (0 &lt; e2 &lt; ½) using M1. The construction procedure is given below.

**Proof Idea:**

Assume that we have PTM M1 with the error probability e1 less than ½.

M2 = “On input w



1. Simulate the M1 for k times on input w for some constant k.
2. Accept if majority of the total k times accepts the input w otherwise reject.”

**Explanation:**



* Stage-1: stage 1 just simulates the M1 on the input w for k times. This is possible because all the probabilistic branches of M1 either accept or reject.
* Stage-2: this stage is based on the overall probability of the machine M1. If the majority of the times M1 accepts that means most probably the machine M1 accepts w.

In the text book you can find more rigorous proof with mathematical analysis. The above proof is enough to understand why this amplification lemma works. The error probability of M2 decreases exponentially with respect to the value of constant k.

**Mathematical proof:**

M2 = “On input x



1. Compute the value of k.
2. Simulate the M1 for 2k times on input x for some constant k.
3. Accept if majority of the total 2k times accepts the input x otherwise reject.”

Explanation:



* First the error probability of M1 e is less than 1/2. In stage 2 the machine M2 simulates M1 for 2k times. If more than k times M1 gives the correct answer(either accept or reject) then M2 gives the correct answer. We assume that M1 gives the wrong answer for more than k time and make the probability of this happening exponentially small.
* If M1 answers c times correctly and w times wrongly among 2k times then c+w = 2k. We assume the value of w >= c. Assume that e1 is the probability the M1 is wrong on input x. If M2 answers wrongly when the majority of the sequence of 2k tests answers wrongly. We call this sequence S. P(S) = (e1)^w (1-e1)^c  is at most (e^w) (1-e)^w. Here e is the probability of the machine M1 independent of input x  and e1 &lt;= e &lt; 1/2
*  Here (e1)(1-e1) &lt;= (e)(1-e) because of two reasons one w>=c. If e1 &lt; e then (1-e1) > (1-e) so this also will affect the above equivalence. But since w >= c the e1 &lt; e will dominate the second part. This equivalence says that the probability of M2 getting the wrong sequence S on input x is less than the probability of M2 getting the wrong sequence in general.
* Since w >= c and w + c = 2k. This will imply that (c &lt;= k &lt;= w). So because of the same reason as above the e^k and e^w will dominate the product with (1-e)^c term. So since w>=k this will imply that (e^w) (1-e)^c &lt;= (e^k) (1-e)^k. This implies that the probability of getting the wrong answer for more than half of the times will have the value of at most the probability of getting equal number of correct and wrong anwers. So we take this maximum possible error probability for the further error calculation. 
* We may get at most 2^2k possible wrong sequences in the machine M2. Here remember that wrong sequence means sequence of simulation of the machine M1. So the probability of getting wrong sequence is** Pr[ M2 outputs wrong answer] = (2^2k) * (e^k)(1-e)^k. = (4e(1-e))^k.**
* To get the written answer we need to make sure this probability is as small as possible. For that we have to make sure of two things. One is e &lt; ½ since this is part of the definition of the BPP itself so we don’t have to worry about it. The second is we have to choose the value of k such that it minimises the value of error probability. To get the error probability 2^-t we have to find the value of k by solving the equation** 2^-t = (4e(1-e))^k.**
* If you do a little bit of algebra by taking base 2 to the other side, we will get k = - t / (log2(4e(1-e))).


#### NP and BPP



* BPP means Bounded-error Probabilistic Polynomial time Turing machine decides a set of languages with error probability at most ⅓.
* Here PTM runs in polynomial time means all of the branches of PTM should halt within some polynomial number of steps. Remember that we are only considering deciders so all the branches will halt at some point. 
* Both NP and BPP are similar. We defined NP using the NTM and BPP using PTM. NTM makes non deterministic choices on each computation step whenever needed. But the PTM chooses one of these non deterministic choices probabilistically. This is the main difference between the two machines.
* **Output NTM**: NTM accepts w when at least one of the non deterministic branches accept its input w. NTM rejects w when all of the non deterministic branches reject.
* **Output PTM**: PTM accepts when the sum of probability of accepting computation branches is greater than the sum of probability of rejecting branches. The error probability e defines the probability of the machine giving the wrong answer about the membership of the language. So don’t confuse the error e with accepting or rejecting the input.
* If you think about it you can understand that the BPP is closed under union and complementation. Because if PTM decides some language then we can flip the accepting and rejecting probabilities to decide the complement language. 
* P is a subset of BPP; it is straightforward. Also BPP is a subset of PSPACE. We can simulate each path probabilistic tree one by one using some PSPACE machine and add up probability values to get the final answer.

**Why can we negate the output of BPP but not for NP?**



* Here we say that PTM decides the language L. So all the probabilistic branches will halt by either accepting or rejecting the input with some error probability. Since this class contains PTM that are decider we can negate the output of the PTM to get the complement language. We defined the NP class also in a similar way, that is a set of languages that are decidable by NTM in polynomial time. But we were not able to negate the output of NTM to get the answer for the Co-NP class. 
* This is because of how we defined the accepting computation in NTM. In NTM we will accept if any one of the non deterministic branches accepts its input. If NTM M accepts a particular string w in one branch and rejects in all other branches. Then when we negate the NTM M it will reject in one branch and accept in all the other branches. So both M and Negation of M will accept the same input w. It is wrong. Because of this restriction we said we can't negate the output of NTM to decide some complement language.
* But this is not the case for PTM. PTM accepts w when Pr[M accepts w] > 2/3. Suppose if some PTM M accepts w means it has the Pr[M accepts w] > 2/3 and Pr[M reject w] &lt;= 1/3. When we negate its output we will have Pr[M rejects w] > 2/3 and Pr[M accepts w] &lt;= 1/3. So M will accept w and negation of M will reject w. It works as expected. That's why we can decide the complement language by negating the output of the PTM.


#### PRIMALITY

The number is called prime when it has no factor other than 1 and itself. If the number is not prime then it is called composite. Now we have a polynomial time algorithm for primality testing but it is too complicated. Instead we will see the probabilistic polynomial time algorithm which is much simpler. Before starting the actual algorithm we will see about Fermat's little theorem without any proof which we will use in our algorithm.

Here ≡ is a congruent symbol and !≡ is not congruent symbol.

**Fermat Little Theorem**: If p is prime and a ∈ Zp+ then a^(p-1) ≡ 1 (mod p). Here Zp+ is a set of  positive prime numbers (Zp+)={1, 2, 3,...,p-1}. 



* This theorem says that if p is a prime number then any number **a** that belongs to the set (Zp+) will have the remainder 1 when we find the value a^(p-1) mod p. We call this a^(p-1) congruent 1 modulo p. This is called the Fermat’s test.
* We say that a number p is a pseudoprime if it passes Fermat’s test for all the elements of the set (Zp+). But in our algorithm we can’t test for all the elements of the set. Because that will take exponential time due to the fact that numbers are exponential in length when we represent them as binary. Because of the above reason we go with a probabilistic algorithm. 
* Remember that If the number is not a pseudoprime then it fails at least half of all the Fermat’s tests. So when we choose k random numbers a1,a2,...,a(k) and do the Fermat’s test. If p is not a pseudoprime then it passes at most half of all the fermat’s test. The probability it passes all the k fermat tests is 1/(2^-k). So the probability of giving wrong answers about composite numbers decreases exponentially with k. Also remember that modular exponentiation(a^(p-1) mod p) is computable in polynomial time.
* **Carmichael Numbers**: There are some infrequent occurrences of numbers called Carmichael numbers. These numbers are composite yet they pass all the fermat’s tests. To rule out the Carmichael number we do some extra thing if a number passes Fermat's test for a number a(i) in the set (Zp+).
* The number 1 has exactly two square roots for any prime number p. Those are 1 and -1. So (1)^2 mod p = 1 and (-1)^2 mod p = 1. But for many composite numbers including all the Carmichael numbers 1 has four or more square roots. For example if you take number 21, then (1^2) mod 21= 1, (-1)^2 mod 21 = 1, (8^2) mod 21 = 1 and (-8)^2 mod 21 = 1.
* **Carmichael number test**: So whenever p passes all the fermat tests we will check whether it is a Carmichael number. When the number a passes Fermat's test then a^(p-1) mod p = 1. 
* Then we can find the square of the 1 by finding the square root of the number a^(p-1) which is a^((p-1)/2). So we check a^((p-1)/2) mod p value is the number other than 1 or -1. If that’s the case then that particular number is the witness that p is not prime. This is because a^(p-1) has remainder 1 when we divide it by p. So when we find the remainder (a^((p-1)/2) / p) it is the square root of the number 1. If we get the value 1 or -1 as the square root remainder then we will divide the value p-1 again by 2^(i) to check for the remainder of the number a^((p-1)/2^(i)). We will do this until division gives non integers or we find the square root of the number that is other than 1 or -1.

**Algorithm:**

PRIME = “On input p:



1. If p is ever and p=2 then accept, otherwise reject.
2. Select k random numbers a1, a2,..., a(k).
3. For each i from 1 to k:
4.    L1: check if a(i)^(p-1) congruent 1 mod p is true. If not then reject.
5.    L1: compute the value of l such that (p - 1) = s 2^l where s is an odd integer.
6.    L1: compute the sequence a(i)^(s 2^0), a(i)^(s 2^1),…, a(i)^(s 2^l) module p.
7.    L1: if some element of the sequence is not 1, find the last element that is not 1 and reject it if that is not -1.
8. If p passes all k tests then accept.”

**Explanations:**



* We say that a(i) is a compositeness witness when PRIME rejects either at stage 4 or 5 for particular number a(i).
* Stage-1: If p is an even number then we are sure that this stage will reject it. Number 2 is an exception because it doesn’t have any factor.
* Stage-2 & 3: select k random numbers that are in the set Zp+ and do the Fermat’s test with each one of them.
* Stage 4: if the congruent modulo p value is not 1 then we know that p is not prime so reject it. If the a(i)^(p-1) congruent 1 (mod p) then do the Carmichael test to reduce the error probability of Fermat’s test.
* Stage 5 & 6: First this stage seems difficult to understand but it’s simple. Here a(i)^(s 2^l) means we have divided the (p-1) by 2 one time, we can divide that number by two for another l times until we reach the odd number s. Since s is an odd integer we can’t divide (s 2^l) further so we stop the sequence there.
* Stage 7: based on the above discussion the prime numbers will have only two possible square roots of 1. But here we have found a square root other than 1 or -1 for the number 1 when we consider modulo p. So this number must be the composite number so we reject it. We will see in the below explanation why this stage reduces the error probability.
* Stage 8: if the number p passed all of the above tests then it must be most probably a prime number so we accept it.

**Pr[PRIME accepts p] = 1 when p is an odd prime number**:



* If p is the prime number then it passes all the tests and this algorithm accepts p. So Pr[PRIME accepts p] = 1 when p is prime.
* Suppose the number p is rejected at stage 4 then Fertmat’s little theorem ensures that p is not prime.
* If the number p is rejected at stage 7 then there exists some b such that b is the square root of the 1 with the square root other than 1 or -1. Here we are saying the square root of the 1 in the sense that b=a(i)^(s 2^k) for which we found the modulo p value to be neither 1 nor -1 in the stage 7 and b^2 ≡ 1 (mod p).
* This means (b^2) -1 ≡ 0 (mod p). This implies that (b-1)(b+1) = cp for some integer c. This is because when we divide b^(2) - 1 by p we will get the remainder as 0. 
* Remember that multiples of prime number p cannot be expressed as the product of two numbers less than p. For example 21 cannot be expressed as the product of two numbers less than 7.
* Here b congruent to neither 1 nor -1 for mod p, the value of (b-1) and (b+1) must be strictly between 0 and p. This is because neither (b+1) nor (b-1) can be divisible by p. So when we take (b+1) mod p or (b-1) mod p we will get numbers strictly between 0 and p. 
* Now these two numbers are the product of (cp). Which means p has some factor that will imply that p is a composite number.
* These two facts ensure that if some number p is rejected by either stage 4 or 5 then that p must be a composite number. 

**Pr[PRIME accepts p] &lt;= 2^-k when p is an odd composite number**:



* Note that in this explanation I am using space as a notation of multiplication.
* **Chinese Remainder Theorem**: two numbers q and r  are relatively prime when they have no common divisors other than 1. In that case this theorem tells that there exists one to one **correspondence** between the set Z(qr) and Z(q) x Z(r). For every t in Z(qr) there exists (a,b) pair in Z(q) x Z(r) such that a belongs to Z(q) and b belongs to Z(r) and they have the following property. (t ≡ a (mod q)) and (t ≡ b (mod r)).
* In stage 6 we will get some sequence for each non witness we find. That sequence will either be all 1 or will contain -1 at some positions. We will select one of those sequences such that -1 appears in the largest j position. Remember that we count from 0 to l. We call that particular a(i) for which we get such a sequence as h. So h^(s 2^j) ≡ -1 (mod p) and h^(s 2^j+1) ≡ 1 (mod p).
* How do we get -1 as remainder? For example  (9 mod 2 =1). But for the divisor either (9 mod 5 =4) or (9 mod 5 = -1) is true. In a way that 2 times 5 = 10 and 10-1=9.
* We are choosing the j such that we get remainder -1 because it will help us find some value t such that t^(s 2^j) !≡ -1 or 1 (mod p). We find largest such position because then only t^(s 2^j+1) ≡ 1 (mod p)
* If p is composite then either it must be the product of two coprime numbers q and r or the power of some prime number q

**First case:** 



* In the first case we will use the Chinese remainder theorem to find the value t in the set (Zp+) such that t^(s 2^j) !≡ 1 or -1 (mod p). This is a composite witness. 
* Chinese remainder theorem says that we can find t in the set Zp+ such that it will have remainder h when we divide by q and remainder 1 when we divide by r. This is possible because (h, 1) is in the set Z(q) x Z(r) and there is one to one correspondence between Z(qr) and Z(q) x Z(r). 
* So we can find t ≡ h (mod q) and t ≡ 1 (mod r) because of the one to one correspondence. So t^(s 2^j) ≡ -1 (mod q) and t^(s 2^j) ≡ 1 (mod r). When we raise the power the first equation becomes -1 because t has remainder h when we divide by q.
* Here we need one remainder to be -1 and another to be 1, that’s the reason we chose the sequence which contains -1 in it for the analysis(remember that this sequence is produced for some h=a(i) where a(i) non witness in the stage 4). Since p=qr we get the witness that** t^(s 2^j) !≡ 1 or -1 (mod p). **
* Here t^(s 2^j+1) ≡ 1 (mod p). For this reason only we choose the largest j that has the value -1 in the sequence for the analysis.** **Then all the numbers after the -1 in the sequence must be 1. Also remember that if the sequence of a particular number has remainder -1 in the position j means, then the number at the j+1 position will have remainder 1. Because we square the number at j’th position to get the number at the (j+1)’th position. For example (9 mod 5 = -1) and (9^2 mod 5 = 1). Another example (8 mod 3 = -1) and (8^2 mod 3 = 1).
* Now we got our first witness. Using this composite witness we can find a unique witness (d t) mod p for each non witness d. Because (d t)^(s 2^j) !≡ 1 or -1  (mod p) and (d t)^(s 2^j+1) ≡ 1 (mod p) because of the way we chose the position j.

**Distinctness:**



* If d1 and d2 are two distinct non witnesses then (d1 t) mod p != (d2 t) mod p. So the witnesses also will have distinct remainders. 
* First let me put some facts in words. d1 and d1 are in the set (Zp+) because they are non-witnesses. (d1 t) !≡ 1 or -1 (mod p) and (d2 t) !≡ 1 or -1 (mod p). Because of the way we chose j the value of t^(s 2^j+1) mod p =1.  Then we can multiply and divide by t on both sides to get (k mod p =1).
* Where k = (t t^((s 2^(j+1)) - 1). Then we get d1 = (k d1) mod p and d2 = ( k d2) mod p. This is true because k ≡ 1 (mod p) and d1 ≡ d1 (mod p). Based on the modular arithmetic rules we can multiply these two in their corresponding positions to get (k d1) ≡ d1 (mod p). So when we can do the following operation (k d1) mod p = d1. Similarly for d2.
* So if (d1 t) mod p = (d2 t) mod p which means (d1 t) ≡ (d2 t) (mod p). Then we can multiply on both sides by (k/t) to get the result that d1 = d2. Multiplying by the same number on both sides won’t change the equivalence of the remainder. The Remaining value itself may change but on both sides we will get the equal remainders.
* So if d1 and d2 are distinct non-witnesses then the witnesses we will get using them are also going to be distinct. So there are as many witnesses as non non-witnesses.

**Second case:** 



* Similarly in the second case if p=q^e, where q is prime and e>1. Then using a particular approach we will find the value of t such that t^p and t !≡ 1 or -1. This number t is a composite witness for the second case. Then using this t we can find a witness (d t) mod p for each non witness d. 
* Here t =(1 + q^(e-1)). We use the binomial theorem to get the series t^p = 1 + p q^(e-1) + multiples of p with higher powers of q^(e-1). So we get that (t^p ≡ 1 mod p). This is true because other than first term 1, all other terms are divisible by p. 
* So this implies that t is the stage 4 witness. This is true because if t were not stage 4 witness then (t^p-1) ≡ 1 (mod p). If you multiply by t on both sides you will get ( t^p ≡ t (mod p)). Since 0 &lt; t &lt; p this implies that (t^p) !≡ 1 (mod p). This contradicts what we proved using the binomial theorem. So t must be a stage 4 witness.
* So using this witness t we can find a distinct witness for each non-witness d.
* **Distinctness**: Here also we can prove the distinctness of the witnesses similar to above. If witnesses are the same then non witnesses are also going to be the same value with respect to the value of k = (t t^(p-1)).

**Summary:**



* There are as many composite witnesses as composite non-witnesses in the set (Zp+). Here non witnesses means( that does not reject in stage 4 and in stage 7) the number a(i) that decreases the probability of number p being a composite even though p is composite number.
* Because of these reasons the probability of finding a non witness for p being composite is at least ½. In other words, the error probability of deciding the composite number as the prime number is less than ½. 
* The probability of finding a composite witness for the p in stage 5, 6 & 7 will increase exponentially for each a(i) we test. So the error probability must be exponentially small with respect to the value of k.


#### Class RP vs BPP:



* PRIMES is in BPP class. Just now we described a probabilistic polynomial time algorithm for PRIMES. This algorithm when it rejects the input we are sure that the number is composite. When it accepts a number it can be either prime or composite. So the error will happen only for composite numbers. But we will reduce this error probability to an exponentially small value.
* **RP**: The above discussed error is called one sided error. We have separate classes for these kinds of errors namely RP. The class of languages that are decidable by PTM when input is in the language then it is accepted with probability ½. When input is not in the language then it is rejected with probability 1. So the COMPOSITE language is in the RP class.


#### Branching Programs(BP)

A Branching Program(BP) is a directed acyclic( no cycles in the graph) graph where the following statements are true.



1. The nodes that are called query nodes are labelled as x(i). Each query node has two outgoing edges either 0 or 1.
2. There are two output nodes labelled 0 and 1 with no outgoing edges.
3. There will be a designated start node.

The graph BP with query nodes x(1), x(2),…, x(m) represents a Boolean function f with m boolean variables and output either 0 or 1. So the output nodes represent these two possible outputs.



* Here whenever particular input to the boolean function is given we can use the BP graph to figure out the output. 
* To do that, start from the start node and check the value of the boolean variable for the query node x(1). Each query node has two outgoing edges. So if x(1)= 1, then follow an edge with label 1. Otherwise follow an edge with label 0. This way at some point we will reach either one of the output nodes 1 or 0. 
* This is not the same as DFA. BP can only accept the input of a particular length. If the number of variables in the BP is m then we can only accept the input of length m. But DFA can accept the input of any length.
* Two branching programs are equivalent if they compute the same boolean function.
* Any Boolean function can be represented as branching programs but conversion may not be possible in polynomial time.

EQ_BP = { &lt;B1, B2> | B1 and B2 are equivalent branches program graphs}

**EQ_BP is Co-NP**:



* How do we prove B1 and B2 are equivalent? For that we have to check whether all the possible inputs to B1 and B2 compute the same output. This will take O(2^n) time for the input length n. There isn’t  any polynomial time verifier that can say whether B1 and B2 are equivalent. We have to check all possible inputs before confirming it. So BP is a Co-NP problem.
* The complement of the EQ_BP problem is a NP problem. This is true because we can give a particular input assignment for which B1 and B2 produce different outputs. This particular assignment is called a certificate. This certification can be used to verify that B1 and B2 are not equal in polynomial time. For Co-NP problems we can give certificates that can be used to check non-membership of the language is polynomial time. For example COMP_SAT we can give a satisfying assignment to show that some string is not in the COMP_SAT language.

**EQ_BP is Co-NP-complete:**



* This proof is not complete. I haven't given a complete reduction from any Co-NP complete problem to EQ_BP. I will add this later.
* First assume that we can reduce any Co-NP language L to a branching program B1 in polynomial time. So B1 accepts its input when w is in the language L. Also assume that using polynomial time we can modify B1 to accept w only when w is equal to particular input w1.
* This modified B1 will accept w only when w is in the language L and w=w1. So if either one of these conditions fails then B1 will accept no input string.
* Then we will construct another BP B2 which is hardcoded to accept only a particular input w1. For each input bit x(i) we will add one query node in B2 such that it will go to the next query node only when x(i) is equal to the corresponding bit y(i) of w1. Otherwise it will straight away go to the node 0.
* B2 always accepts w1 and B1 will accept w only when w is in the language and w=w1. Because of the above statement if B1=B2 then string w1 is in the language. 
* This is the core idea behind the reduction of any Co-NP problem to an EQ_BP problem.

**Note(just trying not sure about correctness)**:



* We generally assumed that there exists polynomial time reduction from any Co-NP problem to an EQ_BP problem. But specifically one way of trying to find a proof is, we can try to find a polynomial time reduction from COMP_SAT(complement of the SAT problem) problem to an EQ_BP problem. Since COMP_SAT is Co-NP complete then EQ_BP also will become a Co-NP complete problem.
* We may construct B2 such that it will go to the output node 0 for all of its inputs. B1 will go to the output node 1 only for the input that satisfies the boolean function B.
* This way B1 and B2 will be equivalent if and only if B is unsatisfiable. if B is satisfiable then B1 will go to the output node 1 for the input that satisfies the boolean function B. Then B1 and B2 will become not equivalent.

**COMP_EQ_BP is NP-complete:**



* Similar to the above problem we will create two BP programs B1 and B2. We will construct B2 such that it will go to the output node 0 for all its inputs. The B1 will go to the output node 0 for all its input except the one that satisfies the boolean expression B. When boolean function B is not satisfiable then B1 will go to the output node 0 for all its inputs. Otherwise B2 will go to the output 1 for the satisfying assignment to B.
* This way B1 and B2 will be not equal only when boolean expressions are satisfiable. 

We don’t know whether EQ_BP is in class BPP. If EQ_BP is in BPP that will imply that all the Co-NP problems are in BPP. Since BPP is deterministic it will also imply that all the NP problems to be in BPP. But we don’t have any proof for this. So we consider a more restricting problem called read once branching program.


#### Read Once Branching Programs(ROBP)


* Read once branching programs are branching programs that never queries the same variable more than once in any path from the start node to one of the output nodes. 
* For example if some BP reads the value of the variable x(1) at some point of computation then it will never read that same variable x(1) again or we can say that the node x(1) will never come in the current path of that BP.

**Side notes**:



* Any Boolean function can be converted to the ROBP but the conversion may not be possible in polynomial time.
* We can convert any BP to ROBP but it also will take exponential time. If you give some thoughts about it, wherever the node x1 is repeated in the same path, then to remove that repeated node x1 we have to keep two copies(just an intuition) of all the nodes below that x1. This is for remembering that one copy belongs to the path that corresponds to x1=0 and another copy is to remember the path that corresponds to x1=1. Like this we can remember the already read node values to create a graph for ROBP. But as you can see this will increase the size of the graph exponentially for each node we are removing from the graph of BP.

EQ_ROBP = {&lt;B1, B2> | B1 and B2 are equivalent read once branching programs}


#### **EQ_ROBP is in class BPP**

**Bad approach:**



* So this EQ_ROBP asks whether two Read Once Branching Programs are equal. One way to answer this question is to try all possible inputs. That will take O(2^n) time for the graph with n nodes. Anyway we are trying to solve this problem probabilistically then lets try that approach.
* First let’s remember that we can create Boolean formulas which will be satisfiable for a single input among 2^n possible inputs. These branching programs are similar to boolean formulas. We can create two branching programs B1 and B2. B1 will go to the output node 1 for all the input. B2 will go to the output node 1 for all the inputs except for the input where all the boolean variables are assigned to 1.
* Then when we randomly choose the input to compare the branching programs B1 and B2. These two branching programs will be equal for almost all of the inputs except that one case. So choosing that one input randomly from 2^n possible inputs has very low probability. So the probability of rejecting this &lt;B1,B2> is very low even though they are not equal. Because of this reason we can’t use the approach of randomly choosing the input.
* Instead we will be seeing a different approach to solve this problem. Before going to that we have to do some labelling for each node and branches of the branching program. These labels will be used in the proof of our new approach. Since we are going to use it just for the proof, even though this labelling process may take exponential time we don’t have to worry about it.

**Labelling of the nodes and branches as 1 or 0:**



* Consider any arbitrary node x in the graph. It will have one or more input branches and exactly two output branches. Input branches correspond to various paths which lead to the node x. Two output branches correspond to two possible ways the current path can proceed from the node x. One output branch b1 corresponds to x=1 and b2 corresponds to x=0.
* What should our labelling represent? It should represent the path from the start node to the output node 1. All the nodes and branches in this path should have the label 1, other nodes and branches should have the label 0.
* We will label the node x as 1 if any one of its input branches has the label 1. If x=1 and x has the label 1 then we will label the branch b2 as 1. If x=0 and x has the label 1 then we will label b1 as 1. So all nodes and branches will have labels either 1 or 0 based on whether that particular node or branch is in the path for a particular input. Also remember that node’s value and node’s label are two different things, don't confuse them. The label represents whether that node is in the output path to either the output node 1 or not. The value represents the input value for the variable node x.
* At the end we will see whether output node 1 is labelled as 1. If yes then that particular input to the branching program will lead to the output node 1. If the output node has label 0 then the input won’t lead to the output node 1. So to see the output we have to see in the single place namely the output node 1.

**Generalisation of the labelling using boolean formula:**



* So instead of labelling for particular input now we are going to create labels that will work for any input. We will do that by representing the labels as Boolean formulas. 
* **Output path:** First we consider the path to the output node 1 as the output path. All the nodes and branches of the output path should be labelled as 1 and all other nodes and branches are labelled as 0. The boolean operations we are going to use are AND(∧), OR(∨) and NOT(¬).
* **Node label:** if you think about this logically, if any one of the input branches of the node x is labelled as 1 then the output path will contain that particular node x. So we have to label that node as 1. To represent this using Boolean formula we have to use the boolean operation OR. The label of the node x will be OR of labels of each of its input branches. For example if input branches of the node x are a,b,c then the label of x = (a ∨ b ∨ c)
* **Branch 0 label(b1)**: Each node x has two outgoing branches. One of them corresponds to the value x=0. This means that branch b1 will be labelled as 1(will be part of the output path) only when the value of x=0 and the node x is in the output path. To represent this as a boolean formula we can negate the value of x and compute the AND operation with the label of the x. Suppose if label of the x = a and the value of x=x1, then the label of the branch b1=a ∧ (¬ x1)
* **Branch 1 label(b2):** This means that branch b2 will be labelled as 1(will be part of the output path) only when the value of x=1 and the node x is in the output path. To represent this as a boolean formula we can compute the AND of the label of the node x and the value of x. Suppose if the label of x = a and value of x=x1, then the label of b2 = a ∧ x1.
* Like this we label all the nodes and branches of the BP. We always assume that the label of the input branch of the start node will be 1.
* Boolean formula F: At the end the label that corresponds to the output node 1 will represent a boolean formula that is equivalent to the output of the branching program. This labelling process may take exponential time. But don’t worry about it. This labelling is done only for the purpose of proving the correctness of the algorithm. In the actual algorithm we don’t need these labels. We will directly apply the values to the branching program.

**Arithmetization of boolean formula:**



* We have constructed a boolean formula F that represents the output of the branching program. But we can only apply boolean values to it. We have already seen that applying random boolean values doesn’t always work. So we are going to construct an arithmetical formula E that is equivalent to the boolean formula F. To do that we will replace all the boolean operations to their equivalent arithmetical operations.
* The following are the equivalence between arithmetic and boolean operations. (a ∧ b)=(ab), (a ∨ b)=(a+b-ab) and (¬a)=(1-a).
* For simplicity we can use this (a ∨ b)=(a+b) for the OR operation. This will work only for the branching programs. Because an arbitrary input to the BP, For any node x at most one of the input branches will have the label 1. So we can avoid the subtraction part.
* Also if we assume that each layer of the branching program has every variable node of the graph. After arithmetization we will get an equation similar to the following equation. This is just an example with random terms. So don’t try to derive some logic from it. 
* E = x1 (1-x2) x3 … x(m) + (1-x1) x2 (1-x3) … x(m) + … + x1 x2 (1-x3) … (1-x(m)).
* The main thing you have to understand from E is that each multiplication term in this equation contains each variable node of the BP exactly once. Each multiplication term corresponds to one of the ways that boolean formula F can be satisfied. So there will be at most a total of 2^m terms in it. So to construct this it will take exponential time. But don’t worry about it. As we have already discussed this is just for the proof. Actual algorithm doesn’t have to construct this equation.
* **Degree of the polynomial E is one**: The same variable appears more than once in the same multiplication term only when the same node appears more than once in the path to the output node 1. Since we are only considering the Read Once branching program no node will appear more than once in the output path. So the degree of each variable in this equation will be at most one. This is important because having power one is very helpful in our next part of the proof.

**The Algorithm:**

D=”On input &lt;B1, B2> B1, B2 are ROBP



1. Select element r=r1,r2…r(m) randomly from the Finite field Z.
2. Evaluate two branching programs for these randomly chosen values.
3. If they agree then accept, otherwise reject”.
* Stage-2: this stage can be achieved only in polynomial time with respect to the number of nodes in the graph. We can compute the label value of each node one by one and find the label value of the output node 1 for both B1 and B2. Here we are not constructing label formulas but rather calculating actual label values so it will only take polynomial time.
* So we are going to assign non boolean values to the boolean variables to figure out whether the branching programs B1 and B2 are equal or not. In actual case we will just directly apply the non boolean values to the Branching Program graph.
* **Accept**: So When B1 and B2 are equal for some non boolean values then B1 and B2 are equivalent. We will accept the &lt;B1, B2> with probability 1.
* **Reject**: When B1 and B2 are not equal for some non boolean values then we will reject the &lt;B1, B2> with probability greater than ⅓. 
* **Finite Field Z**: The finite field Z will contain 3m elements where m is the number of variable nodes in branching programs. We define the set Z by some prime number q. Then if some computation step results in a number that is not in the set Z, Then we will find that number mod q to get the equivalent number from the set Z. Z = {0,1,2,3,...,q-1}

**Core Idea:**



* We have seen that by applying non boolean values to the branching programs we can evaluate their equivalence. To prove that we have also constructed polynomial equations that are equivalent to branching programs. First we have labelled branching program nodes and branches with boolean equations. Those boolean equations will tell whether that particular branch or node will be on the output path. 
* We can use the boolean equation that corresponds to output node 1 to check whether a particular input leads to the output node 1 or not. Then using the arithmetization process we have constructed a polynomial equation E that is equivalent to the boolean equation F. These two equations E and F are equivalent for all the boolean inputs. We will have two polynomials E1 and E2 that are equivalent to F1 and F2 which are equivalent to B1 and B2.
* For non boolean inputs also these two equations E1 and E2 will agree on all of the inputs if the B1 and B2 are equivalent and will disagree for most of the cases when they are not equivalent. So by applying a single set of non boolean values to these two equations we can check whether two branching programs are equivalent or not.
* If branch branching programs B1 and B2 are equal then their corresponding polynomials E1 and E2 will agree for all the non boolean inputs in the finite field Z. if B1 and B2 are not equal then they will agree in a very small number of places. Those places are the roots of the polynomials E1 and E2.

**Roots of the polynomial and The End**:



* So we know that a polynomial of degree k can have at most k number of roots. Here roots means the set of values that we can apply to the equation that will evaluate the polynomial equation to zero. The polynomial itself shouldn’t be zero polynomial(means that polynomial will evaluate to zero in all points regardless of their input).
* **Degree of polynomial E is 1: So we have seen that each multiplication term in the polynomial equation E will contain each variable of the branching program at most once. So This means this whole polynomial can have at most degree 1. Because each multiplication term has at most degree 1 and when we add them together, the degree of the equation doesn’t change.**
* If B1 and B2 are equivalent then E1 and E2 agrees on all the places(even for non boolean inputs)
* If B1 and B2 are not equivalent then E1 != E2, so E1-E2 is not equal to zero. Based on Schwartz-Zippel theorem Pr[ E1(r)=E2(r) ] &lt;= (dm/q) &lt;= (m/3m) = ⅓. This is because the degree of the polynomial d=1, we have chosen a finite field Z with the q = 3m. Here r is the set of random values we choose from the finite field Z. 
* So when we choose the random value, the probability of choosing the root of the polynomials E1 and E2 is less than or equal to ⅓. So using the amplification lemma we can further reduce this error. 
* Hence it is proven that equivalence of branching programs can be checked using Probabilistic Polynomial Time Turing machines using non boolean inputs.


### Alternating Turing machine(ATM)



* This is a kind of nondeterministic Turing machine with some extra features.
* All the states except q(accept) and q(reject) of the machine are divided into two groups: universal states and existential states.
* Like non deterministic Turing machines, ATMs also can make non deterministic choices. But it differs in a way of accepting its input. The NTM accepts when any one of its non deterministic branches accepts whereas an ATM can decide whether all the non branches should accept or just one branch should accept programmatically for each state of the machine. This feature of an ATM will be helpful to analyse the complexity class for time and space. 
* We label each node of the non deterministic tree either with AND or OR based on the configuration of that computation step containing the universal state or existential state.
* Then the node with AND label will be marked as accept only when all of its non deterministic branches accept. The node with OR label will be marked as accept only when any one of its non deterministic branches accept. We say that an ATM accepts its input when the start node is marked as accepted.
* If you think about it now, any Co-NP problem can be solved using an ATM easily when we slightly modify the NP algorithm of its complement language to use it with an ATM. For example take the COMP_SAT problem.

COMP_SAT=“on input boolean formula &lt;B>:



1. Universal select all possible inputs.
2. Evaluate  B for a particular input.
3. If it evaluates to zero then accept, otherwise reject.”


#### Some important theorems that can be proved for ATM

ATIME(f(n)) - when a problem can be decided by an ATM by using at most O(f(n)) time in any of its non deterministic branches.

ASPACE(f(n)) - when a problem can be decided by an ATM by using at most O(f(n)) space in any of its non deterministic branches.



* For f(n)>=n, we have an ATIME(f(n)) ⊆ SPACE(f(n)) ⊆ ATIME(f(n)^2).
* For f(n)>=log(n), we have ASPACE(f(n))=TIME(2^O(f(n))).

These proofs are one common idea: simulation of one kind of Turing machine(ATM or TM) M by another kind of Turing machine(TM or ATM) S within some time or space bound.

**ATIME(f(n)) ⊆ SPACE(f(n))**: 



* We can simulate the O(f(n)) time ATM M by a O(f(n)) space TM S by doing depth first search(DFS) of a non deterministic computation tree of the ATM M. since ATM M uses only O(f(n)) time each branch will have at most O(f(n)) depth. 
* Total space needed = recursion stack(O(f(n) space) + single configuration(O(f(n) spce) + non deterministic choices made in each node of the DFS(O(f(n) space). Because we can always compute the some i’th configuration, if we have start configuration and i non deterministic choices we made during the computation. Storing a single non deterministic choice only requires constant space.

**SPACE(f(n)) ⊆ ATIME((f(n))^2)**: 



* We can simulate O(f(n)) space TM M by an O(f(n)^2) time ATM S by following a similar approach as Savitch’s theorem. An ATM S will Existentially branch into all possible configurations to find the mid configuration c(m) that can be reached from start configuration within t/2 steps and whether an accept configuration can be reached from c(m) within t/2 steps.
* Then we will make two recursive universal calls, one to find mid configuration for c(1) and c(m) and another one to find mid configuration for c(m) and c(accept). 
* O(f(n)) space TM will have at most 2^(O(f(n)) steps.The depth of each non deterministic branch of ATM will be log(2^(O(f(n)))) = O(f(n)) and at each node we will print one configuration of the TM M. The TM M’s configuration length can be O(f(n)). So total time of simulation = O(f(n)^2).

**ASPACE(f(n)) ⊆ TIME(2^O(f(n))):**



* The O(f(n)) space ATM M can be simulated by 2^(O(f(n))) time TM S by constructing a computational graph of ATM M on input w. Each node of the graph is a configuration of M at a particular step for input w. Each edge corresponds to one of the non-deterministic choices of the machine. 
* Since an ATM uses only O(f(n)) space, there will be at most 2^(O(f(n))) nodes in the graph. This can be constructed by TM S by only using 2^(O(f(n))) time. This is because with the space bound O(f(n)), finite number states, input and tape alphabets we can only have at most 2^(d f(n)) configurations for some asymptotic constant d.
* Initially an accept node will be marked as accepted. An Universal branching node will be marked as accepted when all of its direct children are marked as accepted. An Existential branching node will be marked as accepted when any one of its direct children is marked as accepted. We will do this repeatedly until no new nodes are marked as accepted. If the start node is marked as accepted at any stage then M will accept w.
* For each repetition at least one node will be marked. So this simulation can be done within 2^(O(f(n))) time.

**TIME(2^O(f(n))) ⊆ ASPACE(f(n)):**



* This is a bit tricky, But if you understand the logic behind an ATM then it will be a piece of cake. We have to simulate 2^(O(f(n))) time TM M by using O(f(n)) space ATM S.
* If we represent the computation history of TM M as a tableau(note here also state and tape symbols are represented as a single composite character) it will have dimensions 2^(O(f(n))) height and width. So we only have space to store a pointer to the constant number of cells of the tableau or to couldn’t the number of cells in a tableau. 
* **Verify content of the single cell**: ATM S to verify the content d of the single cell will existentially guess the three of its parent cells. Suppose a,b,c are contents of those three parent cells. Then S will universally verify those three values a,b and c. This procedure will be continued recursively for each of the symbols a,b,c. When recursion reaches start configuration S can verify directly because S knows M’s start configuration.
* How can an ATM know which symbol belongs to start configuration? For this an ATM can existentially guess each symbol it encounters either as start configuration symbols or non start configuration symbols.
* We will count the depth of the recursive calls. Recursion can be stopped when count is reached 2^(d f(n)) where d is an appropriate asymptotic constant. To count the current row of the tablea it will only need log(2^O(f(n))) = O(f(n)) space.
* Assume the M moves its tape head to the leftmost cell of the tape when it accepts. Then S can start from the bottom leftmost cell of the tableau and recursively check for their parent cells. To store the pointer of that single cell we will only need O(f(n)) space.


### Interactive Proofs(IP):



* Interactive proofs are a kind of new way of looking into certificates for membership of the string in a particular language L. We have already seen one such class of languages called NP. 
* **NP class** - The class NP is the class of language for which Deterministic Polynomial Time Turing machine exists such that it can verify the membership of the string in particular language L when it is provided with a valid certificate. For example, the SAT problem is NP. We can give a single satisfying assignment to a boolean formula as a certificate. Then the deterministic polynomial time verifier can evaluate the boolean formula on that satisfying assignment to check whether that boolean formula belongs to the SAT language.
* **Co-NP class** - This is a class of problems for which there exists no deterministic polynomial time verifier that can verify the membership of some language L in this class. In other words we are not able to provide a certificate such that a verifier can verify the membership in polynomial time. For example the unsatisfiability(COMP_SAT) problem, there is no straightforward certificate to verify the unsatisfiability of the boolean formula in polynomial time. We have to verify all exponential numbers of possibilities to verify the unsatisfiability.
* **IP** - Class of languages for which some kind of probabilistic polynomial time Turing machine can verify the membership of the language by interacting with the Prover for only a polynomial number of steps. Here the Prover is the one who is trying to prove to the Verifier that a particular string w is a member of a particular language A. Formal definition of the IP class is as follows.
* Note. We can think of BPP as a special case of IP where polynomial verifier V doesn’t need any prover P. It can decide the membership on its own within probabilistic polynomial time. Similarly can think of NP as a special case of IP where the verifier is not probabilistic but rather deterministic.


#### Formal Definition of IP:

We say that the language A is in IP. If some polynomial time computable function V(called the Verifier) exists such that for some function P(the honest prover) and for every function C_P(the crooked Prover) and for every string w the following two statements are true.



1. If w belongs to the A then Pr[ V &lt;-> P accepts w] >=⅔.
2. If w does not belong to the A then Pr[V &lt;-> Q accepts w] &lt;=⅓.

**Explanation**:



* Here Verifiers only have polynomial time. Prover can use any amount time. When w is in the language verifier V should accept the input with high probability by interacting with some honest prover P. When w is not in the language the verifier V should reject the input with high probability by interacting with any Prover C_P(even crooked prover). 
* Here defining two kinds of Provers P and C_P is intentional. If w is in the language A, then P should be an honest prover which tries to prove the membership of the language. But C_P can be any computation function. The prover C_P may try to be correct or wrong, V should reject the string w that is not in the language A with high probability regardless of the action of the C_P.

**Verifier:**



* We will provide three inputs to the verifier. The Verifier doesn't need to remember these information itself; we will provide them as input while simulating the interactive proof system.
* Input string w: this is the string for which the Prover is trying to convince the Verifier about the membership in some language A.
* Random string r: we don’t define the Verifier to have the capability to make probabilistic choices. Instead we provide some random string r as input. The Verifier can make probabilistic decisions based on r. Remember that this is just for convenience not a limitation.
* Partial message history: Both Verifier and Prover don't store the messages that have been interchanged between them so far. We will provide those message history as input to the Verifier in the following format m1#m2#…#m(i).
* Output: Verifier will output either the next message m(i+1) or accept or reject.

**Prover:**



* Input and output: We will provide the Prover with two inputs: input string and partial message history m1#m2#…#m(i). The Prover will provide the next message m(i+1) to the Verifier.
* **Protocol**: We can think of the Prover and the Verifier following some standard protocol to interchange messages. For example when i is an even number, then Verifier sends next message V(w,r, m1#m2#…#m(i)) = m(i+1). When i is an odd number, then the Prover sends next message P(w, m1#m2#…#m(i)) = m(i+1). 


### IP=PSPACE



* This theorem proves that the class IP is equivalent to the class PSPACE. We will prove this in two directions.
* First we will prove that IP is a subset of the class PSPACE (IP ⊆ PSPACE) by simulating the interactive proof system using a polynomial space Turing machine.
* Second we will prove that PSPACE is a subset of the class IP (PSPACE ⊆ IP) by showing the PSPACE complete problem(for example TQBF problem) belongs to the class IP.


### IP ⊆ PSPACE

**Core Idea:**



* We know that the Verifier has the polynomial time bound and the Prover has no time bound. Since the Verifier can only read messages and random strings of polynomial lengths, this gives us a way of simulating the interactive proof system(IP) using the PSPACE Turing machine. 

**Proof:**



* Let A be the language in IP. Let’s assume that the A’s Verifier exchanges exactly p=p(n) messages with the Prover for the input w of length n. Then we construct the PSPACE Turing machine that simulates V. We need to calculate the following probability value to decide the language A.

**Pr[V accepts w] = max_P (Pr[ V &lt;-> P accepts w])**



* The above equation says that the probability that V accepts w is the probability of some Prover P such that the probability of V accepting w by interacting with P is maximum. This value is at least ⅔ if w is in A and at most ⅓ if not.
* This is a general equation. In the next section we will see how we can define this equation for partial message history M(j).
* Let M(j) denote the message history with j messages m1#m2#...#m(j). Then we say that **(V&lt;->P)(w,r,M(j))=accept** when we can extend the M(j) by a series of messages from m(j+1) through m(p) such that m(p) is the accept message. when (0 &lt;= i &lt; p) is an even number, then Verifier sends next message V(w,r, m1#m2#…#m(i)) = m(i+1). When (j &lt;= i &lt; p) is an odd number the Prover sends next message P(w, m1#m2#…#m(i)) = m(i+1). 
* Here when the next message is from the Verifier, It should be consistent with the message history. That means when we choose the next message using some random string r that random string r should be consistent with the message history.
* Also note that for i&lt;j when i is an odd number it can contain any possible messages at the position i+1, because those messages were sent by the Prover which doesn’t depend on the random string r. So for these cases there is no specific connection between message host and random string r. For i>=j odd number we will consider all possible messages of length p.

**Core logic:**

**Pr[V&lt;->P accepts w starting at M(j)] = Pr_r[ (V &lt;-> P)(w,r,M(j)) = accept ]**



* When the value of  i is even, The Verifier will send the next message. This next message will be based on some random string r of length p.There can be multiple such random strings that are consistent with the message history M(j). 
* But the PSPACE machine doesn’t know which one the IP will use. So when simulating the IP it will consider all such consistent strings and take average over all of them. In the next section we will see a more clear definition of how we calculate this average value as a weighted average.

**Pr[V accepts w starting at M(j)] = max_P (Pr[V&lt;->P accepts w starting at M(j)])**



* When the value of i is odd, We have to choose the message for the Prover such that it maximises the probability of accepting string w. The above equation represents the same. We have to consider the message m(j+1) that gives the maximum probability of acceptance when we append it at the end of M(j). 
* Since the PSPACE machine doesn’t know which message the Prover will send, It will consider all possible messages of length p. This is because the prover can’t send messages that are longer than p which will violate the Verifier’s polynomial time bound. So when we simulate the IP using the PSPACE machine we will check for all possible strings m(j+1) of length p and choose the one with the maximum probability.


#### Implementation(Recursion):



* We can implement this simulation using the recursion starting from an empty message stream we can recursively construct the message stream of length p. We will have two kinds of recursive calls. Assume that the random string is of length p. When we reach the message history p then the recursion will stop and return the final probability value of that particular recursive branch.
* In all the places wherever we consider the at most length of p is due to the polynomial time bound on the Verifier.
* **Case 1 - i is odd: **When the value of i is odd, then the Prover will send the next message. The prover doesn’t have any restrictions on how it constructs the message. So when we simulate this case we will consider all possible messages of length p and call the recursive function with each one of these messages. This will create multiple recursive branches.
* **Case 2 - i is even:** When the value of i is even, then the Verifier will send the next message. The verifier will send the next message using some random string r. First the simulator has to exclude all the random strings r that are not consistent with the message history M(i). Then for each consistent value of r we will get one message m(i+1). We will call the recursive function for each such message.
* Here we are checking all the consistent random strings at each step of the computation because we don't know which one the IP will use, So we will take a weighted average over all of them at each step.
* In a few minutes we will see how we can derive the acceptance probability for these different cases of recursive branches.
* **The last message**: For the message stream M(p) with p messages the value N_M(p)=1 when m(p)=accept. Here the messages from the Verifier in the message history that lead to the message m(p) should be consistent with some random string r, Otherwise N_M(p)=0. This is obvious because at each step of the computation we are only considering random strings that are consistent with the message history.
* The recursion will stop when it reaches the message m(p). If that m(p) is an accept message then return the probability N_M(p) = 1 otherwise return the probability N_M(p)=0.
* Then we have two cases for defining the value of N_M(i) using the value of N_M(i+1).

**Case 1- i is odd:**

**N_M(i)=max_m(i+1) [ N_M(i+1)]**



* When the value of i is an odd number, then the simulator will call a recursive function for all possible messages of length p. Based on our assumption any Prover P will try to maximise the probability of acceptance. So in this case we will only consider a branch which has the highest probability and return that value. Remember that for w in A this value will be at least ⅔ and for w not in A this value will be at most ⅓.

**Case 2- i is even:**

**N_M(i)=wt-avg_m(i+1) [N_M(i+1)]**



* When the value of i is an even number, then we will call the recursive function for each possible message that is constructed using each possible random string that is consistent with the message history M(i). Since we don’t know which random string the IP will use we will find the weighted average over all of them.
* For each such message m(i+1) we can get the probability N_M(i+1) recursively. For each recursive branch we will weight that N_M(i+1) by the fraction of the random strings and add them up together to get N_M(i).

**wr-avg_m(i+1) N_M(i+1) = sum over probability of each m(i+1) { Pr[w,r,M(i)] = M(i+1) N_M(i+1) }**



* For example if there are m random strings that are consistent with the message history M(i) then the fraction will be 1/m. This is the probability of IP choosing that particular random string among all possible random strings.
* This way we can get the value of N_M(0) by tracing backwards on the recursive tree, this is the probability that indicates whether the Verifier accepts w or not.
* **PSPACE**: Here the depth of the recursive tree will be p only. So we can do this simulation by following the depth first search(or pre order traversal) method just using polynomial space. Mainly we need to store p probability values and p fraction values on the recursion stack(one value at each recursion level).


#### **Proof (by Induction)**:



* Here we will use the proof by induction to prove that our PSPACE simulation works correctly for some IP that is probabilistically deciding some language A.

**The Base Condition:**



* For every 0&lt;=j&lt;=p and every message stream M(j). We will define the value of N_M(j) inductively for decreasing j. The j value starts from j=p. (Remember that this probability values are calculated using by traversing the recursive tree)
* For the message stream M(p) with p messages the value N_M(p)=1 when m(p)=accept. Here the messages from the Verifier in the message history that lead to the message m(p) should be consistent with some random string r, Otherwise N_M(p)=0.
* If the message stream M(p) consist of m(p)=accept then that means the Verifier will accept w and our probability N_M(p) = 1. This is straightforward and the base condition is true.

**The Inductive Hypothesis:**



* Assume that the claim is true for some j+1&lt;=p and any message stream M(j+1) and then prove this for j and the message stream M(j).
* This base condition implies that **N_M(j+1) = Pr[V accepts w starting at M(j+1)].** We have already discussed how the N_M(j) can be computed using N_M(j+1). It has two cases, one for odd values of j and another for even values of j.

**Induction when j is odd:**



* When the value of j is even, the Verifier will send the next message. So we computed a weighted average over all possible random strings that are consistent with the message history M(j). The following equation defines this idea mathematically.

N_M(j) = (sum over all consistent m(j+1)) { Pr[w,r,M(j)] = M(j+1) N_M(j+1) }



* In the above equation we can get the value of N_M(j+1) using the inductive hypothesis. If you apply that value here you will get the following equation.

N_M(j) = (sum over all consistent m(j+1)) { Pr[w,r,M(j)] = M(j+1) Pr[V accepts w starting at M(j+1)] }



* Based on our definition that Pr[V accepts w starting at M(j)] the above equation is that value.

**Induction when j is odd:**



* When the j value is odd, the Prover will send the next message. So we chose the probability for the m(j+1) that is the maximum among all possible messages. The following equation defines this idea mathematically.

N_M(j) = (choose the m(j+1) with maximum probability) { N_M(j+1) }



* In the above equation we can get the value of N_M(j+1) using the inductive hypothesis. If you apply that value here you will get the following equation.

N_M(j) = (choose the m(j+1) with maximum probability) { Pr[V accepts w starting at M(j+1)] }



* Based on our definition that Pr[V accepts w starting at M(j)] the above equation is that value.

The above two cases complete the inductive proof. So we proved that the IP class is a subset of the PSPACE class.


### Co-NP ⊆ IP(#SAT is in IP)

This containment says that every Co-NP language A will have a probabilistic polynomial time verifier that can verify the membership of the language. We will prove that by showing that Co-NP-complete language #SAT is in the class IP.

#SAT = { &lt;B,k> B is the CNF-formula with exactly k satisfying assignment }



* This language is in Co-NP because to verify some &lt;B,k> we have to check all possible assignments of that boolean formula B.
* This language is Co-NP-hard because By checking whether &lt;B,0> we can decide the Co-NP complete problem COMP_SAT(checks whether B is unsatisfiable boolean formula). So #SAT language is Co-NP-complete.


#### Proof Idea:



* First we will see one direct approach which solves this problem of verifying the number of satisfying assignments to some boolean formula B. But this approach takes exponential time. In the actual proof we will see that slight modification of this idea that will convert this solution from exponential time to polynomial time.
* Before jumping into the idea we need to set some notations. Let B be the boolean formula with variables x1 though x(m). Let’s define the function f_i(a1,a2,...,a(i)) to be the number of satisfying boolean assignments to B, when we fix the values a1 through a(i) for the variable x1 through x(i) respectively. a1,a2,...,a(i) belongs to {0, 1}. These values are fixed to either 0 or 1. Remaining variable values will not be fixed. After fixing the first i boolean values we will calculate the number of satisfying assignments as usual. Here bear with me for using underscore in places of subscript notation(like f_i(…).
* If you notice that in the function f_0() none of the boolean variables has a fixed value. So this function f_0() computes the same value as the number of satisfying assignments of B.

f_i(a1,a2,...,a(i)) = f_i+1(a1,a2,...,a(i),0) +  f_i+1(a1,a2,...,a(i),1)



* Based on our definition so far, we can intuitively understand that the above equality holds for our definition. We will define the following protocol that explains the interaction between the Prover and the Verifier. There are a total of m+1 phases, where m is the number of boolean variables in the boolean formula B. Here P is a Prover and V is a Verifier.

**Protocol:**



* Phase-1: The P sends the value of f_0(). The V checks whether f_0()=k or not. If not then reject.
* Phase-2: The P sends the value of f_1(0) and f_1(1). The V checks whether f_0() = f_1(0) + f_1(1). If not then reject. 
* Phase-2: The P sends the value of f_2(0,0), f_2(0,1), f_2(1,0) and f_2(1,1). Then the V checks whether f_1(0)  and  f_1(1) using those values. If they are not correct then reject. 

…



* Phase-m: The P sends the values of f_m(a1,a2,...,a(m)) for each possible value of a(i)’s. The V checks the 2^(m-1) equations of the format f_m-1(a1,a2,...,a(m-1)). If any one of them is not correct then reject.
* Phase-(m+1): In the Previous phase P sent the f_m(a1,a2,...,a(m)) for all possible values of a(i)’s. The V checks each of these values by directly substituting values a1,a2,…,a(m) in the boolean formula. Rejects if any one of them disagree with the answer sent by the Prover.

**Correctness:**



* Before getting into the correctness we need to define some notations. We call the P an honest prover, which is actually trying to give the correct answer. We call the C_P a crooked prover, which may or may not try to give the correct answer. When C_P gives wrong answers at some phases of protocol we denote those wrong answers c_f_i(a1,a2,...,a(i)) with the prefix c. Here you can think of the prefix c or C denoting the word ‘crooked’.
* When &lt;B,k> is actually in the #SAT language, some honest prover P can make the Verifier accept by giving honest answers at each phase of the protocol.
* When &lt;B,k> is not in the language #SAT language, then no prover(not even crooked prover) can make the Verifier accept the input. The acceptance probability will always be low in this case.
* For example if the actual value of f_0() != k and some prover C_P is giving the wrong value c_f_0() which is equal to k. Then the Verifier will either catch the C_P and reject at the second phase or C_P will again lie at the second phase of the protocol. If it lies at the second phase, then at least one of the values of f_1(0) or f_1(1) will be a lie. 
* Suppose if c_f_1(1) is a lie, then either the Verifier will catch the C_P at phase three or C_P should again lie. If it continues to lie like this at each phase of the protocol, the Verifier will catch the C_P at the phase m+1. Here C_P won’t be able to lie because the Verifier will directly check each possible value directly using the boolean formula B and compare it with the answers of the prover P.
* **The Problem:** So this protocol works correctly. But at each phase number of verifications needed to verify the previous phase doubles. So this will exponentially increase the number of messages shared between the Prover and the Verifier. So this protocol doesn’t work as a polynomial time Verifier.


#### The Proof



* The actual proof uses a similar idea as above. But it uses the arithmetization concepts which we have learned in the ROBP(Read Once Branching Program) problem. Here we use following equivalent arithmetic formulas for boolean formulas:  [note: here * notation defines the short form of the expression 1-(1-a)(1-b) for the simplicity]
    * (a ∧ b) = ab. 
    * (a ∨ b) = a * b = 1 - (1-a)(1-b).
    * (¬a) = (1-a).
* **Important notes:** The degree of the polynomial we get using the arithmetization is at most n for the boolean formula B of length n. This is because initially every boolean variable has degree 1 and the (ab) and (a*b) operations will just increase the power by the sum of powers of individual terms. We call this arithmetic formula p.
* When you apply boolean values to the variable both p and B will give the same results. When you apply non boolean values there is no direct connection between these two. But similar to the ROBP problem here also we will make use of arithmetic formulas to reduce the time complexity of the Verifier to the polynomial time complexity.
* **Finite Field F:** The non boolean values range over the set with q element where q is prime number larger than 2^n. Finding this value may need some special focus but it is achievable in polynomial time so we don’t focus on that now(The more powerful proof of PSPACE ⊆ IP doesn’t have this restriction). For example the  V can ask the P to provide one such prime number then verify whether it is prime or not in polynomial time(can be using some polynomial time algorithm like AKS primality testing).
* The following equation builds upon the previous definition of the f_i(r1,r2,...,r(i)) with minor differences. Here when we fix the variables x1,x2,…,x(i) to the values r1,r2,...,r(i), It will be non boolean random values from the finite field F. Then the remaining variable which doesn’t have a fixed value will take all possible values from the binary set {0, 1}. 
* Note that the value f_0() is computed by not fixing any of the variable values in the polynomial p. So this value is the same as the number of satisfying assignments of boolean formula B. 
* In the new protocol the prover won’t send all possible values of f_i(r1,...,r(i)), Instead it will send the polynomial f_i(r1,...,r(i-1),z). Then the Verifier will use this polynomial to verify the value of f_i-1(...). [Here f_i(...) is just a short notation for not repeating the function arguments] 

**Protocol:**



* Phase-1: The P sends the value of f_0(). The V checks whether f_0()=k or not. If not then reject.
* Phase-2: The P sends the polynomial f_1(z). The V checks whether f_0() = f_1(0) + f_1(1). If not then reject. 
* Phase-2: First the V will send some random value r1. Then the P sends the value of f_2(r1,z). Then the V checks whether f_1(r1) = f_2(r1,0) + f_2(r1,1). 

…



* Phase-m: The V will send the random value r(m-1). The P sends the values of f_m(r1,r2,...,z) Then the V will verify the value of f_m-1(r1,...,r(m-1)) = f_m(r1,...,0) + f_m(r1,...,1). 
* Phase-(m+1): Now the V already has the polynomial f_m(r1,r2,...,z). First the V will choose the next random number r(m). Then to verify the polynomial f_m(…) The V will directly apply the non boolean values r1,r2,...,r(m) to the arithmetized boolean formula and check whether that value is equal to the f_m(r1,...r(m)).

**Core Idea:**

Why do we need these series of checks?



* First in Phase-1 the Prover sends its actual answer to the question that is the number of satisfying assignments to the boolean formula B. Then all the remaining phases are just to verify whether the prover is honest or it is lying.
* The V asks the P for some polynomial equation with the following settings. The V asks to set x(i) = z for the polynomial f_i(...). The V will send random values r(j) from the set F for all the variables x(j) where j&lt;i. Based on our definition of f_i(...), we don’t fix the values for the variable x(j) where j>i. Those variables take all possible binary values from the set {0,1}.
* So because of these reasons the following must be true: f_0() = f_1(0) + f_1(1). If not then the value of f_0() is wrong. If this equation is true then The V must again verify whether the polynomial f_1(z) sent by the P is correct or not.
* To verify the polynomial f_1(z), The V will set x1=r1 and x2=z and ask for the polynomial f_2(r1,z). Then the V will check f_1(r1) = f_2(r1,0) + f_2(r1,1). If not then reject. If they are equal then V must again verify the polynomial f_2(r1,z). To verify that the V will follow a similar idea as we explained now.

**Correctness Case-1:**



* Here also the honest Prover P and the crooked Prover C_P notations are the same as the proof idea. When &lt;B,k> is actually in the #SAT language then some honest prover P can give honest answers at each phase of the protocol to make the Verifier accept the input. 

**Correctness Case-2:**



* So when &lt;B,k> is not in the language #SAT then no Prover(not even crooked Prover) will make the Verifier accept its input. We will make sure by verifying the answer of the P at each phase.
* **Phase-1:** in this case either f_0() should not be equal to k. If the Prover sends the correct value then f_0()!=k. So the V will reject. If P sends some wrong answer c_f_0() and c_f_0()=k then that means the C_P(crooked prover) might have lied at this phase. First to prove itself the C_P will send the f_1(z). Now when the V checks c_f_0() = c_f_1(0) + c_f_1(1). This expression won’t be equal if the P sent the correct answer f_1(z). Otherwise C_P might have lied about the polynomial by sending some wrong answer c_f_1(z).
* **Key Phase-2: **So now to verify the polynomial c_f_1(z), The V will send some random value r1 to the C_P and ask for another polynomial f_2(r1, z). Here r1 is a random value from the finite field F. When the V checks whether c_f_1(r1) = c_f_2(r1, 0) + c_f_2(r1, 1). They will not be equal with high probability if C_P is giving an honest answer f_2(r1,z). If C_P is lucky(either the polynomials agree because of the mathematical reason we will discuss next or C_P might have sent the wrong polynomial which agrees with the c_f_1(z)) then they will be equal then the V will verify the polynomial c_f_2(r1,z) by asking f_3(r1,r2,z) from the P.

**We have to understand one fundamental thing**: Let’s say f_1(z) is a polynomial and f_2(r1, z) is also polynomial which the P claims to be equivalent to the f_1(z). If they are actually equal then f_1(r1) = f_2(r1,0) + f_2(r1,1) should be equal. Why is this the case? Because f_1(z) applied all possible boolean values for all the variables x2,...,x(m) and f_2(r1,z) applied all possible boolean values for all the variables x3,...,x(m). So when we apply 0 and 1 for the variable z in the f_2(r1,z) it should give the same sum as f_1(r1) if these two polynomials are really equivalent. So if these two polynomials are not equivalent then they will give different results with high probability. Only way they are equivalent is either they are actually equivalent or the P might have lied about the polynomial f_2(r1,z). Why will they give different values with high probability when they are not equivalent? It’s because of the following reason.



* **Roots of the polynomial (f = f_1(r1) - f_2(r1, z)):** The roots of the polynomial are the values you apply to the variable of the polynomial for which they evaluate to zero(The polynomial itself shouldn’t be a zero polynomial which will always evaluate to zero). Based on some mathematical theorems the polynomial with the power d can have at most d roots. It can be easily verified. Since the power of f_1(r1) and f_2(r1,z) both can have at most the power n where n is the length of the boolean formula B, the power of the polynomial f must be at most n. So these two polynomials f_1(...) and f2(...) can agree for at most n values from the finite field set. So the probability that f_1(...) and f_2(...) are not equal but they agree for some random value r1 chosen from the set F by the V is **(n / 2^n) &lt;= (1/ n^2) ** for n>=10. So if the polynomials are not equal, then this protocol will reject them with high probability.

**The final check**:


* Like above at each phase the V will check whether the polynomial sent by the P from the previous phase is correct or not. At the Phase-m the P will send the polynomial f_m(r1, r2,...,z). 
* To check whether this polynomial is correct or not the V will arithmetize the boolean formula B itself. Let's call this polynomial q(...). This conversion will only take polynomial time for the Verifier. But we can’t use this polynomial q(…) to directly verify the number of satisfying assignments of B. That’s the reason we ask that answer to the P. Then we can use this polynomial q(…) to verify the answer of the C_P.
* Now by directly applying the values r1,r2…,r(m) to the polynomial q(…) the V can check whether q(...) = f_m(...). Because of the same reason we discussed above, we can catch if the C_P is lying at this phase. If C_P is lying then q(...) and f_m(...) are not actually equal, so they will disagree for most of the random values r(i) from the finite field F. So we will reject the input.

**Useful Note**: 


* We have understood one thing here: if the Verifier tries to multiply and sum each term of the polynomial formula to find each coefficient of the final polynomial it might take exponential time. But the Verifier won’t do that and it won’t simplify the polynomial formula arithmetically. It would rather compute the values numerically. It will directly apply the random values it has chosen from the finite field in the boolean formula and whenever it needs to compute AND, OR or  NOT operations it would use equivalent arithmetic identities for them. This process will only take polynomial time. Also remember that it can apply the (mod p) whenever it needs to keep the computed result values polynomial in size.

* So if you have a polynomial with n variable then it can have exponential number of coefficients with respect to n. That’s the reason at each phase of the protocol the Verifier asks the Prover a polynomial with a single variable. When the polynomial with a single variable has power d(here d is the length of the boolean formula), It can have at most d roots and d+1 coefficients.

**The error probability**:



* At each phase the error probability is (1/n^2). There are a total of m phases, where m is the total number of boolean variables in the boolean formula B. The value of m will be at most n where the n is the length of the boolean formula B. So the error probability = (m)(1/ n^2) = (n)(1/ n^2) = 1/n. 


### PSPACE ⊆ IP(TQBF is in IP)

This containment says that every PSPACE language A will have a probabilistic polynomial time verifier. We will prove that by showing that PSPACE-complete language TQBF(True Quantified Boolean Formula) is in the class IP. This proof is going to be similar to the previous containment that Co-NP is a subset of IP. But here we use some additional logic to reduce the degree of the polynomial. Remember that here the Prover only needs the capability of a PSPACE machine.

#### Proof Idea

* We write the quantified boolean formula in the following format: S = Q1x1 Q2x2…Q(n)x(n) [B]. Here each Q(i) is either universal quantifier(∀) or Existential quantifier(∃). The B is the boolean formula made up of boolean variables x1,x2,…,x(n). Here B is in the conjunctive normal form(CNF-formula).
* Function f_i(...): We define the function f_i(a1,a2,...,a(i)) = 1 if Q(i+1)x(i+1),...,Q(n)x(n) [B(a1,a2,...,a(i))] = 1, the value is 0 otherwise. Here the boolean values a1,a2,...,a(i) is substituted for the boolean variables x1,x2,...,x(i). All the remaining variabel will take all possible values from the binary set {0,1}. This idea is same as what we have done for #SAT. Only difference is that we have taken the quantifiers into consideration.
* The next thing is we have to arithmetize the quantified boolean formula. We can directly arithmetize the CNF formula B as before. The tricky thing is we have to arithmetize the quantifiers. For that we use the following identities.

If Q(i+1) = ∀ then f_i(a1,a2,..,a(i)) = f_i+1(a1,a2,...,a(i),0) . f_i+1(a1,a2,...,a(i),1).

If Q(i+1) = ∃ then f_i(a1,a2,..,a(i)) = f_i+1(a1,a2,...,a(i),0) * f_i+1(a1,a2,...,a(i),1).

* Here also the * operation is used for similar notation as before.(a*b = 1 - (1-a)(1-b)). These two identities are equivalent to the AND and OR boolean operations.

**The Problem**:

* Now we can think of using this f_i(...) as before in the protocol. But the problem is that each time when we apply the identities for the quantifier, it squares the degree of each variable in the polynomial. This will increase the degree of the polynomial to the exponential value with respect to the length of the boolean formula. 
* When the degree is exponential there can be an exponential number of coefficients for that polynomial. Since the Verifier operates in the polynomial time bound the Prover can’t send all these exponential number coefficients to the Verfiere. To solve this problem we introduce one more operator called the Reduction operator. We will see that in the proof.

#### The Proof

* Let S’ be the following boolean formula with reduction operators included in the TQBF formula S. 

    S’ = Q1x1 R1x1 Q2x2 R1x1 R2x2 … Q(n)x(n) R1x1 R2x2…R(n)x(n) [B]. 

* Here Q(i) represents a quantifier and R(i) represents a reduction operator. We will define this reduction operator such that it will reduce the degree of the polynomial which is increased due to the quantifiers, but it won’t affect the equivalence of the f_i() = S in the boolean world. That is when all the variables in the polynomial are fixed to only boolean values then that polynomial is equivalent to the TQBF S.
* We generalise the new boolean formula to the more general form S1y1 S2y2…S(k)y(k) [B]. Here the S(i) can be either quantifiers or reduction operators. The y(i) can be any one of the variables from x(1) through x(n). We defined this general form because next we will see that the protocol will have phase i for each term S(i)y(i).
* We define the following arithmetical identities that are equivalent to the operation S(i) in S’.

If S(i+1) = ∀ then f_i(a1,a2,..,a(i)) = f_i+1(a1,a2,...,a(i),0) . f_i+1(a1,a2,...,a(i),1).

If S(i+1) = ∃ then f_i(a1,a2,..,a(i)) = f_i+1(a1,a2,...,a(i),0) * f_i+1(a1,a2,...,a(i),1).

* These two cases are straightforward. Here f_i+1(...) will depend on one extra variable y(i+1)=x(j) for corresponding j than the f_i(...). For the variable x(i+1) we will substitute both 0 and 1 and compute the AND or OR operation correspondingly. Whenever we apply these two identities it will double the degree of each variable in the polynomial. So we use the Reduction operator.

**How does the reduction operator R work?**

If S(i+1) = R then f_i(...,a) = (1-a) f_i+1(...,0) +  (a) f_i+1(...,1).

* Here we substitute y(i) = a for R(i+1)y(i+1). The first thing to keep in mind is that we have reordered input arguments to the functions f_i+1(...). For example if we do the arithmetization for R1x1 then we move that x1 to the last position of the input arguments in f_i+1(...). 
* Also here f_i(...) and f_i+1(...) have the same number of input arguments. This is because we pass one more argument to the f_i(...,a) stating the value of the reduction variable. So in the case of reduction operator f_i(...) depends on i+1 input arguments.

**Multiply the f_i+1(...,0) by (1-a) and substitute y(i+1)=0:**

* First we substitute y(i+1)=0 in the f_i+1(...). For j&lt;=i we substitute y(i) = a(i) in the f_i+1(...) and for j > i+1 we substitute all possible values from the binary set {0,1}. 
* Remember that in each step of arithmetization we don’t just the sum the results for all possible values {0,1} like we did in the #SAT problem. Rather we will use any one of the above identities for the arithmetization based on the symbol at S(i).
* Whatever numerical value we get by evaluating the f_i+1(..., 0), we will multiply it with the term (1- a).
* The value of (a) can be anything based on the current phase of the protocol. These values are set by the Verifier. For example the Verifier might set that value of y(i+1) to be a(i+1) or variable z. When the value of y(i+1) is some variable z then this reduction R(i+1)y(i+1) will reduce its degree and make the f_i(...,a) linear equation of (a). If y(i+1) = a(i+1) is some numerical value then the R(i+1)y(i+1) won’t do anything and won’t affect the result on the boolean world. 
* By doing this we will linearize(reduce the degree to 1) the polynomial. Initially if the x(j) has some higher degree, after applying this reduction operation R(i+1)y(i+1) where y(i+1) = x(j) for some corresponding j. Then the x(j) will come down to power 1.
* For example, initially if f_i+1(...) = k1x(j)^e + k2(1-x(j)^(e-1)) +... polynomial. If x(j)=a, then this will be reduced to the polynomial (1-a)k. Where k = f_i+1(...,0). So now the x(j) is linearized. 

**Multiply the f_i+1(...,0) by (a) and substitute y(i+1)=1:**


* Similarly we substitute y(i+1)=1 in the f_i+1(...) and multiply it with the term (a). For all the remaining variables we will either put some fixed values or all possible values over the binary set {0,1} and do the arithmetization based on the rules we discussed above.

**Reduction operator on Boolean inputs:**


* Reduction operator won’t affect the boolean world because the term (1-a)f_i+1(...,0) will only contribute to the final result when a=x(j)=0. Similarly the term (a)f_i+1(...,1) will only contribute to the final result when a=x(j)=1.

**Why do we repeat R(i)x(i) for all the Q(i)x(i) through Q(n)x(n)?**


* Theoretically we could have applied all the reduction operators at the end after applying all the quantifiers in the arithmetization process. This is because applying the reduction operator for x(j) single time will reduce the degree of x(j) from any value to 1. There may be some problems, where before applying the reduction operation the degree of the polynomial becomes so big and it becomes intractable in practical use cases.
* So to give the proof which is worthwhile in both theoretical and practical world we need to apply the reduction operation after each time we apply some quantifier operation. This will simplify the polynomial after each quantifier operation.


#### The protocol

Here the P means the Prover, C_P means the crooked Prover and the V means the Verifier. At each phase we choose random numbers from the finite field F. Here the size of the finite field should be q where q is at least n^4. Here this bound is needed to prove the probabilistic correctness of the Verifier. Here also we use the terminology f_i() means the answer is from honest Prover P and c_f_i() means the answer is from the crooked Prover C_P.

 
* **Phase 0**: The P will send the value f_0() and if f_0() !=1 then the V will reject, otherwise go to the next phase

…

…

* **Phase i**: The P will send a polynomial f_i(r1,r2,...,r(i-1), z) to prove that f_i-1(r1,r2,...,r(i-2),z) was correct(the polynomial sent at the previous phase). The P will send the value f_i(r1,r2,...,r(i-1),z) = f_i(...,z). The Verifier checks the value of f_i-1(...) by using the following condition.

**If S(i)= ∀ then f_i-1(r1,r2,...,r(i-1)) = f_i(...,0) . f_i(...,1).**

**If S(i)= ∃ then f_i-1(r1,r2,...,r(i-1)) = f_i(...,0) * f_i(...,1).**

**If S(i)= R then f_i-1(r1,r2,...,r(i-1), r) = (1-r) f_i(...,0) * (r)  f_i(...,1).**

Here the value of the value of x(j) that corresponds to a label y(i). It will be one of the variables for which we have already chosen random values so r = x(j) = a(j).

If f_i-1(...) does not agree with f_i(...) then reject, otherwise,

the V will choose some random value r(i) from the finite field F and send it to the P. 

**Conflict:**


* If S(i) is a universal or existential quantifier then there won’t be any problem. The x(j) that corresponds to y(i) will get the new random value r(i). 
* But if S(i) is some reduction operator then the x(j) that corresponds to y(i) might already have some random value assigned to it, then we will replace the old value of x(j) with this new random value r(i).

   
Go to the next phase i+1 where the P will persuade that f_i(...) is correct. 

…

…

* Phase k+1: In the previous stage the P might have sent the value f_k(r1,r2,...,r(m)). We get the numerical value at phase k because the S(k) corresponds to just a reduction operator. Now the V can directly apply all the random values to the TQBF formula S and check whether f_k(...)=S. If they disagree that means there is a very high probability that the P was lying, so the V will reject. Otherwise the V will accept.

**Explanation:**


* First at the phase i the Prover will send the polynomial with a single variable x(i) = z. All j &lt; i the Verifier will set the value of x(j) = r(j), where r(j) is some random value from the finite field F. 
* For j > i the Prover will compute all the values over a binary set {0,1}. When we compute over set {0,1} we will do an AND operation if the quantifier is universal and an OR operation if the quantifier is existential.
* So at phase i to verify the value of f_i-1(r1,r2,...,r(i-1)) the Verifier will use the polynomial f_i(r1,..r(i-1), z) where x(i) = z. If the Prover just uses S without any reduction operator then this polynomial would have an exponential number of coefficients. But when the P uses S’ with a reduction operator the polynomial will have only the polynomial number of coefficients.

**The correctness:**


* This protocol is correct because of  the same reasons we discussed in the correctness of the protocol for #SAT. When some &lt;S> is in the language then some honest prover P can always make the V accept by giving the honest answer at each phase of the protocol. When some &lt;S> is not in the language then no prover C_P(not even crooked Prover) can make the V accept with high probability. 
* The series of phases will verify the correctness of the previous phase using some random value r(i). So even if C_P lies at each phase of the protocol, it will be caught at the phase k+1 when the V directly checks the correctness of f_k(...) using the formula S.
* The V can directly substitute the random values in the formula S and compute the result in polynomial time. This is possible because the V won’t arithmetize the whole formula instead use the arithmetical equivalent operations for boolean operation on demand in each step of the computation.
* If C_P lies and gives the wrong polynomial c_f_i(...) instead of f_i(...) at each phase, then the polynomial f_i-1(...) will disagree with c_f_i(...) with high probability for almost all the random values we choose from the finite field F. If f_i-1(...) and c_f_i(...) are even slightly different polynomials then they will agree on a very small number of random values in the finite field F. That number depends on the degree of the polynomial. 
* The degree of our polynomials is at most d where d is the length of the boolean formula. So the two different polynomials may agree on at most d number of values. We choose the random values from the finite field with n^4 elements. So the probability we choose those d values from the finite field F is (d/n^4) = (n/n^4) = (1/n^3) where the length of the boolean formula is d=n.
* Since we added extra reduction operators the protocol proceeds for O(n^2) phases. So at phase k the error probability will be O(n^2)O(1/n^3) = O(1/n).

**Why q > 2^n for #SAT but q>n^4 for TQBF: **


* We choose the size of the finite field to be some prime number q. Which should be at least 2^n. Why do we need this upper limit for the #SAT? We could have got the same error probability if we had chosen it to be n^3. But this is not the case for the proof that TQBF is in IP. Here a finite field can have a size of q which is at least n^4.
* I think to understand this we have to notice that all the computation for the polynomial is done using (mod q) during the interaction between the Prover and the Verifier. The boolean formula with n variables can have at most 2^n number of satisfying assignments. So when we compute the number of satisfying assignments (mod q) then that value should have an upper limit 2^n. That’s the reason we chose the value of q to be at least 2^n. There is some correspondence between the number of satisfying assignments and the value of q.
* But in the case of the TQBF problem we are just checking whether a quantified boolean formula is satisfiable or not. We are not counting the number of satisfying assignments to the TQBF. So for proving TQBF is in IP, the q value of at least n^4 is enough.

**This completes the proof that TQBF is in the class IP. Also this completes the proof of the statement IP=PSPACE.**

