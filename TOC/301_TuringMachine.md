
## Computability Theory(Turing Machine)

### Turing machine (TM) 

The main thing that differentiates TM with FSM and PDA is it has infinite tape where it can read or write in arbitrary positions. Both multi tape TM and non deterministic TM are equivalent in power with deterministic TM. The language is Turing Decidable if it either accepts or rejects all input strings. If it loops infinitely for some input then that language is Turing recognisable language. TM either accepts or rejects or rejects by looping.  A language is T-recognisable if and only if some single tape TM recognises it.

A Turing machine is a 7-tuple, (Q, Σ, Γ, δ, q0, q(accept), q(reject)), where Q, Σ, Γare all finite sets and 

1. Q is the set of states, 

2. Σ is the input alphabet not containing the blank symbol ␣, 

3. Γ is the tape alphabet, where ␣ ∈ Γ and Σ ⊆ Γ, 

4. δ: Q×Γ−→Q×Γ×{L,R}is the transition function,

5. q0 ∈ Q is the start state, 

6. q(accept) ∈ Q is the accept state, and 

7. q(reject) ∈ Q is the reject state, where q(reject) != q(accept).


### Equivalent machines 



*  Multitape Turing machine which used multiple tapes. Non deterministic Turing machines which will have more than one transition for the same configuration c. Configuration means TM M’s state, tape symbols and head position. 
* Enumerators which will have a kind of printer attached to it. Enumerator will print all the strings in the language using a printer.


### Multitape TM M 



* Same as TM but contains one input tape and multiple addition tapes which are empty at the beginning. A language is T-recognisable if and only if some Multitape TM recognises it. Multitape TM can read all the tapes and move all the heads at the same time. There will be a single transition that corresponds to a combination of symbols on all the tapes. 
* So we can store all this content in a single tape separated by hashes. We can move the single head of the single tape TM according to the transition function of the multitape TM. We remember the head position on each tape by putting dots on single tape corresponding to the head positions.


### Non deterministic TM (NTM N) 



* A non deterministic machine will kind of guess the correct answer. For example assume we want to check whether some boolean formula B has a satisfying assignment or not. Also assume that it has boolean variables x and y. In the deterministic Turing machine(DTM) we will check each possible value for each variable and substitute them to formula B one by one to find the result. We will first check for x=0 and y=0 then we will check for x=1 and y=0 and and continue. There will be 2^n possible assignments for the boolean formula with n variables. So this approach will take exponential time of O(2^n). Don’t worry about this big O notation, it is a symbol for the upper limit of time used by TM.
* When we use the non determinism we don’t have to check for each value. NTM will guess the correct value for x non deterministically. So when NTM directly guesses values for x and y it will take only polynomial time to find the answer because we can directly substitute the values to the boolean formula.
* The other way to think about this non deterministic guess is that the NTM will check all possible values for each variable in the different non deterministic branches. Here by non deterministic branch I mean assigning x=0 will be one non deterministic branch and assigning x=1 will become another non deterministic branch. The NTM will accept its input when any one of these non deterministic branches accept. So when we calculate time taken by NTM, We will consider any one of these accepting non deterministic branches which took the longest time.
* One more way of thinking about it is that rejecting non deterministic branches does not guarantee that the given input w is not a member of a language. It just means that it doesn’t know whether that input w is in the language or not. So the non-deterministic branch rejection is not the same as an idea of rejecting in the deterministic Turing machine.
* A language is T-recognisable if and only if some NTM recognises it. So it is also equivalent to single tape TM S. We can simulate this NTM N in some TM S by storing all of its computation branches in a same tape separated by #. Then in the case of multitape TM there was only a single state. But in NTM M there will be a state that corresponds to each branch. We will store those states also in a tape. Whenever a new branch is created then the TM S can copy the current configuration into multiple copies. And to avoid being in a single infinite looping branch TM S can simulate one step in all the currently active branches before going to the next step. This way when any one branch accepts then accept the input.

**Why Flipping the output of NTM M won’t give the complement machineNTM M1?**



* If we try to simulate the NTM M1 and accept when all of the non deterministic branches reject then it is not a valid NTM. Valid NTM should accept only when any one of the branches accept.
* **Example 1: **Assume that some NTM M accepts in one branch and rejects in another branch for input w. When we negate each branch output of that NTM M to create a machine NTM M1. Then now M1 should reject w. But since we negated the output of each branch M1 will also accept in one branch and reject in another branch for the same input w. So this logic doesn’t work. 
* The core idea is that when we negate the output of NTM M, then each branch output is negated and later the final result is computed. We can’t just negate the final result itself based on the definition of a non deterministic machine.
* When we convert NTM to DTM(deterministic TM) it will take exponential time. This is because there will be an exponential number of non-deterministic branches in the NTM. So if we try to keep track of whether each non deterministic branch rejects its input or not then it will need an exponential space to store those values. This also means we will need exponential time to write all these exponential number results on the tape. That’s why this logic does not satisfy as a valid non deterministic machine.

Two key points:



* **Point-1:** The NTM does not allow just flipping the answer because flipping the answer will flip the answer in all of the non deterministic branches. This will create conflicting non deterministic branches(similar to example 1 we discussed) because the core idea behind the NTM is that “NTM will accept at least one of the non deterministic branches accepts”
* **Point-2: ** Let’s assume that we have NTM M1. We may try to create the complement of M1 after it has predicted the output. But it doesn’t work quite well. Let’s call the complement of M1 as M2. As soon as we try to use the M1 inside the M2, the M2 itself becomes non deterministic. So now you can’t internally just switch the final output of the M1 inside the M2. No longer we consider the M1 as a separate machine. 
* You can think of it like this: there is no separate non deterministic tree for M1 because now it becomes the whole non deterministic tree of the M2. That’s the reason you can’t just flip the output of M1 inside the M2. If you try to do that, then all you are doing is flipping the output of one of the non deterministic branches of the M2.


### Enumerator TM E



* Enumerator prints out all the strings in the T-recognisable language. It is a deterministic TM E which has a printer and blank tape without any input. It prints periodically all accepting strings on the printer. Here the language of a machine is a set of strings it prints out. It is a generator not a recogniser. 
* To create TM M, M can simulate E and check whether printed string x=w? If yes then accept w, otherwise continue simulation.
* In reverse direction TM E can simulate TM M to check whether it accepts string w and then prints that in a printer. To avoid infinite looping on a single string TM E for each i=1,2,3.. can check an i number of strings for an i number of steps. This way at each time we are increasing the number of strings and also the number of steps(current position of the input symbol).


### Church-Turing Thesis (Algorithm) 



*  The notation of the algorithm is clearly defined by the Church-Turing thesis. Church using lambda calculus and Turing using TM. Instead of just TM we may use any reasonable system to define algorithms. For example lambda calculus, random access machine and any of your favourite programming languages.


### Hilbert’s 10’th problem


* Give an algorithm for deciding diophantine equations. Polynomial equations which have an integer solution. After Church Turing this problem was proven to be undecidable. But it is Turing recognisable because we can try all possible input combinations.