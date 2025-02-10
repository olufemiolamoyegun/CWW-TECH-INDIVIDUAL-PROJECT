CWW-TECH-INDIVIDUAL-PROJECT: Using R to analyze Office Pens and Printers - Product Sales EDA

Problem Overview
In this exploratory data analysis (EDA), we will describe the steps taken to validate and clean the data columns in order to answer key customer questions. This will include:

Conducting exploratory analysis with appropriate visualizations, including at least two separate graphics for single variables and one graphic to examine multiple variables.
Providing a detailed description of the findings.
Defining a business metric that can be tracked and used for monitoring performance.
Business Monitoring and Metric Definition
To monitor the business's performance and track progress toward objectives, we will:

Define a metric for the business to track.
Estimate the initial value of this metric based on the current data.
Provide a final summary and recommendations for business improvement.
Data Cleaning Process
First, let’s load the data and inspect it.

install.packages("ggplot2")
install.packages("dplyr")

# Load the dataset
df <- read.csv("C:/Users/Olufemi/Desktop/personal-project.csv")

# Check data structure
str(personal_project)
head(personal_project)

# Summary of the dataset
summary(personal_project)
The dataset consists of 15,000 records and 9 variables. Key columns include sales methods, customer information, number of items sold, revenue, and state. Next, we check for missing values in the revenue column and impute missing data with the mean value.

# Check for missing values in revenue column
sum(is.na(personal_project$revenue))
mean(is.na(personal_project$revenue))

# Impute missing values with the mean
personal_project$revenue <- ifelse(is.na(personal_project$revenue), mean(personal_project$revenue, na.rm = TRUE), personal_project$revenue)

# Verify changes after imputation
summary(personal_project$revenue)
Data Inspection
After cleaning the data, we proceed to inspect the variables. Key metrics include the number of items sold, revenue, and customer retention (years as a customer). We also look at the sales method and the number of site visits.

str(personal_project)
summary(personal_project)
Exploratory Data Analysis (EDA)
Univariate Analysis

We begin by visualizing single variables. A histogram of the revenue column is generated:

# Histogram of revenue
par(mar=c(1,1,1,1))
hist(personal_project[["revenue"]], main = "Histogram of Revenue", xlab = "Revenue")
Bivariate Analysis

Next, we explore the relationship between revenue, number of items sold, and other variables. A heatmap is used to visualize correlations between these variables:

# Correlation heatmap
ggplot(data = cor_matrix, aes(x = Var1, y = Var2, fill = value)) + 
  geom_tile() + 
  scale_fill_gradient2(low = "blue", high = "red", mid = "white", midpoint = 0, name = "Correlation") + 
  theme_minimal() + 
  theme(axis.text.x = element_text(angle = 45, vjust = 1, hjust = 1))

Key Findings
Revenue vs. Number of Items Sold: There is a positive correlation (0.67), indicating that as more items are sold, revenue increases.
Revenue vs. Week: A slight negative correlation (-0.16) suggests that revenue tends to decrease slightly over time.
Items Sold vs. Week: The weak correlation (-0.04) indicates that the number of items sold does not show a significant trend over time.

Recommendations
Based on the analysis, here are some strategic recommendations for improving business performance:

Increase Sales per Customer: Offer discounts, bundles, or explore cross-selling opportunities to boost the number of items sold.
Customer Retention: Enhance customer retention by providing excellent service, rewards programs, and referral incentives.
Optimize Sales Methods: Test various sales channel combinations (e.g., email, calls) to determine the most effective methods for driving revenue.
Expand Market Reach: Explore opportunities to expand the market by targeting new states or regions, or diversifying customer segments.
Track and Optimize: Continuously monitor average revenue per customer across different categories and time periods to measure profitability.

Conclusion
The analysis suggests that increasing the number of items sold per customer, improving customer loyalty, and refining sales methods are key drivers for boosting revenue. Monitoring the average revenue per customer will also help assess the impact of these initiatives over time.


