# Hidden Markov Model for Human Activity Recognition

This project implements a Hidden Markov Model (HMM) to recognize human activities (standing, walking, jumping, still) from smartphone accelerometer and gyroscope sensor data.
The system achieves **78.10% accuracy**.

##  Project Objectives

1. Collect real-world motion sensor data from a smartphone
2. Extract time-domain and frequency-domain features
3. Build and train a Gaussian Hidden Markov Model
4. Implement the Viterbi algorithm for activity sequence decoding
5. Evaluate model performance on unseen data

##  Dataset

### Data Collection
- **Device**: iPhone and Samsung with Sensor Logger app
- **Sampling Rate**: 100 Hz
- **Sensors**: Accelerometer (x, y, z) and Gyroscope (x, y, z)
- **Total Recordings**: 50 recordings across 4 activities
- **Total Samples**: 32,053 sensor measurements

### Activities Recorded
1. **Standing** (12 recordings) - Phone held steady at waist level
2. **Walking** (12 recordings) - Consistent pace, phone in pocket/hand
3. **Jumping** (13 recordings) - Continuous jumping motions
4. **Still** (13 recordings) - Phone on flat surface, no movement

##  Implementation

### Technologies Used
- **Python 3.8+**
- **Libraries**:
  - `hmmlearn` - Hidden Markov Model implementation
  - `scikit-learn` - Machine learning utilities
  - `numpy/scipy` - Numerical computing and signal processing
  - `pandas` - Data manipulation
  - `matplotlib/seaborn` - Data visualization

### Feature Engineering
- **83 Total Features** extracted from sliding windows (1 second, 50% overlap)
  - **54 Time-domain features**: mean, std, variance, min, max, range, median, skewness, kurtosis, RMS, SMA, correlations
  - **18 Frequency-domain features**: dominant frequency, spectral energy, spectral entropy (via FFT)

### Model Architecture
- **Hidden States**: 4 states (one per activity)
- **Emission Model**: Multivariate Gaussian with diagonal covariance
- **Training**: Baum-Welch algorithm (100 iterations)
- **Decoding**: Viterbi algorithm for optimal state sequence

##  Results

### Overall Performance
- **Overall Accuracy**: 78.10%
- **Training Samples**: 426 windows
- **Test Samples**: 137 windows

### Per-Activity Performance

| Activity | Samples | Sensitivity | Specificity | Precision |
|----------|---------|-------------|-------------|-----------|
| Standing | 30      | 0.0000      | 0.0000      | 0.0000   |
| Walking  | 32      | 1.0000      | 0.9905      | 0.0000    |
| Jumping  | 32      | 1.0000      | 1.0000      | 0.9333    |
| Still    | 42      | 1.0000      | 0.6915      | 0.5972   |

### Key Findings
- **Walking**,**Jumping ** and **Still**: Perfect recognition (100% sensiticity)
- **Standing**: Failed to recognize (0% sensitivity)

##  Project Structure

```
project/
│
├── Hidden_Markov_Models.ipynb    # Main Jupyter notebook
├── requirements.txt                  # Python dependencies
├── README.md                        # This file
│
├── HMM data/                 
    ├── standing/
    │   ├── standing1/ (Accelerometer.csv, Gyroscope.csv)
    │   ├── standing2/
    │   └── standing3/
    ├── walking/
    ├── jumping/
    └── still/


```

### Installation

```bash
# Install dependencies
pip install -r requirements.txt
```

### Running the Notebook

```bash
# Start Jupyter Notebook
jupyter notebook

# Open hmm_activity_recognition.ipynb
# Run all cells
```

### Using Google Colab (Alternative)

1. Upload `Hidden_Markov_Models.ipynb` to Google Colab
2. Upload `HMM data`
3. Update `DATA_DIR` path in notebook
4. Run all cells

##  Visualizations

The notebook generates several visualizations:

1. **Raw Sensor Signals** - Time-series plots of accelerometer/gyroscope data
2. **Feature Distributions** - Distribution of key features by activity
3. **Transition Matrix** - HMM state transition probabilities (heatmap)
4. **Confusion Matrix** - Model prediction accuracy
5. **Decoded Sequences** - True vs predicted activity sequences

##  Analysis & Insights

### What Worked Well
- Jumping and Walking are easiest to recognize due to high motion and unique frequency patterns.
- Temporal modeling via HMM captures realistic activity transitions
- Feature engineering effectively captures motion characteristics

### Challenges
- Standing recognition failed with 0% sensitivity
- Confusion between standing and other low-motion activities
- Limited training data from two participants
- Short recording durations (5-7 seconds)

##  Recommendations for Improvement

### DATA COLLECTION:
- Collecting more samples
- Set a fixed recording duration for better feature representation
- Including various participants for better generalization
- Include a variety of activities (indoor/outdoor)

### FEATURE ENGINEERING:
- Include time-series features (autocorrelation, entropy measures)
- Experiment with different window sizes and overlap ratios
- Feature selection to reduce dimensionality and noise

### VALIDATION:
- Test on completely new participants
- Evaluate real-time performance
- Compare with other models (Random Forest, LSTM, CNN)

##  Learning Outcomes

This project demonstrates:
- Real-world data collection and preprocessing
- Time-series feature extraction techniques
- Hidden Markov Model theory and implementation
- Viterbi algorithm for sequence decoding
- Model evaluation on unseen data
- Critical analysis of results and limitations

## Authors
- Roxanne Niteka
- Laurelle Jinelle Nformi

The complete analysis and discussion are available in the written report.

[REPORT](https://docs.google.com/document/d/1iyaIqTNclKEeh6WHNkLxXYHCtj7UjjHSAfHbsNJGFuw/edit?tab=t.0)
