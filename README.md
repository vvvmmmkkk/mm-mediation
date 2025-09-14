# 📊 Marketing Mix Modeling with Mediation

## 📌 Project Overview
This project builds a **Marketing Mix Model (MMM)** with a **mediation assumption**:  
social media spends (Facebook, TikTok, Instagram, Snapchat) influence **Google spend**, which in turn drives **Revenue**.  

The workflow is designed to be **causal, reproducible, and business-actionable**:  
- **Stage 1:** Model Google spend as a function of social media spends (stimulated search intent).  
- **Stage 2:** Model Revenue as a function of predicted Google spend, direct response levers (email/SMS), price, promotions, and selected direct social spends.  
- Outputs include **direct vs indirect effects**, **price/promotions sensitivity**, and **rolling-window stability checks**.  

---

## ⚙️ Environment Setup
1. **Clone this repository**
   ```bash
   git clone https://github.com/vvvmmmkkk/mm-mediation.git
   cd mm-mediation
**Create and activate a virtual environment and install dependencies**
   ```bash
      python -m venv .venv
      source .venv/bin/activate   # On Windows: .venv\Scripts\activate
      pip install -r requirements.txt



