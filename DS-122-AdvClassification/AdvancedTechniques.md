# Advanced Methods
## Working with Imbalanced Data Sets
When working with imbalanced data sets we can run into:
- Accuracy Paradoxon: 97% of the samples are classified with 1 and only 3% with 0 then an algorithm that classifies all samples as 1 has a 97% accuracy. 
We can either resample or rethink the problem to circumvent this problem. 

- Accuracy: How close is a set of given measures to their true value (bias or inaccuracy)
- Precision: How close are the given measures to each other (?) (variablility or imprecision) -. Habe ich noch nicht verstanden

For imbalanced classification the geometric mean is a good measure. It is the sqrt of specificity and sensitivity.
To evaluate there is imblearn.metrics. 

### Resampling methods:
Oversampling is often used on its own. Undersampling is discouraged to be used alone. The best results are obtained with combinations of the two strategies. 
First Undersample the majority class and then oversample the result. 

### Oversampling:
Create new instances of the minority class by duplication. 
This may lead to huge data sets and increase the time of training. 
Also it is prone to overfitting the training data as samples are presented more often
Use cases: Fraud detection, medical diagnosis, image classification
Algorithms: All are found in imblearn.over_sampling
- Random sampling
- SMOTE: Generates synthetic samples by interpolating between neighbouring instances. Helps to prevent overfitting. 
    - ADASYN: Extension of SMOTE where more samples are generated in sparse regions
    - Borderline-SMOTE: Generates samples at the decision boundary only
- SDA: Generates synthetic samples through data augmentation techniques like rotation, flipping and translation

### Undersampling:
Remove lots of samples from the majority class. 
This decreases training time. 
However, important information of the main class may be lost. 
Use cases: Text classification, credit scoring, anomaly detection
Algorithms:
- Random under sampling
- Tomek Link: Answer to CNN
- Edited nearest neighbours
- One-sided selection
- Condensed NN: Disadvantages: Initially random samples. -> Allow redundancy and select from the inside of the set not on the decision border 

TODO: How to include code?
from imblearn.over_sampling import RandomOverSampler, SMOTE
from imblearn.under_sampling import RandomUnderSampler,  ClusterCentroids
from imblearn.metrics import classification_report_imbalanced, geometric_mean_score


## Model Selection
- Time and Storage are the main determining factors as well as the structure of the data and interpretability. 
- Linear data -> Linear method like linear SVM or logistic regression

Workflow: 
Divide into train, validation and testing data.
Select model and Hyperparams on training data. 
Train selected model with best HP on training + validation and evaluate on test

Nested Cross-validation for model selection:
- For model selection it is not as important to have optimal parameters but to choose a model that generalises well -> Small change to different training sets. 
    1. Divide the data into a training set and a test set.
    2. Perform k-fold cross-validation on the training set, where k is typically set to 5 or 10.
    3. For each fold, divide the data into a training set and a validation set.
    4. Train a set of candidate models on the training set, using different hyperparameters for each model.
    5. Evaluate the performance of each model on the validation set.
    6. Select the model with the best performance on the validation set.
    7. Use the selected model to predict the test set.
    8. Repeat steps 2-7 for each fold of the outer loop.
    9. Calculate the average performance of the selected model across all folds of the outer loop.
    10. CV selected model for best parameters
    11. Train model with best parameters. 

TODO: Make a ipynb where I have an example of a nested cross validation. It looks complicated. 

## Semi-Supervised
sklearn.semi_supervised
	- LabelSpreading

sklearn.metrics
	- kohens kappa

The general idea of semi-supervised learning is to enrich a labeled data set with unable data that Is widely available. So it is especially useful in situations where data is abundant but labelling is expensive. 
(e.g. sentiment analysis.)

The typical workflow is: Train model on labeled data. Use the model to predict the labels of the unlabelled data. Then train the model on the labelled data and relabel. Repeat until you are happy with the results. 

Preprocessing: 
- Assign Label -1 to unlabelled data. 

Label Spreading
1. The algorithm starts by creating a graph representation of the data, where each data point is represented as a node in the graph. The edges between the nodes are determined by the similarity between the data points, where similar points are connected by an edge.
2. The labeled data points are assigned their corresponding labels, and the unlabeled data points are assigned a default label.
3. The algorithm then propagates the labels from the labeled data points to the unlabeled data points through the graph. The propagation process is based on the similarity between the connected nodes and the labeled data points.
4. The propagation process is repeated iteratively until the labels for all data points converge to a stable state.
5. Once the labels have converged, the algorithm uses the labeled data points and their corresponding labels to train a classifier, which can be used to predict the labels for new, unseen data points.
Label Propagation

Evaluation:
TODO: Kohens Kappa

## Unsupervised

Mostly used for compression and clustering

Anomaly detection vs Novelty Detection: 
- Anomaly focuses on identifying outliers within the training data while novelty detection assumes the training data to be uncontaminated and detects new data points to be an outlier. 
Anomaly Detection:
- Is an unsupervised algorithm. No labels are used for the prediction. However, they can be used for the evaluation.
- Single out events that are outliers. Difference to imbalanced data sets: in IBDS we have labels and we know one class is underrepresented. Here we do not have labels and want to predict which samples are outliers. 
- Isolation Forest: 
    - Choose a random feature and a random threshold. Divide samples accordingly. Repeat until all points isolated or a certain max depth is reached. Outliers are those that have a short path. 
    - Assumption: It is easier to isolate outliers. 
    - Advantages: Efficient for complex data sets as only a small number of features is considered. 
    - Pythonfrom sklearn.ensemble import IsolationForest

Novelty Detection:
- Novelty Detection
- One Class SVM

Other Novelty detection algorithms include:
- Elliptic Envelope and 
- Local Outlier Factor.

