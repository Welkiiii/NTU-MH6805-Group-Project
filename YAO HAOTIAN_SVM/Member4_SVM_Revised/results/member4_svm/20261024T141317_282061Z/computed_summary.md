**Main SVM selected by training CV:** RBF. Fixed-test native-margin AP = 0.3483; ROC-AUC = 0.7669.

At the training OOF margin threshold 0.318854, test precision = 0.3117, recall = 0.6021, and F1 = 0.4107. For comparison, the original default margin-zero recall = 0.7801 and F1 = 0.4194.

**Separate sigmoid ensemble:** calibrated AP = 0.3510, Brier score = 0.1161, ECE = 0.0083. Probability scenarios are descriptive and do not select a policy.

**With Month (original):** earlier-month CV selected RBF; Nov-Dec AP = 0.3107, ROC-AUC = 0.6371. This result does not replace the main fixed-split model.

**Without Month (control):** earlier-month CV selected RBF; Nov-Dec AP = 0.3030, ROC-AUC = 0.6425. This result does not replace the main fixed-split model.
