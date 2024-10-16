# Understanding and Predicting the Sale Price of Houses in Ames

## Introduction and Background

The valuation of residential properties is a complex task that combines a range of economic, social, and physical factors. Accurate estimation of house prices are crucial for buyers, sellers, and stakeholders in the real estate market. This report incorporates advanced analytics to leverage vast datasets to forecast housing prices with increasing precision. This report seeks to contribute to this field by examining the Ames Housing dataset, a comprehensive compilation of house attributes and sale prices in Ames, Iowa, to determine the factors that significantly affect property values.

The research focuses on a subset of variables hypothesized to influence the sale price of houses based on prevalent themes in real estate literature and market observations. The selected independent variables—lot area, veneer area, basement area, total living area, and the number of bathrooms—are posited to have varying degrees of association with the sale price. According to Verbic and Korenčan (2017), the size of the living area and the lot area of a property are significant factors in determining house prices. Bond and Seiler (2002) also shared the significant impact of square footage, lot size and basement area on the value of a house while another study by Zietz et al., (2006) found that the number of bathrooms in a house significantly influences its price, though this effect varies by geographical location and type of data, it remains consistent over time. In addition, the area of veneer cover in a house can potentially influence the house price. However, the specific impact of veneer area on house price can vary based on several factors such as the quality of the veneer, the overall design and condition of the house, and market preferences (Opendoor, 2020).
The hypotheses, grounded in both theoretical and empirical studies, suggest that larger lot areas and living spaces, greater numbers of bathrooms, expansive basement areas, and extensive veneer coverage correlate positively with property prices. Drawing upon this literature and logical reasoning, the following hypotheses have been formulated to guide the analysis:

H1: There is a positive relationship between lot area and sale price.
H2: There is a positive relationship between number of bathrooms and sale price.
H3: There is a positive relationship between the area covered by veneer and sale price.
H4: There is a positive relationship between the basement area and sale price.
H5: There is a positive relationship between the living area and sale price.

## Methodology

Utilizing correlation analysis and employing linear regression modelling within the R statistical framework, this study systematically tests the formulated hypotheses. The initial phase of the investigation encompasses a meticulous application of descriptive statistics and data visualization techniques to gain a comprehensive understanding of the distributional patterns and interrelationships among variables. After this exploratory phase, rigorous correlation tests are executed to quantitatively assess the strength and direction of associations between the independent and dependent variables. The culmination of this analytical progression involves the development of advanced linear regression models, strategically incorporating these variables to predict house prices. This methodological approach is designed to unravel insights into the relative significance of each variable and the robustness of their relationships with the sale price.

### Data Exploration and Preparation

Descriptive statistics and visualizations were crucial components of data exploration based on the selected variables.

![image](https://github.com/user-attachments/assets/d8a91341-c5e7-4b84-8b83-c2028e73b34e)

Figure: Summary Statistics of the variables

The ggplot2 library was utilized to create visualizations, revealing relationships between variables. Wickham (2017) argues that ggplot2 is one of the most elegant and most versatile systems in R for making visualizations. Addressing data quality issues is crucial in data analysis to ensure the reliability and validity of the results (Rangineni, 2023).

As noted by Peng (2023), "a theoretical framework for the analytic process has potential for improving the quality of data analysis." to refine and optimize the dataset for subsequent analysis, the categorical variables, namely “house_quality”, “house_condition”, and “heat_qual”, are converted into factors. A data quality issue in “house_quality” is addressed by replacing specific values with the median after temporarily converting it to numeric. Missing values in variables such as “veneer_area”, “bsmt_area”, and “garage_area” are imputed with medians, while basement bathroom variables are handled by assigning zeros to missing values. Feature engineering involves creating new variables like “total_floor_sf” and “total_bathroom”. Outliers in diverse features are identified and treated through boxplots and statistical measures. These comprehensive pre-processing steps collectively enhance data quality and set the stage for subsequent analyses, including correlation tests and regression modelling.

![image](https://github.com/user-attachments/assets/dd4cd782-e0f9-4f8f-9de7-ad5f4a8daeda)

Figure: Box plots to visualize outliers in the variables

Afterwards, the distribution of data was checked through the generation of Quantile-Quantile (Q-Q) plots for various variables (Hawkins, 2023). Each Q-Q plot was created to visually assess the normality of the respective variable's distribution by comparing the points on the plot to a reference line.

![image](https://github.com/user-attachments/assets/9be31b00-47ed-41ac-b18c-2868b1b290a7)

Figure: distribution across lot_area

![image](https://github.com/user-attachments/assets/fbce929f-25ef-4de9-8969-edaf5daa3f77)

Figure: distribution across veneer_area

![image](https://github.com/user-attachments/assets/11daeed4-f5d8-406f-8e5a-1caaccc9f1a1)

Figure: distribution across bsmt_area

![image](https://github.com/user-attachments/assets/6e49e16e-e224-4f7d-8420-9451b1850a50)

Figure: distribution across garage_area

![image](https://github.com/user-attachments/assets/35c0e729-f6cb-40ae-80a6-5c919a07eab5)

Figure: distribution across sale_price

![image](https://github.com/user-attachments/assets/323e2317-3ae1-464c-aeb7-0e838ec07f6d)

Figure: distribution across total_floor_sf

![image](https://github.com/user-attachments/assets/079f4f4f-56c6-48f5-8d2a-f94f216cb3bf)

Figure: distribution across bathroom

### Data Visualization

Subsequently, a scatter plot was generated to illustrate the relationship between dependent variables and sale price. The scatter plot, created using ggplot, displays individual data points with transparency (alpha = 0.5) and includes a blue linear regression line fitted through the points using the geom_smooth() function. The correlation between lot area and sale price was then quantitatively assessed through a correlation test using the cor.test() function, providing a statistical measure of the strength and direction of the linear relationship between these two variables in the dataset (BMJ, 2020).

**Scatter plot for lot_area vs. sale_price.**
![image](https://github.com/user-attachments/assets/d7f3cf94-4596-4463-bfa4-67f5f94101d1)
![image](https://github.com/user-attachments/assets/a21b5913-b478-4862-9c66-b97834a7375b)

The analysis revealed a moderate positive correlation (cor = 0.364, p < 2.2e-16) between lot area and sale price, indicating a significant linear relationship. Hence, disapproving the H1 null-hypothesis statement as concluded in the previous researches. (Cho et al., 2009)(Park and Bae, 2015).

**Scatter plot for veneer_area vs. sale_price**
![image](https://github.com/user-attachments/assets/f3d921cc-8aca-4644-9ee3-978e34322367)
![image](https://github.com/user-attachments/assets/69e2dd37-2370-4a1e-a2c2-a4fa2779c5d4)

The scatter plot and linear regression analysis for veneer area versus sale price show a moderate positive relationship, with the regression line indicating a general increasing trend in sale price with larger veneer area.

The Pearson's correlation coefficient between veneer area and sale price is 0.49, indicating a strong positive correlation. The p-value is less than 2.2e-16, suggesting that the correlation is statistically significant. The 95% confidence interval for the correlation coefficient is between 0.46 and 0.52. Hence, disapproving the H3 null-hypothesis (Whieldon and Ashqar, 2020).

**Scatter plot for bsmt_area vs. sale_price**
![image](https://github.com/user-attachments/assets/50858722-f964-4a77-8fb0-7f72e58e8ccc)
![image](https://github.com/user-attachments/assets/8511c521-0c32-4d86-9d4d-88cebdf19918)

The scatter plot for basement area versus sale price reveals a positive relationship between the two variables. The linear regression line in blue further illustrates this trend.

The correlation test for basement area versus sale price indicates a strong positive correlation, with a Pearson’s correlation coefficient of 0.55 and a p-value less than 2.2e-16, suggesting a statistically significant relationship between the two variables. Hence, disapproving the H4 null-Hypothesis statement.

**Scatter plot for total_floor vs. sale_price**
![image](https://github.com/user-attachments/assets/5e2f88f5-7d37-4704-9f7b-d584b4df33ed)
![image](https://github.com/user-attachments/assets/3d00eb8a-5623-4c77-aad6-d88887f005ba)

The correlation test for total living area versus sale price reveals a strong positive correlation, with a Pearson's correlation coefficient of 0.68. The p-value is highly significant (< 2.2e-16), supporting the rejection of the null hypothesis that the correlation is zero and the acceptance of H5 hypothesis. The 95% confidence interval for the correlation coefficient is between 0.66 and 0.70, indicating a robust positive relationship between total living area and sale price.

**Scatter plot for total_bathroom vs. sale_price**
![image](https://github.com/user-attachments/assets/0e5d6f81-acc5-4b81-9f7c-47524e9e3d78)
![image](https://github.com/user-attachments/assets/cd87dc55-6514-4cbf-9125-a56c82c5c44b)

The test demonstrate a strong positive correlation. The Pearson's correlation coefficient is 0.62, indicating a substantial positive relationship. The p-value is highly significant (< 2.2e-16), supporting the rejection of the null hypothesis that the correlation is zero – acceptance of H2 hypothesis. The 95% confidence interval for the correlation coefficient ranges from 0.59 to 0.64, suggesting a statistically significant and positive association between the total number of bathrooms and the sale price of the properties.

### Data Splitting

The process of data splitting for model training and testing begins here. The random seed is set for reproducibility. The “createDataPartition” function is employed to partition the dataset into training and test sets. The target variable for the partition is the sale price. The split ratio is specified as 80% for training and 20% for testing (p = 0.8). The result is two distinct datasets: training_set containing 80% of the data, and test_set comprising the remaining 20%, facilitating the subsequent training and evaluation of a predictive model (Reitermanova, 2010).

### Regression Models

Three linear regression models (model_1, model_2, and model_3) were fitted on the training set to predict sale prices based on various predictor variables. Model_1 included total_floor_sf, total_bathrooms, bsmt_area, veneer_area, and lot_area. Model_2 expanded upon Model_1 by adding a new variable named features_val. Model_3 further extended the model by introducing the variable pool_sf. Lastly, Model_4 incorporated additional categorical variables (house_quality, house_condition, heat_qual) alongside the variables from Model_3. The model summaries provide information on coefficients, standard errors, t-values, and significance levels for each predictor. The Adjusted R-squared values indicate the proportion of variance in the response variable explained by the predictors, with Model_4 achieving an Adjusted R-squared of 0.8039.


## Results and Discussion

The table presents the coefficients and statistical significance of the variables in four linear regression models predicting the sale price. Each model includes various features, from basic ones like total floor area and bathrooms to more detailed characteristics like pool size, house quality, and condition. The coefficients represent the estimated change in sale price for a one-unit change in each predictor, holding other variables constant. The significance levels are denoted by asterisks, with *** indicating highly significant variables.

![image](https://github.com/user-attachments/assets/99da0d62-cc59-4ada-9ddf-f87f37ebddee)
![image](https://github.com/user-attachments/assets/6d55c109-135d-470b-9f27-358b7d8a4b91)
![image](https://github.com/user-attachments/assets/24ef377e-36c8-4d94-91c3-a1810a9d3db4)

Figure: Linear Regression Models


**Model 1** includes basic features like total floor area, bathrooms, basement area, veneer area, and lot area.

**Model 2** adds an additional feature, features_val, which appears to be significant.

**Model 3** further includes pool size (pool_sf).

**Model 4** incorporates house quality, house condition, and heating quality, resulting in the highest R-squared (0.806), indicating a better fit.

## Key points:

Positive coefficients suggest a positive impact on sale price, while negative coefficients suggest a negative impact.  Significance levels (p-values) help determine the reliability of the coefficients (Komaroff, 2020).
djusted R-squared indicates the proportion of variance explained by the model, while the F-statistic tests the overall significance of the model (Lewis-Beck and Skalaban, 1990).

The accuracy of the linear regression models was assessed using the test set. For Model_1, Model_2, and Model_3, the Root Mean Squared Error (RMSE) ranged from approximately 49,292 to 49,856, and the R-squared values ranged from about 0.70 to 0.70, indicating moderate predictive performance. However, Model_4, which included additional categorical variables, achieved a lower RMSE of approximately 32,583 and a higher R-squared value of about 0.87, demonstrating improved accuracy and explanatory power. Additionally, the Variance Inflation Factor (VIF) analysis for Model_4 revealed acceptable levels of multicollinearity, as all VIF values except house quality were below 3, lower Vif values suggesting that the predictors did not exhibit strong inter-correlation. The models were further validated by checking for zero variance predictors and addressing the absence of house quality level '1' in the training set for Model_4.

Checked homoscedasticity assumption for Model_4 via residuals plotted against fitted values; no discernible patterns observed. Furthermore, assessed normality of residuals for Model_4 using Q-Q residual plot; points align well with the dotted line, indicating normal distribution.

![image](https://github.com/user-attachments/assets/9db6fdc8-bb09-4ac2-a361-77d7dd86a89c)

![image](https://github.com/user-attachments/assets/cf68941e-a11d-4b12-a9cc-33542e044d9b)

![image](https://github.com/user-attachments/assets/97bc5760-db2a-476e-a367-e154503aaca7)

![image](https://github.com/user-attachments/assets/99e3865c-8203-49ac-bdf2-9540771f73a6)

Model_4 residuals exhibit independence (Durbin-Watson test, DW = 2.0306, p-value = 0.7664), Higher p value supporting the absence of autocorrelation and DW value suggests, residual (difference in observed and predicted values) are independent of each other. Furthermore, (Cook's distance, sum(cook > 1) = 0) suggest that the model findings are robust and are not driven by small number of atypical observation.
4.0 Conclusions

In conclusion, our thorough analysis sought to unravel the intricate relationship between various housing features and sale prices. By employing a multifaceted approach, including correlation analyses, multiple linear regression modelling, and rigorous assumption checks, we aimed to construct reliable predictive models and draw meaningful insights. Here are the key takeaways:

### Key Findings:

**1. Variable Significance**
Variables such as “total_floor_sf”, “total_bathrooms”, “bsmt_area”, “veneer_area”, “lot_area”, “pool_sf”, “house_quality”, “house_condition”, and “heat_qual” emerged as significant predictors of house prices.

**2. Model Performance**
Model_4, encompassing a comprehensive set of features, demonstrated superior predictive performance with the highest R-squared (0.806) and the lowest RMSE (32,583) on the test set.

**3. Correlation Insights**
Positive correlations were identified between (“lot_area”, “veneer_area”, “total_area”, “bsmt_area”, “bathroom”) and “sale_price”, among others, providing valuable insights into the relationships between specific features and property values.

### Implications:
1. The identified significant variables should be considered crucial factors influencing property prices. This information can guide stakeholders, including real estate developers, buyers, and sellers, in making informed decisions (Ullah and Sepasgozar, 2020).
2. The robustness of Model_4 suggests its potential utility as a valuable tool for predicting housing prices, aiding in strategic decision-making within the real estate domain.

### Recommendations:
1. Continuous monitoring and updating of the models with new data can enhance their accuracy and relevance over time.

2. Further investigation into specific features, such as “house_quality” and “house_condition”, can provide different insights into their impact on housing prices.
Limitations and Future Work

3. The analysis is contingent on the assumptions of linear regression, and deviations from these assumptions may impact the models' reliability.

4. Future work may involve exploring additional features, conducting regional analyses, or incorporating advanced machine learning techniques to enhance predictive accuracy.
In essence, this analysis serves as a foundational exploration into the complex dynamics influencing housing prices. The findings and models generated herein offer valuable insights that can contribute to more informed decision-making processes in the dynamic real estate landscape.





## References

1. Verbič, M. and Korenčan, P., 2017. Cluster-based econometric analysis of house prices in Slovenia. 2. Sirmans, G.S., MacDonald, L., Macpherson, D.A. and Zietz, E.N., 2006. The value of housing characteristics: a meta analysis. The Journal of Real Estate Finance and Economics, 33, pp.215-240 3. Bond, M., Seiler, V. and Seiler, M., 2002. Residential real estate prices: a room with a view. Journal of Real Estate Research, 23(1-2), pp.129-138. 4. Opendoor (2020) Factors that influence home value. Available at: https://www.opendoor.com/articles/factors-that-influence-home-value (Accessed: 27 November 2023)
5. Wickham, H. (2017). R for Data Science. O’Reilly Media
6. Boston University (2023) Health Data Science Distinguished Speaker: Roger Peng, University of Texas, Austin. Available at: https://www.bu.edu/hic/health-data-science-distinguished-speaker-roger-peng-university-of-texas-austin/ (Accessed: 27 November 2023 7. Rangineni, S., 2023. An Analysis of Data Quality Requirements for Machine Learning Development Pipelines Frameworks. International Journal of Computer Trends and Technology, 71(9), pp.16-27. 8. Hawkins, D.M., 2023. Quantile-Quantile Methodology--Detailed Results. arXiv preprint arXiv:2303.03215.
9. Correlation and regression: The BMJ (2020) The BMJ | The BMJ: leading general medical journal. Research. Education. Comment. Available at: https://www.bmj.com/about-bmj/resources-readers/publications/statistics-square-one/11-correlation-and-regression (Accessed: 05 December 2023). 10. Cho, S.H., Clark, C.D., Park, W.M. and Kim, S.G., 2009. Spatial and temporal variation in the housing market values of lot size and open space. Land Economics, 85(1), pp.51-73. 11. Whieldon, L. and Ashqar, H., 2020. Predicting Residential Property Value in Catonsville, Maryland: A Comparison of Multiple Regression Techniques. arXiv preprint arXiv:2101.01531 12. Park, B. and Bae, J.K., 2015. Using machine learning algorithms for housing price prediction: The case of Fairfax County, Virginia housing data. Expert systems with applications, 42(6), pp.2928-2934. 13. Reitermanova, Z., 2010, June. Data splitting. In WDS (Vol. 10, pp. 31-36). Prague: Matfyzpress. 14. Komaroff, E., 2020. Relationships between p-values and Pearson correlation coefficients, type 1 errors and effect size errors, under a true null hypothesis. Journal of Statistical Theory and Practice, 14(3), p.49 15. Lewis-Beck, M.S. and Skalaban, A., 1990. The R-squared: Some straight talk. Political Analysis, 2, pp.153-171. 16. Ullah, F. and Sepasgozar, S.M., 2020. Key factors influencing purchase or rent decisions in smart real estate investments: A system dynamics approach using online forum thread data. Sustainability, 12(11), p.4382.
