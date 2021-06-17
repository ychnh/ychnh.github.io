# Math

## Algebra

**Current**

* Previous Material
	* Semigroups, Monoids, Groups
	* Homomorphism and Subgroups
	* Cyclic groups
	* Cosets, Partition of
* Normal, Quotient Groups, Homomorphism
	* Review/Explore
	* Preservation of structure of quotient groups in relation to parent groups

**Future**

* Characterization of finite groups
* Galois

--------------------------------------

## Adv Calc

**Current**

* sequence and characterization of infinity

**Future**

* Derivation of derivative
* Fund Theorem of Calc

--------------------------------------


## Lin Alg

* Review back to Determinants
* Orthogonal Theorems
* Fund Thm of Algebra
 

--------------------------------------

# PharmCadd

## Masking?
* Better loss masked categorical cross entropy. Make unavailable values not contribute to loss
* complete_structures_only:
	* Update SCN
* thinning:

## Make current one more efficient (Memory)
* Optimization Attention
* Combination of Convolutions?
	* How many blocks should we put?
* spatial loss? reward more for pairs further apart ( no reduce, mult by guassian further away _| -shaped weights)
	* W[i,j] = sqrt(abs(i-j))
	* Stack to same shape and mult
* Dataloader memory issue with cycle()

## Coordinate Prediction
* trunk_coord module
	* MDS differentiable
* structure module
	* x,coords = SE3Transformer(x,coords)
		* x
			* x (b i j d) <- output from attention
			* x = linear(x)
			* various things(Embeddings add)
			* x 'b i d'
		* coords
			* coords = trunk_to_coords[ MDScaling(distm) ]
* Loss
	* Coordinate
		* Centering
		* RMSD
	* Distance Matrix

## Coordinate prediction approach guide

* SO3 group
	* rotation about x,y,z axis. Right hand rule
	* invertible, identity, 
	* closed under operation
		* **Euler's Sperical Theorem**
* Group Representation
* Irreducible representation
* Wigner-D matrix
* Clebsch-Gordan matrcies
* Equivarient what is v,y
* General Linear Group

## Is there a way to use persistent homology for shape formation?


--------------------------------------

# AI

## RL
* Tic Tac Toe
	* Fix the crash and make it work for larger boards

* Why is RL important? It generates it's own information.
    * It is not learning from data
* But if you think about it the rules and these things are kinda like 'data'
    * It learns from them
    * And uses the learning to explore the data space some more.


--------------------------------------

## Face latent space generation


--------------------------------------

## NLP
* Text generation
* Chat

--------------------------------------

## Text to image generation


--------------------------------------

# LIFT
* Focus on form. The weight will come after.
* Lifts
	* Bench
	* Squat
	* Row
	* OHPress
	* Pullup
	* Deadlift
