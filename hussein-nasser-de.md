# phantom read - 
- if another row or column added or deleted

![alt text](images-db-hussein/image.png)
![alt text](images-db-hussein/image-1.png)

# in non-relational databases
eventual consitency happens
![alt text](images-db-hussein/image-2.png)

# B-trees and B+ trees
![alt text](images-db-hussein/image-3.png)
![alt text](images-db-hussein/image-13.png)
- when we have to read pages for entire table 
- we have to go one by one
- for example find person with id5
![alt text](images-db-hussein/image-4.png)
![alt text](images-db-hussein/image-5.png)
- a node is a complete page means 8k rows are inserted in onenode
![alt text](images-db-hussein/image-6.png)
![alt text](images-db-hussein/image-7.png)
#limitations
![alt text](images-db-hussein/image-8.png)
solution
![alt text](images-db-hussein/image-9.png)
![alt text](images-db-hussein/image-14.png)
![alt text](images-db-hussein/image-15.png)
![alt text](images-db-hussein/image-10.png)
![alt text](images-db-hussein/image-11.png)

how postgre store indexes
![alt text](images-db-hussein/image-12.png)

# indexing helps
![alt text](images-db-hussein/image-16.png)
![alt text](images-db-hussein/image-17.png)
 there is a data block and it depends on disk size
 ![alt text](images-db-hussein/image-18.png)
 # there are two types of indexing
 ![alt text](images-db-hussein/image-19.png)
 ![alt text](images-db-hussein/image-20.png)
 ![alt text](images-db-hussein/image-21.png)
 in non-clustered index ususally what happens is we do indexing on secondary index so it does not remain in order as of offset
 whereas in clustered-index the way index happens - same way it is pointed in offset

 # key vs non-key index