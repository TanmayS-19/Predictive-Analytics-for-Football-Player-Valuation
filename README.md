# Predictive Analytics for Football Player Valuation

## 1.Introduction
![image](https://github.com/user-attachments/assets/cdc7ba54-6168-4012-b5c7-a133c9f8a9ee)
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

FBRef: We collected detailed football player statistics from FBRef, which provided a rich set of attributes across various categories, including:

Standard Stats: Basic performance metrics.
Goalkeeping: Specific stats for goalkeepers.
Advanced Goalkeeping: In-depth metrics for goalkeepers.
Shooting: Stats related to shot attempts and goals.
Passing: Pass completion rates, assist-related data, etc.
Pass Types: Different categories of passes (e.g., through balls, crosses).
Goal and Shot Creation: Metrics capturing offensive creation.
Defensive Actions: Data on tackles, interceptions, and clearances.
Possession: Metrics related to a player’s ball control and possession.
Miscellaneous Stats: Other performance-related data that may not fall under the above categories.
FBRef provides per 90-minute (P90) stats, allowing for an accurate comparison across players with different amounts of playing time.

FotMob: The performance column data, representing a player’s overall performance in matches, was sourced from FotMob. This column proved to be a crucial factor in the project, providing an additional dimension to player valuation beyond traditional stats.

Transfermarkt: Transfer values, considered the gold standard for player market valuation, were gathered from Transfermarkt. These values serve as the target variable (Y) in our predictive models.

### 2.2 Data Preprocessing
Once the data was gathered, we faced several challenges in combining and cleaning the data:

Concatenation of DataFrames: We used Pandas to concatenate the 10 different dataframes from FBRef into a single dataset. This process involved merging data across various columns representing different player stats.

Missing Data Handling: One of the major issues encountered was the presence of missing values across different player positions. Goalkeepers, for instance, lacked many of the attributes related to shooting and passing, while outfield players had missing values for goalkeeper-specific stats. To handle this, we filled missing values with 0. While this might seem like an oversimplification, it allowed us to proceed with model training without introducing any biases or unnecessary complications in the dataset.

Position-Specific Data Handling: Not all players had the same set of attributes. For example, midfielders and forwards would have fewer goalkeeping-related stats, and defenders would have fewer passing stats. The filling of NaN values with 0 helped maintain consistency across the dataset, while not artificially inflating stats for positions that didn't require certain attributes.

Performance Data: We merged the performance data from FotMob into the dataset. This column helped provide a more holistic view of a player’s abilities and was one of the key features influencing our market value prediction model.

### 2.3 Data Transformation
After gathering and cleaning the data, we proceeded to transform the dataset into a format suitable for machine learning:

Feature Engineering: We selected relevant features (e.g., shooting, passing, defensive actions, etc.) for each position (Goalkeeper, Defender, Midfielder, Forward) to train position-specific models.







