# Report for the Impact of ChatGPT on Stock Performance from Nov 2022 - Dec 2022

## Introduction
The purpose of this analysis is to investigate how different textual variables from the 10-K filings influence firm performance after the introduction of ChatGPT in late 2022. By classifying firms based on their exposure to six key textual measures, we can observe whether companies with higher or lower exposure to AI, automation, and related concepts were more or less affected by the rise of generative AI tools.

We perform the analysis by dividing firms into two portfolios: one with high exposure to specific textual variables and the other with low exposure. We then compute cumulative returns for these portfolios from November 15 to December 15, 2022. By visualizing these returns, we aim to understand the potential economic impact of exposure to ChatGPT and similar technologies.

## Methodology
### Data Collection and Preprocessing
- S&P 500 Dataset:  A dataset of S&P 500 companies was used, with CIK (Central Index Key) and accession numbers to retrieve relevant 10-K filings.
- Textual Features: The 10-K filings were processed to extract textual features such as:
    + **AI_Exposure**:
1. Economic Logic: Firms with high AI exposure are likely to be early adopters of generative AI tools like ChatGPT. Such firms might gain significant efficiency gains, leverage AI for cost reduction, or offer AI-driven products/services. These advantages can make them more competitive in the market.
2. Expected Impact: Firms with high AI exposure should see a positive impact on returns as they benefit from technological advancements, especially in automation and data processing.
    + **Automation_Focus**:
1. Economic Logic: Companies focused on automation are likely investing in robots, AI-powered systems, or self-driving technologies, which can reduce labor costs and improve productivity. These firms are likely better positioned to adapt to disruptions brought by AI technologies.
2. Expected Impact: High automation focus should correlate with positive returns, as these firms can scale operations efficiently without significant increases in labor costs.
    + **Human_Capital_Impact**:
1. Economic Logic: Firms with a strong focus on upskilling or reskilling their employees can adapt to AI-driven automation and new business models more effectively. However, layoffs or job displacement might harm firms that do not invest in retraining.
2. Expected Impact: High human capital focus should have mixed effects: companies investing in reskilling will likely see better long-term returns, while those focusing on job cuts might see short-term cost reductions but suffer from employee morale issues.
    + **Innovation_Focus**:
1. Economic Logic: Firms with a focus on research and innovation are generally better positioned to create disruptive technologies. These firms are more likely to develop AI solutions or AI-driven products that can lead to market leadership.
2. Expected Impact: Firms with strong innovation focus should see positive returns, as they will be first movers in developing new solutions using AI technologies, gaining a competitive edge.
    + **Regulatory_Risk**:
1. Economic Logic: Firms with high regulatory risk are more likely to face restrictions and costs associated with data privacy regulations, AI ethics issues, or cybersecurity compliance. These risks can lead to higher operational costs or reputational damage.
2. Expected Impact: High regulatory risk firms may experience negative returns, as they might face higher costs to comply with evolving laws related to AI and data privacy.
    + **Productivity_Gains**:
1. Economic Logic: Firms that focus on productivity gains and cost optimization are likely to adopt AI tools like ChatGPT to streamline operations, reduce overheads, and improve decision-making. This makes them more adaptable to the changes brought about by AI adoption.Expected Impact: High productivity focus should lead to positive returns, as these firms will benefit from the efficiency improvements that AI technologies bring.
- Stock return data from CRSP was used to calculate cumulative returns from November 15 to December 15, 2022 for both high and low portfolios.

### Portfolio Formation
- We divided the firms into high and low portfolios for each textual variable based on the top 10% and bottom 10% thresholds, respectively. The portfolios were then evaluated over the event window from November 15 to December 15, 2022. Cumulative returns were calculated for both portfolios, and we compared the performance of firms with high exposure to each textual measure against firms with low exposure.

### Robustness Tests
- Equal-Weighted Portfolio Returns: The portfolios were also analyzed using equal weights (where each firm contributes equally, irrespective of market size).

## Results and Discussion
### Cumulative Return Differences

**Based on the build_sample file**
- From first graph: **Impact of CHATGPT on firms by Textual Exposure**:
  + Regulatory_Risk had a negative impact, with firms that are more exposed to regulatory concerns seeing poorer performance during this period.
  + Automation_Focus and Innovation_Focus seems to have higher return differences, suggesting that firms with higher exposure to automation and innovation experienced better returns.
- From second graph: **Cumulative Return Difference**:
*The second graph compares the cumulative return for the high and low portfolios based on equal weighting. Firms in the high return portfolio generally performed better, with positive returns on certain days, while firms in the low return portfolio showed negative performance across the same period. (2022-11-17)*

## Summary



```python

import pandas as pd
import numpy as np
import os
from tqdm import tqdm
from near_regex import NEAR_regex
from bs4 import BeautifulSoup
import re
from time import sleep
from io import BytesIO
from zipfile import ZipFile
from urllib.request import urlopen
import datetime
import seaborn as sns
import matplotlib.pyplot as plt
import pandas_datareader as pdr
import statsmodels.api as sm


```


```python
sp500 = pd.read_csv('output/analysis_sample.csv')

merged_data_clean = sp500.dropna(subset=['AI_Exposure', 'Automation_Focus', 'Human_Capital_Impact', 'Innovation_Focus', 'Regulatory_Risk', 'Productivity_Gains'])

# Summary statistics of the final analysis sample
summary_stats = merged_data_clean.describe()
print(summary_stats)
print(f"Variation in 'AI_Exposure': {merged_data_clean['AI_Exposure'].nunique()}")
print(f"Variation in 'Human_Capital_Impact': {merged_data_clean['Human_Capital_Impact'].nunique()}")

```

                    ret   AI_Exposure  Automation_Focus  Human_Capital_Impact  \
    count  10956.000000  10956.000000      10956.000000          10956.000000   
    mean      -0.000299      0.000020          0.000050              0.000004   
    std        0.019315      0.000047          0.000146              0.000016   
    min       -0.163848      0.000000          0.000000              0.000000   
    25%       -0.010776      0.000000          0.000000              0.000000   
    50%        0.000454      0.000000          0.000000              0.000000   
    75%        0.010645      0.000018          0.000041              0.000000   
    max        0.250239      0.000559          0.001801              0.000263   
    
           Innovation_Focus  Regulatory_Risk  Productivity_Gains  
    count      10956.000000     10956.000000        10956.000000  
    mean           0.000525         0.001091            0.000124  
    std            0.000617         0.000425            0.000133  
    min            0.000013         0.000313            0.000000  
    25%            0.000134         0.000807            0.000037  
    50%            0.000305         0.001021            0.000086  
    75%            0.000681         0.001349            0.000171  
    max            0.004259         0.003506            0.001248  
    Variation in 'AI_Exposure': 161
    Variation in 'Human_Capital_Impact': 77
    

**REGRESSION ANALYSIS**
