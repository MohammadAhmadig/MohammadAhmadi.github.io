---
title: "Hybrid and Wrapper Feature Selection Algorithms"
collection: projects
permalink: /project/project-01
excerpt: 'Design and implementation of three new feature selection algorithms for high-dimensional data and the Implementation of tens Hybrid, Wrapper, and filter Feature Selection Algorithms'
date: 2022-02-04
venue: ''

---

Feature selection methods can choose a proper subset of relevant and representative features to the corresponding class label and remove the irrelevant and redundant features. It is noticeable that applying feature selection sometimes enhances the performance of clustering and classification tasks.

Feature selection methods can be generally divided into the filter and wrapper approaches. In the filter approach, some features are selected using a statistical or an information-based criterion. In fact, filter methods try to select proper features based on their intrinsic relations. Although ignoring the accessible knowledge (classifier feedback) probably decreases the classification performance, the filter approach's fast execution and classifier independency properties tempt the researchers to use this approach even in the classification tasks. From another perspective, wrapper methods select a subset of features to enhance classification accuracy. In other words, instead of fast filter-based criterion, wrapper methods use the classifier feedback to choose a proper subset of features. Wrapper methods consider the label of samples (prior knowledge) through the feature selection at the cost of a much higher execution time. Recently, a few hybrid approaches have been suggested to combine filter and wrapper approaches for HD samples. These hybrid methods obey a common procedure in which a filter approach is applied to HD samples to reduce their dimension and find features with more relevancies remarkably. Next, a wrapper method is applied to the new instances, which are no more HD. Applying wrappers to such samples speeds up the computations remarkably. It should be considered that the complexity of sequential applying of filter and wrapper must be lower than applying a wrapper solely. Moreover, the combination of filter and wrapper should provide better results than just applying a filter. Preserving these two conditions is not an easy task, and just a few attempts have tackled this issue.


--> [Link of Project ](https://github.com/MohammadAhmadig/Hybrid-and-Wrapper-Feature-Selection-Algorithms---Complete-Package) <--
