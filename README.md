# residue-interaction-project
Residue Interaction Networks are derived from protein structures based on geometrical and physico-chemical properties of the amino acids. RING (https://ring.biocomputingup.it/) is a software that takes a PDB (https://www.rcsb.org/) file as input and returns the list of contacts (residue-residue pairs) and their types in a protein structure. RING contact types include:

●	Hydrogen bonds (HBOND)
●	Van der Waals interactions (VDW)
●	Disulfide bridges (SBOND)
●	Salt bridges (IONIC)
●	π-π stacking (PIPISTACK) 
●	π-cation (PICATION)
●	Unclassified contacts

Together with my colleague we developed a software that can predict the RING classification of a contact based on statistical or supervised methods, rather than geometrical constraints. The program should is able to calculate the propensity (or probability) of a contact belonging to each of the different contact types defined by RING, starting from the protein structure. I was mostly responsible for developing the AI predictor and my collegue modified a repository of codes and created the command cotrol launcher of the software

description of the training 
Introduction:
Here we have implemented a multiclass classifier deep neural network (DNN) model to predict the contact types (residue-residue interactions) in a protein structure based on statistical data extracted from proteins PDB file.

Dataset and Preparation and Preprocessing:
1807 TSV formatted file with each containing 33 features, broadly categorized into source residue identifier and features , target residue Identifier and features and one target column , Interaction; containing both numerical and categorical features.
Given the volume of the data points, 2.333.422 to be exact, using the One hot encoding or other measures of transforming the categorical features were unfeasible as they would’ve resulted in a practically intractable size for our dataset, therefore we only used the numerical features.
Our target is comprised of seven values, namely 'HBOND', 'VDW', nan, 'PIPISTACK', 'SSBOND', 'IONIC', 'PICATION'
Missing values of our features were filled with median value and in the target (nan) were replaced by “NI” as in Not Included since they were representing our unclassified group.
Since our targets were in string values the values were transformed into numericals and back to string for training and representation purposes respectively.
Due to the massive imbalance in our dataset which would’ve resulted in a distorted training process, over sampling of small classes performed.


description of model :

20 percent of the data was put aside for testing a further 20 percent was put aside from the remaining 80 percent for validation that resulted in the following data proportions and numbers:
Training = 64% validation: 16% and testing: 20%

•	A four layer deep neural networks was used with the following properties:
structure and dimensions excluding the input:  512, 256, 128, 7
•	Activation functions : relu for hidden layers and Softmax for the output as soft max produces class probability for each class which was required for this project
•	Loss = sparse_categorical_crossentropy, optimization technique: Adam (l=1e-3)
•	Regularization techniques for better generalization: dropout rate of 0.5 for each hidden layer and l1_l2 regularization with respective learning rates of 1e-5, 1e-4.
•	Two fold cross validation and 20 epochs
Since the volume of the data would’ve increased training time impractically for more cross validation 2 was used.


Results:
Several performance measures were calculated. Precision, Recall and F1 score for individual classes were measured. Overall model performance is shown by Mathew’s correlation coefficient, average balanced accuracy and average ROC AUC score
Macro avg and weighted avg were also measured 
Following is the performance on test set
29168/29168 [==============================] - 109s 4ms/step
29168/29168 [==============================] - 91s 3ms/step
Average Matthews correlation coefficient: 0.7615310228550466
Average Balanced Accuracy: 0.7945011960210235
Average ROC AUC Score: 0.9496070315674514
14584/14584 [==============================] - 43s 3ms/step
              precision    recall  f1-score   support

       HBOND       0.70      0.61      0.66     66669
       IONIC       0.88      1.00      0.93     66669
          NI       0.53      0.56      0.54     66669
    PICATION       0.92      1.00      0.96     66670
   PIPISTACK       0.91      1.00      0.95     66669
      SSBOND       0.99      1.00      1.00     66669
         VDW       0.53      0.39      0.45     66670

    accuracy                           0.79    466685
   macro avg       0.78      0.79      0.78    466685
weighted avg       0.78      0.79      0.78    466685
