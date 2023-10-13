## Automata Theory(DFA, NFA, Regular Lnaguages):

Some useful proof methods:

* Proof by construction(constructing actual machines like PDA) constructing DFA to show that union of two Regular languages is also regular.
* Proof by contradiction(assuming something and proving that contradicts) example proving halting problems using A_TM
* Proof by induction (assuming for i’th step and proving for (i+1) step). Example proving sum of first n numbers is n(n+1)/2
* Proof by cases(dissecting the proof into several cases)

I am giving very brief information about the basic topics like FSM, DFA  and NFA because these are so common topics. You can refer to the book if you want more clear definitions or if you want me to give a more clear explanation on some topic feel free to let me know, I will try to add more content on those topics.

### FSM 

Finite state machine is the most basic mathematical model for computation. This will read the sequence of input symbols and based on the description of the machine it will produce an output that corresponds to that particular input.

Finite state machines can be represented either by a state diagram or by a 5-tuple as given below.

(Finite set of states, Start state, accept state, finite set of  input symbols, transition functions)

Remember that FSM can only read the inputs that also only once.

States- states are like memory nodes. It can help remembering one piece of information based on how we use them. States are represented using a circle in a state diagram.

E.g s1, s2, s3, ….

Input symbol- input symbols is the way of interacting with FSM. FSM will read the input and based on the input symbol it will change its current state of the machine and some FSM will optionally output some output symbol.

E.g a,b,c… 1,2,3,… &,@,(,… any symbol you can think of 

Transition function- is a way of defining the functionality of the FSM. It is like telling the route to some destination to some new person in the city. We will define rules(or tell directions) of what to do on reading a particular input symbol. We will define whether we should change to some new state, output a symbol(optional in some cases). Transition functions are represented using arrows in the state diagram.

E.g (s1, a-> s2) this means if FSM is in s1 and it reads input a then it should move to state s2. We can add an output symbol on RHS if we need.

Start state- start state is the initial state of the FSM before reading any input symbol.

There are two ways of producing output in FSM,

1. First one is as we mentioned previously, The FSM on reading each input symbol can produce an output symbol. E,g (s1, a-> s2, b)
2. The most common is using an accept state to indicate the output. In this approach FSM does not output any symbols but rather go to an special state called accepting state when the input string is in the desired form.

### DFA

 Deterministic Finite automata is a finite state machine(FSM). At each step this machine will have deterministic behaviour means it will have only one possible way for moving forward. This means for each state and input symbol pair, the machine will have exactly one next state. This means we cannot move to more than one next state from a current state on reading any input symbol.

Analogy- Assume that you are in a new city and you want to go to some place. Then DFA is like one person giving you the exact route to your destination. You can just follow that route to reach the destination.

### NFA 

 Non Deterministic Finite Automata is the same as DFA, but it can decide which next state to go nondeterministically. This means for each state and input pair there will be a set of next states. So the machine will non deterministically choose one state and move forward with it. Note that NFA allows us to move from one state to another state without any input symbol also(meaning empty string symbol). In NFA out of all branches if any one of the branches accept the input then the machine will accept the input.

Analog- if you take the same analogy as DFA. NFA is like giving you a map of the city and asking you to navigate to your destination using that map. But the trick is that the map does not guarantee that you will reach your destination. It will give you all possible routes and some of the routes may lead to your destinations or none of them may lead to your destination. So you have to try all the possible routes to reach your destination.

### GNFA

It is NFA such that it can contain regular expressions as their labels, not just a single symbol. Usually NFA can read one input symbol at a time, so each label will be a single symbol. But in GNFA you can have labels such as a*, (ab)*, (aa U bb),... these are all called regular expressions. For example here a* means that the machine can read zero or any number of a’s to go to the next state.

* We will add a new start and accept state to convert NFA to GNFA such that there are no incoming transitions in the start state and there are no outgoing transitions on the accept state and use that to convert NFA to regular expression. We will also have some more assumptions before doing this.
* We are adding this new start and accepting state in NFA to get GNFA because it will help convert NFA to the regular expression. When we simplify the GNFA at each step of the process we will remove one node n1 and add more complicated regular expressions as the label to some edges to adjust the removal of that node n1. This way at the end of this process we will only have two newly added start and end nodes and edge in between them will have an equivalent regular expression for NFA.


### NFA to DFA 

Every NFA has an equivalent DFA. We can convert NFA to DFA by following a particular procedure. 

We will create a state in the DFA for each possible subset of states in the NFA. These new states will help us keep track of multiple possible transitions of NFA in the DFA. So when a state moves to a set of states in NFA we will represent a set of states using that single state in DFA. For each input symbol we will go to a set of states which can be reached from a current set of states. Note that we also include a state to a particular set of states when they are reachable on empty string input.


### Regular operations and expressions 

union,  concatenation and star operation are regular operations. These are used to form a regular expression. Regular expressions represent a regular language which is recognised by DFA or NFA. We will prove this by converting DFA to regular expression and vice versa. We will use NFA or GNFA to prove this.


### Regular language



*  a set of strings recognised or accepted by DFA or NFA is a language L. This language L is also called regular language R. If a language is recognised by DFA or NFA then that language is Regular vice versa is also true. 
* Firstly We have to prove this by constructing NFA from a regular expression. Second we have to convert the DFA to the GNFA then by ripping off one state at a time(representing  the ripped off part by one or more transitions with a regular expression as its label.) to get a regular expression at the end. At the end we will have just two states start and accept and one transition between these two states which has the final regular expression as a label.


### Closure under union, concatenation, intersection, complementation and star 

 We can build NFA which can represent these operations, proving that regular expressions are closed under these operations. This will help us prove the equivalence between regular expressions and DFA. For all these things we can build NFA N from the two given NFAs(one NFA in case of star). For example, we can construct new NFA N from NFA N1 and MFA N2 that will accept the input w only when both N1 and N2 accept the input to prove for intersection.


### Pumping lemma for regular language



* We will use the pumping lemma to prove that some languages are not recognised by the FSA; These languages are not regular languages. Strings from these languages cannot be pumped by this particular pumping lemma. This pumping lemma states three rules: those are as follows.

For any regular language L, there exists an integer P, such that for all inputs w in the language L

    |w|>=P

We can break w into three strings, w=xyz such that.



1. lxyl &lt; P
2. lyl > 1
3. for all k>= 0: the string x(y^k)z is also in the same language L.

If any one of these conditions fails then the language is not Regular language.



* When we split the string w into three parts x and y should be shorter than P and length of y should be greater than 1. 
* Then even if we repeat the y any number of times the string should stay in the language. Here if k>1 means we call it pumping up and k=0 means we call it pumping down. 


### **Summary**: 



* Basically DFA and NFA both are FSMs which are equivalent in power. Every NFA can be converted to DFA. Also DFA and Regular languages are equivalent, only differing in the way that the DFA or NFA accepts the string of a particular language and the Regular Language generates the string of a particular language.
* To prove that Regular languages are equivalent to DFA we will use NFA because NFA and DFA are equivalent models. We can also use NFA to prove the closure property of the Regular language(RL) under all regular operations(union, concatenation and start). 
* The above Pumping lemma helps us to prove that some languages cannot be recognized by DFA. So this proves that there are some languages that do not come under the class of Regular languages. 
* Next we will see one of those kinds of languages called Context free languages(CFL). Context Free languages are generated by the Context Free Grammars(CFG). Regular language has an equivalent model called DF. Just like that CFG has an equivalent model called Push Down Automata(PDA) which can accept the strings in a particular context-free language.

