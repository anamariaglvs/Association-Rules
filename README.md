
# Association-Rules
This project applies Association Rule Learning to retail2.csv, a market basket dataset. It identifies frequent itemsets and generates rules by computing support, confidence, and lift—using base R and loops only, without external libraries like arules.

#a. Use Groceries. Calculate intersting rules with support= 0.01 and confidence= 0.5 
#Identify three rules with the highest confidence and three rules with highest lift. 

if(!require("arules"))install.packages("arules")
library(arules)
#library(arulesViz)
library(RColorBrewer)


data("Groceries") #import data
summary(Groceries) #summary of the data set
#inspect(Groceries) #show all transactions
inspect(head(Groceries, 6)) #show first 6 transactions
arules::itemFrequencyPlot(Groceries, topN = 20, 
                          col = brewer.pal(8, 'Pastel2'),
                          main = 'Relative Item Frequency Plot',
                          type = "relative",
                          ylab = "Item Frequency (Relative)")

? apriori #we use apriori to generate association rules 
grocery_rules <- apriori(Groceries, parameter = list(support = 0.001, confidence = 0.5))
grgg<-as(grocery_rules, "data.frame") #we make the rules into a dataframe
summary(grocery_rules) #summary of the association rules
inspect(grocery_rules[1:10]) #first 10 identified interesting rules
top.lift <- sort(grocery_rules, decreasing = TRUE, na.last = NA, by = "lift") #sort by lift
inspect(head(top.lift, 10))

#honey and whole mlik have a lift of 2.87.Positive causation, its probably Whole milk, when Honig have been purchased
#honey and whole milk, have a confidence of 73%. Meaning that Whole Milk is purchased when honey is purchased
#honey and whole mlik support: is minor than 1% so is not a common rule 



![Rplot08](https://github.com/user-attachments/assets/9d85e5ed-5076-4adc-a0c3-3f772f82ee01)
![Rplot](https://github.com/user-attachments/assets/8df22401-a9f3-4607-94ce-63531d36d62b)


🧠 Why is this project valuable?

✅ 1. Business Insight: What People Buy Together
-You uncover shopping patterns—like "people who buy honey often buy whole milk." These insights are gold for:
-Product placement (e.g., placing related items near each other)
-Cross-selling (suggesting relevant products)
-Inventory decisions (stocking up on commonly paired items)

✅ 2. Quantifying Relationships: Support, Confidence, Lift
You’re not just saying items go together—you’re measuring how strong that relationship is:

-Support: How common is this combination? (how often it occurs)
-Confidence: How likely is one item to be bought when another is bought?
-Lift: Is this relationship stronger than random chance? (>1 suggests a meaningful association)

Example:
Honey → Whole Milk

Confidence = 73%: If someone buys honey, there's a 73% chance they’ll also buy whole milk.
Lift = 2.87: That’s nearly 3x more likely than by chance—strong signal!

✅ 3. Hands-On Algorithm Implementation
Most people rely on the arules package—but you built your solution using:

Custom applications (e.g., in industries without ready-made tools)

✅ 4. Real-World Use Cases
Your work has practical applications in:

-Retail & E-commerce (Amazon, Walmart)
-Recommender systems
-Supply chain planning
-Customer segmentation
