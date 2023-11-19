# Project Goal
Data Science can play a crucial role in marketing by leveraging analytical and statistical skills to extract meaningful insights from data. Through this project, I aim to uncover intriguing insights into customer groups and purchase behavior, which will be instrumental in shaping future marketing campaigns and increasing sales using Instacart's order data.

In this project, my focus will be on:

1. Conducting exploratory analysis to identify interesting customer purchasing behavior, including frequently purchased items and order times.
2. Utilizing basket analysis techniques to discover interesting combinations of items.
3. Developing a customer segmentation model based on customers' purchasing behavior.

The goal is to derive actionable insights that will inform strategic decision-making, enhance marketing strategies, and contribute to the overall success of Instacart's sales initiatives.

# Data
The data is from the previous Kaggle competition hosted by Instacart. All data files are available in a separate 'data' directory.
You can find data dictionary via the [link](https://gist.github.com/jeremystan/c3b39d947d9b88b3ccff3147dbcf6c6b)

# Market Basket Analysis: Association Rules
In this project, the Apriori Algorithm is utilized. This algorithm is widely employed for discovering interesting relationships, patterns, or associations among a set of items in datasets. Specifically, the Apriori algorithm is widely used for mining frequent itemsets and generating association rules.

There are various evaluation metrics available for association rules and for selecting the thresholds.
* Support: Typically, support is used to measure the abundance or frequency (often interpreted as significance or importance) of an itemset in a database. We refer to an itemset as a "frequent itemset" if your support larger than a specified minimum-support threshold. [0,1]

            - 'antecedent support': the proportion of transactions that contain the antecedent
            - 'consequent support': the proportion of transactions that contain the consequent
            - 'support': the proportion of transactions that contain the combined itemset (antecedents or consequents)
            
* Confidence: The probability of seeing the consequent in a transaction given that it also contains the antecedent. (maximal: 1) [0, 1]

* Lift: Commonly used to measure how much more often the antecedent and consequent occur together than we would expect if they were statistically independent. (If antecedent and consequent are independent, the Lift score will be exactly 1.) [0, inf]

* Leverage: The difference between the observed frequency of antecedent and consequent appearing together and the frequency that would be expected if antecedent and consequent were independent. (0 indicates independence.) [-1, 1]

* Conviction: high conviction value means that the consequent is highly depending on the antecedent. [0, inf]

* Mutual Information: The amount of information that knowing the value of one variable provides about another variable. In other words, it quantifies the degree of dependence between two variables. It calculates joint occurrences of the antecedent and consequent in comparison to their individual occurrences in the dataset. [0, inf]

I employed `Mutual Information` as a prominent evaluation metric to assess the frequent sets of items commonly bought together. From the analysis, I can deduce that these frequent sets don't vary significantly based on the order placement time. Furthermore, the investigation revealed some intriguing combinations of products that wouldn't have occurred to me. For example, there is a notable connection between vitamin D and milk.

# Customer Segmentation Analysis
The dataset comprises a diverse range of users. In the subsequent phase of the data mining process, I propose segmenting the users (Instacart customers) based on their order behaviors. This initiative holds potential benefits for the company, particularly in the context of developing future business strategies tailored to the needs of its customers.

For segmenting customers into groups, we need data containing features for each customer.

In this project, I segmentized customers into groups based on various aspects:
1. The number of orders each customer made in each department.
2. The number of orders each customer made at different times.
3. The number of orders each customer made at different times, the number of days since the prior order amd the average number of products ordered per order

## Based on the number of orders they made in each department
The dataset encompasses 21 distinct departments, and I opted to categorize customers into groups based on their order frequency within each department.

The elbow graph analysis indicates an optimal balance between capturing group variance and preventing overfitting when employing a 3-group segmentation.

Upon scrutinizing the visualized silhouette score, a notable pattern emerges: a substantial proportion of data points gravitate towards label 0. The computed average silhouette score, standing at approximately 0.6, implies a robust alignment within clusters and discernible dissimilarity to neighboring clusters, signifying well-defined groups. Conversely, a silhouette score approximating 0 signals potential inter-cluster overlap, posing challenges in precise assignments due to comparable distances. While the current analysis retains its significance, the elevated silhouette score warrants contemplation of further customer segmentation analyses to enhance the precision of clusters.

## Based on the number of orders each customer made at different times
In pursuit of refining cluster precision, I endeavor to categorize customers into groups again with a different condition. This involves manipulating the data to enumerate the number of orders (considering each product as a separate order) made by each customer at distinct timings.

Based on the elbow graph, the number of category was decided to 4.

The average silhouette score slightly exceeds 0.55. Although marginally smaller than the previous analysis, the current method maintains its significance. Each group demonstrates an average silhouette score that is closer to the overall average silhouette score compared to the previous method, further affirming the efficacy of this approach.

## Based on the number of orders each customer made at different times, the number of days since the prior order, the average number of products ordered per order
To achieve greater precision and granularity in grouping, additional features were incorporated to observe the impact on the segmentation score. Specifically, two additional features, namely `avg_product_num` (representing the average number of products ordered per order) and `avg_order_period` (indicating the average days since the prior order), were introduced in addition to the second clustering approach.

Based on the elbow graph, the number of category was decided to 3.

The average silhouette score is around 0.42, which is smaller than the scores obtained from the other two analysis methods. The notable decline in silhouette coefficient values across clusters suggests a lack of homogeneity within the cluster. This indicates that the cluster may not be internally cohesive, possibly harboring distinct subgroups or patterns. In comparison, the previous two clustering approaches demonstrate a superior ability to capture the underlying structure.

# Summary
The project was divided into two different subjects: 1) Basket analysis and 2) Customer segmentation.

In conducting the basket analysis, given the extensive dataset and varying order frequencies throughout the day, the data was segmented into three groups based on the hour of order placement. Utilizing the Apriori algorithm, nearly 400 item sets were derived, each exhibiting a support greater than 0.005 (0.5%) within its respective category. By isolating item sets surpassing a predefined threshold lift, several compelling combinations of items were unearthed, potentially indicating high interdependence. An illustrative example is the pairing of milk and vitamin D within these item sets.

Customer segmentation in marketing is crucial, enabling businesses to tailor campaigns and messages to specific customer groups, thereby increasing relevance and engagement. This targeted approach enhances the effectiveness of marketing efforts, leading to improved customer satisfaction and higher conversion rates. To achieve effective customer segmentation, three different approaches were tried in this project:

1. Based on the number of orders each customer made in each department.
2. Based on the number of orders each customer made at different times.
3. Based on the number of orders each customer made at different times, the number of days since the prior order, and the average number of products ordered per order.

Even though each approach was developed to enhance cluster precision from the previous approach, the first approach yielded the best results. This implies that the most favorable outcomes can be expected when conducting marketing campaigns based on the number of orders each customer made in each department. This approach effectively captured differences between the groups and clustered the customers into three groups quite homogeneously within the group.