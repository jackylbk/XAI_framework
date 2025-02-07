# XAI Framework API

## 📖 Overview

The **XAI Framework API** is a Flask-based machine learning model deployment that allows users to:

- **Make predictions** using a trained model (`/predict`)
- **Get model explanations** using LIME (`/explain/lime`)

This API is hosted on **Swedish Science Cloud (SSC)** and can be accessed via HTTP.

### API Base URL
```
http://130.238.27.150
```
The API listens on **port 80**, so no need to specify the port number explicitly.

---

## 🔧 API Endpoints

### 🩺 `/` - Check API Health
- **Method:** `GET`
- **Example Request:**
  ```bash
  curl http://130.238.27.150/
  ```
- **Example Response:**
  ```json
  {"message": "Hello from Flask!"}
  ```

### 🔮 `/predict` - Get Model Prediction
- **Method:** `POST`
- **Request Format:**
  ```json
  {
    "features": [500, 150, 120, 300, 600, 400, 0, 28]
  }
  ```
- **Example Request:**
  ```bash
  curl -X POST http://130.238.27.150/predict        -H "Content-Type: application/json"        -d '{"features": [500, 150, 120, 300, 600, 400, 0, 28]}'
  ```
- **Example Response:**
  ```json
  {"prediction": [54.7911]}
  ```

### 🔍 `/explain/lime` - Get LIME Explanation
- **Method:** `POST`
- **Request Format:**
  ```json
  {
    "features": [500, 150, 120, 300, 600, 400, 0, 28]
  }
  ```
- **Example Request:**
  ```bash
  curl -X POST http://130.238.27.150/explain/lime        -H "Content-Type: application/json"        -d '{"features": [500, 150, 120, 300, 600, 400, 0, 28]}'
  ```
- **Example Response:**
  ```json
  {
    "lime_explanation": {
      "age > -0.73": 0.06499621343278504,
      "blast_furnace_slag > -0.85": 0.060632492025681904,
      "cement > -2.63": 0.06784425864499531,
      "coarse_aggregate > -12.37": 0.06737374806495669,
      "fine_aggregate <= -9.54": 0.06893856659681971,
      "fly_ash > -0.82": 0.06063971309659764,
      "superplasticizer > -0.90": 0.06919737735657927,
      "water > -8.50": 0.065032041417252
    }
  }
  ```

# **Concrete Strength Dataset Description**

## **Input Variables (X1 - X8)**

| **Variable** | **Description** | **Unit** |
|-------------|---------------|----------|
| **X1 (Cement)** | The amount of cement used in the mixture. Cement is a key binding material in concrete. | kg/m³ |
| **X2 (Blast Furnace Slag)** | A byproduct of iron production used as a partial cement replacement to improve durability. | kg/m³ |
| **X3 (Fly Ash)** | A fine powder byproduct of burning coal, used as a supplementary cementitious material. | kg/m³ |
| **X4 (Water)** | The amount of water added to the mixture, essential for the hydration process. | kg/m³ |
| **X5 (Superplasticizer)** | A chemical additive that enhances the workability and strength of concrete. | kg/m³ |
| **X6 (Coarse Aggregate)** | Large stones or gravel that provide bulk and structural integrity to concrete. | kg/m³ |
| **X7 (Fine Aggregate)** | Sand or crushed stone that fills gaps between coarse aggregates, improving cohesion. | kg/m³ |
| **X8 (Age)** | The curing time of the concrete before testing its strength. | Days |

## **Output Variable (Y)**

| **Variable** | **Description** | **Unit** |
|-------------|---------------|----------|
| **Y (Concrete Compressive Strength)** | The measured compressive strength of the concrete, indicating its load-bearing capacity. | MPa (Megapascals) |

This dataset is commonly used in machine learning applications to predict the strength of concrete based on its composition and curing time. If you need further analysis, visualization, or model training, feel free to ask! 🚀

# **Example Test Command for Different Operating Systems**

| OS                     | Command |
|------------------------|---------|
| **Windows (cmd)** | `curl -X POST http://130.238.27.150/predict -H "Content-Type: application/json" -d "{\"features\": [500, 150, 120, 300, 600, 400, 0, 28]}"` |
| **Windows (PowerShell)** | `Invoke-RestMethod -Uri "http://130.238.27.150/predict" -Method Post -Headers @{"Content-Type"="application/json"} -Body '{"features": [500, 150, 120, 300, 600, 400, 0, 28]}'` |
| **Mac/Linux (Bash)** | `curl -X POST http://130.238.27.150/predict -H "Content-Type: application/json" -d '{"features": [500, 150, 120, 300, 600, 400, 0, 28]}'` |





---

## 🚀 Deployment Details

- Hosted on **Swedish Science Cloud (SSC)**
- Running with **Gunicorn** and **Nginx** for stability
- API is accessible globally via HTTP without specifying a port
- **Machine Learning**: Scikit-learn, SHAP, LIME
- **Maintainer**: Bokai Liu

## 🛠 Setup Instructions (For Developers)

To run this API locally:

```bash
# Install dependencies
pip install -r requirements.txt

# Start API with Gunicorn
gunicorn -w 4 -b 0.0.0.0:8000 app:app
```

Make sure your server's firewall and security group allow access on port **80**.

---

## Contributing
If you have suggestions or find any issues, feel free to open an issue or submit a pull request.

For any questions, contact bokai.liu@umu.se




## 📝 License

This project is licensed under the MIT License.

---
