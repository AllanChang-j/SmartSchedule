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

### Duration Prediction Comparison:
- **DNN-only model**: DNN_Only_MSE: 13.884   Fast convergence but unstable validation loss (overfitting)  
  <img width="446" alt="截圖 2025-07-05 下午6 10 35" src="https://github.com/user-attachments/assets/871c8d2b-0e66-484d-bba4-dffec8250c1c" />

- **RF-only model**: RF_Only_MSE: 10.757   Feature importance was scattered and less semantically meaningful  
  <img width="446" alt="截圖 2025-07-05 下午6 11 19" src="https://github.com/user-attachments/assets/0bbe6e82-8d57-4fe4-9a47-287ce2a64136" />

- **DNN + DNN pred + RF model**: Combines DNN output and mid train pred with embeddings for final RF regression.
  The MSE was 14.177, indicating a drop in performance. This may be due to an overly dense feature space or a low correlation between the DNN intermediate layer outputs and the prediction target.Due to time and technical constraints, we did not specifically validate these two hypotheses.

- **DNN + RF model**: DNN_RF_MSE: 4.578   Combines DNN output with embeddings for final RF regression (final usage plan)
  <img width="419" alt="截圖 2025-07-05 下午6 38 02" src="https://github.com/user-attachments/assets/65a8f529-e767-4e31-b158-97fdacaf9b0b" />


  
### Urgency Prediction:
- **DNN-only model**: DNN_Only_MSE: 0.686   Fast convergence but unstable validation loss (overfitting)
    <img width="448" alt="截圖 2025-07-05 下午6 33 01" src="https://github.com/user-attachments/assets/5aceab1b-af49-4b94-affb-09daaaa1c292" />

- **RF-only** RF_Only_MSE: 0.0649   model achieved best performance (final usage plan)
  <img width="448" alt="截圖 2025-07-05 下午6 34 40" src="https://github.com/user-attachments/assets/c03f2202-ebb3-4ba8-9ab0-3faaa7791c5b" />

## Results
Final system configuration:
- **Duration prediction**: DNN + RF hybrid model (MSE = 4.578)
- **Urgency prediction**: RF-only model (MSE = 0.0649)
- **Priority scoring**: Weighted formula using predicted duration, urgency, and remaining time
<img width="560" alt="截圖 2025-07-05 下午6 36 46" src="https://github.com/user-attachments/assets/e8c55020-1d90-48e1-be86-0bfba67cd330" />

Users interact with a Gradio-based UI to plan weekly schedules, exportable as `.ics` files to sync with Google Calendar.  
The system balances accuracy and usability, making it suitable for students and freelancers managing busy schedules.

## Contributors
111zu1024 – 朗慕恆 (Konstantin Muheng Lackner)

   Served as a presenter for Innofest and contributed to report checking.

112102031 – 陳以欣 (Chen Yi-Hsin)

   Focused on writing and structuring the report content.

112zu1023 – 蕾蕾 (Sirinsara Wararuttanapisoot)

   Served as a presenter for Innofest and assisted with final report checking.

113zu1042 – 黃彥誠 (Napat Rungrueangaree)

   Served as a presenter for Innofest and contributed to final report checking.

113zu1049 – 張峻翔 (Chang Allan)

   Responsible for coding and drafting key sections of the report.
