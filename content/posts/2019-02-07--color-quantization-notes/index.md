---
title: Notes on Color Quantization
categories: "zombie notes"
cover: color_thumbnail.jpg
---

The process of color quantization is mainly comprised of two phases: **palette design (the selection of a small set of colors that represents the original image colors) and pixel mapping (the assignment of each input pixel to one of the palette colors)**. 

The primary objective is to reduce the number of unique colors, N′, in an image to K, where K ≪ N′, with minimal distortion. 
in general algorithms for color quantization can be broken into two categories: Uniform and Non-Uniform. 
- Uniform: Here the color space is broken into equal sized regions where the number of regions, NR is less than or equal to K. 
- Non-Uniform: Here the manner in which the color space is divided is dependent on the distribution of colors in the image. 

###Uniform Quantization 
- in uniform quantization each acts of the color space is treated independently. 
- each axis is them divided into equal sized segments. 
- the number of these regions is depended on the scheme used for dividing the color space. one possible scheme is to divide the red and green axis into 8 segments and the blue axis into 4 segments resulting in 256 segments. 
- once the color space has be divided each of the original colors is then mapped to a region which it falls in. the representative colors for each region is then the average of all the colors mapped to that region. 
- does not yield very good results. often regions in the color space will not have any colors mapped to them resulting in color map entries being wasted. 
- this algorithm can also be applied in a non-uniform manner if the axis are broken on a logarithmic scale instead of linear with slightly better results. 

###Popularity Algorithms 
- a form of uniform quantization where algorithms break the color space into much smaller, and consequently more, regions. for example, regions 4x4x4 in size (262144 regions). the representative color for each region is then the average of colors mapped to it. 
- the color map is selected by taking the representative colors of the 256 most popular regions (the regions that had the most colors mapped to them). 
- if a non-empty region is not selected for the color map its index into the color map (the index that will be assigned to colors that map to that region) is then 
- the entry in the color map that is closest (Euclidean distance) to its representative color). 
- these algorithms are also easy to implement and yield better results than the uniform quantization algorithm. they do, however, take slightly longer to execute and can have a significantly larger storage requirement depending on the size of regions. 
- depending on the image characteristics this may not produce a good result. this can be said about all uniform sub-division schemes, because the method for dividing the color space does utilize any information about the image. 

###Median Cut Algorithms 
- the premise behind median cut algorithms is to have every entry in the color map represent the same number of pixels in the original image. 
- these algorithms divide the color space based on the distribution of the original colors. 
- the process is as follows: 
    1. Find the smallest box which contains all the colors in the image. 
    2. Sort the enclosed colors along the longest axis of the box. 
    3. Split the box into 2 regions at median of the sorted list. 
    4. Repeat the above process until the original color space has been divided  into 256 regions. 
- the representative colors are found by averaging the colors in each box, and  the appropriate color map index assigned to each color in that box. 
- because these algorithms use image information in dividing the color space this class of algorithms consistently produce good results while having memory and time complexity no worse than popularity algorithms.  

###Octree Algorithm 
- the principle of the octree algorithm is to sequentially read in the image. every color is then stored in an octree of depth 8 (every lead at depth 8 represents a distinct color). a limit of K (in this case K = 256) leaves is placed on the tree. 
- insertion of a color in the tree can result in two outcomes 
    1. if there are less than K leaves, the color is filtered down the tree until either it reaches some leaf node that has an associated representative color or it reaches the leaf node representing the unique color. 
    2. if there are greater than K leaves in the tree some sets of leaves in the tree must be merged (their representative colors averaged) together and a new representative color stored in their parent. 
- once the entire image has been processed in this manner the color map consists of the representative colors of the leaf nodes in the tree. the index of the color map is then stored at that leaf, and the process of quantizing the image is simply filtering each color down the tree until a leaf is hit. 
- because a limit is placed on the number of leaves in the tree this algorithm has a modest memory complexity, O(K), compared to the median cut and popularity algorithms. 

###Minimum Variance Algorithm 
- the minimum variance quantization method (Heckbert, 1982b), divides the color space into boxes in the red, blue and green directions until obtaining a predefined number of colors. Then, the averages of the pixel values are represented as palette colors, as in uniform quantization. 

###K-Means 
- firstly, the initial centroids are randomly generated. 
- after that, the pixels are assigned to the closest centroid and each centroid is then modified by averaging the pixel values in each class. 
- his process is repeated until the predefined convergence. 
- being very simple, it is highly dependent on initial conditions. 

###Fuzzy-C-Means 
- the soft version of the K-means, is proposed by Dunn so as to decrease the adverse effects of initial conditions. 
- FCM generally performs better than K-means in terms of finding the optimal solution and FCM is less influenced by existence of uncertainty in the data set. 
- however, it might be highly affected from the noise and imaging artifacts (Forouzanfar et al., 2010). 
- recently, the new versions of FCM such as, robust fuzzy C-means (RFCM) (Pham, 2001), possibilistic C-means (PCM) (Krishnapuram and Keller, 1993) and generalized Color Image Quantization: A Short Review and an Application 489 FCM (GFCM) (Jian and Miin-Shen, 2007) etc., were developed by modifying equations based on objective functions. 
