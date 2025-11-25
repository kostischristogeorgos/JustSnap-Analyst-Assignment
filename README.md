# JustSnap-Analyst-Assignment


## Project Overview
This project implements a **product matching system** that:  

- Takes **unstructured product descriptions** as input.  
- Extracts **structured attributes** such as size, color, brand, material, season, and year.  
- Finds the **top matching SKUs** from the product catalog.  
- Provides **confidence scores** and alternative matches.
- Uses a **hybrid similarity approach** combining semantic text embeddings with rule-based attribute extraction.  
- Ranks products based on a **weighted scoring system** that balances text similarity and attribute match quality.


**Goal:** Reduce manual matching time, improve inventory tracking, and increase sales by automatically suggesting the most relevant products.

---

## Setup and Installation

1. Install **Python 3.7+** if not already installed.
2. If the notebook is run on colab environment then sentence-transformers and rapidfuzz need to be installed with
   ```bash
   !pip install sentence-transformers
   !pip install rapidfuzz
   ```
3. If the notebook is run on a fresh install, then:
   ```bash
   !pip install pandas numpy scikit-learn matplotlib seaborn rapidfuzz sentence-transformers torch
   ```

---

## How to run the matching system
1. Open the jupyter notebook in the 'Python Files' folder after installing all the libraries.
2. Upload the 3 files in the 'CSV Files' into the environment
3. Run each cell of the notebook

**Note**: The **'test_descriptions.csv'** file contains the descriptions used to test the matching algorithm. You may modify this file with your own descriptions, but be sure to assign the correct label corresponding to the intended matched product from the 'b_product_catalog.csv' file.

---


## Results
After having run the final cell that produces the results, in the **all_results[]** list you will be able to see the output for each description by providing its index.

The format of the list for each item is as follows:

```python
{
    "description_index": 0,  # Index of the description in df_desc_features
    "description": "Looking for green boots, size L.",  # Original unstructured description
    "extracted_attributes": {
        "size": "L",
        "color": "green",
        "season": "Fall 2025",
        "year": "2025",
        "brand": "Nordic",
        "material": "Leather",
        "category": "Footwear",
        "subcategory": "Boots",
        "features": "Waterproof"
    },
    "primary_match": {
        "SKU": "SKU1000037",
        "Product_Name": "Nordic Green Boots",
        "Category": "Footwear",
        "Subcategory": "Boots",
        "Brand": "Nordic",
        "Color": "Green",
        "Size": "L",
        "Material": "Leather",
        "Features": "Waterproof",
        "Season": "Fall 2025",
        "Year": "2025",
        "Price": 125.93,
        "Confidence": "92.50%"
    },
    "top_3_alternatives": [
        {
            "SKU": "SKU1000023",
            "Product_Name": "Nordic Green Sneakers",
            "Category": "Footwear",
            "Subcategory": "Sneakers",
            "Brand": "Nordic",
            "Color": "Green",
            "Size": "L",
            "Material": "Leather",
            "Features": "Quick-dry",
            "Season": "Fall 2025",
            "Year": "2025",
            "Price": 119.50,
            "Confidence": "88.75%"
        },
        {
            "SKU": "SKU1000045",
            "Product_Name": "Premium Green Boots",
            "Category": "Footwear",
            "Subcategory": "Boots",
            "Brand": "Premium",
            "Color": "Green",
            "Size": "L",
            "Material": "Suede",
            "Features": "Waterproof",
            "Season": "Fall 2025",
            "Year": "2025",
            "Price": 140.20,
            "Confidence": "85.30%"
        },
        {
            "SKU": "SKU1000021",
            "Product_Name": "Elite Green Boots",
            "Category": "Footwear",
            "Subcategory": "Boots",
            "Brand": "Elite",
            "Color": "Green",
            "Size": "L",
            "Material": "Leather",
            "Features": "Breathable",
            "Season": "Fall 2025",
            "Year": "2025",
            "Price": 130.00,
            "Confidence": "82.00%"
        }
    ]
}
```
**Notes**:

1. **primary_match** is the top **recommended SKU**.

2. **top_3_alternatives** are the next **3 most probable matches**.

3. **Confidence** combines cosine similarity + attribute boosts, expressed as a percentage.

4. **extracted_attributes** are parsed from the unstructured description.

**The results are stored in 'results_from_test_descriptions.json' file where they can be views independently**, the notebook also provides visualizations for the confidence distribution and error analysis per category. 
