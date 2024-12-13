# Predictive Analytics for Football Player Valuation
![image](https://github.com/user-attachments/assets/cdc7ba54-6168-4012-b5c7-a133c9f8a9ee)
## 1.Introduction
Football has transformed from a beloved sport into a global phenomenon, influencing both the hearts of fans and the financial strategies of clubs. In this era, clubs are not just athletic organizations but intricate business entities navigating the complexities of a multi-billion-dollar industry. At the heart of this transformation lies the valuation of players—once solely based on on-field performance, now a critical factor in strategic decision-making.

### 1.1 The Evolution of Football Analytics
![image](https://github.com/user-attachments/assets/75dc6c25-ac08-4e83-8056-111df361db72)
The rise of sports analytics has revolutionized football, offering clubs the ability to gain deep insights into player performance, team dynamics, and transfer strategies. Modern football has moved from relying on intuition and tradition to adopting data-driven approaches that optimize outcomes across various domains, including recruitment, injury management, and financial planning.

This shift is especially evident when contrasting wealthy, state-owned clubs like Manchester City and PSG—capable of extravagant spending on marquee players—with resource-constrained clubs like Brighton, Dortmund, and Liverpool. The latter have excelled in leveraging smart signings and data-informed strategies to compete at the highest levels. For these clubs, effective recruitment is not just a strategy for success but a necessity for survival.

Brighton’s sharp recruitment policies, Liverpool’s analytical prowess, and Dortmund’s ability to unearth hidden gems are testaments to how clubs can challenge financial powerhouses through data-driven decision-making. These strategies emphasize sustainability, long-term planning, and finding undervalued talent—changing the narrative that success in football hinges solely on financial muscle.

### 1.2 The Role of Data in Transfer Markets
Player valuation has become a cornerstone for clubs, shaping their ability to balance squad quality and financial sustainability. In an era of skyrocketing transfer fees and thin margins between success and failure, accurate player valuation ensures clubs allocate resources optimally. This project aims to contribute to this critical aspect by building predictive models tailored to football’s unique ecosystem.

We focused on position-specific analysis—goalkeepers, defenders, midfielders, and forwards—using machine learning algorithms to predict market values based on performance metrics. By exploring relationships between attributes such as age, playing time, and contribution to team success, we provide a transparent and interpretable valuation model. This approach ensures clubs have actionable insights for real-world scenarios, from player negotiations to squad planning.

### 1.3 Motivation Behind the Project
Driven by our passion for football and analytics, this project represents more than a technical exercise. It’s an exploration of the sport’s dynamic ecosystem, where emotion, strategy, and data intersect. By analyzing the Premier League player dataset, we delve into the stories hidden in the numbers, unraveling patterns and trends that contribute to understanding player performance and value.

Our ultimate goal is to equip clubs, agents, and analysts with practical tools for smarter decision-making in an increasingly complex transfer market. In doing so, we align with the broader narrative of using data-driven methodologies to enhance the beautiful game.

This project demonstrates how technology can empower clubs to compete effectively, regardless of financial constraints, and underscores the vital role of data in shaping the future of football.

## 2. Data Collection and Preprocessing

### 2.1 Data Sources
Our dataset for this project was sourced from three primary platforms:

#### [**FBRef**](https://fbref.com/):
We collected detailed EPL football player statistics for the 2022-23 season from **FBRef**, which provided a rich set of attributes across various categories, including:

![image](https://github.com/user-attachments/assets/abf29678-4200-434f-8b38-a7a4dc77d838)

- **Standard Stats**: Basic performance metrics.
- **Goalkeeping**: Specific stats for goalkeepers.
- **Advanced Goalkeeping**: In-depth metrics for goalkeepers.
- **Shooting**: Stats related to shot attempts and goals.
- **Passing**: Pass completion rates, assist-related data, etc.
- **Pass Types**: Different categories of passes (e.g., through balls, crosses).
- **Goal and Shot Creation**: Metrics capturing offensive creation.
- **Defensive Actions**: Data on tackles, interceptions, and clearances.
- **Possession**: Metrics related to a player’s ball control and possession.
- **Playing Time**: Number of minutes that a player has spent on the field.
- **Miscellaneous Stats**: Other performance-related data that may not fall under the above categories.

**FBRef** provides per 90-minute (P90) stats, allowing for an accurate comparison across players with different amounts of playing time.

#### [**FotMob**](https://www.fotmob.com/):
The performance column data, representing a player’s overall performance in matches, was sourced from **FotMob**. This column proved to be a crucial factor in the project, providing an additional dimension to player valuation beyond traditional stats.

#### [**Transfermarkt**](https://www.transfermarkt.com/):
**Transfermarkt** provides transfer values, which are considered the gold standard for player market valuation. These values serve as the target variable (Y) in our predictive models.

### 2.2 Data Preprocessing
Once the data was gathered, we faced several challenges in combining and cleaning the data:

- **Concatenation of DataFrames**: We used Pandas to concatenate the 10 different dataframes from **FBRef** into a single dataset. This process involved merging data across various columns representing different player stats.
  
- **Missing Data Handling**: One of the major issues encountered was the presence of missing values across different player positions. For example, goalkeepers lacked many of the attributes related to shooting and passing, while outfield players had missing values for goalkeeper-specific stats. To handle this, we filled missing values with 0. While this might seem like an oversimplification, it allowed us to proceed with model training without introducing any biases or unnecessary complications in the dataset.

- **Position-Specific Data Handling**: Not all players had the same set of attributes. For instance, midfielders and forwards would have fewer goalkeeper-related stats, and defenders would have fewer passing stats. The filling of NaN values with 0 helped maintain consistency across the dataset while preventing artificial inflation of stats for positions that didn't require certain attributes.

- **Performance Data**: We merged the performance data from **FotMob** into the dataset. This column helped provide a more holistic view of a player’s abilities and was one of the key features influencing our market value prediction model.

### 2.3 Data Transformation
After gathering and cleaning the data, we proceeded to transform the dataset into a format suitable for machine learning:

- **Feature Engineering**: We selected relevant features (e.g., shooting, passing, defensive actions, etc.) for each position (Goalkeeper, Defender, Midfielder, Forward) to train position-specific models.

## 4. Data Exploration

### Distribution of Players by Position
![image](https://github.com/user-attachments/assets/0edd43c5-9e97-48ac-8e4c-d363577895fe)

The pie chart depicting the distribution of player positions shows a balanced composition of defenders, midfielders, and forwards in the dataset. Goalkeepers make up 8.1% of the dataset, reflecting the typical single goalkeeper role on the field. The presence of defenders at 35.5% highlights their strategic importance in defense, while midfielders, accounting for 29.7%, emphasize their crucial role in both attack and defense. Forwards, representing 26.8%, underscore the focus on goal-scoring abilities. This distribution illustrates a well-rounded squad structure, balancing various roles needed for a competitive team.

### Frequency of Ages (15 to 37)
![image](https://github.com/user-attachments/assets/f461a55e-d38a-432f-9d4f-d48bc628b5b4)

The age distribution of players in the Premier League forms a bell-shaped curve, with a peak around the 22-30 age range. This indicates that the majority of players fall within their prime years, a common trend in professional football. The decrease in players over the age of 30 reflects the challenges of maintaining a top-tier career in the physically demanding Premier League. This pattern underscores the league's emphasis on players at their peak performance levels, contributing to its reputation as one of the most competitive leagues globally.

### Number of Players per Team
![image](https://github.com/user-attachments/assets/5853cfb5-f3d4-49fc-944f-a7e8bc1ca244)

The distribution of the number of players per team, while showing some variation, primarily reflects each club's squad management and recruitment strategy. Differences in the number of players from team to team are influenced by factors like budget, injury management, and tactical preferences, which can shape the size and composition of the squad.

### Number of Players per Nation
![image](https://github.com/user-attachments/assets/5b2d8186-e440-490f-88cb-9d4e975e4d41)

The dataset reveals a significant number of English players compared to other nationalities, likely due to the Premier League's origin and the requirement for homegrown talent. The league's international appeal is evident, with players recruited from all over the world, contributing to the diverse skill sets and backgrounds of the teams. This mix enhances the global viewership and fan engagement of the league, reinforcing its cosmopolitan nature.

### Age vs. Market Value with Regression Line
![image](https://github.com/user-attachments/assets/be616090-fd07-4690-ac8d-eed1dcec4a6a)

The regression plot illustrating the relationship between age and market value reveals a clear downward trend in player market value as age increases. Younger players tend to command higher market values due to their potential, athleticism, and future prospects. This negative correlation is visually emphasized by the regression line, which highlights the significant impact of age on player valuation. This insight is valuable for teams and analysts when making decisions regarding player recruitment and market strategies.

### Goal Distribution for Each Team
![image](https://github.com/user-attachments/assets/0b345987-7d7c-4247-86af-b46d342ed5de)

The analysis of goals scored and conceded by teams in the Premier League for the 2022/2023 season provides valuable insights into team performance. Teams with a balanced approach, such as Manchester City, which boasted the highest number of goals scored and the fewest conceded, had a clear competitive advantage and secured top positions in the league. In contrast, teams struggling in both offense and defense, like Southampton, Leeds United, and Leicester City, faced relegation, demonstrating the importance of a balanced team structure for success.

### Clustered Correlation on Matrix for Relevant Features
![image](https://github.com/user-attachments/assets/f8480d7a-1a6c-4639-b781-ba095dc160e0)

The correlation matrix reveals that goalkeeping-related features are positively correlated with each other, while other position-specific features, such as shooting and passing, also show strong correlations within their respective categories. This pattern is visually evident in the matrix, where similar features tend to group together, indicating that certain attributes are inherently linked to specific positions and roles on the field. This insight helps in understanding the relationships between different player metrics and can guide feature selection for predictive modeling.


## 5. Predictive Analytics Performance Results

### Introduction
In this section, we evaluate the performance of our predictive models across different player positions: Goalkeepers, Defenders, Midfielders, and Forwards. Each position requires a tailored approach to account for its unique attributes and contributions to the game. Therefore, instead of a single model, we built separate models for each position.

We chose **Multiple Linear Regression (MLR)**, **Random Forest (RF)**, and **Extreme Gradient Boosting (XGB)** due to the following reasons:
- **MLR**: A straightforward model to establish baseline performance and interpret relationships between features and market value.
- **RF**: A powerful ensemble learning method to handle non-linear relationships and capture feature interactions effectively.
- **XGB**: Known for its efficiency and performance, XGB can handle large datasets and complex feature dependencies while avoiding overfitting.

To optimize performance, we implemented **automated hyperparameter tuning** using iterative looping techniques. This approach allowed us to identify the most optimized parameters for each model and maximize their predictive accuracy.

Separate models for each position were essential to account for the distinct statistical profiles of goalkeepers, defenders, midfielders, and forwards. This specialization allows each model to focus on the features most relevant to its respective role, thereby improving prediction accuracy.

---

### Multiple Linear Regression (MLR) Results
The results for MLR highlight its performance across different positions. While the model performs well for most positions, certain challenges are evident, especially in predicting market values for forwards, where variability in features like goal contributions creates additional complexity.

### Visualizing Results: Actual vs. Predicted Market Values
For each position, the scatter plot visualizes the predicted market values against the actual values, highlighting the regression line to observe model fit.

#### Goalkeepers
- **Mean Squared Error (MSE):** 17.17  
- **Root Mean Squared Error (RMSE):** 4.14  
- **R² Score:** 0.89  
![image](https://github.com/user-attachments/assets/de2688e2-2ff7-4aa2-b486-d1b6dec69961)


#### Defenders
- **Mean Squared Error (MSE):** 38.22  
- **Root Mean Squared Error (RMSE):** 6.18  
- **R² Score:** 0.82  
![image](https://github.com/user-attachments/assets/19829e80-4221-4cf6-9065-b2880fa918c0)


#### Midfielders
- **Mean Squared Error (MSE):** 45.74  
- **Root Mean Squared Error (RMSE):** 6.76  
- **R² Score:** 0.89  
![image](https://github.com/user-attachments/assets/9ed03e6e-ef9b-43f0-9ec6-c105d7396294)


#### Forwards
- **Mean Squared Error (MSE):** 111.43  
- **Root Mean Squared Error (RMSE):** 10.56  
- **R² Score:** 0.83  
![image](https://github.com/user-attachments/assets/e40a6321-ebda-4fe1-9603-a5afec444ec8)


### Model Evaluation: Overall Performance of MLR

To assess the overall effectiveness of the MLR model, we computed the average performance metrics across all positions:

- **Overall Mean Squared Error (MSE):** 53.39  
- **Overall Root Mean Squared Error (RMSE):** 6.91  
- **Overall R² Score:** 0.86  

These results indicate that the MLR model provides a solid baseline, achieving good predictive accuracy across all positions. Its high R² score (0.86) reflects strong alignment between predicted and actual market values. However, the model demonstrates variability in performance, with higher error rates for forwards compared to other positions. This suggests that while MLR effectively models simpler relationships, it may not fully capture the complexity of market valuation for attacking players.

By benchmarking these metrics against other models (RF and XGB), we can determine the best-fit model for this dataset in the final conclusion.


## Random Forest (RF) Results
The Random Forest model was selected for its ability to handle non-linear relationships and capture feature interactions effectively. With its ensemble learning approach, RF combines multiple decision trees to reduce overfitting and improve predictive accuracy. This model demonstrates robust performance across all positions, offering a balance between interpretability and accuracy.

### Visualizing Results: Actual vs. Predicted Market Values
For each position, the scatter plot visualizes the predicted market values against the actual values, highlighting the regression line to observe model fit.

#### Goalkeepers
- **Mean Squared Error (MSE):** 7.30  
- **Root Mean Squared Error (RMSE):** 2.70  
- **R² Score:** 0.92  

![image](https://github.com/user-attachments/assets/fe198a9f-be4e-42d9-ae83-0190369266ea)


#### Defenders
- **Mean Squared Error (MSE):** 34.26  
- **Root Mean Squared Error (RMSE):** 5.85  
- **R² Score:** 0.85  

![image](https://github.com/user-attachments/assets/1bdcbbb3-5004-4a93-a01e-1f551f51aaa8)


#### Midfielders
- **Mean Squared Error (MSE):** 49.50  
- **Root Mean Squared Error (RMSE):** 7.04  
- **R² Score:** 0.84  

![image](https://github.com/user-attachments/assets/f1df6189-2467-476e-943a-f7da9985f08a)


#### Forwards
- **Mean Squared Error (MSE):** 60.68  
- **Root Mean Squared Error (RMSE):** 7.79  
- **R² Score:** 0.91  

![image](https://github.com/user-attachments/assets/3e58b1c3-ef9b-4edb-9498-4fe83bda368d)


### Model Evaluation: Overall Performance of RF
To assess the overall effectiveness of the RF model, we computed the average performance metrics across all positions:

- **Overall Mean Squared Error (MSE):** 37.94  
- **Overall Root Mean Squared Error (RMSE):** 5.85  
- **Overall R² Score:** 0.88  

These results highlight the Random Forest model's ability to generalize well across all player positions. Its lower error rates (MSE and RMSE) and higher R² scores, particularly for goalkeepers and forwards, indicate strong predictive accuracy and robust handling of non-linear feature interactions. The RF model consistently outperforms MLR in capturing complex patterns, making it a strong contender for the best-fit model. 

Further comparisons with the XGB model will determine its relative standing as the optimal predictive model.


## XGBoost (XGB) Results
The XGBoost model was chosen for its high performance, efficiency, and ability to handle complex feature interactions while minimizing overfitting. By leveraging gradient boosting, XGB provides superior accuracy and scalability, making it an excellent fit for predictive analytics in this project.

### Visualizing Results: Actual vs. Predicted Market Values
For each position, the scatter plot visualizes the predicted market values against the actual values, highlighting the regression line to observe model fit.

### Feature Importance Visualization
In addition to the Actual vs. Predicted Market Values result visualization, we analyzed the top features contributing to market value predictions using XGBoost's feature importance metric. The bar charts mentioned along with the Actual vs. Predicted Market Values result visualization highlights the top 10 features for the each position using XGB model.
This visualization provides insights into the most influential variables, helping us understand the model's decision-making process.


#### Goalkeepers
- **Mean Squared Error (MSE):** 3.16  
- **Root Mean Squared Error (RMSE):** 1.78  
- **R² Score:** 0.96  

![image](https://github.com/user-attachments/assets/33b74e70-34a6-4c84-a8ec-cfc9c7564060)
![image](https://github.com/user-attachments/assets/d543779d-951c-4342-bb60-5bd4e0dec65e)


#### Defenders
- **Mean Squared Error (MSE):** 27.01  
- **Root Mean Squared Error (RMSE):** 5.20  
- **R² Score:** 0.88  

![image](https://github.com/user-attachments/assets/e8879deb-118b-4072-bb37-52185b91440d)
![image](https://github.com/user-attachments/assets/c5a41645-223c-4f3c-a5ef-f27ce3c8b655)


#### Midfielders
- **Mean Squared Error (MSE):** 54.50  
- **Root Mean Squared Error (RMSE):** 7.38  
- **R² Score:** 0.87  

![image](https://github.com/user-attachments/assets/98a3f16c-ffca-4cca-88cd-161334f0ab3d)
![image](https://github.com/user-attachments/assets/db8991d2-9dac-47ad-81b9-3c4f8aad7863)


#### Forwards
- **Mean Squared Error (MSE):** 47.49  
- **Root Mean Squared Error (RMSE):** 6.89  
- **R² Score:** 0.89  

![image](https://github.com/user-attachments/assets/9aebcf1a-cdcb-4d90-a507-f043a23d5088)
![image](https://github.com/user-attachments/assets/9a46dafd-3630-4af8-8d13-65dce9811d39)


### Model Evaluation: Overall Performance of XGB
To assess the overall effectiveness of the XGBoost model, we computed the average performance metrics across all positions:

- **Overall Mean Squared Error (MSE):** 33.04  
- **Overall Root Mean Squared Error (RMSE):** 5.31  
- **Overall R² Score:** 0.90  

These results underscore XGBoost's superior performance, achieving the lowest overall error rates (MSE and RMSE) and the highest R² scores among all models tested. Its ability to generalize well across diverse positions and identify critical features makes XGBoost a top candidate for the best-fit model. 


### Implementation of XGBoost on New Data:

We implemented a pipeline to process newly added data by:

1. **Identifying the player's position**  
   - Determines the player's position (e.g., GK, DF, MF, FW) based on input data.

2. **Selecting the appropriate position-specific XGBoost model and feature set**  
   - Uses pre-trained XGBoost models tailored for each position with relevant feature sets.

3. **Scaling the player's feature values**  
   - Applies the corresponding pre-trained scaler to normalize the feature values.

4. **Predicting the player's market value**  
   - Outputs the predicted value alongside the actual value for evaluation.

This approach ensures that the model remains relevant for updated datasets and real-time player evaluations. Below is a sample output demonstrating this functionality:

![image](https://github.com/user-attachments/assets/9e287282-9166-4ca4-8679-6115ecdbf3b8)


## 6. Conclusion
Our approach to building separate predictive models for each player position stems from the unique characteristics and statistical profiles of Goalkeepers, Defenders, Midfielders, and Forwards. By tailoring the models to each position, we ensured that position-specific attributes were appropriately weighted, leading to better performance compared to a one-size-fits-all approach.

After evaluating the results, XGBoost emerged as the best-fit model for our dataset, achieving the lowest overall error rates (Mean Squared Error and Root Mean Squared Error) and the highest R² scores across all positions.

XGBoost demonstrated consistent and superior performance across Goalkeepers, Defenders, Midfielders, and Forwards. Its overall metrics—MSE: 33.04, RMSE: 5.31, R²: 0.90—were better than both RF and MLR. The model's ability to provide clear interpretability through feature importance analysis helped identify the most critical factors influencing market value predictions. Its ability to model complex, non-linear relationships between features and target variables makes it particularly effective for diverse datasets like ours.

By leveraging gradient boosting techniques, XGBoost captures intricate patterns in the data without overfitting. The automated hyperparameter tuning process further improved its accuracy, ensuring it was well-calibrated for each position. Additionally, XGBoost’s scalability makes it highly efficient for large datasets, ensuring it is suitable for more extensive and complex football data.

This model has significant real-world applications. Clubs can use it to estimate player market values, aiding in transfer decisions and budget planning. Scouts can identify undervalued players to optimize recruitment strategies. Agents and players can utilize the model's insights to justify contracts or transfers. Investors or sponsors can assess a player’s monetary potential based on their performance metrics, promoting data-driven decision-making. Furthermore, football federations can use this model to monitor and regulate market value trends, promoting fair play and equity.

This project bridges the gap between advanced data science techniques and football analytics, offering a reliable and interpretable tool for player valuation. It adds value by promoting transparency in market value estimations, supporting informed decision-making for stakeholders, and emphasizing the importance of position-specific analytics to enhance talent management. By focusing on both accuracy and interpretability, our models align with real-world requirements, demonstrating the power of data-driven insights in modern football.







