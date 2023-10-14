
## Complexity Theory(Intractability)

* We have seen so for some of the important complexity classes. As for our understanding, below is the order. 

**                   L ⊆ NL ⊆ P ⊆ NP⊆ PSPACE**



* One thing we know is that when we give TM a bit more space or a bit more time then it can do more. So this implies L != PSPACE and since NL has O(log(n))^2 bound NL != PSPACE. We will see this idea clearly in Time and Space Hierarchy theorems.

                   **TIME(n^2) ⊂ TIME(n^3)**

**                   SPACE(n^2) ⊂ SPACE(n^3)**



*  Certain computational problems are solvable in principle, but the solutions require so much time or space that they can’t be used in practice. Such problems are called intractable.


### Hierarchy Theorems

We can understand that when we give a Turing machine more time or space then it should increase the class of problems it can solve. The hierarchy theorem proves exactly this.


#### Space Constructible



* We can call a function f(n) space constructible, if it maps the input 1^n to the output f(n) just by using O(f(n)) space. Here note that 1^n represents number n by putting n consecutive 1’s on the tape(we call this unary format). So the Turing machine has to compute the function f(n) using that n value and output the computed result in the binary format. To do that machine should only use O(f(n)) space.
* Here note that f(n) should be at least O(log(n)) space. This is because even if we store input in separate input tape we will need at least log(n) space in work tape to store the current head position on the input tape.
* For example if f(n)=n^2, then we have to compute the square of the number n by just using O(n^2) space. For this we know the solution is that we can convert 1^n to the binary format and use any standard procedure to compute n^2 and output the n^2 value in the binary format by just using the O(n^2) space.
* Here there is a catch. Assume that the function f(n) is o(n) and we need to store n value in unary format 1^n. Then how can we store that in the tape which should use only the space &lt; n. For this we use the separate input tape just like what we did for the sublinear space or in other words log space models.

Why do we need this space constructibility?



* If the f(n) is bigger than g(n) in a very small amount( or increases by a constant factor) then that would not help the machine with f(n) space to solve more problems than the machine with g(n) space. So using the space constructibility ensures that the f(n) machine can solve more problems than the g(n) machine.
* Another example is f(n)=log(log(n)). As n grows bigger we won’t be able to compute the f(n) by just using O(log(log(n)) because to store the pointer for the input tape head itself will need O(log(n)) space. This is why we set the lower limit to O(log(n).


#### Space Hierarchy Theorem

For any space constructible function f(n) there exists a language A such that we can solve the problems in that language using O(f(n)) space but not using just the o(f(n)) space.



* This implies that SPACE(o(f(n)) is a proper subset of SPACE(O(f(n)).

Idea:



* So we will use the idea of diagonalisation here. We have to prove that there exists some language A such that it is decidable in O(f(n)) space but not with o(f(n)) space.
* We will construct a TM D that will take any other encoded Turing machine M as an input and try to simulate that Turing machine using o(f(n)) space. If it uses more than o(f(n)) space or input is not of the format &lt;M> then we will reject it.
* If D is able to simulate M using just o(f(n)) space then D will do the opposite of whatever M decides. By doing this D makes sure that it is different from the Turing machine M.

Algorithm:

TM D=“On input w



1. Let n be the length of w
2. Compute the value of f(n) using space constructibility and mark off that much space of the tape. At any point of time if later steps try to use more space than this then reject.
3. If w is not of the form &lt;M>10* for some TM M then reject.
4. Simulate the Turing machine M on input w while counting the number of steps used by the simulation. If the number of steps used in the simulation ever exceeds 2^f(n) then reject.
5. If M accepts w then reject or if M rejects then accept.”

Explanation:



* Stage 1-2: Our goal here is we want to find some language that is in SPACE(O(f(n))) but not in SPACE(o(f(n))). So for that we will compute the value of f(n) for the length of the input w. Since we already know the function f(n) we can compute this value based on space constructibility.
* Stage 3: Sometimes for small values of n the function f(n) might not be enough to simulate M in just o(f(n)) space when that machine has some big asymptotic constant. For example for n&lt;n0 the function g(n)= 10000*g(n) for the Turing machine M. To avoid this problem we modify D so that it runs M whenever it receives the input of the form &lt;M>10*. Now since the length of w becomes very large the asymptotic constant won’t have any effect on this simulation. Also remember that we will remove this extra part 10* to get the description of the Turing machine M.
* Stage 4: Now we will simulate machine M. The machine M may run for infinite time by just using o(f(n)) space. To avoid an infinite loop we count the number of steps used by simulation. This will take only f(n) space because to store the counter for number 2^f(n) will need log(2^f(n))=f(n) space only. This way we can reject the machine which rejects its input by looping. 
* Stage 5: this stage is very crucial. This differentiates machine D from any other machine M that used o(f(n)) space. If any machine completes stage 4 that means that machine will operate just using o(f(n)) space. In stage 5 by doing the opposite of machine M we can ensure that the Turing machine D is different from that Turing machine M.

How?



* First note that in any of the stages if it tries to use more than o(f(n)) space then we will reject it. 
* Assume that some language A is decided by D using the O(f(n)) space and we can’t simulate that using o(f(n)) space.
* On the contrary , if we assume that some Turing machine M decides A in o(f(n)) space. Then we pass the &lt;M>10* to the Turing machine D and it will simulate M successfully and do the opposite of what M does. This is a contradiction. This means there exists no such Turing machine M.

Corollary:



* For any two real numbers x and y such that x&lt;y then SPACE(n^x) is a proper subset of SPACE(n^y). **SPACE(n^x) ⊂ SPACE(n^y).**
* NL is a proper subset of PSPACE. By Savitch’s theorem we know that NL is a subset of the SPACE((log(n))^2). So by using the Space Hierarchy theorem we can prove that NL is the proper subset of PSPACE. **NL ⊂ PSPACE.**


#### Time Constructible

A function t(n) which is at least of O(n log(n)) is time constructible if that function can compute the value of t(n) in the binary format for the input 1^n(unary format) by just using O(t(n)) time. Here we represent input value n by putting n consecutive 1’s on the input tape.



* Why is the lower limit for the time constructible is O(n log(n)). This is because to convert the unary format input to the binary format itself will take this much time. This is because we will use O(n) steps to count the number of 1’s in the input tape and for each one to increment the binary counter we will use O(log(n)) steps.


#### Time Hierarchy Theorem

   For any time constructible function t(n) there exists some language A such that A can be decided using O(t(n)) time but can’t be decided using o(t(n) / log(t(n))) time. 



* This implies that **TIME(o(t(n) / log(t(n))) ⊂ TIME(O(t(n))**

Idea:



* This theorem is similar to the SPACE hierarchy theorem. We will construct a Turing machine D such that some language A can be decided by D using O(t(n)) time and this language can’t be decided by any other Turing machine M by just using o(t(n) / log(t(n))) time.
* Here note that there is 1/log(t(n)) factor in the theorem. This is because we need to count the number steps used by Turing machine M to decide some language A and make sure it doesn’t exceed o(t(n)/ log(t(n))) time. 
* So now the machine M itself will use t(n) / log(t(n)) time and the Turing machine D will take extra log(t(n)) time for each step of the Turing machine M to keep track of that counter. Finally machine D will take O(t(n)) time to decide its language.
* Remember when M uses t(n) / log(t(n)) time then only D will use t(n) time otherwise D will use more than t(n) time. This is the reason for that extra log(t(n)) factor in the time hierarchy theorem. Also remember that in the space hierarchy theorem we only had constant factor overhead for the simulation of Turing machine M.

Algorithm:

TM D=“On input w



1. Let n be the length of w
2. Compute the value of t(n) / log(t(n)) using time constructability and decrement this counter before each step of the simulation of the TM M. If it ever hits the value 0 then reject.
3. If w is not of the form &lt;M>10* for some TM M then reject.
4. Simulate the Turing machine M.
5. If M accepts w then reject or if M rejects then accept.”

Explanation:



* Stage 1 & 2: These two stages are similar to the first two stages of the space hierarchy theorem. Only thing is here we are counting the number of steps used by the machine instead of space used by the Turing machine. Since we are already counting the number of steps used by the Turing machine M we don’t need a separate counter for checking an infinite loop like we did in the space hierarchy theorem.
* Stage 3, 4 & 5: These stages are also similar to the Space hierarchy theorem. To avoid the the problem created by the large asymptotic constant we accept all inputs of the format &lt;M>10*. Then we simulate the Turing machine M and do the opposite of what M does by just using o(t(n) / log(t(n))) time and D uses O(t(n)) time for doing that.

How?



* The core logic is similar to the space hierarchy theorem. If M uses more than o(t(n) / log(t(n))) time then we will reject and if M uses just o(t(n) / log(t(n))) time then D will do the opposite of what M does to ensure that D is deciding the different language than M.

Why?



* Here why M uses o(t(n) / log(t(n))) time but D uses O(t(n)) time to simulate M? This is because D uses O(log(t(n)) time to keep track of the number of steps used by M. For doing this D uses multiple tracks on the single tape of the turing machine.
* If we don’t use multiple tracks then D will use more than O(t(n)) time. To avoid that only we use multiple tracks. For example two tracks means some content will be stored in then even positions of the tape and some content will be using odd positions of the tape. We used the similar logic to simulate the multitape turing machine in the single tape turing machine.
* Why do we need multiple tracks? First we need one track to store the input of the turing machine M. Then for each time to decide the next step of the Turing machine M we need to look up its transition table. For that we need to store its transition table in the second track. This will add only constant overhead for the simulation time because the transition table doesn’t depend on the input length. Also each time when we move the tape head to the next position we will also shift the content of the second track correspondingly near to the head position. This shifting also will take only constant time overhead.
* We need to keep track of the number of steps used by the Turing machine M to do this we need a third track. But this counter length depends on the input length. We need to decrement the value of (t(n) / log(t(n)) to do this we will need log(t(n) / log(t(n))) = log(t(n)) space. So we will need a third track to keep track of this counter. We will shift this third track near the head position of the Turing machine M for that we will need O(log(t(n)) time. This is that 1/log(t(n)) time overhead we were discussing. 
* Also note that in some places above we assumed that the asymptotic constant is 1 and used t(n) / log(t(n)) instead of O(t(n) / log(t(n))).

Corollary:



* If t1(n) = o(t2(n) / log(t2(n))) then TIME(t1(n)) **⊂ **TIME(t2(n)).
* For any two real numbers x and y, If 1&lt;=x &lt; y then TIME(n^x) **⊂**TIME(n^y).
* The above two corollaries implies that P **⊂ **EXPTIME

**EXPTIME-complete:**

  The language B is EXPTIME-complete if it satisfies following two conditions.



1. B is in EXPTIME.
2. Every problem A in B is polynomial time reducible to B.

Suppose if some language is in EXPTIME-complete then we can prove that that problem will never be in P. This is because if it is in P then all the problems in EXPTIME are also in P. That means P=EXPTIME contradicting the TIME hierarchy theorem.


### EXPSPACE Completeness

**Intro:** 



* First note that the language B is in EXPSPACE if B can be decided using  exponential space SPACE(O(2^n)).
* By hierarchy theorems we know that EXPSPACE has more languages than the PSPACE. Together with this we use the fact that some problem called generalised regular expressions(GREX) is EXPSPACE-complete to show that some problems are intractable. This is because we don’t have practical capability to solve the EXPSPACE problems in any modern day computers. 

**The generalised regular expressions(GREX): ** 



* The normal regular expression(REX) allows us to use a null symbol, empty string symbol and any symbol from the alphabet set together with three regular operations to generate various strings in a particular language. The three regular operations are Union, Concatenation and Start operation denoted by **∪** , o and * respectively. We know that we can check the equivalence of two regular expressions by just using polynomial space. For this we can convert the regular expressions to the NFA then to the DFA then check the equivalence of two DFA by simulating them in polynomial space.
* **Exponentiation operation:** But by allowing one more operation to the regular expression we can increase its complexity drastically. By adding exponentiation operations we can show that this new generalised regular expression(GREX) will need exponential space to check their equivalence. For exponentiation operation we can represent it by R^k for simplicity here where R is the regular operation, k is some positive integer and R^k means repeating R for k time. 
* After adding this new operation the regular expression represents the same set of languages as before only there is change in the space used by them. This is because we can replace the exponential constant k by repeating R for k times.

We create one new language with this new definition of regular expression.

EQ_GREX = { &lt;Q,R> | Q and R are two equivalent generalised regular expression with exponential operation } 

**EXPSPACE-complete:**

       We say that some language B is EXPSPACE-complete if it satisfies the following two conditions.



1. B is in EXPSPACE.
2. Every language A in EXPSPACE is polynomial time reducible to the language B.

Here note that if some problem is in EXPSPACE-complete that means it can’t be solved in PSPACE. Suppose if we can solve in PSPACE then the PSPACE will become equal to the EXPSPACE which will contradict the SPACE hierarchy theorem.


#### EQ_GREX is EXPSPACE-complete:

Core Idea:



* We will first prove that EQ_GREX is in EXPSPACE by converting GREX R^k  to REX by repeating R for k times. Then convert those REX into a NFA. Then we can check the equivalence of two NFAs just using polynomial space. We will see how we can achieve it.
* Then we can use the reduction by computation history method to reduce every language A in the EXPSPACE to the language EQ_GREX. These two points will imply that EQ_GREX is EXPSPACE-complete.

**EQ_GREX is in EXPSPACE:**

Algorithm-1:

COMP_EQ_NFA = “on input &lt;N ,M>:



1. Mark the start state of NFAs M and M.
2. L1:Repeat the following for 2^q times where q is the sum of the number states N and M.
3.     L2: Non-deterministically choose input symbols from the alphabets and change the current state marker in both NFAs for that input symbol.
4. If at any time a marker of any one NFA is placed on accept state but not for the other NFA then accept, otherwise reject.”

Explanation:



* So actually this is kind of basic for proving that two GREX are equivalent. This COMP_EQ_NFA will accept its input when N and M decide different languages; we will use that to construct the EQ_GREX. Here stage 1 just marks the start state of both NFAs.
* **Stage 2 & 3:** We are going to non deterministically check all possible strings of length less than or equal to 2^q. This way if any one of the strings is accepted by one NFA but not by another one that will imply that two NFAs are different. So we will accept that input. Here q is the sum of the number of states in both NFAs. 
* Here we use the fact that If some NFA N accepts some string then there must be one such string with length less than or equal to the number of states of that NFA N. On the contrary assume that N accepts a string that is longer than the number of states then there must be some repetition in the series of marked states that will imply that there is some repeating part in that long string. We can remove the repeating part to get some shorter accepting string.
* **Stage 4:** If at any non deterministic branch one NFA accepts but not the other one this will imply that both the NFAs are different so we will accept in that non deterministic branch then the whole machine will accept.

Space complexity:



* This algorithm only uses linear space(O(n)) to store the position of the current state of both the markers and the counter that will check for 2^q steps which will need log(2^q)=q which is the sum number of states of each NFA. 
* By Savitch’s theorem the equivalent deterministic algorithm will only take O(n^2) space. So we can convert this machine to its deterministic version. The complement of that deterministic machine will solve the EQ_NFA problem by just using O(n^2) space. 

Algorithm -2:

EQ_GREX = “On input &lt;P^k, R^m>:



1. First remove the exponentiations k and m by repeating P for k times and R for m times.
2. Convert those abbreviated regular expressions to their equivalent NFA.
3. Use a deterministic version of COMP_EQ_NFA to decide where two NFAs are equivalent. If yes then regular expressions are equal.”

Explanation:



* **Stage 1:** This is straight forward we will just repeat the P and R for k and m time and remove those exponentiations. You can notice that this stage will require exponential space to store both the abbreviated regular expressions.
* **Stage 2:** We already know that the regular expression of length n will only take O(n) space to convert them to NFA. We will first create equivalent NFAs for Union, concatenation and start operations. Then we will use them as building blocks to convert the regular expression to a NFA.    
* **Stage 3:** Then we can use the COMP_EQ_NFA to determine whether two NFA are equal. 

Space complexity:



* Suppose k is in binary format and its length is 5 means it can increase the length of P by at most O(2^6) times. Because that is the upper limit for the largest number that can be represented by 5 bits. 
* Now if the input length of the EQ_GREX machine is n then it can increase the length of regular expression by at most n2^n. Here we are considering that P and R’s length is n and also k and m’s length is n. But the actual values will always be less than that. Then the non deterministic version of COMP_EQ_NFA will take O(n 2^n) space and the deterministic version will use O(n^2 (2^n)^2) space. This makes sure EQ_GREX will only use exponential space.

** EQ_GREX is in EXPSPACE-hard:**



* Assume that there is some Turing machine M that uses 2^(n^k) space to decide some language where k is some constant. We will create two regular expressions R1 and R2 for this Turing machine M on input w such that if those two regular expressions equal if and only if M accepts w. Here R1 and R2 will represent the different computation histories of the Turing machine M.
*  R1 is the all possible strings of length 2^(n^k) using the tape alphabets, state symbols of the turing machine M and the symbol #. The hash symbol is used for separating two configurations in the computation history. So R1 will represent all the possible computation histories of the Turing machine M with space 2^(n^k).
* R2 is all possible computation histories that are not rejecting computation histories of the Turing machine M on input w. M will accept w if and only if it has no rejecting computation history for M on input w. So this R2 will contain all the computation histories that are accepting computation histories. Similar to accepting computation history, rejecting computation history will end with the configuration which contains q(reject) state in it.
* There are three ways that the computation history will fail to become a valid rejecting computation history. First one is invalid start configuration, Second one is invalid end configuration and final one is invalid middle configuration which does not follow from previous configuration legally. We call these three cases R(bad-start), R(bad-end) and R(bad-window). These three are similar to previous computation history methods we have seen.

**Core Idea:**



* Suppose if M accepts w then R2 won’t have any rejecting computation histories so it will generate all possible computation histories for the Turing machine M. Here note that we are not saying all possible computation histories for M on w. This is intentional because R2 only makes sure it won’t generate any rejecting computation histories but that doesn’t mean R will generate all accepting computation histories. We don’t need only accepting computation histories but rather all the computation histories that are possible for the Turing machine M that are not the rejecting computation history for the M on w.
* This way when there is no rejecting computation history for M on w then both R2 and R1 will generate the same set of computation histories, So both of them will be equal. If there is some rejecting computation history for M on w then R2 will avoid generating it and R1 generate everything including that rejecting computation history. So this will result in R1 and R2 to generate different languages.
* **Important**: Also let **E = Q ∪ F ∪ {#}** where Q is a set of states and F is a set of tape alphabets of the Turing machine M. E(-q0) means all the symbols in the E except q0. E^k means repeat E for k times. Here we use ^ this symbol as an exponentiation operation.
* Building R1 is simple it will generate all possible possible string with tape alphabets and state symbols of M and #**. So R1 = E***. Next we will see how we can construct R2.

**Construction of R2:**



* We assume that all the configurations are of exactly 2^(n^k) length. If some configuration is shorter than that then we will add padding of blank symbols to get the same length. **R2 = R(bad-start) ∪ R(bad-end) ∪ R(bad-window)**. Remember that I use an underscore( _ ) character to represent a blank symbol.

Construction of R(bad-start):



* This will generate all the strings that are not starting with valid start configurations. The valid start configuration will be C1 = q0w1w2…w(n)_ _…_ _#. So we will construct R(bad-start) as the union of multiple small parts. **R(bad-start) = S0 ∪ S1 ∪ S2 ∪ … ∪ Sn ∪ Sb ∪ S#**
* **S0:-** This will generate all the configurations that are not starting with start state q0 in its first position. S0 = E(-q0) E*. This regular expression will have any symbol other than q0 in first position and any symbol from the set E in all the remaining positions. Note that we are using the star regular operation here.
* **S1:-** This will generate all the configurations that fail to have w1 in the second position. S1 = E E(-w1) E*. In general for any i from 1 to the n the S(i) = E^i E(-w(i)) E*. This regular expression will generate all the configuration that has any symbol in the first i positions and any symbol except w(i) in the i+1 position and any symbol in all the remaining positions. Here note that we have used the exponentiation operation. E^i means repeating E for i times. We have used exponentiation just for convenience here. Later we will see that exponentiation will be necessary to keep the reduction time polynomial.
* **Sb:-** This will generate all the strings that fail to have a blank symbol from the position n+2 to 2^(n^k). For this also we could have used Sn+2, Sn+3… S2^(n^k) but that will increase the length of the configuration to the exponential value, which will lead to the exponential time reduction. To avoid this problem we use the exponentiation regular operation. Note that the first n+1 symbols of the configuration can be any symbol from the set E. 
* Sb = E^(n+1) (E** ∪ **ε)^((2^(n^k)) - n-2) E(-_ ) E*. Here ^ this symbol I used for both exponentiation regular operation and normal mathematical exponentiation operation. E^(n+1) means any symbols from the set E for the first **n+1 **positions. Then the second part implies that for the remaining (**2^(n^k))-n-2** positions can be either an empty string symbol or the symbol from the set E. Then the remaining one symbol E(- _ ) can be any symbol other than the blank symbol and the remaining symbol can be any symbol from the set E. 
* Why do we need E* at the end? Here, notice that the second part doesn’t cover all the remaining (2^(n^k)) -n-2  symbols; some of them can be empty string symbols. This is the reason we add E* at the end. Why should we do that? Because the E(-_) symbol won’t always be the last symbol. It can come in any of the (2(n^k)) - 1 positions. For this reason only we added empty string symbol in the second part and E* at the end.
* S#:- This will generate all the configurations that fails to have # symbol at the (2^(n^k)) +1 position. S# = E^(2^(n^k)) E(- #) eE*.

Construction of R(bad-end):



* R(bad-end):- will generate all the configurations that fail to have q(reject) in its end configuration. R(bad-end) = E*(-q(reject)).

Construction of R(bad-window):



* R(bad-window):- will generate all the configurations that fail to legally follow from the previous configuration. Here legally means the tape symbols of the current configuration should follow the transition table rules of the Turing machine M to go to the next configuration. 
* Each configuration is of exactly 2^(n^k) length and it will have # symbol in the next position. So for each symbol of the first configuration the corresponding symbol in the next configuration will be exactly (2^(n^k)) - 2 symbols apart. We can cover all the illegal moves in the whole computation history using the following regular expression. 
* Note that here the total number of symbols are (2^(n^k))+1 and we subtract the first three symbols namely ‘abc’ that we selected from the string to get the remaining length. We are assuming that all the configuration will be in a single row separated by # symbol. In that way this way approach will be meaningful.
* R(bad-window) = Union of all all the bad(abc, def) { E* abc E^((2^(n^k)) - 2) def E* }. Here this regular expression will generate all configurations where the three symbols **def** does not follow from the three symbols **abc** of the previous configuration. We will generate this unioned regular expression for all such bad(abc, def) for the Turing machine M. 
* There will be only a finite number of such pairs for the set E. Remember that the set E doesn’t depend on the length of the input w for the Turing machine M. The set E is a part of the definition of the Turing machine M.

Space Complexity:



* R(bad-start) is linearly dependent on the input length w so it will only take polynomial time to construct them. R(bad-end) and R(bad-window) are  only depending on the set E which does not depend on the input length. So we can generate both of them in polynomial time with the help of exponentiation operation. So the whole process only takes polynomial time which implies that EQ_GREX is EXPSPACE-hard.

**Summary: **EQ_GREX is in EXPSPACE and in EXPSPACE-hard so it is EXPSPACE-complete.


### Relativization



* Relativization shows a strong possibility that we can’t solve the P vs NP problem using the proof by diagonalization method.
* We can give some information to the Turing machine for free. Based on the information we give to the Turing machine it can solve some problems more easily than before. For example if we give some Turing machine M one black box kind of machine which can decide the satisfiability problem in just one step. Then we can use the Turing machine M to solve any problem in NP class by just using the polynomial time. Here we say that the Turing machine M solves those NP class problems relative to the satisfiability problem. Hence the name Relativization.
* We call this block box machine which solves the SAT problem in just one step, the Oracle. The Turing machine M that uses that oracle for the language SAT is called the Oracle Turing machine M_SAT. The term Oracle can be used for any kind of language for membership checking, not just for the SAT. 
* P_A is the class of languages that are decided by M_A in polynomial time. NP_A is the class of languages that are decided by N_A in non deterministic polynomial time where the N_A is the non deterministic Turing machine N that uses the oracle A.
* Note that if we had such an oracle Turing machine M_SAT for SAT then NP and coNP would become subsets of P_SAT. coNP is here because M_SAT is deterministic and closed under complementation.


#### COMP_MIN_FORMULA:



* Another example can be a complement of MIN_FORMULA. The MIN_FORMULA language contains all the boolean formulas which can’t be written in a shorter equivalent form. COMP_MIN_FORMULA contains all the languages that have a shorter equivalent boolean formula. We don’t know COMP_MIN_FORMULA is in NP but we know that it is in NP_SAT.
* Actually checking whether two boolean formulas are not equivalent is an NP problem because if input for which two formulas disagree is given as a certificate then we can verify it in polynomial time. Then checking for the equivalent boolean formula is a Co-NP problem which doesn’t have any polynomial time verification algorithm in normal cases. Because to check whether two formulas are equivalent we have to check whether it agrees for all the possible inputs. 
* We can use P_SAT to build a Turing machine M  that will check if two formulas are not equivalent. Since P_SAT is deterministic we can complement the output of M to construct COMP_M which is the equivalent boolean formula problem. 
* Then we can non deterministically guess the shorter boolean formula B2 with the same variables that might be equivalent to the longer formula B1. We can use COMP_M to test whether B1 and B2 are equivalent and accept if it is. 


#### Limits of the diagonalization method:



* First of all, the diagonalization method takes one Turing machine X and simulates some other machine M and acts differently than that other machine M. For example we have proved the halting problem using the diagonalization method and proved that there exists no turing machine that can decide the halting problem. If we give the same oracle for both the simulating Turing machine and the other Turing machine that is being simulated then also diagonalization still works in the same way.
* For example take a halting problem, Assume that there is an oracle HALT that can say whether some Turing machine M halts or not. Since we gave the same oracle for both Turing machine X and the other machine M, the simulator can query the HALT oracle for the M and still do the opposite of what oracle says. Now if we give the definition of the X to itself as an input then it will do the opposite of wherever the oracle says. So still this creates the contradiction.

**There exists oracle B such that P_B = NP_B:**



* Assume that we used a diagonalization proof method to prove that NP and P are not equal. Then we can give the same oracle B for both NP and P. Then it is straightforward that both P_B and NP_B are equal. 
* For example, to solve the TQBF problem we can use some oracle TQBF which can be used for the membership of the TQBF problem. Then NP_TQBF ⊆ NPSPACE  ⊆ PSPACE  ⊆ P_TQBF.
* First containment is true because we can use oracle TQBF to achieve it. We can convert that ORACLE machine to a normal NPSPACE machine by removing oracle from it and using usual computation. We can do this in non deterministic polynomial space because TQBF is a PSPACE problem. So when we remove the oracle for TQBF we will non deterministic guess the satisfying assignment and check whether it satisfies the TQBF formula. This way each of the non deterministic branches will take only the polynomial space. 
* Second containment is true because of Savitch’s theorem. 
* Third containment is true because we can solve the TQBF problem using polynomial time when we use the oracle TQBF. Since TQBF is PSPACE-complete every problem in PSPACE can also be solved in polynomial time.

**There exists oracle A such that P_A != NP_A:**



* Similarly If P and NP are shown to be equal using the diagonalization method then we can show that there exists oracle A such that P_A and NP_A are different. Though showing that P_A and NP_A are different will need some extra work from us, this is the core idea. 

L_A = { w | x belongs to A and |x| = |w|}



* Here A is any oracle and L_A is language such that if w belongs to L_A there there exists string of same length in A. Now we can design A such that to decide whether the string of length 1^n belongs to L_A can be decided only by a non deterministic polynomial time Turing machine but not by any of the deterministic polynomial time Turing machines.
* Assume that the polynomial time Turing machine M(i) runs in n^i time. Then choose the n values such that 2^n is larger than n^i. What does this mean there are more than n^i possible strings of length n. 
* We design A such that whatever M(i) queries for if we already responded then we respond with the same answer. If we didn’t respond for that string then we will answer ‘NO’ saying that string is not in L_A.
* Now If we ask M(i) whether 1^n belongs to L_A then M(i) won’t be able to check all possible strings using the oracle A. This is because there are more strings of length n than what we can check in the polynomial time n^i. Suppose if M(i) accepts 1^n that means 1^n is in L_A. But A already rejected all the string M(i) has queried for. Now A will reject all the remaining strings making sure that M(i) was wrong on its decision. If M(i) rejects 1^n A will find the string that is not queried by M(i) and will define that string to be L_A again making sure that M(i) is wrong.
* This way we prove that there exists no polynomial time Oracle Turing machine that can decide L_A. But there exists a non deterministic polynomial time Oracle Turing machine that can decide L_A. So P_A is not equal to NP_A.


### Circuit Complexity 



* Why do we need this? Researchers believe that the theoretical models for digital circuits which we call boolean circuits are better than the Turing model to solve the P vs NP problem.
* A Boolean circuit is a collection of gates connected by wires and input wires to pass the input values. Gates include three fundamental gates AND, OR and NOT. Wires can carry the bit info 1 or 0 through low or high voltage and gates can process that info to give a particular output.
* For example AND will output if both of its inputs are 1 and OR will output 1 if any one of its inputs is 1. NOT gate will output 0 for input 1 and vice versa.
* **Boolean function:** f(a1,a2,...,a(n)) = (b1,b2,...b(m)) is the function which has n input wires and m output gates. When inputs x1 through x(n) is assigned a1 through a(n) then the boolean function f will compute output the values b1 through b(n).
* **Membership of the language:** We can encode the input and output of any language in {0,1} to use circuits to decide the membership of that language. The boolean function will output b1 = 1 for input w=a1 a2 … a(n) only when w belongs to the language. In this case output is single gate.
* **Circuit Family:** A single circuit can handle only a fixed length of input. So we use a collection of circuits to decide the membership of a particular language. Circuit family is the infinite collection of circuits {C0, C1, C2, C3, …} where the circuit Cn will decide for the input length of n. Cn(w) = 1 only when w belongs to the language A where n is the length of w.
* **Size complexity: **the size complexity of a circuit is a number of gates in the circuit. The size complexity of the circuit family is the function f(n) where the circuit Cn will have the size complexity of f(n).
* **Depth Complexity:** the depth complexity of the circuit is the length of the longest path from the input to some output gate. The depth complexity of the circuit family is defined similarly to size complexity.
* **Equivalent circuits:** Two circuits are equivalent when both of them have the same input length and give the same output for the same input.
* **Minimal circuit:** The minimal circuit is such that there exists no smaller circuit which is equivalent to it. The circuit family is minimal when all the circuits in the family are minimal. 
* Circuit complexity of Language: is the size complexity of the minimal circuit family for that language. Circuit depth complexity is the depth complexity of the depth minimal circuit family for the language.


#### Theorem: Circuit Complexity vs Time complexity:

Let t be the function where t(n) >= n. If some language A belongs to TIME(t(n)) then it has the circuit complexity of O( (t(n))^2 ).

Tableau:



* We have already seen how we can represent the computation history of some Turing machine using the tableau format. In the tableau i’th row corresponds to the configuration of a machine in the i’th step. First row corresponds to the start configuration of a machine. Last row corresponds to the accepting configuration of a machine. We have seen this tableau in the Cook-Levin theorem.
* But there are some differences here: we represent the current state and tape symbol on the current head position as a single tape symbol. For example we have previously represented the tape head in the second position and current state q as five cells in the table like 1q011. Now we will represent it as four symbols in the tape 1[q0]11. Here whatever you see in the square brackets represents a single composite character. In the composite character q represents the state and 0 represents the tape symbol.
* If some Turing machine M takes t(n) time to decide some language then its configuration will be of length t(n) and it will run for at most t(n) time so there will be t(n) configuration before machine M halts. To represent all these t(n) number configurations we will need a tableau of dimension t(n) x t(n). Remember that we are ignoring the asymptotic constant here for simplicity.
* Since we modified the Turing machine to use composite characters there will be a total of k tape symbols from the set F and (Q x F). Here F represents tape symbols and Q represents the state symbols. Each cell in the tableau can have anyone these k symbols.

Circuit:



* We will create a circuit family where the circuit Cn will process the input w of length n. 
* We modify the Turing machine to encode its input in the binary format and once the machine accepts it will move its tape head to the leftmost position and change that symbol to the blank symbol( _ ). This way we can process the inputs as ones and zeros. The output can be seen at the single place, namely the first cell of the last row in the tableau.
* We will make sure that once the Turing machine goes to accept state then it will never change from that configuration.
* We will create a circuit for each input length n. The whole circuit family will decide the language of M.

Circuit for tableau:



* So we have seen that we are going to represent the computation history as the tableau. We are going to convert that tableau into a Boolean circuit Cn which will simulate the computation history of M on input w of length n. This is the core idea behind the proof.
* We will represent each row of the tableau with one row of circuit. So our final boolean circuit will have t(n) rows. Each row will get the input from the previous row and pass the output to the next row. First and last layer are exceptions. Note that here each row corresponds to each configuration of the computation history.

Light for each cell:



* To understand this idea clearly we will represent each cell in the tableau with one light. In practice we don’t need these lights, we will just connect input and output wires according to the tableau to get the output at the final layer of the circuit.
* If cell(i,j) contains the symbol the s then the  light(i, j, s) will be on. In this way we are trying to represent the tape symbol in the j’th position of the i’th configuration with lights.
* Remember that we had a total of k symbols, so there will be k lights for each cell of the tableau. There will be a total of (k x (t(n))^2) lights in the boolean circuit.

Wiring of the lights:



* This is where everything will come together. We will use wires and gates to connect lights so that they will represent the computation history tableau of M on input w.
* We can decide the content of each cell by looking into the three adjacent cells in the previous row.  Based on those three cells content and transition function of M we can decide the content of the current cell. This same logic we are going to use in the construction of the circuit.
* Suppose that cell(i, j-1) = a, cell(i, j) = b and cell(i, j+1) = c and based on transitions function the cell(i+1, j) =s. Then we can connect the output of light(i, j-1, a), light(i, j, b) and the light(i, j+1, c) to the light(i+1, j, s) using AND gate. Wherever all three of those lights are ON then the light(i +1, j, s) will be ON. This means cell(i+1, j) = s.
* Suppose if there are more than one ways to make cell(i+1, j) = s then we can first connect each such group of three lights to different AND gates. Then we can connect the light(i+1, j, s) to all these AND gates using OR gates. This way if any one of the possibilities is true then the cell(i+1, j) will be filled with the symbol s.
* Why are there multiple ways that the cell(i+1, j) = s? This is because there can be different transition functions that can lead to the same result. These different possible transition functions are represented using OR gates in the circuit.
* Like this we will connect AND and OR gates for each cell(i,j). For the same cell we will have k lights that will represent the k possible symbols that can be filled with. At any moment there will be only one light glow for each cell.
* When there is some accepting computation history for M on w then the light light(t(n), 1, _ ) of the circuit will be ON. This is because we modified M so that when accepting its input it will move the tape head to the leftmost position and change that symbol to blank symbol.

Exceptions:



* The cells in the first column and last column won’t have three adjacent cells in the previous row. But rather there will be only two adjacent cells for them. We will connect those lights accordingly only to those two adjacent cells.
* The first row won’t have any previous to be connected. First row is going to be a input. The light(1, 1, [q(0)1]) will be connected to the input w1. This is because start configuration will always begin with start state q(0) and this light should be ON when w1=1. Then light(1, 1, [q(0)0]) will be connected to the input w1 using NOT gate. Because this light should be ON when w1=0. Like this we will do the input w1 through w(n). 
* Then light(1, n+1, _) … light(1, t(n), _) will be ON by default because all these cells should be blank symbols in the start configuration. All the other lights in the first row are OFF by default.
* light(t(n), 1, [q(accept)_ ]) will be ON when Turning machine M accepts its input w.

Time complexity:



* Each cell of the tableau only needs a constant number of gates that only depends on the definition of the Turing machine M such as the state and tape symbols and transition function. Total number of cells in the tableau are (t(n))^2.
* So the circuit complexity of this circuit family will be O((t(n))^2).


#### CIRCUIT_SAT is NP-Complete

CIRCUIT-SAT = { C | C is a satisfiable circuit}



* Satisfiable circuit is similar to the satisfiable boolean formula. Here we will construct a circuit using  AND, OR and NOT gates. The satisfiable circuit will have input assignment which will make the output 1.
* To show that this language is NP-complete we have to show two things. CIRCUIT_SAT is in NP and it is NP-hard. First one is straightforward: we can check all the 2^n possible inputs non deterministically to decide whether it is satisfiable.
* We can reduce all the languages in NP to the CIRCUIT_SAT problem. If the language A in NP then it will have a polynomial time verifier V. We will convert the verifier to the boolean circuit using the same procedure as above. We can then pass the input &lt;x,c> to the boolean circuit to verify the membership.
* Here c is the certificate that will prove that x belongs to the language A. The verifier will take both these as input and produce the output. 
* For example in the HAM_PATH problem x is the graph and c is the Hamiltonian path of that graph. The verifier V will verify whether graph x is in the HAM_PATH class.


#### 3-SAT is NP-complete



* We have already seen the 3-SAT problem. It is a boolean formula in conjunctive normal form(CNF) with three literals in each clause. We already know that 3-SAT is in NP and also seen the reduction from SAT to 3-SAT. Now we will describe the core idea behind the reduction from CIRCUIT_SAT to 3-SAT. 

Core Idea:



* Previously we have seen how we represent the whole computation history as a boolean circuit. Now we will construct a boolean formula that is equivalent to the boolean circuit.
* The formula will contain one variable for each input and each gate of the circuit. We will replace each AND, OR and NOT with the following boolean formulas to construct a final boolean formula which represents the whole circuit. These formulas are constructed first by writing the boolean formula with implication operation( -> ). Then converting them to their equivalent formulas which uses only AND, OR and NOT operators.
* NOT - (wi ∨ wk) ∧ (~wi ∨ ~wk).
* AND - (wi ∨ wj ∨ ~wk) ∧ (wi ∨ ~wj ∨ ~wk) ∧ (~wi ∨ wj ∨ ~wk) ∧ (~wi ∨ ~wj ∨ wk).
* OR - (wi ∨ wj ∨ ~wk) ∧ (wi ∨ ~wj ∨ wk) ∧ (~wi ∨ wj ∨ wk) ∧ (~wi ∨ ~wj ∨ wk).
* Here wi and wj are two inputs of the gate and wk is the output of the gate. Also note the tilt(~) sign corresponds to a NOT gate here.

How?



* When we find a satisfying assignment to the boolean formula we find the satisfying input and output for each gate in the circuit directly. Vice versa is also true.
* Since each gate in the circuit is replaced by a constant length boolean formula this whole construct will only take polynomial time.

