There are 6 folders with scripts and results, corresponding to each dataset: Explainer_Abalone, Explainer_Diabetes, Explainer_Fetal, Explainer_Hepatitis, Explainer_Liver, Explainer_Water.
They contain the following Python scripts:

- LIME_Anchor_LOOCV_name_of_the_dataset.ipynb: generates predictions and explanations for the LIME and Anchors methods using Leave-One-Out Cross-validation and saves the results in the output_name_of_the_dataset_AnchorLOOCV_100_99thr.xlsx and output_name_of_the_dataset_LIMELOOCV_100.xlsx files

- TreeSHAP_name_of_the_dataset.ipynb: generates predictions and explanations for the TreeSHAP method using Leave-One-Out Cross-validation and saves the results in the output_name_of_the_dataset_TreeShapLOOCV_1.xlsx file

- KernelSHAP_name_of_the_dataset.ipynb: generates predictions and explanations for the KernelSHAP method using Leave-One-Out Cross-validation and saves the results in the output_name_of_the_dataset_KernelShapLOOCV_1.xlsx file

- AlignRankingsName_of_the_dataset_.ipynb: generates rankings using formulas (3) and (4) starting from the feature attribution scores saved in the files: output_name_of_the_dataset_LIMELOOCV_100.xlsx, output_name_of_the_dataset_AnchorLOOCV_100_99thr.xlsx, output_name_of_the_dataset_TreeShapLOOCV_1.xlsx, output_name_of_the_dataset_KernelShapLOOCV_1.xlsx.
The rankings are saved in the files: rankingsName_of_the_dataset_KernelShap.xlsx, rankingsName_of_the_dataset_TreeShap.xlsx, rankingsName_of_the_dataset_LIME.xlsx, rankingsName_of_the_dataset_Anchor.xlsx.
For scheme R (Rankings), we used a vector containing only the rankings.
For each instance from the dataset, we aligned the matrices M_Anchors, M_LIME and M_SHAP in a pairwise fashion using the cluster-based Global Alignment approach and then we calculated the GAME metric for each pair (Anchors-Anchors, Anchors-LIME, Anchors-SHAP, LIME-Anchors, LIME-LIME, LIME-SHAP, SHAP-Anchors, SHAP-LIME, SHAP-SHAP).
For each dataset, the GAME scores have been stored in a .xlsx file having 9 columns (for each GAME value corresponding to the pairwise combinations of explainers - Anchors-Anchors, Anchors-LIME, Anchors-SHAP, LIME-Anchors, LIME-LIME, LIME-SHAP, SHAP-Anchors, SHAP-LIME, SHAP-SHAP) and a number of rows equal to the number of instances from the dataset. The file is called resultsRankingsName_of_the_dataset_MSPMS.xlsx

- AlignSignsName_of_the_dataset_.ipynb: extracts the signs (0 or 1) from the feature attribution vectors saved in the files: output_name_of_the_dataset_LIMELOOCV_100.xlsx, output_name_of_the_dataset_TreeShapLOOCV_1.xlsx, output_name_of_the_dataset_KernelShapLOOCV_1.xlsx.
The signs are saved in the files: signsName_of_the_dataset_KernelShap.xlsx, signsName_of_the_dataset_TreeShap.xlsx, signsName_of_the_dataset_LIME.xlsx.
For scheme R (Rankings), we used a vector containing only the signs.
For each instance from the dataset, we aligned the matrices M_LIME and M_SHAP in a pairwise fashion using the cluster-based Global Alignment approach and then we calculated the GAME metric for each pair (LIME-LIME, LIME-SHAP, SHAP-LIME, SHAP-SHAP).
For each dataset, the GAME scores have been stored in a .xlsx file having 9 columns (for each GAME value corresponding to the pairwise combinations of explainers - LIME-LIME, LIME-SHAP, SHAP-LIME, SHAP-SHAP) and a number of rows equal to the number of instances from the dataset. The file is called resultsSignsName_of_the_dataset_MSPMS.xlsx

- AlignSignsRankingsName_of_the_dataset_.ipynb: extracts the signs (0 or 1) and generates rankings using formulas (3) and (4) from the feature attribution vectors saved in the files: output_name_of_the_dataset_LIMELOOCV_100.xlsx, output_name_of_the_dataset_TreeShapLOOCV_1.xlsx, output_name_of_the_dataset_KernelShapLOOCV_1.xlsx.
The signs & rankings are saved in the files: signs_rankingsName_of_the_dataset_KernelShap.xlsx, signs_rankingsName_of_the_dataset_TreeShap.xlsx, signs_rankingsName_of_the_dataset_LIME.xlsx.
For scheme SR (Signs + Rankings), we used a vector containing signs and rankings.
For each instance from the dataset, we aligned the matrices M_LIME and M_SHAP in a pairwise fashion using the cluster-based Global Alignment approach and then we calculated the GAME metric for each pair (LIME-LIME, LIME-SHAP, SHAP-LIME, SHAP-SHAP).
For each dataset, the GAME scores have been stored in a .xlsx file having 9 columns (for each GAME value corresponding to the pairwise combinations of explainers - LIME-LIME, LIME-SHAP, SHAP-LIME, SHAP-SHAP) and a number of rows equal to the number of instances from the dataset. The file is called resultsSignsRankingsName_of_the_dataset_MSPMS.xlsx

- CalculateRankingsName_of_the_dataset_.ipynb: for the R (Rankings) scheme, calculates the explainer confidence vector A and the  consensus feature attribution weight vectors. It has as input the file resultsRankingsName_of_the_dataset_MSPMS.xlsx and the files containing rankings: rankingsName_of_the_dataset_LIME.xlsx, rankingsName_of_the_dataset_Anchor.xlsx, rankingsName_of_the_dataset_KernelSHAP.xlsx, rankingsName_of_the_dataset_TreeSHAP.xlsx.
We weighted the feature space of a k-NN classifier with the aligned importance of each feature and compared the prediction accuracy against a non-weighted k-NN classifier. 
We tested the k-NN (k = 5) algorithm using the following feature overlap explanation weights:
	R_AVG – the mean of rankings. When computing R_AVG, in equation (9), the explainer confidence vector A contained only values of 1. 
	R_FI – the mean of feature importances as obtained from the XGBoost classifier using the feature_importances_ function from the xgboost Python library. 
	R_AVG_FI – the mean of rankings multiplied by the mean of feature importances
	R_A – the mean of rank alignments obtained from the Global Alignment Measurement described in subchapter 4.6.
	R_A_FI – the mean of rank alignments obtained from the Global Alignment Measurement described in subchapter 4.6., multiplied by the mean of feature importances as obtained from the XGBoost classifier using the feature_importances_ function from the xgboost Python library.
The following files have been generated with results:
Rankings_accuraciesName_of_the_dataset__50_AverageRankings.xlsx
Rankings_accuraciesName_of_the_dataset__50_AverageRankingsFeatureImportance.xlsx
Rankings_accuraciesName_of_the_dataset__50_FeatureImportance.xlsx
Rankings_accuraciesName_of_the_dataset_MSPMS_50_Align.xlsx
Rankings_accuraciesName_of_the_dataset_MSPMS_50_AlignFeatureImportance.xlsx

- CalculateSignsName_of_the_dataset_.ipynb: for the S (Signs) scheme, calculates the explainer confidence vector A and the  consensus feature attribution weight vectors. It has as input the file resultsSignsName_of_the_dataset_MSPMS.xlsx.
We weighted the feature space of a k-NN classifier with the aligned importance of each feature and compared the prediction accuracy against a non-weighted k-NN classifier. 
We tested the k-NN (k = 5) algorithm using the following feature overlap explanation weights:
S_A – the mean of sign alignments obtained from the Global Alignment Measurement described in subchapter 4.6.
S_A_FI - the mean of sign alignments obtained from the Global Alignment Measurement described in subchapter 4.6., multiplied by the mean of feature importances as obtained from the XGBoost classifier using the feature_importances_ function from the xgboost Python library
The following files have been generated with results:
Signs_accuraciesName_of_the_dataset_MSPMS_50_Align.xlsx
Signs_accuraciesName_of_the_dataset_MSPMS_50_AlignFeatureImportance.xlsx

- CalculateSignsRankingsName_of_the_dataset_.ipynb: for the SR (Signs + Rankings) scheme, calculates the explainer confidence vector A and the  consensus feature attribution weight vectors. It has as input the file resultsSignsRankingsName_of_the_dataset_MSPMS.xlsx.
We weighted the feature space of a k-NN classifier with the aligned importance of each feature and compared the prediction accuracy against a non-weighted k-NN classifier. 
We tested the k-NN (k = 5) algorithm using the following feature overlap explanation weights:
	SR_A – the mean of the vector containing rank and sign alignments obtained from the Global Alignment Measurement described in subchapter 4.6.
	SR_A_FI - the mean of the vector containing rank and sign alignments obtained from the Global Alignment Measurement described in, multiplied by the mean of feature importances as obtained from the XGBoost classifier using the feature_importances_ function from the xgboost Python library.
The following files have been generated with results:
SignsRankings_accuraciesName_of_the_dataset_MSPMS_50_Align.xlsx
SignsRankings_accuraciesName_of_the_dataset_MSPMS_50_AlignFeatureImportance.xlsx

Reviewer 1 asked us to make a comparison with the with a weighted algorithm where the weights are produced by a single explanation method.  To make a comparison with LIME, SHAP and Anchors, the following files have been added:
CalculateRankingsName_of_the_dataset_-Anchor.ipynb
CalculateRankingsName_of_the_dataset_-LIME.ipynb
CalculateRankingsName_of_the_dataset_-SHAP.ipynb
CalculateSignsName_of_the_dataset_-LIME.ipynb
CalculateSignsName_of_the_dataset_-SHAP.ipynb
CalculateSignsRankingsName_of_the_dataset_-LIME.ipynb
CalculateSignsRankingsName_of_the_dataset_-SHAP.ipynb

They generated the following files with results (accuracy, F1-score and ROC-AUC score) to show that aggregating the explanations works, by comparing with a weighted algorithm where the weights are produced by a single explanation method (either LIME, SHAP or Anchors):
Rankings_accuraciesName_of_the_dataset_MSPMS_Anchor_50.xlsx
Rankings_accuraciesName_of_the_dataset_MSPMS_LIME_50.xlsx
Rankings_accuraciesName_of_the_dataset_MSPMS_Shap_50.xlsx
Signs_accuraciesName_of_the_dataset_MSPMS_LIME_50.xlsx
Signs_accuraciesName_of_the_dataset_MSPMS_Shap_50.xlsx
SignsRankings_accuraciesName_of_the_dataset_MSPMS_LIME_50.xlsx
SignsRankings_accuraciesName_of_the_dataset_MSPMS_Shap_50.xlsx

The Statistics folder contains scripts for statistics tests (Friedman Chi Square and Wilcoxon signed-rank - as we performed multiple tests, we applied the Holm-Bonferroni correction method, that is fairly simple to implement and more powerful than the single-step Bonferroni) and for generating various plots to highlight the results. 

The results_correction.xlsx file presents a summary of the results for comparing the accuracy, F1-score and ROC-AUC score of the feature weighted k-NN algorithm to the non-weighted k-NN algorithm.

The files results_Shap.xlsx, results_Anchors.xlsx, results_LIME.xlsx present a summary of the results for comparing the accuracy, F1-score and ROC-AUC score of the feature weighted k-NN algorithm where the feature were represented by aggregated weights to the feature weighted k-NN algorithm where the weights are obtained from a single explanation method.
