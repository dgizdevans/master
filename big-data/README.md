# **BD_project_v2: Analyzing E-commerce Product Data**

This repository contains the coursework project for the **Big Data Analytics and Applications** module. The project demonstrates how to leverage Google Cloud Platform (GCP) tools for processing, analyzing, and visualizing large datasets. The main focus is on analyzing the relationship between product image quality and customer ratings, while showcasing the practical application of cloud-based big data solutions.

---

## **Project Overview**

The objective of this project is to explore the potential of GCP in handling real-world big data problems. The project workflow includes:

1. **Data Collection and Preparation**:
   - Sourced from the [Amazon Products Dataset](https://www.kaggle.com/datasets/lokeshparab/amazon-products-dataset) on Kaggle.
   - Cleaned and transformed using GCP services like Dataflow and BigQuery.

2. **Semi-Structured Data Management**:
   - Transformed product metadata and image quality scores into JSON format.
   - Stored in Firestore for real-time access and flexible querying.

3. **Ontology Creation**:
   - Developed using relationships exported from Cloud SQL and visualized with tools like Graphviz and Neo4j.

4. **Data Analysis**:
   - Performed correlation analysis between image quality and customer ratings.
   - Used BigQuery ML for machine learning directly within the database.

5. **Challenges and Solutions**:
   - Overcame service integration issues with Colab and debugging complexities using robust logging mechanisms.
   - Demonstrated the scalability and flexibility of GCP for data projects.

---

## **Key Findings**

- A moderate positive correlation (0.62) was observed between image quality and customer ratings.
- Semi-structured data enabled real-time access and integration with structured data workflows.
- BigQuery ML significantly simplified machine learning operations without requiring external transformations.

---

## **Tech Stack**

### **Google Cloud Platform Services**:
- **BigQuery**: For structured data querying and ML operations.
- **Dataflow**: For data cleaning and transformation.
- **Firestore**: For managing semi-structured data.
- **Cloud SQL**: For relational database management.
- **Cloud Run**: For deploying the image quality assessment model.

### **Python Libraries**:
- **Data Processing**: `Pandas`, `NumPy`
- **Ontology Tools**: `rdflib`, `sqlalchemy`
- **Visualization**: `Graphviz`, `NetworkX`
- **Cloud Integration**: `google-cloud-*` libraries

