# SmartSchedule: A Semantic-Aware Task Prioritization and Scheduling System

## Project Description
SmartSchedule is a semantic-driven intelligent task management system that helps users input tasks in natural language and automatically predicts task duration and urgency. Based on these predictions, it provides visual scheduling suggestions.

The system integrates OpenAI’s semantic embedding model, Deep Neural Networks (DNN), and Random Forest (RF) to estimate task workload and urgency. The outputs include task priority rankings and exportable .ics calendar files for Google Calendar integration.

The dataset sources include:
- Public freelancing platforms (e.g., Upwork, Freelancer)
- Online course platforms (e.g., Coursera, edX)
- User-submitted task logs

After standardization and anonymization, the data was used for model training and inference. Experimental results show that SmartSchedule significantly improves scheduling efficiency and time allocation quality.

## Getting Started
This system is designed to run in Google Colab. Follow the steps below:

1. Open the GitHub repository and upload the code to Colab.
2. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the following notebooks:

   - To train the task duration and urgency models:
     ```python
     # Open modle_trainning.ipynb and run each block step by step.
     ```

   - To perform task prediction, ranking, and calendar export:
     ```python
     # Open pipelinz_newest_version.ipynb and execute each block.
     # Input: CSV file with task title and description
     # Output: predicted duration, urgency score, priority score, and .ics file
     ```

4. If you prefer not to retrain models, download pre-trained models from GitHub Releases:
   - [`dnn_model.h5`](#)
   - [`rf_duration_model.pkl`](#)
   - [`rf_urgency_model.pkl`](#)

## File Structure
```
SmartSchedule/
├── modle_trainning.ipynb         # Model training (task duration and urgency using DNN + RF)
├── pipelinz_newest_version.ipynb # Inference, prioritization, and calendar export
├── requirements.txt              # Python dependencies
└── README.md                     # Project documentation
```

## Analysis
We conducted comparative experiments on three model configurations for task duration and urgency prediction:

### Duration Prediction:
- **DNN-only model**: Fast convergence but unstable validation loss (overfitting)  
  *(Insert image: Figure 3-1)*
- **RF-only model**: Feature importance was scattered and less semantically meaningful  
  *(Insert image: Figure 3-2)*
- **DNN + RF model**: Combines DNN output with embeddings for final RF regression, achieving best performance  
  *(Insert image: Figure 3-3)*

### Urgency Prediction:
- **RF-only** model achieved best performance, MSE = 0.0649  
  *(Insert image: Figure 3-4, 3-5, 3-6)*

## Results
Final system configuration:
- **Duration prediction**: DNN + RF hybrid model (MSE = 10.62)
- **Urgency prediction**: RF-only model (MSE = 0.0649)
- **Priority scoring**: Weighted formula using predicted duration, urgency, and remaining time

Users interact with a Gradio-based UI to plan weekly schedules, exportable as `.ics` files to sync with Google Calendar.  
The system balances accuracy and usability, making it suitable for students and freelancers managing busy schedules.