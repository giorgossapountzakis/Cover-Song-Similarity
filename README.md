## Cover-Song-Similarity
# Goal 
The goal of the task was to analyse the TACOS dataset and address the problem of cover song detection. In other words we were asked to find a way to compare two music tracks on whether they are covers of the same song or not and define a metric about in an quantification attempt.

# Dataset Analysis
TACOS is a vast dataset, with many GBs worth of performances provided along with their hpcp and crema data, in the form of .h5 files. We used the subsets of “da-tacos_benchmark_subset_crema” and “da-tacos_benchmark_subset_hpcp” for our work along with the metadata data, as they had considerably smaller size. 
We analyse the dataset providing added functionalities like searching by artist name and save parts of our analysis in cover_relationships.txt and cover_mapping.json respectively. We also visualise the chromagrams using both the crema and hpcp sequences.

# Aproach 1 - DTW distances
The first method we use is Dynamic Time Warping. We basically try to find the optimal key shift of each crema sequence (and hpcp sequence respectively) so that the sequence is most similar to the original song. After we analyse a sample of the dataset we try to set a threshold based on which we would decide if two songs are covers or not. The threshold can be more precise the more data we analyse. The main problem of this method is the computational efficiency as the comparisons scale enormously and as a result we are forced to perform heavy downsampling losing and generally computational reductions that make our approach inefficient.

# Approach 2 - Siamese network
Due to the scalability problem of our statistical approach we resolve to machine learning to solve this problem too. Our proposed solution is no other than a Siamese network, consisting of two identical feature extractors (CNNs) that try to embed the sequences provided in a way that the more similar they are the smaller their distance will be. To do so we add a custom loss function that encourages similar inputs to have small distances. In the process a similarity metric is produced and a more accurate distance threshold is set. We see that even with few samples and little training we achieve remarkable results as seen on the validation_distance_distribution plot.

# Conclusion
While the DTW method theoretically should work, given that it takes into account key and tempo variation that are typical of song covers, the computational requirements prohibit us from reaching a robust conclusion. On the other hand the Siamese network logic is very promising as with minimal training it seemed able to identify reasonably whether songs are covers or not. the similarity metric and distance threshold can be optimized of course.

# Further Work
Investigating the state of the model with more training, meaning training on the whole dataset possibly to find the optimal threshold distance and similarity metric in which we should base our decisions upon.



