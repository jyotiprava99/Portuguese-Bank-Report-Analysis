# Portuguese-Bank-Report-Analysis
#### **1. Introduction**
 
   The purpose of the analysis is to how the bank runs a marketing campaign to bring customers on board with the term deposits.


#### **2. Data Overview**

 - Number of rows: 41188
 - Number of columns: 21
 -  Featues: Age, Duration, Campaign, Pdays, Previous, Emp.var.rate, Cons.price.idx, Cons.conf.idx, Euribor3m, Nr.employed, Job, Martial, Education, Default, Housing, Loan, Contact, Month, Day_of_week, Poutcome, y(Target.))
 - Target Variable : y(Bank Term Deposit Subrcription).
#### **3. Data Preprocessing and Feature Engineering**
   
- **Handling Missing Values** : The dataset contains no missing values, ensuring data completeness and consistenc.
 - **Handling categorical data** : For the categorical features like Job, Marital, Education, Default, Housing, Loan, Contact, Month, Day_of_week, Poutcome, and y (Target) in the Portuguese bank data, a combination of one-hot encoding and label encoding was applied based on real-world hierarchies and domain understanding. One-hot encoding was used for features without inherent order, such as Job, Martial, Contact, Month, Day_of_week, Poutcome. Meanwhile, label encoding was applied to ordinal features like Education and Default, Housing and Loan, reflecting their natural ranking to improve model interpretability and performance. And for target variable(y) manual encoding was done. This balanced approach captures both nominal and ordinal relationships effectively
 - **Outliers** : Handling outliers was crucial for improving model accuracy, but in some cases, extreme values might represent valid customer behaviors, so after careful analysis. The data includes records of students under 18, which is unrealistic for opening a bank term deposit or obtaining loans like housing or personal loans. Therefore, removing these values is a logical step to ensure data relevance and accuracy. In the Campaign feature lot of data lies after 75th percentile so it would make no sense to those values, it is significant from the box plot above as well. So we removed the extreme value 56
- **Feature Transformation**:  MinMax scaling was applied to the features Age, Campaign, Pdays, Emp.var.rate, Cons.price.idx, Cons.conf.idx, Euribor3m, and Nr.employed because the data was not normally distributed, making standard scaling less appropriate. By using MinMaxScaler, the features were scaled to a range of 0 to 1, preserving the original distribution of the data while normalizing the feature values. This ensures that no feature disproportionately influences the model due to diffrent scales.

#### **4. Exploratory Data Analysis (EDA)**

- **Age vs Subscription**: Older customers and younger ones (20-30) tend to subscribe more frequently than middle-aged customers (30-40), who have lower subscription rates.
- **Job vs Subscription**: Job types like "admin", "blue-collar", and "technician" have higher subscription rates, while other workers have lower subscription rates.
- **Duration vs Subscription**: Longer call durations are positively correlated with higher subscription rates. Calls lasting over 300 seconds (5 minutes) are more likely to result in a subscription.
- **Education vs Subscription**: Customers with higher levels of education (tertiary) tend to subscribe more frequently than those with lower levels of education (primary).
- **Previous Campaign Outcome vs Subscription**: If the customer had a successful outcome in the previous campaign, they are much more likely to subscribe again.
- **Default and loan vs Subscription**: People without loans tend to subscribe more frequently.
- **Demographic Variables**: Variables like age, job, and education are strong indicators of whether a customer will subscribe. Younger, highly educated customers with professional jobs are more likely to subscribe..
## **Model Tuning Summary**

The primary goal of model tuning was to enhance the performance of the Random Forest (RF) and Gradient Boosting (GB) models, particularly focusing on improving recall for the minority class (customers likely to subscribe to term deposits).

**Tuning Process**

In this tuning process, RandomForest and GradientBoosting classifiers were subjected to hyperparameter tuning in an effort to improve the model's performance, particularly for the minority class (class 1). Despite tuning, the recall scores for class 1 (indicating the model's ability to correctly identify positive instances) showed little to moderate improvement in both models. For RandomForest, recall slightly increased from 40% to 43%, and for GradientBoosting, recall decreased from 53% to 37% as boosting focuses on best balance between precision, recall and overall performance

To further improve the results, Recursive Feature Elimination (RFE) was applied to Logistic Regression, Gradient boosting where the goal was to enhance the recall for class 1. This method yielded a significant improvement, achieving a recall of 70% for class 1 in Logistic Regression although at the cost of some accuracy in the overall classification.

**Conclusion**

The tuning efforts for RandomForest and GradientBoosting provided marginal improvements in recall for class 1, but they still struggled to correctly predict the minority class. By switching to Logistic Regression combined with Recursive Feature Elimination (RFE), a much better recall was achieved for class 1, improving from 58% to 70% and accuracy of 75. This suggests that RFE with Logistic Regression can be a more effective approach when the primary objective is to improve recall for the minority class, especially in imbalanced dataset.

## **Suggestions to the Bank market team to make customers buy the product.**

The most important features which the bank should focus on to attract more customers to buy term deposit are:
- Duration
- Age
- Campaign
- Euribo3
- nr.employed


1.Duration being one of the most influential factors,i.e. the higher the call duration the higher the chances of a sale. So the bank should focus on enhancing the quality of calls by building a rapport with the customers, decreasing wait time, checking in with the customers, and most importantly take feedback from the customers.

2.Age feature demonstrates that the majority term deposit purchasing capacity lies within the age group of 25-58 yrs adults. So, the bank should target this age group more and allocate more resources in getting in the customers from this particular ag

3.Campaign feature is important as it indicates the number of calls made during the current campaign. The customers do not like to get bothered with too many calls so a sweet spot lies within 1-5 calls, again depending upon the interest of the customer. So the bank should focus on training the sales team so that they can know the interested and non-interested customers based on the behavior,voice modulations, tone, and pitch of the customer.

4.Euribo3 is indicative of the trend that the higher interest rates attract more customers. So there are two things which the bank can pursue which are as follows: -Target the age group which is liable to get higher interest rates (4.5-5) particularly. -Increase the marketing campaign when the interest rates are higher, which can help in bringing more clients on board with the term deposits.

5.nr.employed trend indicates that more number of employees leads to more number of customers, which makes sense because if there are more employees, more leads can be targeted, proper followups and check-ins can be done. On the other hand, customer satisfaction could be achieved by creating a dedicated after-sales team. So, the bank should focus on hiring more people.e group.

## **Report on Challenges faced**

**1.Imbalanced Dataset**:

- Challenges : The dataset exhibited significant class imbalance, with a predominant number of 'No' responses compared to 'Yes' for term deposits. This imbalance led to models that performed well on accuracy but failed to adequately predict the minority class.
- Solution : Implementing oversampling techniques like SMOTE effectively balanced the classes, allowing for improved model training and better identification of the minority class.

**2.Model Performance Variability**:

- Challenges : Different models, including Logistic Regression, Random Forest, and Gradient Boosting, demonstrated varying performance metrics, particularly in terms of recall for the positive class. Initial iterations yielded low recall rates for potential customers.
- Solution : Utilizing advanced metrics such as F1-score and precision-recall curves provided a clearer evaluation of model performance, ensuring a focus on improving recall for the positive class.

**3.Hyperparameter Tuning**:

- Challenges : Tuning hyperparameters for complex models like Random Forest and Gradient Boosting was time-consuming and resource-intensive. Despite various tuning attempts, improvements were minimal, leading to a need for an effective strategy to optimize model performance without excessive computational load.
- Solution : By using more efficient search strategies like RandomizedSearchCV, along with systematic evaluation of a reduced set of hyperparameters, streamlined the tuning process and reduced computational load.

**4.Feature Selection Complexity**:

- Challenges : Identifying relevant features that contributed significantly to model performance was challenging. Implementing Recursive Feature Elimination (RFE) revealed that while some features were beneficial, others introduced noise, complicating the model training process.
- Solution : Combining RFE with domain knowledge helped in selecting impactful features while reducing noise, leading to enhanced model performance.

**5.Evaluation Metrics Confusion**:
- Challenges : The reliance on accuracy as a metric was misleading due to the imbalanced nature of the dataset. This necessitated a shift in focus toward metrics like precision, recall, and F1-score to better assess model performance, particularly in correctly identifying the minority class.
- Solution : Establishing a consistent evaluation framework centered on precision, recall, and F1-score ensured a comprehensive assessment of model effectiveness, particularly for the minority class.

**6.Computational Resource Limitations**:
- Challenges : Some models, particularly ensemble methods like Gradient Boosting, required substantial computational resources, resulting in longer training times and kernel crashes. This created bottlenecks in the model development process.
- Solution : To address computational resource limitations, I relied solely on local resources without utilizing cloud computing or distributed systems. This approach led to longer training times, requiring patience while the kernel executed the model training processes.
