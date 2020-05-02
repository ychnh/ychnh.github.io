# 5/2

Different states of objects

* A) Game level state
* B) XY state
* C) grid state
* D) world generation logic (rect split)

We have functionality to go from A->B
We need to build functionality to go from D->C->B->A

* Clean code library
* Check mask collision and see if it alligned with centering method
* We primarliy want to operate off the grid. So the level of object states shold be stored in the grid form.
	* So we need to know the size
