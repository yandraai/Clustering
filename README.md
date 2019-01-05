Linear Regression 
===================

- Data set Used: HW4GaussianClustersData (Please look in DATA folder)

Question 1 
------------

- Plot the data on a 2-D scatter plot and mark by hand the boundaries of the ideal clusters that you would like discovered in this dataset. 		
  
  Scatter plot of the data points:
  
  ![image](../master/Dataset.PNG) 
  
  
  I have marked the clusters intuitively based on the alike nature of the points. 
  
  ![image](../master/Intuitive_Clusters.png) 
  
  
Question 2
------------
  
- Run the k-means algorithm for k = 3, 5, 7, 9, 11, 13, 15, 17 and 19. Plot the total SSE and BIC values for the above values of k. 
  What is the best number of clusters for this dataset? How did you find the best number of clusters, briefly explain.
  
- **SSE** :: Sum of squared Error is the sum of all euclidian distances from each data point to the centroid of a cluster. A lower value suggests that the cluster is closely packed.
- **BIC** :: It is one of the criterion for model selection among a finite set of models. Lower value indicates a good model.
  
  We would be using both SSE and BIC values to choose the best k value for the dataset in use.
  
- Please refer to the imgae sse_bic to find that, the knee point is obtained at the k =11 ie., the change in SSE or BIC is not very significant or almost remains same when compared to the other k values earlier in the curve. 
  Though the errors of the higher k value is low it is deceptive in the sense that it breaks the original clusters into smaller clusters and so the error decreases.
  
  **Hence k =11 is chosen as the best number of clusters.**

Question 3
------------  
- For the best number of clusters selected above, plot the scatter plot of the data showing the points of each cluster with a different color/symbol. 
  Mark the points on the scatter plot that belong to clusters other than what your intuition says. Why did k-means algorithm place them in these different clusters – explain very briefly.   

- Scatter Plot of the Clusters Formed:
 
 ![image](../master/Kmeans_clusters.png)

- Kmeans differed from my intuition for the marked points: 
 
 ![image](../master/points_that_differd.png)
 
- Commments on the points that differed in the above intuite and k means clusters :

  - K means clustering is a **center based clustering technique**. Hence, to a greater extent depends on the initial centroids chosen. Now once the centroids are chosen initially, iteratively the distances are calculated from all the other data points to the centroid and all the data points nearest to the centroid are made into a cluster.
   
  - **Hence, K means tend to give the globular shaped structures and may not be very effective for others.**
   
  - In our example as well, the points marked are all points that are marked are nearer to the centroids that the k means chose and so are placed in that way, which is different from the intuition.
  - This is one of those situations where we can see that the K means may fail with the non-globular structures.

 Question 4
------------
- Plot the silhouette diagram for the best clustering you have selected. Comment on the characteristics of the silhouette diagram that you think are informative about this clustering. 
  Comment using the cluster numbers and their plots on the silhouette diagram.  

- Silhoutte Diagram 

	![image](../master/Silhoutte.PNG)  
  
  **The silhouette value is a measure of how similar an object is to its own cluster (cohesion) compared to other clusters (separation).**
  
- So in the above figure, the clusters (8)yellow,(4) and (3)blue are having data points with higher values which means that they are closely packed and are nearer to their centroids and far away from other centroids. And the width of the clusters depict the number of data points.
 
  However, the clusters (5) green,(9) orange,(10)red are loosely packed as they have points that are away from the centroid of its own cluster.
 
- The cluster (4) is a good cluster with greater number of points closely bounded followed by (8).
  
  On the whole the coefficient is very much nearer to 0.6 which means the points are well in cohesion and the clusters are well separated to some extent. Though this is not very great, they are not bad as well.
 
 Question 5
------------
- Perform single-linkage hierarchical clustering for this data and cut the dendrogram to obtain 11 clusters. There are options/parameters in most toolboxes to generate a given number of clusters. Plot the 2-D scatter plot of the dataset showing data points of each of the 11 clusters with different color/symbol.  
 
-Function Used: 

```
 z=sc.cluster.hierarchy.linkage(X_set,method='single',metric='euclidean)
 r=sc.cluster.hierarchy.dendrogram(z,no_plot=False)
```
- Dendogram built:
  
  ![image](../master/Dendogram.png)

- Cut the dendogram at the 3.2 distance to obtain the ideal 11 clusters.

```
 fc=fcluster(z,3.2,criterion='distance')
```

- Scatter plot of the clusters formed by the single link clustering.

 ![image](../master/single link clusters.png)

 Question 6
------------

- Mark any data points on this scatter plot that are clustered differently from your intuitive view of the correct clusters. Explain why Single-linkage clustering may have placed them in counter-intuitive clusters.

 - Single Linkage clustering is a type of Agglomerative Hierarchical clustering where the clusters are merged when the nearest points between clusters have a minimum distance. 

 - The clustering starts from the individual points starting at random and iteratively combines the clusters that have minimum distances between its nearest points.
 
- Outlier points made into separate clusters.

 ![image](../master/2e.png)
 
 - Except the points that are marked all the other are intuitively placed into separate clusters but the single linkage placed them into 2 clusters. This happened because it forms contingency clusters which is one of the major drawbacks of single linkage clusters. 
 
 - Single linkage cannot identify the clusters that have data points between them, even if they are scarce it combines them. 

 - All the clusters here have at least few data points between them , hence they are formed as one cluster. *** Proving that single link clusters fail with such data.***

	