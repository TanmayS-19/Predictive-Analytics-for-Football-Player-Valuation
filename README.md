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









