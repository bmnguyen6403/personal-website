# About Me

*Lehigh University, Class of 2025*  
College of Business – Finance and Business Analytics

<p align="center">
  <img src="images/Minh Nguyen.png" alt="Minh Nguyen" width="60%">
</p>

---

# Portfolio

## 📈 Stock Return Survival Analysis

<p align="center">
  <img src="images/decay_graph.png" alt="Signal Decay Analysis" width="70%">
</p>

This section presents our **signal decay analysis** across 20 financial signals. Rather than simply asking whether a signal is predictive, we focus on a more valuable question: **how long does that predictive power last**?

In real-world investing, not all signals behave the same over time — some are effective for just a month, while others remain useful over longer horizons. To evaluate this, we compute the **Information Coefficient (IC)** — specifically the **Spearman Rank Correlation** between a signal and future returns.

IC is a preferred metric because:
- It **does not assume linear relationships**
- It is **robust to outliers**
- It captures **relative performance**, which aligns with portfolio selection needs

We calculate ICs at **1-month, 3-month, and 6-month forward returns**, then average them to obtain `IC_avg` — a measure of consistency over time.

The chart below visualizes signal strength over time for our **top 5 signals**:

- **DelDRC** gains strength over time — ideal for long-term strategies.
- **roaq** is powerful short-term but decays rapidly — useful for quick alpha capture.
- **XFIN** strengthens gradually, favoring longer holding periods.
- **TrendFactor** shows medium-term stability.
- **NetEquityFinance** is strong early on but fades — best for short-duration strategies.

By analyzing **how signals decay**, we can align them to specific investment horizons. For example, combining persistent signals like **XFIN** and **DelDRC** with fast-decaying ones like **roaq** can lead to **more resilient and better-timed portfolios**.

_“Instead of just asking ‘Does the signal work?’, we ask ‘How long does it work for?’ — a more strategic question for investment design.”_
---

## 🤝 Team Project: [Stock Prediction Analysis](https://www.theasians.streamlit.app)

<p align="center">
  <img src="images/Cum vs Act.jpeg" alt="Cumulative Return Graph" width="70%">
</p>

This team project compares cumulative returns across signal-level portfolios using the **Open Asset Pricing (OpenAP)** library and a variety of machine learning models:

- Linear Regression  
- MLP Regressor  
- Random Forest  
- SVR (Support Vector Regressor)  
- XGBoost

---

# Career Objectives

I aspire to launch my own startup in the future, combining my background in Finance and Business Analytics with technology to solve meaningful, real-world problems. My long-term goal is to build a data-driven company that creates impact at scale — whether in financial services, consumer tech, or sustainability. In the near term, I’m focused on gaining hands-on experience in product development, market strategy, and venture operations to prepare for the challenges of founding and scaling a business.


---

# Hobbies

📚 Reading nonfiction — especially on behavioral economics, psychology, and tech innovation  
🎨 Digital design and UI experimentation  
🛫 Traveling to experience new cultures and cuisines  
🧠 Solving logic puzzles and brain teasers  
🎮 Competitive gaming (strategy and team-based games)


---

# 📬 Contact

- **Email**: bmnguyen6403@gmail.com
- **Phone**: (484) 935-9166 
- **Location**: Bethlehem, PA  
- **Portfolio**: [theasians.streamlit.app](https://www.theasians.streamlit.app)
