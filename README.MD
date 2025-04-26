# Smart Trash Bin - Deep Learning Model Training

This repository contains the data generation, model exploration, and final training scripts for the **Cloud and Fog Computing in the Internet of Things** course project.

The main focus of the overall project is on cloud integration rather than artificial intelligence, thus the dataset was synthetically generated to mimic real-world sensor conditions across 8 different trash bin locations.

## Dataset Generation

- Synthetic dataset was generated using `generate-data.ipynb`.
- The dataset replicates realistic weight, gas sensor readings (CH4 and NH3), and trash fill levels over time.
- Each trash bin location has its own dataset and model to better represent localized behavior.

## Model Exploration

Initial experiments were conducted using several models:

- **SARIMAX**
- **Prophet**
- **LSTM**
- **LightGBM**
- **XGBoost**

The experiments showed:

- **SARIMAX** and **Prophet** underperformed in terms of predictive accuracy.
- **LightGBM** and **XGBoost** models exhibited strong overfitting to training data.
- **LSTM** provided the most reasonable and generalizable results with an evaluation score of **4.03**.

You can find the exploration details in `explore.ipynb` and `training.ipynb`.

## Final Model: LSTM

After identifying LSTM as the best candidate, extensive hyperparameter tuning was conducted.  
The hyperparameter search was performed through multiple training runs (see `training LSTM code.ipynb`).

### Final Selected Hyperparameters:

```python
{
  'units': 128,
  'dropout': 0.1,
  'learning_rate': 0.01,
  'batch_size': 128,
  'look_back': 336
}
```

### Final Model Evaluation:

| Metric                            | Fill_Percentage (%) | CH4 (ppm) | NH3 (ppm) |
| --------------------------------- | ------------------- | --------- | --------- |
| **MAE (Mean Absolute Error)**     | 3.50                | 2.49      | 0.88      |
| **RMSE (Root Mean Square Error)** | 7.98                | 4.54      | 1.53      |

## Repository Contents

- `generate-data.ipynb`: Synthetic data generation script
- `explore.ipynb`: Model exploration and comparison
- `training.ipynb`: Model training experiments across different algorithms
- `training LSTM code.ipynb`: Focused LSTM model training and hyperparameter tuning

## Project Structure

This repository is part of a broader project composed of:

- **Arduino Firmware** [here](https://github.com/satyaadhiyaksaardy/CFiot-arduino)
- **Model Training** (this repository)
- **AWS Lambda Functions** [here]()

---

## License

This project is intended for educational purposes as part of the **Cloud and Fog Computing in IoT** course.
