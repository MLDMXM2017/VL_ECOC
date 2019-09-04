VL_ECOC.py:

The files contain the following functions:
1) Distance calculation
	- euclidence_distance(x, y, soft=True): To calculate the Euclidean distance between two points. x and y are the two points; soft if True. It only calculates the distance not 0 coordinate.
	
	- hamming_distance(x, y, soft=True): To calculate the hamming distance between two points. x and y are the two points; soft if True. It only calculates the distance not 0 coordinate.
	
2) image drawing 
	- plot_matrix(save_path, matrix_list, matrix_column_accuracy_list, ylabel=None): matrix_list is the coding matrix in different stages,  matrix_column_accuracy_list is the accuracy of each column. y_label is to specify the ordinate label.
	
	- plot_confusion_matrix(save_path, predicted_label_list, xlabel=None, ylabel=None): To draw the obfuscation matrices. The first line of predicted_label_list includes the real labels, and the subsequent labels are the prediction results of different stages. xlabel and ylabel are the labels of the horizontal and vertical coordinates, respectively.

	- plot_train_test_metric(save_path,  predicted_train_label_list, predicted_test_label_list, metric=accuracy_score, **metric_param): To plot the change curve of training set and test set with different metric. predicted_train_label_list and predicted_test_label_list are labels of training set and test set, respectively. The first line is the real label, and the subsequent labels are prediction results of different stages. The default metric is accuracy, and metric_param is the parameter of metric.

3) VL_ECOC class 
	- Constructor：__init__(self, data, label, base_classifier=SVC, feature_ratio=0.8, sample_ratio=0.8, accuracy_threshold=0.6, class_level_matrix_threshold=2, sample_level_matrix_threshold=2, save_path=None): Data and label are the data sets to be modeled, which are divided into training set, verification set and test set by the constructor with the partition ratio of 2:1:1. base_classifier is the base classifier used, feature_ratio and sample_ratio are the feature sampling ratio and sample sampling ratio respectively. accuracy_threshold is the accuracy threshold, and the base classifier lower than the accuracy threshold will be discarded. class_level_matrix_threshold and sample_level_matrix_threshold are the thresholds that stop growing after the stability of the two stages, respectively. save_path is where the final model results are stored.

4) Matrix generation 
	- make_matrix(self): It contains the following important functions：
		Seed column generating function： make_seed_column(self)
		The first stage is matrix generation function： make_class_level_matrix(self)
		Add the minimum hamming distance function of the first phase matrix： increase_hamming_distance(self)
		The second stage is matrix generation function： make_sample_level_matrix(self)
		Result visualization function： visualization(self)
		Storing evaluation result function： persistence_record(self)
		
5) runner function
	- Runner is a function used for final running, which mainly accepts the following parameters:
		file_name:Data file name
		data_path:Data storage path
		save_path:Result store path


Execute the following command to run the demo:
	python3.6 VL_ECOC.py


The results are stored in the result dictionary. The UCI datasets are available in UCI_data dictionary. 


The default demo will run 3 iterations for each datasets in the UCI_data dictionary. The result/zoo dictionary consist of all the results. The file description is as follows：
- accuracy.csv: The accuracy for each dataset and each iteration.
	- fscore.csv: The F-score for each dataset and each iteration.
	- matthews.csv: The MCC for each dataset and each iteration.
	- predict_time.csv: The predicted time for each dataset and each iteration.
	- train_time.csv: The training time for each dataset and each iteration.
	- zoo dictionary: The detail result for each iteration of zoo dataset.
	- matrix_record.json and Coding Matrix: The different matrix in the growth process.
	- Test Data Confusion Matrix: The different confusion matrix in the growth process on test dataset.
	- Train Data Confusion Matrix: The different confusion matrix in the growth process on train dataset.
	- Validate Data Confusion Matrix: The different confusion matrix in the growth process on validate dataset.
	- test_predicted_code_record.json: The predicted code in the growth process on test dataset.
	- test_predicted_label_record.json: The predicted label in the growth process on test dataset.
	- train_predicted_code_record.json: The predicted code in the growth process on train dataset.
	- train_predicted_label_record.json: The predicted label in the growth process on train dataset.
	- validate_predicted_code_record.json: The predicted code in the growth process on validate dataset.
	- validate_predicted_label_record.json: The predicted label in the growth process on validate dataset.
	- Validation Test Accuracy.png: The trend of accuracy on validation and test datasets.
	- Validation Test Fscore.png: The trend of F-score on validation and test datasets.
	- Validation Test MCC.png: The trend of MCC on validation and test datasets.


Environement:	- Linux Ubuntu 16.04; 
		- Python3.6;
		- Scikit-Learn 0.18; 

This code is the source code of the paper:
Kai-Jie Feng, Sze-Teng Liong, Kun-Hong Liu, The Design of Variable Length Based Coding Matrix for Improving Error Correcting Output Codes.
