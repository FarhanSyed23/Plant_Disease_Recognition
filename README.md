# Plant_Disease_Recognition

**NOTICE:** At first, [All_Segmentation_Techniques.ipynb](https://github.com/FarhanSyed23/Plant_Disease_Recognition/blob/main/All_Segmentation_Techniques.ipynb) file includes three segmentation techinques in one place. The results aren't shown here. To see the results, please go to individual folders named according to the segmentation techniques. The files are loaded with image and they are so large in size that github can't render them at this moment. If you want to see the results, you can see the **"readme"** files in those folders or you can download the ipynb files. 

As a part of research works, I looked for various segmentation methods to improve the accuracy of correctly identifying the plant disease from images.
 
In this research, I present some probabilistic data where we trained various machine learning classification algorithms with previously classified healthy and diseased plants’ images. From these images, I used three better working image segmentation methods to simplify the images into most important features from where it was easier to classify some different types of diseases such as Cherry Powdery Mildew, Corn Common Rust, Grape Isariopsis Leaf Spot and so on. Image segmentation is typically used to locate objects and background in images. Thresholding is the very basic segmentation method. I used RAG thresholding, Region Rag thresholding and Grab Cut segmentation method and classified the new segmented images with Decision tree, Random Forest, Naïve Bayes, SVM, xgBoost and K-Nearest Neighbors classifiers. The main idea of this research is that, these segmentation methods can work effectively to classify plant diseases. 

# RAG Thresholding

The regions of an object obtained by many segmentation methods in images taken under slightly different imaging conditions differ significantly. This is because the existing segmentation algorithms do not always produce perceptually meaningful regions. This results in splitting and merging of adjacent regions, even if the contrast changes very slightly. This technique results in over segmented graphs which requires merging techniques until a required number of regions are obtained. Computing the region adjacency graph (RAG) simplifies the problem of merging. In constructing a RAG for an image, each region can be represented as a node and an edge connecting two nodes are inserted if two regions are adjacency. It allows different sub images that are adjacent but cannot be merged in the quadtree to be merged. First, the nearest common ancestor is determined that connects the current end node with the neighbour. Next, the path is mirrored about an axis formed by the common boundary between the adjacent sub images.

<p align="center">
    <img width="800" src="https://github.com/FarhanSyed23/Plant_Disease_Recognition/blob/main/Rag%20Thresholding%20Segmentation/Screenshots/RAG_Thresholding.PNG" alt="RAG Thresholding">
</p>

# Hierarchical Merging of Region Adjacency Graphs (Region RAG)

Region Adjacency Graphs model regions in an image as nodes of a graph with edges between adjacent regions. Superpixel methods tend to over segment images, i.e., divide into more regions than necessary. Performing a Normalized Cut and Thresholding Edge Weights are two ways of extracting a better segmentation out of this. We could combine two small regions into a bigger one. If we keep combining small similar regions into bigger ones, we will end up with bigger regions which are significantly different from its adjacent ones. Hierarchical Merging explores this possibility. A function known as merge_hierarchical function performs hierarchical merging on a RAG. It picks up the smallest weighing edge and combines the regions connected by it. The new region is adjacent to all previous neighbours of the two combined regions. The weights are updated accordingly. It continues doing so till the minimum edge weight in the graph in more than the supplied threshold value.

<p align="center">
    <img width="800" src="https://github.com/FarhanSyed23/Plant_Disease_Recognition/blob/main/Region%20Rag%20Segmentation/Screenshots/Region_Rag.PNG" alt="Region RAG">
</p>

# Grab Cut

Grab Cut augments graph cut by iteratively minimizing the energy in an image to find the local optimal binary segmentation. The method features a simple user interface which only requires the user to draw a rectangle around the object to be cut. This initialization defines only the background pixels, and then iteratively improves the segmentation by recalculating the probability distributions of the background and foreground colours and then uses these estimates in graph cut. Hard segmentation is performed to create a foreground and background pixel sets. The background pixels go into the background pixel set. The unknown pixels are the foreground set. Starting with a user-specified bounding box around the object to be segmented, the algorithm estimates the colour distribution of the target object and that of the background using a Gaussian mixture model. This is used to construct a Markov random field over the pixel labels, with an energy function that prefers connected regions having the same label, and running a graph cut based optimization to infer their values. As this estimate is likely to be more accurate than the original, taken from the bounding box, this two-step procedure is repeated until convergence. Estimates can be further corrected by the user by pointing out misclassified regions and rerunning the optimization. The method also corrects the results to preserve edges. 

<p align="center">
    <img width="800" src="https://github.com/FarhanSyed23/Plant_Disease_Recognition/blob/main/Grab%20Cut%20Segmentation/Screenshots/Grab_Cut_Pic.PNG" alt="Grab Cut">
</p>


