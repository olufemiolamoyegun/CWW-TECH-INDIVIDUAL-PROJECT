# CWW-TECH-INDIVIDUAL-PROJECT USING R Office Equipments and Stationaries Product Sales EDA

PROBLEMS 

Describe the validation and cleaning steps for every column in the data
 Exploratory Analysis to answer the customer questions ensuring you include:
 Two different types of graphics show single variables only
At least one graphic showing two or more variables ©Description of your findings
e Definition of a metric for the business to monitor
1. How should the business monitor what they want to achieve?
o Estimate the initial value(s) for the metric based on the current data.
e Final summary including recommendations that the business should undertake


install.packages("ggplot2")
install.packages("dplyr")
dim(personal_project) 
df <- read.csv("C:\\Users\\Olufemi\\Desktop\\personal-project.csv")
str(personal_project) 
head(personal_project) 
str(personal_project); summary(personal_project)
sum(is.na(personal_project$revenue)); mean(is.na(personal_project$revenue)) 
#Impute the missing values in the revenue column using the mean of the non-missing values
personal_project$revenue <- ifelse(is.na(personal_project$revenue), mean(personal_project$revenue, na.rm = TRUE), personal_project$revenue) 

#Check the summary of the revenue column after imputation
summary(personal_project$revenue) 
 dim(personal_project) 
[1] 15000     9
> str(personal_project) 
spc_tbl_ [15,000 × 9] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ week             : num [1:15000] 2 6 5 4 3 6 4 1 5 5 ...
 $ sales_method     : Factor w/ 3 levels "Call","Email",..: 2 3 1 2 2 1 2 2 2 1 ...
 $ customer_id      : chr [1:15000] "2e72d641-95ac-497b-bbf8-4861764a7097" "3998a98d-70f5-44f7-942e-789bb8ad2fe7" "d1de9884-8059-4065-b10f-86eef57e4a44" "78aa75a4-ffeb-4817-b1d0-2f030783c5d7" ...
 $ nb_sold          : num [1:15000] 10 15 11 11 9 13 11 10 11 11 ...
 $ revenue          : num [1:15000] 97.1 225.5 52.5 97.1 90.5 ...
 $ years_as_customer: num [1:15000] 0 1 6 3 0 10 9 1 10 7 ...
 $ nb_site_visits   : num [1:15000] 24 28 26 25 28 24 28 22 31 23 ...
 $ state            : chr [1:15000] "Arizona" "Kansas" "Wisconsin" "Indiana" ...
 $ client_cat_yrs   : chr [1:15000] "New Customers" "New Customers" "Advocates" "Existing Clients" ...
 - attr(*, "spec")=List of 3
  ..$ cols   :List of 9
  .. ..$ week             : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ sales_method     : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  .. ..$ customer_id      : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  .. ..$ nb_sold          : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ revenue          : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ years_as_customer: list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ nb_site_visits   : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ state            : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  .. ..$ client_cat_yrs   : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  ..$ default: list()
  .. ..- attr(*, "class")= chr [1:2] "collector_guess" "collector"
  ..$ delim  : chr ","
  ..- attr(*, "class")= chr "col_spec"
 - attr(*, "problems")=<externalptr> 
> head(personal_project) 
# A tibble: 6 × 9
   week sales_method customer_id      nb_sold revenue years_as_customer nb_site_visits
  <dbl> <fct>        <chr>              <dbl>   <dbl>             <dbl>          <dbl>
1     2 Email        2e72d641-95ac-4…      10    97.1                 0             24
2     6 Email & Call 3998a98d-70f5-4…      15   225.                  1             28
3     5 Call         d1de9884-8059-4…      11    52.6                 6             26
4     4 Email        78aa75a4-ffeb-4…      11    97.1                 3             25
5     3 Email        10e6d446-10a5-4…       9    90.5                 0             28
6     6 Call         6489e678-40f2-4…      13    65.0                10             24
# ℹ 2 more variables: state <chr>, client_cat_yrs <chr>
> str(personal_project); summary(personal_project)
spc_tbl_ [15,000 × 9] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ week             : num [1:15000] 2 6 5 4 3 6 4 1 5 5 ...
 $ sales_method     : Factor w/ 3 levels "Call","Email",..: 2 3 1 2 2 1 2 2 2 1 ...
 $ customer_id      : chr [1:15000] "2e72d641-95ac-497b-bbf8-4861764a7097" "3998a98d-70f5-44f7-942e-789bb8ad2fe7" "d1de9884-8059-4065-b10f-86eef57e4a44" "78aa75a4-ffeb-4817-b1d0-2f030783c5d7" ...
 $ nb_sold          : num [1:15000] 10 15 11 11 9 13 11 10 11 11 ...
 $ revenue          : num [1:15000] 97.1 225.5 52.5 97.1 90.5 ...
 $ years_as_customer: num [1:15000] 0 1 6 3 0 10 9 1 10 7 ...
 $ nb_site_visits   : num [1:15000] 24 28 26 25 28 24 28 22 31 23 ...
 $ state            : chr [1:15000] "Arizona" "Kansas" "Wisconsin" "Indiana" ...
 $ client_cat_yrs   : chr [1:15000] "New Customers" "New Customers" "Advocates" "Existing Clients" ...
 - attr(*, "spec")=List of 3
  ..$ cols   :List of 9
  .. ..$ week             : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ sales_method     : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  .. ..$ customer_id      : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  .. ..$ nb_sold          : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ revenue          : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ years_as_customer: list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ nb_site_visits   : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ state            : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  .. ..$ client_cat_yrs   : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  ..$ default: list()
  .. ..- attr(*, "class")= chr [1:2] "collector_guess" "collector"
  ..$ delim  : chr ","
  ..- attr(*, "class")= chr "col_spec"
 - attr(*, "problems")=<externalptr>

EXPLANATORY ANALYSIS
      week             sales_method  customer_id           nb_sold     
 Min.   :1.000   Call        :4962   Length:15000       Min.   : 7.00  
 1st Qu.:2.000   Email       :7466   Class :character   1st Qu.: 9.00  
 Median :3.000   Email & Call:2572   Mode  :character   Median :10.00  
 Mean   :3.098                                          Mean   :10.08  
 3rd Qu.:5.000                                          3rd Qu.:11.00  
 Max.   :6.000                                          Max.   :16.00  
    revenue       years_as_customer nb_site_visits     state          
 Min.   : 32.54   Min.   : 0.000    Min.   :12.00   Length:15000      
 1st Qu.: 52.65   1st Qu.: 1.000    1st Qu.:23.00   Class :character  
 Median : 90.95   Median : 3.000    Median :25.00   Mode  :character  
 Mean   : 95.58   Mean   : 4.959    Mean   :24.99                     
 3rd Qu.:107.75   3rd Qu.: 7.000    3rd Qu.:27.00                     
 Max.   :238.32   Max.   :39.000    Max.   :41.00                     
 client_cat_yrs    
 Length:15000      
 Class :character  
 Mode  :character  
                   
                   
                   
> str(personal_project); summary(personal_project)
spc_tbl_ [15,000 × 9] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ week             : num [1:15000] 2 6 5 4 3 6 4 1 5 5 ...
 $ sales_method     : Factor w/ 3 levels "Call","Email",..: 2 3 1 2 2 1 2 2 2 1 ...
 $ customer_id      : chr [1:15000] "2e72d641-95ac-497b-bbf8-4861764a7097" "3998a98d-70f5-44f7-942e-789bb8ad2fe7" "d1de9884-8059-4065-b10f-86eef57e4a44" "78aa75a4-ffeb-4817-b1d0-2f030783c5d7" ...
 $ nb_sold          : num [1:15000] 10 15 11 11 9 13 11 10 11 11 ...
 $ revenue          : num [1:15000] 97.1 225.5 52.5 97.1 90.5 ...
 $ years_as_customer: num [1:15000] 0 1 6 3 0 10 9 1 10 7 ...
 $ nb_site_visits   : num [1:15000] 24 28 26 25 28 24 28 22 31 23 ...
 $ state            : chr [1:15000] "Arizona" "Kansas" "Wisconsin" "Indiana" ...
 $ client_cat_yrs   : chr [1:15000] "New Customers" "New Customers" "Advocates" "Existing Clients" ...
 - attr(*, "spec")=List of 3
  ..$ cols   :List of 9
  .. ..$ week             : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ sales_method     : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  .. ..$ customer_id      : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  .. ..$ nb_sold          : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ revenue          : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ years_as_customer: list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ nb_site_visits   : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
  .. ..$ state            : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  .. ..$ client_cat_yrs   : list()
  .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
  ..$ default: list()
  .. ..- attr(*, "class")= chr [1:2] "collector_guess" "collector"
  ..$ delim  : chr ","
  ..- attr(*, "class")= chr "col_spec"
 - attr(*, "problems")=<externalptr> 
      week             sales_method  customer_id           nb_sold     
 Min.   :1.000   Call        :4962   Length:15000       Min.   : 7.00  
 1st Qu.:2.000   Email       :7466   Class :character   1st Qu.: 9.00  
 Median :3.000   Email & Call:2572   Mode  :character   Median :10.00  
 Mean   :3.098                                          Mean   :10.08  
 3rd Qu.:5.000                                          3rd Qu.:11.00  
 Max.   :6.000                                          Max.   :16.00  
    revenue       years_as_customer nb_site_visits     state          
 Min.   : 32.54   Min.   : 0.000    Min.   :12.00   Length:15000      
 1st Qu.: 52.65   1st Qu.: 1.000    1st Qu.:23.00   Class :character  
 Median : 90.95   Median : 3.000    Median :25.00   Mode  :character  
 Mean   : 95.58   Mean   : 4.959    Mean   :24.99                     
 3rd Qu.:107.75   3rd Qu.: 7.000    3rd Qu.:27.00                     
 Max.   :238.32   Max.   :39.000    Max.   :41.00                     
 client_cat_yrs    
 Length:15000      
 Class :character  
 Mode  :character  
                   
                   
                   
> sum(is.na(personal_project$revenue)); mean(is.na(personal_project$revenue)) 
[1] 0
[1] 0
> personal_project$revenue <- ifelse(is.na(personal_project$revenue), mean(personal_project$revenue, na.rm = TRUE), personal_project$revenue) 
> summary(personal_project$revenue) 
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  32.54   52.65   90.95   95.58  107.75  238.32 
> par(mar=c(1,1,1,1))
> hist(personal_project[[“revenue”]], main = “Histogram of Number of Items Sold”, xlab = “Number of Items Sold”) 
ggplot(data = melted_cor, aes(x = Var1, y = Var2, fill = value)) +
  geom_tile() +
  scale_fill_gradient2(low = "blue", high = "red", mid = "white", 
                       midpoint = 0, limit = c(-1, 1), name = "Correlation") +
  geom_text(aes(label = value), size = 4) +
  theme_minimal()
>
> # Calculate the correlation matrix between revenue, nb_sold, and sales_method
ggplot(data = cor_matrix, aes(x = Var1, y = Var2, fill = value)) + geom_tile() + scale_fill_gradient2(low = “blue”, high = “red”, mid = “white”, midpoint = 0, name = “Correlation”) + theme_minimal() + theme(axis.text.x = element_text(angle = 45, vjust = 1, hjust = 1))  


The result is a heatmap that shows the correlation between revenue and products sold for different weeks. You can see that there is a positive correlation between revenue and products sold (0.67), a negative correlation between revenue and week (-0.16), and a weak correlation between products sold and week (-0.04).

Conclusion and Summary 

The result is a heatmap that shows the correlation between revenue and products sold for different weeks. You can see that there is a positive correlation between revenue and products sold (0.67), a negative correlation between revenue and week (-0.16), and a weak correlation between products sold and week (-0.04). 

- Increase the number of items sold per customer by offering discounts, bundles, or cross-selling products.
- Increase the retention and loyalty of the customers by providing excellent customer service, rewards, or referrals.
- Increase the effectiveness of the sales methods by testing different combinations of email, call, and other channels, and measuring their impact on the revenue
•	Increase the market share and reach of the business by expanding to new states or regions, or by targeting different segments of customers.
•	Monitor the average revenue per customer over time and across different categories, and evaluate the performance and profitability of the business.

