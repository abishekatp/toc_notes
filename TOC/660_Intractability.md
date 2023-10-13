
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


### Co-NP** **⊆IP(#SAT is in IP)

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
* So if you have a polynomial with n variable then it can have exponential number of coefficients with respect to n. That’s the reason at each phase of the protocol the Verifier asks a polynomial with a single variable. When the polynomial with a single variable has power d, It can have at most d roots and d+1 coefficients.

**The error probability**:



* At each phase the error probability is (1/n^2). There are a total of m phases, where m is the total number of boolean variables in the boolean formula B. The value of m will be at most n where the n is the length of the boolean formula B. So the error probability = (m)(1/ n^2) = (n)(1/ n^2) = 1/n. 


### PSPACE ⊆ IP(TQBF is in IP)

This containment says that every PSPACE language A will have a probabilistic polynomial time verifier. We will prove that by showing that PSPACE-complete language TQBF(True Quantified Boolean Formula) is in the class IP. This proof is going to be similar to the previous containment that Co-NP is a subset of IP. But here we use some additional logic to reduce the degree of the polynomial.

