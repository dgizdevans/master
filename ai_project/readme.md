# **YOLOv8 Model Training, Validation, and Testing Report**

---

## **Introduction**
This report details the process and results of YOLOv8 model training, validation, and testing, along with the evaluation of augmented data to improve the model's performance. The goal is to compare the model trained with standard data to the one trained with augmented data for detecting three classes: **Passenger Vehicles (V)**, **Cargo Vehicles (C)**, and **Buses (S)**.

---

## **Step 1: Data Preparation**
### Objective
Prepare labeled data for training, validation, and testing the YOLOv8 model.

### Tasks
- Raw data collected and uploaded to **Google Cloud Platform (GCP)**.
- Manual annotation of a subset of data using **CVAT**, focusing on three classes:
  - **Passenger Vehicles (V)**  
  - **Cargo Vehicles (C)**  
  - **Buses (S)**  
- Labeled data split into:
  - **Train**: 60%
  - **Validation (Val)**: 20%
  - **Test**: 20%
- Data formatted to YOLO-compatible structure:
  - `images/` and `.txt` annotation files.

### Files
[data_sorter_for_model.ipynb](https://github.com/dgizdevans/master/blob/main/ai_project/data_sorter_for_model.ipynb)

---

## **Step 2: Model Training**
### Objective
Train YOLOv8 to detect three classes (V, C, S) using labeled data.

### Process
- Pre-trained YOLOv8 weights were loaded for transfer learning.
- Training conducted with the following parameters:
  - **Epochs**: 50  
  - **Image Size**: 640x640  
  - **Batch Size**: 16  
  - **Optimizer**: AdamW  
- Intermediate results saved to GCP during training.

### Outcome
- Trained model (`best.pt`) saved for further evaluation.

### Files
[object_detection_yolov8_training.ipynb](https://github.com/dgizdevans/master/blob/main/ai_project/object_detection_yolov8_training.ipynb)

---

## **Step 3: Validation**
### Objective
Validate the trained YOLOv8 model on the validation dataset to ensure generalization.

### Process
- The `val` dataset was used to calculate metrics:
  - **Precision**  
  - **Recall**  
  - **mAP@0.5**  
  - **mAP@0.5:0.95**  
- Metrics displayed in the notebook and saved as part of the validation output.

### Outcome
Validation confirmed the model's ability to generalize, with **mAP@0.5 exceeding 80%** across classes.

### Files
[object_detection_yolov8_training.ipynb](https://github.com/dgizdevans/master/blob/main/ai_project/object_detection_yolov8_training.ipynb)

---

## **Step 4: Testing on Unlabeled Data**
### Objective
Evaluate the trained YOLOv8 model on unlabeled datasets to assess its generalization capabilities.

### Process
1. Loaded the trained model from `models/yolov8_training/weights/best.pt`.
2. Ran predictions on unlabeled datasets (`test_set_1` to `test_set_5`).
3. Calculated metrics such as average confidence, median confidence, and class distributions.

### Results
| **Test Set** | **Average Confidence** | **Median Confidence** | **Standard Deviation** |  
|--------------|-------------------------|------------------------|-------------------------|  
| Test Set 1   | 0.8067                 | 0.8511                | 0.1317                 |  
| Test Set 2   | 0.8095                 | 0.8569                | 0.1301                 |  
| Test Set 3   | 0.8082                 | 0.8560                | 0.1321                 |  
| Test Set 4   | 0.8087                 | 0.8579                | 0.1323                 |  
| Test Set 5   | 0.8073                 | 0.8491                | 0.1303                 |  

### Files
[data_sorter_for_unlabeled_data.ipynb](https://github.com/dgizdevans/master/blob/main/ai_project/data_sorter_for_unlabeled_data.ipynb)  
[yolov8_unlabeled_data_testing.ipynb](https://github.com/dgizdevans/master/blob/main/ai_project/yolov8_unlabeled_data_testing.ipynb)

---

## **Step 5: Perform Data Augmentation**
### Objective
Augment training data to evaluate if it improves model performance.

### Outcome
Augmented training dataset created and backed up for retraining.

### Files
[yolov8_augmented_model_training_and_evaluation.ipynb](https://github.com/dgizdevans/master/blob/main/ai_project/yolov8_augmented_model_training_and_evaluation.ipynb)

---

## **Step 6: Augmented Model Training and Evaluation**
### Objective
Train a new YOLOv8 model on the augmented data and evaluate it using the same methodology.

### Outcome
The augmented model showed the following performance improvements:
- **Confidence Improvement**:  
  - Average Confidence increased across all test sets by approximately 2.2% to 2.3%.  
  - Median Confidence also saw improvements of around 2.0% to 2.2%.  
- **Reduced Variability**:  
  - Standard Deviation decreased by 5.5% to 6.5%.  

### Files
[yolov8_augmented_model_training_and_evaluation.ipynb](https://github.com/dgizdevans/master/blob/main/ai_project/yolov8_augmented_model_training_and_evaluation.ipynb)

---

## **Step 7: Comparative Analysis and Conclusion**
### Objective
Compare the metrics from the baseline and augmented models to evaluate the impact of augmentation.

### Results
| **Metric**           | **Without Augmentation** | **With Augmentation** | **% Change** |  
|-----------------------|--------------------------|------------------------|--------------|  
| Average Confidence    | 0.807                   | 0.826                  | +2.3%        |  
| Median Confidence     | 0.854                   | 0.870                  | +1.9%        |  
| Standard Deviation    | 0.131                   | 0.124                  | -5.3%        |  

### Conclusion
- Data augmentation consistently improved average and median confidence across all test sets while reducing variability.
- Augmentation provides a scalable strategy for improving YOLOv8 performance, especially on real-world datasets.

---

### **Next Steps**
- Investigate multiple augmentation cycles to further improve performance.
- Deploy the augmented model in real-world applications and monitor its efficacy.
