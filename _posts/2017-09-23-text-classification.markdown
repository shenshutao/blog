---
layout: post
title: "Text Classification"
date:   2017-09-23 10:06:46 +0800
categories: machine learning
---

# 1. Brief
Categorization system automatically classify the category of the text.

# 2. Common Usage
- Assigning subject categories to documents
> <img src="{{ site.baseurl }}/img/tc01.png" alt="tc01" style="width: 500px;"/>

- Email spam detection
> As gmail will block a lot of junk mail for us.

- Medical diagnosis
- Identifying a language (before further processing)
- Etc.

# 3. How does automatic text categorization work ?
#### Phase one - Training – creating the text “classifier” (automatic categorization engine)
- You need a set of documents, already categorized
- Divide the set into training (typically 70%) and testing (30%)
- Build your classifier such that it’s able to accurately classify the training
	- set of documents to your level of comfort
	- “level of comfort” depends on how hard is the task!  
- Evaluate your classifier on the test set  ensure sufficient accuracy

#### Phase two - Running – using your classifier on new sets of documents
- You will not know how well it performs
- Need to “audit” the results occasionally (use an assessor)
	- Assess random sample of the documents against the predicted categories

# 4. Classifiers
#### Hand-coded classifiers (the “good old days!”)
> If <conditions> then <category> else NOT<category>

#### Probabilistic Classifiers

#### Decision Tree Classifiers
> Decide if a name is male or female.    
> <img src="{{ site.baseurl }}/img/tc02.png" alt="tc02" style="width: 500px;"/>   
> From: http://nltk.googlecode.com/svn/trunk/doc/book/ch06.html

#### The Rocchio Classifiers

#### Support Vector Machines (SVMs)

# 5. Evaluation
> Confusion Matrix.  
> <img src="{{ site.baseurl }}/img/tc03.png" alt="tc03" style="width: 400px;"/>   
> Look at matrixs from two classifiers as below, which classifier is better ?    
> <img src="{{ site.baseurl }}/img/tc04.png" alt="tc04" style="width: 800px;"/>    
> Answer is: Depends, different businesses will have different opinions.


# 6. Running the classifier
- Avoid overfitting
- Hard and Soft Categorization    
  Soft Categorization as below:    

>Rank | Category | Probability
----|------|----
1 | Z  | 0.76
2 | X  | 0.72
3 | Y  | 0.54


# 7. Unsupervised text categorization
Input variables without label. No categories are given to the machine, machine figure it out.    
Such as clustering below.

# 8. Document clustering
Samples on youtube:
- https://www.youtube.com/watch?v=CHlrx4gsoJI
- https://www.youtube.com/watch?v=Z-4S7kIoHa8 


# 9. Topic modeling
Sample on youtube: classify wikipidia topic from the article content, link as below.    
- https://www.youtube.com/watch?v=3mHy4OSyRf0 