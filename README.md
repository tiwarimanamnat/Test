# Wearable Stress Recovery Analysis Pipeline

A comprehensive machine learning pipeline for analyzing physiological stress and recovery using wearable device data (Fitbit/Empatica E4).

## 📊 Pipeline Architecture

```mermaid
graph TD
    A["🔵 Wearable data acquisition<br/>Fitbit / Empatica E4<br/>HRV, EDA, HR, Temp"] --> B["🟢 Data preprocessing<br/>Noise filter · normalize<br/>Extract 18 features"]
    
    B --> C["18 physiological features"]
    
    C --> D["🟢 HRV features<br/>RMSSD, SDNN<br/>LF/HF"]
    C --> E["🟢 EDA / HR / Temp<br/>Mean, Std, slope"]
    C --> F["🟢 Activity / Workload<br/>Movement<br/>self-report"]
    
    D --> G["🟣 MC-UDE framework<br/>dS/dt = -β·S + Σα·F(t) + NN(S,F)<br/>ODE solver torchsdeq<br/>2-layer neural net"]
    E --> G
    F --> G
    
    H["🔴 Neural NN(S,F)<br/>Nonlinear correction"] --> G
    G --> I["🔴 β(S(t))<br/>Stress recovery"]
    
    G --> J["🟡 Cohort clustering K-means<br/>Cardiac · Anxiety<br/>Respiratory · Cognitive"]
    
    J --> K["🟣 Symbolic regression<br/>Discover interpretable<br/>per-subject equations"]
    
    K --> L["🟢 Stress prediction<br/>60-step burnout trajectory"]
    K --> M["🟢 Readable equations<br/>α coefficients + β recovery rate"]
    
    L --> N["🟢 Intervention dashboard<br/>Risk score · what-if simulation<br/>cold-start 10 min"]
    M --> N
    
    style A fill:#cfe9ff
    style B fill:#d4edda
    style C fill:#fff3cd
    style D fill:#d4edda
    style E fill:#d4edda
    style F fill:#d4edda
    style G fill:#e7d4f5
    style H fill:#f8d7da
    style I fill:#f8d7da
    style J fill:#fff3cd
    style K fill:#e7d4f5
    style L fill:#d4edda
    style M fill:#d4edda
    style N fill:#d4edda
```

## 🔄 Pipeline Stages

### 1. **Data Acquisition**
- **Input**: Wearable sensors (Fitbit / Empatica E4)
- **Signals**: Heart Rate Variability (HRV), Electrodermal Activity (EDA), Heart Rate (HR), Temperature

### 2. **Data Preprocessing**
- Noise filtering
- Normalization
- Feature extraction → **18 physiological features**

### 3. **Feature Extraction** (3 Categories)

| Category | Features |
|----------|----------|
| **HRV Features** | RMSSD, SDNN, LF/HF ratio |
| **EDA / HR / Temp** | Mean, Standard Deviation, Slope |
| **Activity / Workload** | Movement metrics, Self-reported workload |

### 4. **Stress Dynamics Modeling (MC-UDE)**
- **Framework**: Neural ODE with Physics-Informed Learning
- **Model**: 
  ```
  dS/dt = -β·S + Σα·F(t) + NN(S,F)
  ```
- **Components**:
  - **β(S(t))**: Stress recovery rate (nonlinear)
  - **α coefficients**: Feature sensitivity weights
  - **NN(S,F)**: Neural network correction term
- **Solver**: torchsdeq ODE solver + 2-layer neural network

### 5. **Cohort Clustering**
- Algorithm: K-means clustering
- Dimensions:
  - Cardiac stress patterns
  - Anxiety indicators
  - Respiratory responses
  - Cognitive load markers

### 6. **Symbolic Regression**
- Discovers **interpretable per-subject equations**
- Converts complex dynamics into human-readable mathematical expressions

### 7. **Prediction & Interpretation**
- **Stress Prediction**: 60-step burnout trajectory forecasting
- **Readable Equations**: α coefficients + β recovery rate parameters

### 8. **Intervention Dashboard**
- Risk scoring
- What-if simulation capabilities
- Cold-start capability (10 minutes of data)

---

## 🛠️ Technical Stack

| Component | Technology |
|-----------|-----------|
| **Data Source** | Fitbit / Empatica E4 wearables |
| **Preprocessing** | Signal filtering, normalization |
| **Feature Extraction** | HRV, EDA, HR, Temp analysis |
| **ODE Solver** | torchsdeq |
| **Neural Network** | 2-layer MLP |
| **Clustering** | K-means |
| **Symbolic Regression** | Physics-informed discovery |

---

## 📈 Key Features

✅ **Physics-Informed Learning**: Combines domain knowledge with neural networks  
✅ **Interpretability**: Symbolic regression for human-readable equations  
✅ **Personalization**: Per-subject model discovery  
✅ **Real-time Prediction**: 60-step burnout trajectory  
✅ **Interactive Dashboard**: Risk assessment & scenario simulation  
✅ **Fast Onboarding**: 10-minute cold-start capability  

---

## 📋 Input/Output

### Inputs
- Wearable device streams (HRV, EDA, HR, Temperature)
- Demographic/contextual metadata
- Self-reported stress/workload

### Outputs
- **Stress dynamics parameters** (β recovery rate, α feature weights)
- **Cohort membership** (Cardiac/Anxiety/Respiratory/Cognitive clusters)
- **Interpretable equations** per subject
- **Risk scores** and burnout trajectory
- **Intervention recommendations**

---

## 🎯 Use Cases

1. **Burnout Prevention**: Early detection of unsustainable stress patterns
2. **Personalized Recovery**: Subject-specific recovery rate optimization
3. **Clinical Monitoring**: Anxiety, cardiac, respiratory pattern classification
4. **Wellness Interventions**: Real-time feedback & scenario planning
5. **Research**: Understanding stress-recovery dynamics at scale

---

## 📚 References

- **MC-UDE Framework**: Neural Ordinary Differential Equations with physics-informed constraints
- **Symbolic Regression**: Discovering interpretable governing equations
- **Wearable Sensors**: Validation against clinical-grade physiological monitoring

---

## 📝 License

[Specify your license here]

## 👥 Contributing

[Add contribution guidelines]

---

*Generated from wearable stress-recovery analysis pipeline*
