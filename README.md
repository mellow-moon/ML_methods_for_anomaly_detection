# ML_methods_for_anomaly_detection

Anomaly detection using K-Means, Isolation Forest, SVM and LOF.

# Dataset

In this project we will use dataset with sensor's measurements. One row contains measurements from 50 sensors, time when measurement was taken and machine status in that moment (NORMAL, BROKEN, RECOVERING). Data has 220320 rows and 55 columns.

First we need to clean the data.

Columns sensor 15 and unnamed is unnecessary so we will drop them.

<img src="img/sensor15_unnamed.png" width="800"/>

Next let's calculate the percentage of missing values.

<img src="img/missing_percantage.png" width="800"/>

We can see that sensor 50 has too many missing values, so we will drop that.

<img src="img/sensor50_drop.png" width="800"/>

After that we will convert our timestamp column to datetime and use it as index.

<img src="img/datetime_index.png" width="800"/>

# Explorational Data Analysis

Let's take a look at distribution of machine status column in our data. We can see that the majority of our data is normal data and we have only 7 broken examples.

<img src="img/machine_status_count.png" width="800"/>

# Scaling Data and Dimensionality Reduction

First we want scale the data and reduce dimensionality of the data to pass it to our models. To do that we will use StandardScaler and PCA.

<img src="img/standardscaler.png" width="800"/>

We will calculate PCA with 2 components according to importance of PCA components.

<img src="img/pca.png" width="800"/>

Let's also make autocorreleation plot.

<img src="img/autocorr.png" width="800"/>

# Model-1 - K-Means Clusting

We will use K-Means model to cluster our data. Then we will calculate the distances between every point and centroid of a cluster. After that we will choose a threshold. If distance is above that threshold we will mark it as anomaly.

<img src="img/k-means_import.png" width="800"/>

Let's plot our clusters.

<img src="img/k-means_clusters.png" width="800"/>

Next we need to calculate the distances and choose a threshold. We assume that 13% of the entire data set are anomalies. As the threshold we will take the minimum of the largest 13% of the distances.

<img src="img/distance_calc.png" width="800"/>

Now we can plot K-Means anomalies.

<img src="img/kmmeans_anomaly_plot.png" width="800"/>

# Model-2 - Isolation Forest

Isolation Forest will mark our data as normal and anomaly. Let's see the output prediction of a model (1:normal, -1:anomaly).

<img src="img/if_model.png" width="800"/>

Let's plot Isolation Forest anomalies.

<img src="img/if_anomaly_plot.png" width="800"/>

# Model 3 - One Class SVM

We will use One Class SVM with parameters: kernel = 'rbf', gamma = 0.001, nu = 0.13. Let's see the output prediction of a model (1:normal, -1:anomaly).

<img src="img/svm_model.png" width="800"/>

Let's plot One Class SVM anomalies.

<img src="img/svm_anomaly_plot.png" width="800"/>

# Model 4 - LOF

We will use LocalOutlierFactor with parameters: n_neighbors = 50, metric = 'manhattan', contamination = 0.13. Let's see the output prediction of a model (1:normal, -1:anomaly).

<img src="img/lof_model.png" width="800"/>

Let's plot LOF anomalies.

<img src="img/lof_anomaly_plot.png" width="800"/>

# Models evaluation

Next we will calculate some metrics to see how well the models work. We will calculate precision, recall, f1-score, AUC for every model and plot a Confusion Matrix.

# K-Means

# Classification Report

<img src="img/k-means_report.png" width="800"/>

# Confusion Matrix

<img src="img/k-means_confusion_matrix.png" width="800"/>

# Roc Curve

<img src="img/k-means_auc.png" width="800"/>

# Isolation Forest

# Classification Report

<img src="img/if_report.png" width="800"/>

# Confusion Matrix

<img src="img/if_confusion_matrix.png" width="800"/>

# Roc Curve

<img src="img/if_roc_auc.png" width="800"/>

# One Class SVM

# Classification Report

<img src="img/one_clss_svm_report.png" width="800"/>

# Confusion Matrix

<img src="img/one_clss_svm_confusion_matrix.png" width="800"/>

# Roc Curve

<img src="img/one_clss_svm_roc_auc.png" width="800"/>

# LOF

# Classification Report

<img src="img/lof_report.png" width="800"/>

# Confusion Matrix

<img src="img/lof_confusion_matrix.png" width="800"/>

# Roc Curve

<img src="img/lof_roc_auc.png" width="800"/>

# Hyperparameter tuning

As we can see LOF AUC = 0.67. Let's try to increase LOF value. We will try to train LOF models with different parameters to find best model.

<img src="img/lof_tuning_parameters.png" width="800"/>

Let's calculate precission, recall, f1-score, ROC AUC score and make a dataframe with parameters and metrics.

<img src="img/lof_best_model_calc.png" width="800"/>

# Classification Report for best LOF

<img src="img/lof_best_report.png" width="800"/>

# Confusion Matrix for best LOF

<img src="img/lof_best_confusion_matrix.png" width="800"/>

# Roc Curve for best LOF

<img src="img/lof_best_roc_auc.png" width="800"/>

LOF value increased from 0.67 to 0.69.
