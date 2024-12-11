# **YOLOv8 Model Training, Validation, and Testing Report**

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

https://github.com/Takosaga/ai_group_project/blob/main/notebooks/data_sorter_for_model.ipynb

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
https://github.com/Takosaga/ai_group_project/blob/main/notebooks/object_detection_yolov8_training.ipynb

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
https://github.com/Takosaga/ai_group_project/blob/main/notebooks/object_detection_yolov8_training.ipynb

---

### **Step 4: Testing on Unlabeled Data**
- **Process:**
  1. Loaded trained model from `models/yolov8_training/weights/best.pt`.
  2. Ran predictions on `test_set_1` to `test_set_5`:
      - Annotated images saved locally and to GCP.
      - Predictions saved in `predictions.json` files for each dataset.
  3. Calculated metrics:
      - Average confidence, median confidence, and class distribution per dataset.

- **Metrics:**
  - **Test Set 1:**
    - Average Confidence: 0.8067
    - Median Confidence: 0.8511
    - Class Distribution: S (428), V (3564), C (438)
  - **Test Set 2:**
    - Average Confidence: 0.8095
    - Median Confidence: 0.8569
    - Class Distribution: S (419), V (3526), C (447)
  - **Test Set 3:**
    - Average Confidence: 0.8082
    - Median Confidence: 0.8560
    - Class Distribution: S (425), V (3455), C (434)
  - **Test Set 4:**
    - Average Confidence: 0.8087
    - Median Confidence: 0.8579
    - Class Distribution: S (430), V (3601), C (432)
  - **Test Set 5:**
    - Average Confidence: 0.8073
    - Median Confidence: 0.8491
    - Class Distribution: S (443), V (3502), C (420)

### Files
data prep: https://github.com/Takosaga/ai_group_project/blob/main/notebooks/data_sorter_for_unlabeled_data.ipynb
main notebook: https://github.com/Takosaga/ai_group_project/blob/main/notebooks/yolov8_unlabeled_data_testing.ipynb

---

### **Step 5: Visualization of Results**
- Randomly selected 25 annotated images from different datasets.

https://github.com/Takosaga/ai_group_project/blob/main/notebooks/unlabaled_images_annotation.ipynb
---

### **Conclusion**
- The YOLOv8 model demonstrates consistent performance across all test sets, with average confidence scores exceeding 0.8 and stable class distributions.
- The results indicate the model's readiness for deployment on real-world, unlabeled data.

---

### **Next Steps**
- Refine testing pipeline for further datasets.
- Evaluate the model in a production environment to identify areas for improvement.
