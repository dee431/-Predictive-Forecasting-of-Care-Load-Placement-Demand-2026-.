# -Predictive-Forecasting-of-Care-Load-Placement-Demand-2026-.
🛡️ HHS UAC Program: Predictive Care Load & Placement Demand 📊🔮
An operational intelligence dashboard providing real-time time-series forecasting, capacity stress monitoring, and discharge placement demand modeling for the Unaccompanied Alien Children (UAC) program.

🌟 Overview
Managing shelter capacity and tracking care load demands requires rapid, data-driven forecasting. This project delivers an end-to-end Machine Learning pipeline and interactive web interface designed to:
📉 Predict future shelter care loads using ensemble ML models and exponential smoothing.
🚨 Calculate capacity breach probability before shelter stress occurs.
🚪 Model discharge demands and monitor net intake vs. outflow pressure in real time.
⚡ Deploy seamlessly on cloud environments (Google Colab) with direct zero-trust web access via Cloudflare Tunnels.
✨ Key Features
🧼 Automated Data Cleaning & Deduplication Pipeline
Parses complex dates, cleans financial/comma-separated numerical formats, and resolves duplicate date entries automatically.
Handles time-series continuity with smart forward/backward fill and temporal interpolation.
⚙️ Advanced Feature Engineering
Auto-generates rolling moving averages (7-day and 14-day windows), rolling standard deviations, lag variables, and temporal calendar features (Day of Week, Month).
🤖 Multi-Model Forecasting Suite
Gradient Boosting Regressor (GBR): Captures non-linear trend interactions and temporal dynamics.
Random Forest Regressor (RF): High-stability ensemble prediction for surge forecasting.
Holt-Winters Exponential Smoothing: Classic statistical benchmark for baseline trend decomposition.
📈 Interactive Visual Analytics Dashboard
95% Confidence Interval Shading: Quantifies prediction uncertainty dynamically.
Capacity Threshold Alerts: Instant metric callouts flagging capacity breach risks.
Net Flow Pressure Charts: Highlights inflow vs. outflow momentum to give early lead-time warnings.
🛠️ Tech Stack & Architecture
Category	Technology	Usage
Language	🐍 Python 3.10+	Core computational logic
Web Framework	🎈 Streamlit	Dynamic interactive web application
Data Processing	🐼 Pandas & 🔢 NumPy	Data transformation, deduplication, & feature engineering
Machine Learning	🤖 Scikit-Learn & 📈 Statsmodels	Gradient Boosting, Random Forest, & Holt-Winters models
Visualization	📊 Plotly Express & Graph Objects	Interactive charts, threshold lines, & confidence intervals
Tunneling / Hosting	☁️ Cloudflare Tunnels (cloudflared)	Instant secure public deployment from notebook environments
🏗️ Data Processing Pipeline
[📥 Raw CSV Dataset] 
         │
         ▼
[🧼 Clean & Convert Types] ──► (Remove commas, parse dates)
         │
         ▼
[🔄 Deduplicate Dates] ──────► (Group by Date & pick latest entries)
         │
         ▼
[📅 Time-Series Resampling] ──► (Set daily index .asfreq('D') & interpolate)
         │
         ▼
[⚡ Feature Generation] ─────► (Lags, Rolling Means, Rolling Std, Calendar)
         │
         ▼
[🤖 Model Training & Forecast] ► (GBR / Random Forest / Holt-Winters)
         │
         ▼
[📊 Streamlit Dashboard] ─────► (Metrics, Plots & Risk Alerts)
🚀 Getting Started
Prerequisites
Python 3.10+
Google Colab or local GPU/CPU environment
🔧 Local Installation
Clone the repository:
Bash
git clone https://github.com/your-username/hhs-uac-forecasting.git
cd hhs-uac-forecasting
Install required dependencies:
Bash
pip install streamlit plotly pandas numpy scikit-learn statsmodels
Run the Streamlit application:
Bash
streamlit run app.py
⚡ One-Click Deployment (Google Colab)
Run the entire pipeline—from synthetic dataset generation to web deployment—in a single cell inside Google Colab:
Python
# 1. Install Dependencies & Cloudflare CLI
!pip install -q streamlit plotly pandas numpy scikit-learn statsmodels
!wget -q -O cloudflared.deb https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
!dpkg -i cloudflared.deb

# 2. Launch Streamlit Application in Background
import subprocess, time
subprocess.Popen(["streamlit", "run", "app.py", "--server.port=8501", "--server.headless=true"])
time.sleep(3)

# 3. Expose Streamlit via Cloudflare Tunnel
!cloudflared tunnel --url http://localhost:8501
📊 Dashboard Metrics & Visuals
🟢 Current Care Load: Tracks live operational child count in HHS facilities.
🎯 Target Forecast: Project demand over 7 to 60 day horizons.
🛡️ Forecast Accuracy: Evaluates inverse Mean Absolute Percentage Error (MAPE).
🚨 Capacity Breach Probability: Percent chance of exceeding set shelter limits over the forecast horizon.
🤝 Contributing
Contributions, issues, and feature requests are welcome! Feel free to check the issues page.
📜 License
Distributed under the MIT License. See LICENSE for more information.
