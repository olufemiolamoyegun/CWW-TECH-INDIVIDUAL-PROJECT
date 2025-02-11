# 📊 CWW-TECH INDIVIDUAL PROJECT: Office Pens & Printers - Product Sales EDA  

## 🚀 Project Overview  
This project analyzes office pen and printer sales using **R** to extract insights and track business performance metrics.  

## 🏆 Key Objectives  
- ✅ Clean & validate sales data  
- ✅ Conduct Exploratory Data Analysis (EDA)  
- ✅ Identify sales trends and business opportunities  
- ✅ Define a business metric for performance tracking  

## 📂 Dataset Information  
- **Records:** 15,000  
- **Variables:** 9 (Sales method, Customer details, Revenue, etc.)  

## 🛠️ Technologies Used  
- **R** (ggplot2, dplyr)  
- **Data Visualization** (Histograms, Heatmaps)  

---

## 📌 Data Cleaning Process  
### 🔹 **Step 1: Load Required Libraries**
```r
install.packages("ggplot2")
install.packages("dplyr")
library(ggplot2)
library(dplyr)


# Load the dataset
df <- read.csv("C:/Users/Olufemi/Desktop/personal-project.csv")

# Check data structure
str(df)
head(df)

# Summary of dataset
summary(df)


# Check for missing values in revenue column
sum(is.na(df$revenue))

# Impute missing values with the mean
df$revenue <- ifelse(is.na(df$revenue), mean(df$revenue, na.rm = TRUE), df$revenue)

# Verify changes after imputation
summary(df$revenue)


# Histogram of revenue
hist(df$revenue, main = "Histogram of Revenue", xlab = "Revenue", col = "blue")



📈 Key Findings

1️⃣ Revenue vs. Number of Items Sold → Strong positive correlation (0.67) 💰
2️⃣ Revenue vs. Week → Slight negative trend (-0.16) 📉
3️⃣ Items Sold vs. Week → Weak correlation (-0.04), suggesting a stable sales trend.



📢 Recommendations for Business Growth

🔹 Increase Sales per Customer – Offer discounts, bundles, or explore cross-selling opportunities.
🔹 Improve Customer Retention – Use rewards programs and referral incentives.
🔹 Optimize Sales Channels – Test various methods (e.g., email, calls) to determine the most effective approach.
🔹 Expand Market Reach – Target new regions or customer segments.
🔹 Monitor Revenue Trends – Track average revenue per customer to assess profitability over time.
