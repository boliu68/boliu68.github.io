#Algorithms and Complexity:

---

##Convex Hull for 3D

**1.Combinatorial Complexity:**
$$n_f = 2n_v - 4$$
$$n_e = 3n_v - 6$$

**2. Representation method**
	
	1. list of vertex
	2. list of faces
	3. adjacent list
	4. face based sturcture
	5. edge based sturcture
	
**3. Gift Wrapping, like Javaris**

$$T=O(nH)$$

**4. Graham approach**
$$T=\Omega(n^2) \text{ in worst case.}$$
$$T=O(nlogn) \text{ randomized}$$ 

**Divide and Conquer**

**Prune Divide and Conquer**
$$O(nlog^2h)$$
**Group and Wrap**
$$T = O(nlogh)$$
**Higher Dimension**

1. gift wrapping: $$$O(nH)$$$
2. incremental: $$$O(n^{d/2})$$$
3. dual sweap: $$$O(n^{d/2})$$$

##VD and DT:
1. gift wrapping: $$$O(n^2)$$$
2. incremental
3. divide and conquer
4. Fortune sweap

##Linear Programming:
**Trival Algorithm**

$$$O(nlog) \text{ time for } d= 2,3 \text{ ad worst for }d\geq4$$$

**Prune and Search**
 in 2D
 
$$T(n)\leq T(\frac{3}{4}n)+O(n)=O(n)$$

In 3D:

$$T(n) = T(\frac{15}{16}n)+O(n)=O(n)$$

**Higher Dimension**:

**Best:** $$$O(d^{O(d)}n)$$$


**Seidal Rand Incemental Algorithm:**

Using backward analysis:
$$T(n)=T(n-1)+\frac{2}{n}O(n)+(1-\frac{2}{n})O(1)=O(n)$$
$$T(d,n)=O(d!n)$$

**Clarkson's Random Sampling Algorithm**

iterate d+1 times

$$T(n)=O(n)\text{ for constant d expected}$$

**Clarkson's second algorithm reweighting**

$$T(n)=O(nlogn)$$ 

##Line intersection

**3 Approaches:**
	
Lower Bound: $$$\Omega(nlogn +k)$$$
	
	1. Incremental
	2. sweap line
	3. Divide and Conquer

**Naive Algorithm**
$$T = O(n^2logn)$$ by sort on the intersection on each line.

**Incremental Algorithm**

 by insert a new line and locate all the cells cut by new line This can calculate the arrangement.
 $$T=O(n^2)$$

**Sweap Line Algorithm**

$$T=O((n+k)logn), S=O(n)$$

can calculate the arrangement and trapezoidal decomposition.

**Divide and Conquer Algorithm**

$$O(\sum(l_vlogn + (n_v+l_v)logn))=O(nlog^2n + klogn)$$

Refinement 1: Keep the long segment sorted.
$$O(nlog^2n+k)$$

Refinement 2: Fractional Cascading

$$O(nlogn + k)$$


##Point Location:

**Brute Force**
$$Q(n)=O(logn), S(n)=O(n^2),P(n)=O(n^2)$$

**Segment Tree**

$$Q(n)= log^2n$$
$$S(n)= nlogn$$
$$P(n)=nlogn$$

**Persistent Search Tree**

backward analysis

$$P(n)= O(nlogn)$$
$$S(n)=O(nlogn)$$
$$Q(n) = O(logn)$$


**Kirkpartik**

$$P=O(n)$$
$$S=O(n)$$
$$Q=O(logn)$$

##Polygon Triangulation

**First TD and Connect Diagonal**

$$O(nlogn)$$

**Lower Bound**

Simple Polygon: O(n)

Special Polygon: O(n)

disjoint line segment: $$$\Omega(nlogn)$$$

polygons with holes: $$$\Omega(nlogn)$$$

##Range Search:

**kd tree**
$$S(n)=n$$
$$Q(n)=\sqrt{n}$$
$$P(n)=O(nlogn)$$

**Range Tree**
$$S(n)=P(n)=nlog^{d-1}n$$
$$Q(n)=log^{d-1}n$$

**Partition Tree**
$$Q(n)=O(n^{log_4^3})$$
$$P(n)=O(nlogn)$$
$$S(n)=n$$

$$$Q(n) = n^{\frac{1}{2}+\epsilon}$$$ for best

**Cutting Tree**
$$P(n)=S(n)\leq4S(\frac{7}{8}n)+O(n)=O(n^{log_{8/7}^4})$$
$$Q(n)=logn$$


**Final**
$$P(n)=O(m)$$
$$Q(n)=O(\frac{n}{m^{1/d}})$$


