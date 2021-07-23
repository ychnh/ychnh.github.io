# 20200722
* Dont giveup keep trying
* look for small patterns, keep digging, 
* try to master the small parts
* Save your energy
* How can you write/think/do Math more effectively without getting tired?


# 20200611 (Fri)

## Working again
* Dont fill your mind with social media
* Value your time and attention

## Hungerford Problem 1.5.19

Suppose $H\leq G, N\trianglelefteq G$, then $([G:H],|N|)=1 \rightarrow N<H$ and $([G:N],|H|)=1) \rightarrow H<N $


* I spent alot of time on this problem, and also learned a number of things.
* How can I improve?
	* I think I need to improve in seeing connections and pathways I can go down
	* Also understanding the problem and related questions at hand

## Prove that every permutation is a product of distjoin cycles

* given a cycle, orbit creates a equi relation btw the elements of {1...N}
	* given a permutation, can you have an orbit? Yes
* The elements of the orbin form a cycle
* The cycle is unique up to permutation
  * a0,a1,a2,a3
  * b0,b1,b2,b3
  * Suppose they are not same according to permutation 
  * this means there is one disjoint cycle in a that is diff froma disjoint cycle in b
  * then any element in the orbit of this cycle should belong in one of the disjoint cycles since it is an element that is changed (non-ident)
  * DISJOINT cycles which share same element are the same if they define the same function

## Cor order of ab is lcm of the order of a and b 
## Cor order of product of cycles is lcm of the orders of the cycles
* Need to extend this to work on disjoint cycles
    * order is the least number where a^m=1. Which means it divides every other number.
* restrict the product of disjoint cycles on their orbit
## Any Sn can be decomposed into transpositions
* $(1234) = (12)(13)(14)$


* When I first went through, I did not really think of the concepts such as orbit.
* How does this kind of idea arise? How does this kind of naming arise?

* can you show that this is unique? No it is not.
* Is the number of transpositions unique? (No you can easily add identity) is even odd transposition well defined?

# 20200615 (Tue)
* Show that every permutation can be classified as odd xor even
* Now a transposition swaps two elments
* Is it possible to have a odd number of swaps from identity be equal to even number of swaps?

* IDEA (A) Is it possible to extend by induction?
  * S2 is very simple

* IDEA (B) How can we use commutativity? transpositions are mostly disjoint, and dijoint cycles commute
  * (ab)(ac) = a-b, b-c, c-a abc
  * $(abc)(ax) = (abcx)$
  * $(bca)(bx) = (bcax)$
  * Ok so every permutation is a unique product of disjoint cycles (up to reordering)
  * Then if we can prove that a cycle-s even odd even is unique then we can show odd/even is unique.
  * Every cycle can be broken into transpositions
  * And it can be either one of these two cases
  * $(abc)(ax)$
  * $(abc)(ab)$ (cb)
  * $(abc)(ac)$ (ab)
  * $(abcd)(ac)$ (ab)(dc)
  * (ab)(dc)(ac) = (ab)(cd)(ca) = (ab)(cda) = (ab)(acd) = (abcd)
  * A transposition applied to a cycle can either increase it by one or split it
  * if it is split, precisely one transposition is required to recover it?
  * After some thinking we realize approach B is not bery fruitful because one can have many different representsations and adding of transpositiosn
  * might end up with structures were we dont necessarily have cycles even.
  * STUCK
* IDEA So we move back to considering case (A) and look at for case S2 and our hypothesis is clearly true
  * Let us also use (B) and restrict our view on cycles of size 2 (because any permutation in S2 is a cycle) and it makes our analysis down the line simpler
  * Now we consider the SN case. And look at what needs to happen right before the final transposition is applied. We must have a map where only 2 elements are out of place.
  * Final Cycle = X(ab) what is the shape of X? If it is a cycle or a product of 2 smaller cycles we are in luck since we can definitely determine the odd/even of those
  * Is there a way we can change our view so that the final is a ident? (NO but we can view FINAL as a cycle)
  * So now we need information on how to deduce the shape of X, the thing right before a cycle which when multipllied by a transpose will give our cycle
      * How do we get it?
      * Take a cycle and change 2 elements
      * (V) Great so if you can write a formal way to state this the proof will fall out then
      * Since X is decomposed into smaller cycles who,s total sum is N-1
        * So X will break up into cycles whose combined lengths is N-1
          * N even number -> N-1 odd: (Odd+Even=Odd) or (Odd) -> X is composed of odd -> X+1= N is composed of Even
          * N odd number -> N-1 even: (Even+Even = Odd+Odd=Even) or (Even) -> X is composed of Even -> X+1 = N is composed of Odd
        * Which implies X is 
* Formalization of (V)
  * Since we have a cycle, we can take one of the elements being swapped as the first.
  * Let 2a be the two elements being swapped per our notation
  * The placement of the 2nd element will create 2 disjoint cycle ( 1abc... )  and the remainder ( 234...(a-1) )
  * Examples
    * 123456
    * 234561
    * 123456
    * 324561
    * 123456
    * 534261
* Great a cycle can be 

## How can you 
* Train your ability to seek out different avenues and attack the problem from these angles?
* Perhaps ability to quickly rule out some of the options?
## After working independently and deriving the next two steps of the book, I've come to realizations
* Thinking on your own and asking questions
  * This is definitely the way to study. 
* (Peristence and Tenacity) Some theorems and ideas are difficult and may take time and effort. Dont get frustrated
* You have to put in work. Be serious about it. Make a genuine effort and think hard.
* (Branch) out different paths of attack and explore the problem. 
  * (Prune/Evaluate) Check and find counter examples or counter proofs to prune your branches.
  * (Isolate) Do explore different subset of ideas and isolated events. And consolidate and organize your findings in this area
  * (Reuse) what you find in a different branch. What you study in one area is useful and meaningful to the whole picture.
* Question everything

## Even permutations is a normal subgroup
* Subgroup is clear $a$
* Ok so it does not commute but clearly the $oeo^{-1} \in EVEN$
* Great it is normal. What is structure of $\dfrac{G}{EVEN}$? or Size of [G:EVEN]
    * Consider the mapping from even to odd by removing the last element from each even element, wait this is not well defined.
  * consider mapping from EVEN-> ODD by mult by single transpose (12)
      * Well defined since mult is well def
      * Surjective because for any odd o, f(o(12)) = o
      * Injective b/c f(o)=f(j) = o(12)=j(12) -> o=j
  * So cardinality of two sets are equal => [G:EVEN]=2
## Subgroup is simple if it has no other trivial subgroup
* Odd is not subgroup because it does not contain identity
## No other subgroup has index 2
* I thought about how to draw contradiction
* The most direct line of thought that helped me was this 
  * Take any subgroup that has index 2.
  * For all we know, this subgroup could be the alternating subgroup. 
    * So what makes it different from An?
    * What must this object be or not be?
    * **(Pruning)**
      * **If I work/play with the current assumptions, what possible conclusions can I arrive at?**
      * **If it is an absurd conclusion, we must change/modify the assumptions.**
  * It must contain an odd element and even elements
oe=j

## Even permutation is the unique subgroup of index 2 in Sn
* I tried many many different approaches 
  * I even explored the consequences of the assumption of another index existing
      * the cosets of index 2 are contained by inverses
      * S, the other subgroup must contain odd numbers
      * The even subset of S is N/4
          * This is instrumental because it shows that it is only posible for Sn that are divisible by 4
      * S is normal
  * I feel like where I looked today, there isn't really an answer because I am showing things which are already true
  * i.e using normality to show normality
  * I must find some special connection that uses the even/odd structure of Sn
  * Have faith, if it is true, then the solution and the nature of the explanation exists.
    * It is much difficult if you do not know if it is true or not. This is where your intuition? No you guess XD

## Really difficult and stuck on (prev problem)
* Ok it was a excepttional difficult exercise that requires a hint of use of a lemma
* I think my advice is to look at a specific example and draw some inspiration

## The time is now
* I dont want to be fake. I want to be fing legit

##  Examples of Sn
* How does S2 extend to S3? or SN to SN+1
  * Well... cycles of 2 and 3
  * How does one extra value change the existing structure permutation combination wise
      * Consider the set of cosets $[ SN(x,N+1) | x\in 1..N+1 ]$
      * Show that each coset is disjoint
          * suppose f(x,N+1) = g(y,N+1)
              * f = g(y,N+1)(x,N+1) = g (yxN+1) Can we get f by itself? Yes!
              * This means that for g(a)=x where a is a member of 1..N f(x)=N+1 which means f is not in SN
                * Or just that fact that N+1 maps to y is a more direct contradiction
      * So one can form a mapping from the elements int he union of these cosets into SN+1 and it must be bijection since their sizes are the same
          * (RECALL) One intresting proof about same cardinality being a bijection
      * In conclusion the additional set of transpositions introduced by N+1 is precisely enough
* Another question: How many isomorphic subgroups of SN is there in SN+1? You can have SN while keeping the ith element fixed (and just rename the numbering)
    * But there is definitely overlap. Just look at identity, it is shared by all isomoprhic subgroups of SN
* So S4 is just [S3(x4) | x in 1..4]
  * S2 
    * (11) (12)
  * S3
    * (11)(13), (12)(13)
    * (11)(23), (12)(23) 
    * (11)(33), (12)(33) 
    * 012
    * 132
    * (13), (12)(13)
    * (23), (12)(23) 
    * iden, (12)
  * S4 2*3*4=24
    * (11)(13)(14), (12)(13)(14)
    * (11)(23)(14), (12)(23)(14)
    * (11)(33)(14), (12)(33)(14) 
    * _
    * (11)(13)(24), (12)(13)(24)
    * (11)(23)(24), (12)(23)(24)
    * (11)(33)(24), (12)(33)(24) 
    * _
    * (11)(13)(34), (12)(13)(34)
    * (11)(23)(34), (12)(23)(34)
    * (11)(33)(34), (12)(33)(34) 
    * _
    * (11)(13)(44), (12)(13)(44)
    * (11)(23)(44), (12)(23)(44)
    * (11)(33)(44), (12)(33)(44) 
    * _
    * 1/2 1/3 1/4
    * 1/2*1/3*1/4 have cycle 0
    * _
    * (12)(13)(14), (13)(14), (12)(23)(14), (23)(14), (12)(14), (14)
    * (12)(13)(24), (13)(24), (12)(23)(24), (23)(24), (12)(24), (24)
    * (12)(13)(34), (13)(34), (12)(23)(34), (23)(34), (12)(34), (34)
    * (12)(13), (13), (12)(23), (23), (12), Identity
* Ok now split S4 into 4 parts, even,odd,even,odd
* What elements are closed under multiplication?
  * Lets study the orbit of our elements
  * (12)(13)(12) = (231)(12) =  (23)
  * (123)
  *  (21)(31) = (231) 
  *  (ab)(ac) = (abc)
  * (ab)(ac)(ab) = (abc)(ab) = (bc)
  * (ab)(ac)(bc) = (ac)
  * (ab)(ac)(ac) = (ab)
* What is structure of S4 where we can possibly have another subgroup of index 2

* (13), (12)(13)
* (23), (12)(23) 
* iden, (12)
* $<(12)(13), (12), ident>$ will add  (13), (23)
So if you had a 3 cycle and transposition which contains 2 of the cycle elements, then you'll get all the other transpositions
* Is this true for all cases? Yes The posible transpositions involving 3 elements (ab) (bc) (ac)
  * (abc) = (ab)(ac)
  * (abc) = (bca) = (bc)(ba)
  * (abc) = (cab) = (ca)(cb)
  * 
  * (ab)(ac)(ab) = (bc)
* What happends when you mult (ab)(ac) by itself?
  * (ab)(ac)(ab)(ac) = (bc)(ac) = (cba) = (acb) = (ac)(ab)
* 3 times? (bc)(ac)(ab)(ac) = (bc)(cb) = ident


* if you have 2 transpositions with 1 common link, you can generate the last of the 3 transposition


* How many transpositions are there?

$N*(N-1)/2$
One odd subset cannot contain them all in a subgroup because this would generate the entire subgroup
Can a subgroup contain all the transpositions?
In S3 product of 2 3-cycles is another cycle how does this extend to S4?

* Suppose what you want is true and the branch out based on this assumption .
* Then come back and prove the desired property


* Can you show a 3cycle exists in our S?
* Then use normality

* Not all learning is equivalent
* Why did I decide to read book for guidance?


* given a fixed r,s (rsk) where k!=r,s generates An
    * Yes, the goal is to show that we can make (abc) and 3 cycles, which are the generators of An.
    * (rsa) = (rs)(ra)
    * (rsb) = (rs)(rb)
    * (ra)(rs)(rs)(rb) = (ra)(rb) = (rab)
    * Conclusion: we can form and (rab) where we choose ab
    * (rab) = (bra) = (br)(ba)
    * (rcb) = (brc) = (br)(bc)
    * (ba)(br)(br)(bc) = (ba)(bc) = (bac) = (acb)

* if S normal and S contains a 3 cycle, then S generates An
  * Show you can generate any given (abx) show you can make any (abc) using normality
      * (xc)(ab)(bx)(xc) is in S
      * (ab)(xc)(bx)(xc) = (ab)(bc) = (bac)
        * Replacement operator: (xc)(bx)(xc) = (xc)(xbc) = (cb) = (bc)
      * (bac)(bac) = (abc)

* Finally show S must contain a 3 cycle (ab)(ac)

* An is simple?
G   An
2    1
6    3
24  12
S=3 4 cosets 6 transposition
2345
n*(n-1)/2 = n!/2k

k = (n-2)!
k divsor of n!/2
n=4 k=2
n=5 k=6


# 20205020

## Burn out
* I have stopped making progress on the problem. Why?
	* I felt stuck.
	* It was not going as easy as b4.
	* Fatigue

* Why did you feel stuck?
	* progress wrt chapters completed
		* assumed all chapters are equal
	* There were many ideas that are new and unexplored. Many questsions.
	* I felt like I was rushing through it.


* Conclusions 
	* Work on another study subject
	* A new chapter with many new ideas will take time to explore
		* chapters are not equal

* How can I over come?
	* Take your time, and be consistant
		* When you rush, you take the magic out of it
	* Push through. Inner strength.
	* Recharge, Rest really well.
	* Think of the bigger goal

* GO HARD



# 210507

## HUNGERFORD THM 1.4.8 
$|H:H \cap K| \leq |G:K|$. If $|G:K|$ is finite $|H:H \cap K| = |G:K| \leftrightarrow HK = G$

* I began the problem by trying to understand what the statement was asking me to prove and the significance.
	* That $K$ has more cosets in $G$ than $|K \cap H|$ has in $H$
* First, I started the problem by looking at the relationship between the set and subset and number of cosets.
* But it became clear that this would not lead to any significant result or show interesting relationship.
* Then I looked for a mapping between the LHS to the RHS that was a function and injective.
	* This gave me the solution.

* I have overlooked on how to show inequalities or counting, which is by showing a function from A to B.
* I should review the different approaches and select the probable one before diving in

* When I was trying to show the equality part, I approached it first by drawing out all the equalities and trying to match
together a solution by guessing.
	* I was getting stuck due to a similar reason as 1.4.7 and I looked for a clear direction.
	* I realized that all i needed was to show that the mapping i showed was surjective under the the condition $|HK| = |G|$
	* I was looking at $|G:K|$ and the cosets $Kg = Khk$ and wishfully thought what if $Kkh$?
	* Turns out it HK = KH!

* I am really proud that I learned from my previous mistake. and was able to look for a different approach and not keep guess



# 210506


## HUNGERFORD THM.1.4.7
$|HK| = \dfrac{|H||K|}{|H \cap K|}$

* ISSUE: Stuck working on cosets order of HK
* Got  stuck because I was trying to piece together bits of what I guessed was the solution.
And was hoping would eventually just give me the solution through guessing.
* I needed a clear sense of direction that I understand
* Also needed to invest more time understanding/organizing the properties of the elements in the problem which came up while I was working on the problem.

## Break
* Prevent burnout
* Something you find rewarding
	* Social activity?
* Something which you enjoy
* Something which gives you closure
	* Walk, food, lifting, movie

## Warning
* Be mindful how you fill up the pages and what you write. Too much and it will clutter.

## Motivation
* If what you are trying to prove is true, there IS a natural solution/connection/reason to get there!
* Like programming was difficult when I was young, I am beginning to understand and get better at mathematics.
It is certainly something that you can get better at!
Keep doing what you are doing. Work through the book. Organize. Review. Improve yourself.
Blind think. See what you can extend.
* Thinking is a muscle. It is something that you can improve.

## Questions
* Do I understand all the members/elements/components of the problem?
* What should I do if I am not interested in a topic?
	* Find something that is interesting about it.
* What am I looking for? Did i understand the problem?
* What properties does it have?
* What is it made of?
* What does it belong to?
* Do existing things play/act with it?
