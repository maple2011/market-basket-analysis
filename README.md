# market-basket-analysis
Discuss the methodology of market basket analysis. How to identify what products are purchased together. Cross-sell opportunity. Recommend product according to the likelihood of purchasing.

Association rule has being an approach to determine what products/items are purchased together. For example, if the probability of purchasing item B is 5% overall, and the probability of purchasing item B given the customer also purchased item A is 50%, then there is a strong association between items B and A. Co-occurrence of Items table can also be built to study what items are more likely to occur together. Concepts such as Lift=prob(item A and item B)/[prob(item A)*prob(item B)] describes whether item A and item B are more likely purchased together.

However, the traditional approach faces challenges when the number of items or their combinations become large. This is true in the real world. 

Unsupervised machine learning provides a solution to identify the items that tend to be purchased together from a large number of items purchase transaction data. Cluster approach provides a solution to idenitfy which items are correlated closely as oppose to other items that show lower correlations.


