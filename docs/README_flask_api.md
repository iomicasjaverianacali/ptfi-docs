# MS2 Prediction Flask API

This Flask API provides 4 endpoints that correspond to the main steps in the end-to-end MS2 spectra prediction and validation pipeline.

## Installation

1. Install the required dependencies:
```bash
pip install -r requirements_flask.txt
```

2. Make sure you have the `ptfifrijolpujc` package installed in your environment.

## Running the API

Start the Flask server:
```bash
python flask_api.py
```

The API will be available at `http://localhost:5000`

# API Endpoints

### Usage examples using CURL

1. **Compute MS2 spectra and download pickle file:**

*CURL WORKING: CHECKED*

```bash
curl -X POST http://localhost:5000/compute_ms2 \
  -H "Content-Type: application/json" \
  -d '{
    "chromatograms_dir": "/path/to/chromatograms",
    "ddas_dir": "/path/to/ddas",
    "project_name": "my_project",
    "ground_truth_ms2_filename": "ground_truth"
  }' \
  --output ground_truth.pkl
```

more detailed example:

```bash
curl -X POST http://localhost:5000/compute_ms2 -H "Content-Type: application/json" -d "{\"chromatograms_dir\": \"/mnt/c/Users/daniel.sinisterra/Documents/repos/data/Datos .mzML/MS1 test/ABC-22393-DM_pos\", \"ddas_dir\": \"/mnt/c/Users/daniel.sinisterra/Documents/repos/data/Datos .mzML/DDA test/ABC-22393-DM_HE_pos\", \"project_name\": \"my_project\", \"ground_truth_ms2_filename\": \"ground_truth\"}"
```


2. **Predict SMILES:**

*CURL WORKING: CHECKED*

```bash
curl -X POST http://localhost:5000/predict_smiles \
  -H "Content-Type: application/json" \
  -d '{
    "data_file_path": "path/to/ground/truth/ms2.pkl",
    "path_to_mdl": "/path/to/model",
    "trained_model_name": "model.pth",
    "project_name": "my_project",
    "num_pred": 5,
    "predict_approach": "greedy",
    "device": "cpu"
  }'
```

more detailed example in windows:

```bash
curl -X POST http://localhost:5000/predict_smiles ^
  -H "Content-Type: application/json" ^
  -d "{\"data_file_path\": \"C:\\\\Users\\\\daniel.sinisterra\\\\Documents\\\\repos\\\\results\\\\test_postman\\\\ground_truth.pkl\",\"path_to_mdl\": \"C:\\\\Users\\\\daniel.sinisterra\\\\Documents\\\\repos\\\\models\",\"trained_model_name\": \"dd_arch1_lf1_data_1.pth\",\"project_name\": \"test_postman\",\"num_pred\": 5,\"predict_approach\": \"greedy\",\"device\": \"cpu\"}"
```

more detailed example in WSL:

```bash
curl -X POST http://localhost:5000/predict_smiles ^
  -H "Content-Type: application/json" ^
  -d "{\"data_file_path\": \"/mnt/c/Users/daniel.sinisterra/Documents/repos/results/my_project/ground_truth.pkl\",\"path_to_mdl\": \"/mnt/c/Users/daniel.sinisterra/Documents/repos/models\",\"trained_model_name\": \"dd_arch1_lf1_data_1.pth\",\"project_name\": \"my_project\",\"num_pred\": 5,\"predict_approach\": \"greedy\",\"device\": \"cuda\"}"
```


3. **Generate predicted MS2:**

*CURL WORKING: CHECKED*

```bash
curl -X POST http://localhost:5000/generate_predicted_ms2 \
  -H "Content-Type: application/json" \
  -d '{
    "project_name": "my_project",
    "predicted_ms2_filename": "predicted_ms2",
    "ionization": "[M+H]+"
  }'
```

a more detailed example in windows or WSL:

```bash
curl -X POST http://localhost:5000/generate_predicted_ms2 ^
  -H "Content-Type: application/json" ^
  -d "{\"project_name\": \"my_project\", \"predicted_ms2_filename\": \"predicted_ms2\", \"ionization\": \"[M+H]+\", \"device\": \"cpu\"}"
```

4. **Validate predictions:**
```bash
curl -X POST http://localhost:5000/validate_predictions \
  -H "Content-Type: application/json" \
  -d '{
    "project_name": "my_project",
    "predicted_ms2_filename": "predicted_ms2",
    "ground_truth_ms2_filename": "ground_truth",
    "predicted_smiles_filename": "final_predictions"
  }'
```

a more detailed example:

```bash
curl -X POST http://localhost:5000/validate_predictions ^
  -H "Content-Type: application/json" ^
  -d "{\"project_name\": \"my_project\", \"predicted_ms2_filename\": \"predicted_ms2\", \"ground_truth_ms2_filename\": \"ground_truth\", \"predicted_smiles_filename\": \"final_predictions\", \"weight_mass_missmatch\": \"0.5\", \"weight_dreams\": \"0.5\"}"
```

### Using Python requests

```python
import requests
import json

# Base URL
base_url = "http://localhost:5000"

# 1. Compute MS2 spectra and download pickle file
response = requests.post(f"{base_url}/compute_ms2", json={
    "chromatograms_dir": "/path/to/chromatograms",
    "ddas_dir": "/path/to/ddas",  # optional
    "project_name": "my_project",
    "ground_truth_ms2_filename": "ground_truth"
})

# Save the pickle file
with open("ground_truth.pkl", "wb") as f:
    f.write(response.content)

print("MS2 spectra computed and saved to ground_truth.pkl")

# 2. Predict SMILES
response = requests.post(f"{base_url}/predict_smiles", json={
    "intensities": [[1.0, 2.0, 3.0]],
    "masses": [[100.0, 200.0, 300.0]],
    "path_to_mdl": "/path/to/model",
    "trained_model_name": "model.pth",
    "project_name": "my_project",
    "num_pred": 5,
    "predict_approach": "greedy",
    "device": "cpu"
})
print(response.json())

# 3. Generate predicted MS2
response = requests.post(f"{base_url}/generate_predicted_ms2", json={
    "project_name": "my_project",
    "predicted_ms2_filename": "predicted_ms2",
    "ionization": "[M+H]+"
})
print(response.json())

# 4. Validate predictions
response = requests.post(f"{base_url}/validate_predictions", json={
    "project_name": "my_project",
    "predicted_ms2_filename": "predicted_ms2",
    "ground_truth_ms2_filename": "ground_truth",
    "predicted_smiles_filename": "final_predictions"
})
print(response.json())
```

## Error Handling

All endpoints return appropriate HTTP status codes:
- `200`: Success
- `400`: Bad Request (missing or invalid parameters)
- `500`: Internal Server Error

Error responses include an `error` field with a description of what went wrong.

## Configuration

The API uses hardcoded paths:
- **Base output directory**: `C:\Users\daniel.sinisterra\Documents\repos\results\`
- **Protocol**: Always "PTFI"
- **Project folders**: Created automatically under the base output directory

## Notes

- All project files are stored in `C:\Users\daniel.sinisterra\Documents\repos\results\PROJECT_NAME\`
- The project folder will be created automatically if it doesn't exist
- The `/compute_ms2` endpoint always returns the pickle file as a download
- Protocol is hardcoded to "PTFI" for all operations
- Make sure you have sufficient disk space for processing large datasets
- The pickle files contain numpy arrays and can be loaded using `pickle.load()` 