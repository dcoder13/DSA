# SEGMENT TREE

- The leaf layer stores the array, and each parent level stores the sum/ (any other associative combination) of the two child nodes
- thus we need to make a complete binary tree
- increase the size of array to the closest power of 2 
- **This wont affect the time complexity of operations since the size will go max up to 2.n**


*array* :

![array](./assets/array1.png)
<br/>
<br/>
<br/>

*segment tree* :

![](./assets/array-segtree.png)

# Operations:
## Changing array element
	
![](./assets/set-operation.png)
- **O(logN)**
## SUM OF SEGMENT L TO R
	
![](./assets/sumOperation.png)

- sum from index 2 to 6
<br/>

- **CASE 1 :**
	
	![](./assets/case1.png)
	- The segment corresponding to the current node completely lies between L and R
	- **Add value at current node to total sum**
	- **Return!! no need to traverse further**
- **CASE 2 :**
	
	![](./assets/case2.png)
	- The segment corresponding to the current node lies partially inside the L to R range
	- **Keep traversing**
- **CASE 3 :**
  	
	![](./assets/case3.png)
	- The segment corresponding to the current node lies completely outside L to R range
	- **Return!! no need to traverse further**
### Time:
- Till we keep getting **case 2**, we'll keep going deeper in the tree
	- Until we either get **case 1** or **case 2**
	- In order for none of the cutoffs to work (**WORST CASE**), the corresponding segment must intersect the query segment
- Thus there can be no more than 2.logN nodes at which cutoffs did not work
- TIME : **O(logN)**


## MINIMUM IN L TO R

- This time create a segment tree, where parent node stores the minimum of its children.
- just like the range sum operation, traverse and find the minimum element.


**NOTE : OTHER THAN ADDn AND MIN, WE CAN USE SEGMENT TREE FOR ANY ASSOCIATIVE OPERATIONS LIKE BITWISE, MUL, ETC**


[IMPLEMENTATION](./IMPLEMENTATION.md)




