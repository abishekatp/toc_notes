
## Computability Theory(Reducibility)


### Reducibility 


* In complexity theory if we can reduce A to B means A will not have more complexity than B that doesn’t mean A will be equally complexity to B. Because A may be less complex than B. in decidability if we can reduce from A to B means we can use the solution of B to construct the solution of A. Here B is decidable means A is also decidable. But this doesn’t mean if B is undecidable then A is also undecidable. 
* But When A is undecidable then B must also be undecidable. If A reduces to B means,

B is easy —> A is easy.

A is hard —> B is hard. Hard here means anything like undecidable, unrecognisable…


### Reduction of A_TM to HALT_TM 

 assume there is some TM R which decides the halting problem. Then we can construct TM S that will decide A_TM using R. It will reject if TM R says “M on input w never halts”, if R says “M will halt” then simulate M on input w to decide A_TM.


### E_TM is undecidable 

 if some TM R decides E_TM then we can use that to solve A_TM as follows. Here we create some TM M1 which will simulate M on input x only when x=w. This way if M1 is empty then M rejects w. Note that to create M1 we can just add some new states and transition functions to M. Also remember that we are creating M1 just to feed it as input to R. So we don’t think about whether M halts on w because that’s what R is saying it can decide.

TM S = “on input &lt;M,w>:

1)Create TM M1=“on input x:

          1)If x!=w then reject 

          2)Else simulate M on input x. Output whatever N outputs.

2)Simulate G on input &lt;M1,w>

3)if M is empty then reject otherwise accept.


### Mapping Reducibility 

Computable function - f is a computable function if some TM F on input w halts with f(w) on the tape.

 A is mapping reducible to B if there is some computable function f such that w belongs to A if and only if f(w) belongs to B. Then we can use the solution to B to check whether w belongs to A by checking whether f(w) belongs to B. Here note that we can’t use the solution of A to solve B because function f only converts w to f(w). To do the reverse we may need f^-1(w). Then only we can get w for every f(w) to use A to find the solution of B. But note that inverse function is not always possible.


### A_TM is mapping reducible to the complement of E_TM 

The computable function is f(&lt;M,w>)=&lt;M1>. Here complement of E_TM would accept if language is not empty. Here we choose this complement of E_TM because A_TM should accept w without doing anything if E_TM accepts f(w) according to the definition of mapping reducibility. That’s why mapping reducibility is not the most general form of reducibility. More general form of reducibility is Turing reducibility which uses an Oracle machine.

-> A is mapping reducible B and A is undecidable means then B is undecidable.

-> if A is mapping reducible to B means complement of A is mapping reducible to complement of B. Remember that f maps elements in A to elements in B and elements not in A to the elements not in B.


### Diff between general and mapping reducibility 

->note that A is reducible to complement of A. But A may not be mapping reducible to complement of A.

-> if A is mapping reducible to B then it’s sure that if B is T-recognisable then so is A. But if A is generally reducible to B then it is not always true. Because A_TM is generally reducible to complement of A_TM, but we know that since A_TM is not decider but only T-recognisable, complement of A_TM must not be T-recognisable. This is because when we complement recognizable languages we won't know whether the machine rejects by looping.

-> general reducibility is useful in proving undecidability of a language and mapping reducibility is useful in proving un-recognizability of a language.


### E_TM is T-unrecognisable 

 A complement of A_TM is mapping reducible to E_TM. we will have a mapping function same as mapping reducible of A_TM to complete of E_TM. Function f will construct M1 from &lt;M,w> where M is TM that recognises A_TM.

TM M1 = “on input &lt;x>:



1. if x!=w then reject 
2. Else run M on w
3. Accept if M accepts”

If M accepts w means the complement of A_TM will reject w that directly maps to E_TM will reject M1 because M1 is not empty.


### EQ_TM and complement of EQ_TM both are T-unrecognisable 

 mapping functions f will construct M1 where 

M1=“on input x



1. ignore input x
2. Simulate M on w”

Here note that if M accepts w then M1 will always accept all the inputs. If M rejects w then M1 will always reject regardless of its input x.

1)Now we can simulate EQ_TM on input &lt;M1,M(reject)> if these two are equal means M does not accept w. So if M accepts w that means both complement of A_TM and EQ_TM will reject.

2) Similarly we can use the complement of EQ_TM to check &lt;M1,M(accept). If M accepts w then both complement of A_TM and complement of EQ_TM both will reject their respective inputs.


### Computation history method 

 It is used in reducing methods. First, Computation history means the sequence of configurations C(i) of a machine. Each configuration contains the current state of the machine, content on tape and position of machine head on a tape. We can reduce the particular problem A’s computation history to another problem B such that if problem B is solved then that solution will directly lead to the accepting computation history of problem A.

Example configuration aaa(q3)bbbba here current state is q3 and head position is 4th position on a tape. We can write the computation history as a string C1#C2#…#Cn


### Accepting computation history

 is a sequence of configurations where the first configuration is the starting configuration of a machine. Each configuration legally follows from the previous configuration based on the transition functions. Any one of the configurations has an accept state in it. E.g C1#C2#…#C(accept)


### Diophantine problem 

D = { &lt;p> | where p is a polynomial p(c1,x2,…,xn)=0 has an integer solution}. We can reduce the problem A_TM to this problem so it is undecidable. This original proof is very long to go through. So we will look into a toy problem called post correspondence problem(PCP) which has the same idea in a simple manner. Here we convert A_TM problem to some polynomial equation where the solution to this equation will have some values for variables. One of the variables is going to be a particular number which corresponds to accepting computation history in some encoded form; other variables are going to help us to decode that value.


### Post correspondence problem(PCP) is undecidable 

 We have a bunch of dominos where t is in the numerator and b is in the denominator. { [t1, b1], [t2, b2],…, [tn, bn] }. Here t and b can be any strings. Problem is to arrange these dominos such that the final numerator and denominator are equal which is called match. We can reduce the problem of finding the accepted computation history of the A_TM problem to finding the match of a PCP problem. If there is some TM R that can decide whether a collection of dominoes has a match then we can use that R to build TM S.

TM S=“on input &lt;M,w>:



1. Create an instance of PCP problem P(M,w) where the match in this collection of dominos will correspond to an accepting computation history of M on input w.
2. Then use R to decide whether this collection of dominos has a match.
3. If yes, accept, no then reject.”

Building P(M,w):



1. To accommodate start configuration we will have domino [t, b] = [#    , #w1w2…wn#]. This is going to be the first domino in the collection. We will always use this first when we are finding a match. This restriction can be easily removed.
2. To accommodate del(q,a)=(r,c,R) we will have [t, b] = [qa, cr]. t=qa corresponds to current state q and reading input a. b=cr corresponds to next state r and rewriting a to c and moving the tape head to the right side of c.
3. To accommodate del(q,a)=(r,c,L) we will have [t, b] = [dqa, rdc]. t=dqa corresponds to current state q and tape head on symbols a and left side of a there is the symbol d. Then b=rdc corresponds to the next state r, rewriting a to c and moving the tape head to the left of the symbol d.
4. To copy all the remaining symbols which are not near the tape head we will have one domino for each tape symbol [t, b]=[a, a].
5. Each time when we add [t,b] we are copying denominator symbols of previous domino to the numerator. But also adding new denominator symbols which will continue to have mis-match. When b contains q(accept) we want to copy all the denominator symbols to the numerator without adding new denominator symbols. For that purpose we have a domino of kind [t,b]=[aq(accept), q(accept)] and [q(accept)a, q(accept)] and [q(accept)##, #]. It will remove all the symbols around q(accept) one step at a time.
6. To add blank symbols at the bottom we will have domino like this [#, _#]. Here the underscore symbol represents a blank symbol.

These dominos will have a match only when there is an accepting computation history on M on input w. PCP is T-recognisable and T-undecidable so the complement of PCP is T-unrecognisable.


### LBA(Linear Bounded Automata) 

It's a TM with single fixed length tape. Note that this Turing machine can’t move its head to the right any more than its input length. But remember that tape length can vary however we want based on the input. For particular input x if tape length is n means the tape head can’t move to the cell n+1. So we can have different tape length for each input x.

->Since the tape length n is fixed for any given input x, it will have a finite number of configurations in a computation history of a LBA. LBA is decidable because when we run this LBA for some particular number of time then according to pigeon hole principle one of the computation history configurations will repeat itself because there are finitely many configurations available. This repetition means loop. Because the same computation history means we have reached the same state, with the same tape symbols with the head in the same place on the tape. So this will again do the same computation which we have done so far. So we can decide to reject this input because it’s going to loop.

Total number of computation histories= qn(g^n)

q=number of states

n= tape length or number of possible places head can be

g^n = number of possible combinations of tapes symbols that can be arranged on a tape of length n.


### E_LBA is undecidable

If there is some TM R that can decide E_LBA then we can use that to decide A_TM using TM S,

S=“on input x:



1. construct TM M1 which will decide whether given input x is an accepting computation history of M on input w. Accept x only if it’s an accepting computation history.
2. Test M1 using R whether it’s empty.
3. If yes means reject because that means M1 does not have any x such that it’s an accepting computation history for M on w.”

Based on the definition of LBA we can’t use tape cells that are more than input length. But there is no restriction on input length. Also remember that length of computation history is always going to be finite.

We know that we can check for an accepting computation history by checking start configuration, verifying that each configuration is legal and the last configuration has an accept state. We don’t need an extra tape cell to check any of these things.


### ALL_CFG is undecidable

Emptiness of CFG is decidable but testing whether CFG accepts all strings is undecidable. We can prove this by reducing A_TM to ALL_PDA using the computation history method. If some TM R decides ALL_PDA then we can build TM S as follows.

TM S=“on input &lt;M,w>;



1. Construct a PDA B(M,w) where this PDA will accept all inputs x and reject input x if x is an accepting computation history of M on input w.
2. Test B(M,w) using TM R to test whether it accepts all inputs.
3. If yes then reject, because this means there is no accepting computation history for M on w. If not then accept.”

Building B(M,w):

This PDA will read an input from the tape and check whether it has a valid starting configuration, each configuration C(i) legally follows from C(i-1) and the last configuration is accepting configuration by pushing them into stack because PDA can’t edit input tape. To make the computation easier we will write the configurations in the even places in a reverse order.

Note- we accept all the rejecting computation histories and reject only the accepting computation history for a reason. Here we use PDAs non determinism to test whether any configuration C(i) illegally follows from previous configuration C(i-1). If any one of the branches finds such a pair then it will accept. Then the whole PDA accepts.

-> But to accept the accepting configuration we have to test that each configuration legally follows from the previous configuration. If we compare C1 and C2 then we have already read C2 so we can’t read it again to compare C2 with C3. Also we are using stack to store C1 value so we can’t use stack for storing C2. If we try to use the non deterministic way then we should accept computation history only when all of its branches accept(means all pairs of configurations are legal) which is not how non determinism works. Because of this same reason we won’t be able to find a reduction from A_TM to E_CFG. Because in the E_CFG case PDA must accept all the accepting computation histories.


### SELF Reference 

Self reproducing seems impossible at first but it’s possible and all living things seem to do that. Assume that q is some computable function which takes any input w and creates a Turing machine which prints w. Here we build the TM SELF in two parts A and B.

Here A needs a description of B to call computable function q. But the description of B needs the output of A to construct the description of A. Why are we not using the description of A directly inside B? Because the description of A itself needs the description of B(which will create a circular definition). So we are building B such that it uses the output A to construct the description of A itself.

It works because A is just a machine which prints the description of another machine which in our case is  B and A will be another independent machine which reads input from a tape and does the operation q(tape content)tape-content. So now we don’t use the description of A inside B because the description of A is not yet complete. That’s why we define B such that it doesn’t directly depend on A. So B is a machine which reads any input &lt;M> from tape and outputs q(&lt;M>)M. So in our case after A ran A will print a description of B on tape. So B will take that as input and will print q(&lt;B>)B=AB=SELF. It generally works on any machine M. This logic will be used in the recursion theorem.

Note:- For an analogy, the English statement below is similar to what we are trying to do.

Write the the following sentence twice first time without quotes

“Write the the following sentence twice first time without quotes”

Here the first line is an action which writes whatever follows it and the second line is just a template.

In TM SELF it is a reverse thing A is just a template and B is actually some action which prints whatever on the tape.


### Recursion theorem

The Recursion theorem says that not only the machine can print the copy of itself, it can also obtain the copy of itself and do some computation using it. For every TM T there exists TM R such that for all input w, R is going to operate on w in the same way as T on input &lt;w,R>.

 To build R with recursion inside it we define a computation function t(&lt;R>,w). So now define this TM R in three parts. Part A will print the encoding (w&lt;BT>). Part B will print (&lt;q(&lt;BT>)BT>, w)=(&lt;ABT>,w)=(&lt;R> ,w)on tape and then T will do the actual computation using this.

So when T gets the encoding (&lt;R>, w) as the input it is going to run R on w(note that at the end this is what R also does since it executes T). Now we see when T executes R on input w it will again go to the recursive call.

 R contains three parts A,B,T. Note that before Executing R on input w T can manipulate w however it wants. When T executes R on manipulated input w, TM A will append &lt;BT> to it. Then TM B will again construct new (&lt;R>,w) and pass on to the TM T. So this way recursion continues.

Note: here TM T will be independent of A and B it will take any input &lt;M,x> and it may do some manipulation with it and execute M on input x.

Example:-

For example we take TM T which has input (&lt;M>,w) will shrink input w by one bit and apply w as input to the M. Then this description will be printed on tape by TM A as w&lt;BT> then TM B will construct (&lt;ABT>,w). Then TM T will take over and it will again shrink the input w by 1 bit and call the TM R on new input w. This way this R will do the same thing again. If we want we can put one condition inside T to run R on input w only when input w length is greater than 0.

This way inside T we will get its own description using TM R.

E.g one practical application can be computer viruses.


### A_TM is undecidable

 This is proof by contradiction using recursion. Suppose that TM H decides A_TM problem. Previously we proved this by passing to the TM G its own description as an input and doing the opposite of what the H says the machine will do. But here instead of explicitly passing input, we will get the machine's own description and do the opposite of what the H says the machine will do.

TM R = “on input w



1. Get own description &lt;R>
2. Run TM H on input &lt;R,w> to determine whether R accepts w.
3. Then do the opposite of what H is saying.”


### Fixed Point Theorem

Assume that there is some computable function f which will transform some input program R to some output program S. Then this theorem says there is always some TM R such that this computable function f will leave R unchanged after transformation. For example below machine R does not change by f.

TM R=“on input w



1. Get own description &lt;R>
2. Compute f(&lt;R>) and call it S
3. execute S on input w”


### MIN_TM is T-unrecognisable

TM M is a minimal machine if there is no machine M1 that recognises the same language as M but has a shorter description than M.

Suppose Enumerator E prints out all the minimal machines, then we can construct TM R to prove that one of the printed machines is not actually the smallest one.

TM R=“on input w
1. Get its own description &lt;R>
2. Run enumerator E until it finds some TM B such that description of &lt;B> is larger than &lt;R>
3. Simulate B on input w”

Why not simulating B inside R implies that the size of R will be larger than B? Simulating B inside means we will have all state and transition function encoding of B inside R right?

The answer is that the TM B is not actually included in the description of the R, but rather R computes B at runtime using the enumerator E. So the description of B will be just a tape content for R rather than its own description. But note that the description of the R will include the description of the enumerator E which is some fixed length.

Now machine R has the same language as B but it is shorter than &lt;B>. So there can’t be such an enumerator E that can recognise all the minimum Turing machines.

Note: there can be T-recognisable infinite subset for a T-unrecognisable infinite set. For example, the complement of A_TM is T-unrecognisable(this accepts w when M doesn’t accept w). We can have an infinite subset of finite automatas of this set where this subset is T-recognisable and it’s even become decidable. TM M is a finite automaton if it never writes on the tape.

But for the MIN_TM problem we can always use the above proof as long as the subset is infinite to prove that the MIN_TM is unrecognisable.


### Godel’s first Incompleteness theorem

In any reasonable formal systems there are true statements which are not provable.

Proof property:



1. Soundness- if A has a proof p then A is true.
2. Checkability- then language {&lt;A,p> l p is the proof of statement A } is decidable. Note that we can only verify that proof of A is p or not using a computer.

Collection of all the provable statements which has proof {A | A has a proof} is T-recognisable because we can check a set of all possible proofs one by one whether that proves the statement A and if yes then accept it.

Similarly we know that there are some &lt;M,w> which belong to the language of the complement of the A_TM. If we can prove for all such pairs &lt;M,w> that it belongs to the complement of the A_TM then the complement of A_TM would be T-recognisable. We know that is not true. So there are some pairs &lt;M,w> (in analogy to true statement) that belong to the complement of A_TM but we won’t be able to prove it.

The true but unprovable statement- “This statement is unprovable”

PI is the statement that &lt;R,w> belongs to the complement of A_TM.

TM R=“on input w:



1. get own description &lt;R> and construct a statement PI
2. For each possible proof p:

                 Test whether p is the proof that the show PI is true. If yes then accept, otherwise continue.”

Theorem:



1. PI has no proof
2. PI is true

Proof:



1. If the PI has a proof then from the definition of TM R stage 2 we know that the PI accepts 0. Then &lt;R,0> does not belong to the complement of A_TM. This means the PI is false. Then the PI cannot have proof.
2. If the PI is false, it means &lt;R,0> does not belong to the language of the complement of the A_TM. which means R accepts 0. That implies that R found proof in stage 2 for statement PI. That implies that the PI is true. Contradicting the assumption.


### Model M, L(M) and Theory of M

The universe over which variables can take value together with assignment of relations to the relational symbol is called a model. Formally the model M is a tuple (U,P1,P2,…,Pk) where U is the universe and P1 through Pk are relations assigned to symbols R1 through Rk.



* Language of a model L(M) is a collection of formulas that use only relations in the model with a correct arity. Those formulas are either true or false. Note that statements can use quantifiers and Boolean operations and relations in the model to create a formula.
* Theory of a model is a collection of true sentences in the language of a model. Eg. Th(N,+) is the Theory of model in which variables can take any value from the natural numbers set and can use only one operation +.

E.g.  ∀x∃y[x+x = y] is true but ∃y∀x[x+x = y] is false because there can’t be such y that fulfil the condition for all x.


### TM M to add Two numbers:

For this we use the special encoding of numbers. In this encoding to find the sum of i numbers we need 2^i special symbols. Then i binary numbers will be written in i rows. You can see that if we read the binary form of the i binary numbers in the vertical order(one bit from each number) we can represent these i bits using one of the 2^i symbols. For example to add any two numbers we use A=00, B=01, C=10 and D=11. to add 1+2

4 = 100

3 = 011

encoded input=CBB

TM M:

states:

S1 means no carry

S2 means carry=1

input and output symbols = {0,1,_,A,B,C,D}

Transition functions: input

(S1,A)->(S1,0,L), (S1,B)->(S1,1,L), (S1,C)->(S1,1,L), (S1,D)->(S2,0,L),

(S2,A)->(S1,0,L), (S2,B)->(S2,0,L), (S2,C)->(S2,0,L), (S2,D)->(S2,1,L).

(S2,_)->(S3,1,L), (S1,_)->(S3,0,L)

if you use this TM to the input CBB you will get the output=111


### Th(N,+) is decidable

Th(N,+) is the Theory of model in which variables can take any value from the natural numbers set and can use only one operation +. So we can build a Turing machine to decide this language(means can say whether the formula is true or false). For this we have to know how we can do the addition of numbers using the Turing machine which we already discussed.

Constructed Formula:  P = Q1x1Q2x2…Q(l)x(l)[S]

Here each Q(i) is a one of the quantifiers(There exists or For all). S is the formula without quantifiers without quantifiers which has variables x1,x2…x(l).



* We create new formulas from P for each i from 0 to l. P(i) contains i free variables from a(1) to a(l) corresponding to x(1) to x(l). Now we construct for all i from 0 to l we construct the Turing machine A(i) to recognize P(i). First we start with P(l). For each i we use A(i+1) to construct A(i). First note that A(l)=S it is just a boolean formula with a + relation. We can easily construct the A(l) using our previous summation logic, union, concatenation and complementation logics.
* Then from l down to 1 we use A(i) to construct A(i-1). First A(l-1) will simulate A(l). for example if P(i+1) = ∃x(i+1)P(i+1), here first i variables are fixed to a(1) to a(i) and A(i) will guess the x(i+1) non deterministically and simulate this input on A(i+1). In this way A(0) will have to non deterministically guess x(1), A(1) will non deterministically guess x(2) and so on. So when we pass empty string input to A(0) it will non deterministically guess all the numbers and if A(0) accepts empty string then given boolean formula P is true.
* Note: if P(i+1) = ∀x(i+1)P(i+1) then we can use its complement form P(i+1) = ~∃x(i+1)~P(i+1) for the construction. Second, how are we going to guess the value of x(i) non deterministically. We are going to do this bit by bit. Each time A(i) reads the input symbol it non deterministically guesses the bit z of  the x(i+1) number and simulates the input symbol on A(i+1).


### Th(N, + , x)  is undecidable

We prove this by reducing the A_TM problem to Th(N, +, x) problem using the computation history method. we give a mapping reduction from the input &lt;M,w> to P(M,w). Then we create a boolean formula ∃xP(M,w) such that this formula will be true only when M accepts w. Here x is just an integer that represents the accepting computation history of M on the input w in some encoded form. This construction of the boolean formula is rather complicated. It extracts the individual symbols of the computation history with + and x operations to check that the start configuration is valid, each configuration legally follows from the previous one and there is an accepting configuration. This theorem has a philosophical importance because it proves that mathematics cannot be mechanised.


### Kurt Godel’s Incompleteness theorem

Some true statements are unprovable. First we have to know some important properties of proofs.



1. The correctness of a proof of a statement can be decided by a machine. {&lt;P,B>| B is a proof that P} is decidable.
2. The system of proof is sound. That means if a statement is provable(has a proof) means it is true.

Theorem 1: The collection of provable statements in Th(N,+,x) is Turing recognisable. Turing machine M can check all possible strings one by one whether that is a proof of a statement. If yes then accept, otherwise reject.

Theorem 2: Some true statements are unprovable. We can prove this by contradiction. If some D decides whether a statement P is true or not, then we can use that to test against both P and ~P and either one of them will become true. So this implies we can decide the Th(M,+,x) which is not true.

Theorem 3: The statement S(unprovable) is unprovable.

TM M=”on any input:



1. Obtain its own description &lt;M> using recursion theorem
2. Construct Turing machine S=~∃c[P(M,0)]. Here P(M,w) will construct some boolean formula from input M and w.
3. Run TM D that decides whether S is true or not.
4. If yes then accept any input.”

Note that if S is provable that means S should be true means M rejects 0. But if D says S is provable then M accepts any input including 0. This contradiction says S is unprovable.


### Turing Reducibility- The Oracle Turing machine

This is a more general form of reducibility than the mapping reducibility. An oracle for a language B is an external device that is capable of reporting whether any string w is a member of B. An Oracle Turing machine is a modified Turing machine which has an additional capability of querying an oracle. For example if we have an oracle for the A_TM then using that we can decide the A_TM problem itself so the Turing machine with an oracle is more powerful than the normal Turing machine. We can also decide the E_TM emptiness testing problem using an oracle of A_TM.

T_A_TM =”on input &lt;M> where M is TM:



1. Construct TM N = “on any input:

                   1.Run M on all possible inputs in parallel

                   2.If M accepts any of these string then accept input

     2. Then check the oracle if &lt;N,0> belongs to A_TM

     3. If yes then reject, if No then accept”

This is because N will accept all the inputs only when M is not empty. So E_TM is decidable relative to A_TM.

**Language A is Turing reducible B if A is decidable relative to B.**        


### Information

We define the quantity of the information contained in the object to be the object’s smallest description or representation. By a description of an object we mean a precise and unambiguous representation of an object such that we can get the original object from that description alone. **So this shortest description of an object is called information contained in the object.** 

Minimal Description: Let x be the binary string, the minimal description of x written as d(x) is the shortest string &lt;M,w> such that M on input w halts with x on its tape. If multiple such w exists we choose the one that is lexicographically first.

Description complexity or Kolmogrov-Chaitin complexity: The description complexity of x is written as K(x)=|d(x)|. 

Theorem-1: ∃c∀x [K(x) &lt;= |x| + c]. This theorem gives an upper bound for the description complexity. It must be some fixed constant c more than the x(independent of x). This is true because we can construct TM M that leaves the input tape as it is. Then |&lt;M>|=c and total length will be just |x|+c. 

Theorem-2: ∃c∀x [K(xx) &lt;= K(x) + c]. Here we can construct TM M that prints x on the tape. So the length of the description of the x is the K(x). Then TM N just simulates the N and prints the output of M two times. Then total description length will be K(x)+|&lt;N>| = K(x)+c.

Theorem-3: ∃c∀x,y [K(xy) &lt;= 2K(x) + K(y) + c]. We have 2K(x) because to separate the description of x from the description of y we store each bit of x two times and terminating with 01. There can be more efficient ways such as just storing the length of the string x at the beginning and doubling the bits of that number. That will have length 2log2(K(x)) + K(x) + K(y) + c.

Optimality of the definition: Consider any computable function p:input->output. The minimal description of x with respect to p is written as dp(s)=x. Then Kp(x) = |dp(x)|.

Theorem-4: ∀x [K(x) &lt;= Kp(x) + c]. For example if you define the computable function p in python then Kp(x)=dpython(s). Then some TM M can just simulate dpython(s) to produce the output x.


### Incompressible strings and Randomness

c-compressible: A string x is c-compressible if K(x)=|x|-c. If x is not c-compressible then the x is incompressible by c. This means when we try to compress x we can’t compress it to the length less than or equal to the |x| - c. if string is incompressible by 1, that means x is incompressible.

This K compressible function is not computable. There is no algorithm that can generally decide that the strings are incompressible.

Theorem-5: Incompressible strings of every length exist. This is because there are 2^n binary strings of length n which is greater than all the possible binary strings of length less than n that is (2^n)-1. So if we assign a string of length n to some shorter string there will be at least one string of length n that will be left out without any such assignment.

Corollary-1: from theorem-5 we can say that if string s is c-compressible that means we can compress it shorter or equal than n-c. so there will be 2^0 + ...+ 2^n-c = (2^n-c+1)-1 compressed descriptions available. so remaining (2^n)-((2^n-c+1)-1) strings are not compressible to the length that is less than or equal to the length n-c. For those remaining strings we must use the description of length greater than n-c.

The property of a string is a computable function f that maps a string to {TRUE,FALSE}. We say that the property holds for almost all the strings if the fraction of strings of the length n on which it is false approaches 0 as n grows large.

Theorem-6: Let f be a computable property that holds for almost all the strings. Then for any b>0, Only finitely many strings that are incompressible by b will fail to have this property.

We list all the strings of length n or less that fail to have the property. Then the string in the i’th position of this list will have i(x)=i in binary form. So the description of that string will be &lt;M,i(x)>.

To prove this we select n such that m=1/(2^b-c-1) fraction of all the strings of length n or less will fail to have this property. For any sufficiently large n this holds because property holds for almost all the strings. Total number of strings of length n or less is t=(2^n+1)-1. 

So i(x)&lt;=t*m&lt;=(2^n-b-c)

Here i(x) is just an integer in binary form. When we take log2() on all the sides we get the actual length of i(x). That will be

|i(x)| &lt;= n-b-c

Then total length of description = c+|i(x)|=n-b. This c is the length of &lt;M>. So this implies that every sufficiently long x that fails to have this property is compressible by b. So only finitely many long strings that fail to have this property are incompressible by b.

Theorem-7: we can find constant b, for every string x, the minimal description d(x) of x is incompressible by b. Note that this is about compressing d(x) itself again to some shorter string.

For example take b=|&lt;M>|+1. Then if d(x) is b compressible then |d(d(x))|=|d(x)|-b. This is also the description of x whose length is at most  |&lt;M>| + |d(d(x))| = |d(x)| - 1. Contradicting the minimality of x so d(x) is incompressible by b.

