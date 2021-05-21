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

**Current**

* Make current one more efficient (Memory)
	* Masking?
		* Scale down the loss for those values?
	* Optimization Attention
	* Combination of Convolutions?
		* How many blocks should we put?
	* spatial loss? reward more for pairs further apart ( no reduce, mult by guassian further away _| -shaped weights)
		* W[i,j] = sqrt(abs(i-j))
		* Stack to same shape and mult
* Coordinate Prediction
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




--------------------------------------

# AI

## RL
* Tic Tac Toe
	* Fix the crash and make it work for larger boards

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
