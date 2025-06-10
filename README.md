# Bird-Migration-Stage-Classification

This project focuses on building a machine learning classifier to predict the **migration stage** of birds (e.g., herons and egrets) based on GPS tracking data.

We use features such as location coordinates, movement speed, and time of observation to classify bird behavior into:
- `migrating`
- `resting`
- `foraging`

---

## 📁 Dataset

The dataset consists of timestamped GPS coordinates (`latitude`, `longitude`), and some metadata from bird tracking studies.

**Original Columns Include:**
- `lat`, `lon`
- `eobs:start-timestamp` (recorded timestamp in timedelta format)
- `individual-local-identifier` (unique bird ID)

---

## ⚙️ Project Workflow

### **1. Data Preprocessing**
- Construct a synthetic full datetime column from relative timestamps using a known base date.
- Compute `hour_of_day` and `day_of_year` from datetime for temporal context.
- Calculate movement **speed (km/h)** using haversine distance between successive GPS points.
- Drop rows with missing or incomplete data.

### **2. Visualization**
- Plot bird movement paths on a scatter map using longitude and latitude.
- Color-code paths by migration stage to visually verify stage transitions.

### **3. Feature Engineering**
Final feature set:
- `lat`, `lon`
- `hour_of_day`, `day_of_year`
- `speed_km`

### **4. Model Training**
- Used `RandomForestClassifier` to classify the migration stage.
- Dataset was split into training and testing sets (e.g., 80-20 split).
- Model was evaluated using a **confusion matrix** and classification report.

### **5. Saving Model**
- The trained model is serialized using `joblib` to allow future use without retraining.

### **6. Testing on Unseen Data**
- The saved model can be loaded to make predictions on new bird tracking data.
- The same preprocessing pipeline is applied to ensure consistent input features.

---

## 📦 Requirements

- Python 3.9+
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- geopy
- joblib

## 📦 Data Access

The full dataset is too large to include in this repository.

You can download it from this Google Drive link:
➡️ [Download Full Dataset](https://drive.google.com/drive/folders/1cOHfzNM6QEv6d_dgDom7f6TK-9Ng0xX4?usp=drive_link)



Install dependencies using:

```bash
pip install -r requirements.txt
