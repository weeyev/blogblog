## lets talk about incidence matrices 
 
they are used to represent something that we can actually see but just like every other thing that we convert into something that machines can understand (eg. images into pixel values, graph to adjacency matrices and so on..), incidence matrices serve the same purpose of showing which node is connected to which other node via an edge or in which edge subset is that node present in

we make this matrix for all the nodes present in the simplicial structure ofc, but for you to get some feeling lets take a small example of a simplicial complex and its incidence matrix

simplicial complex S1:

vertex set : [1,2,3,4,5]
edge set : [[1,2],[1,3],[2,3],[2,4],[3,4],[2,5],[4,5]]
face set : [[2,3,4],[2,4,5]]

which looks like 

[![image.png](https://i.postimg.cc/X7rqLpBf/image.png)](https://postimg.cc/LnMm64T5)

the incidence matrix of order 0 for this is 

[[-1. -1.  0.  0.  0.  0.  0.]
 [ 1.  0. -1. -1. -1.  0.  0.]
 [ 0.  1.  1.  0.  0. -1.  0.]
 [ 0.  0.  0.  1.  0.  1. -1.]
 [ 0.  0.  0.  0.  1.  0.  1.]]

now we see that what it does is if the node is there in the edge relationship we add a +1 if the node is head in the relationship (tail->head) otherwise a -1, if it is not found in the edge subset we put a zero



## moving on to laplacian matrices 

[![image.png](https://i.postimg.cc/htY4P3Vz/image.png)](https://postimg.cc/hX9R2syc)

whenever someone asks me this question, depending on the situation i either say this exact thing think this in my mind - imagine if you had a long lost brother and you wanted to find them, possibly the best common thing that exists between you and them to facilitate this process is that you both have the same parents.

in the same way we can generalize different components of rank n in the structure on the basis of their common n+1 ^th rank element, eg. for edge subset {2,3} if we want to find what other edges are like it - i.e share a same face or any other parent property, we use laplacians 

a better way to imagine this is going through each rank laplacians and slowly building up the idea 


[![image.png](https://i.postimg.cc/Jh3Fdsrg/image.png)](https://postimg.cc/d71nhtTm)

## up laplacians 

rank 0 up laplacian relation - if any 2 nodes have a shared edge between them 

take the node 1 in the previous simplicial structure and look out for its incident edges, from there look out for what other nodes are those edges incident to, in our case the edges are [1,2] and [1,3] and the consequent nodes from them are {1},{2},{3} that share a common property of edges, mathematically this is done by either doing the matrix multiplication of the already found rank 0 incidence matrix with its transpose or doing the subtraction of adjacency matrix from the degree matrix 

[![image.png](https://i.postimg.cc/dQgz3Pfw/image.png)](https://postimg.cc/fkjHqFZr)

L_0 = 	

[[ 2. -1. -1.  0.  0.]
 [-1.  4. -1. -1. -1.]
 [-1. -1.  3. -1.  0.]
 [ 0. -1. -1.  3. -1.]
 [ 0. -1.  0. -1.  2.]]

here the diagonal elements have a weight due to them being the degree of that specific node, another interesting property of this matrix is that the sum of each row is 0 leading to more useful things like graph clustering and partitioning 

also laplacians are used in diffusion models for finding out what amount of values should be transmitted between neighborhood nodes, this wouldn't work out if it didn't sum up to zero (law of conservation required)

rank 1 up laplacian relation - if any 2 shared edges have a shared face between them 

extending this concept over to an even higher rank: to get the edges that share a common face/form the sides of a triangle (a simple 2-d simplex)


however in a normal graph the highest rank we can achieve is 2 as there are no other higher ranked simplexes existing in the structure



## down laplacians 

rank 1 down laplacians relation - if any 2 edges have a shared node 
rank 2 down laplacians relation - if any 2 faces have a shared edge 

just like in up laplacians we had an upper bound condition of limiting to rank 2 similarly no rank 0 down laplacians can exist for the same reasons of no simplex of -1 rank being present in the structure.

[![image.png](https://i.postimg.cc/65LYXkJ8/image.png)](https://postimg.cc/7fhg1QL4)

## hodge laplacians
add both the up and down laplacians and you get the hodge laplacian, thereby in a sense seeing the whole structure of graph in all the ways possible, but remember that with the exception of down in rank 0 and up in rank 1 

## how multiplying incident matrices gives laplacian?

you might wonder how multiplying the matrix that captures whether an element exists in a subset with itself can lead to extracting relationship between elements using a higher dimension as base, for starters theres this amazing response that you can read on general laplacian operators and then we 
will get onto how this works in graph laplacians

[insert link also - https://www.reddit.com/r/math/comments/3yofdn/is_there_a_good_intuitive_explanation_of_the/] 


[![image.png](https://i.postimg.cc/rwjpBXGF/image.png)](https://postimg.cc/CRZY826W)

in graph laplacians at the same time when we multiply B.B^T the B^T is doing the difference operation i.e finding the difference between the values at i and j -> f[i] - f[j] and then when it is multiplied with B which 
penalizes/awards the deviation from the average by multiplying our terms with +/- 1


\[ (Lf)[i] = \deg(i)\, f[i] - \sum_{j \sim i} f[j] \]

