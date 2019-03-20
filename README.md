## Market-basket-analysis
Discuss the methodology of market basket analysis. How to identify what products are purchased together. Cross-sell opportunity. Recommend product according to the likelihood of purchasing.

Association rule has being an approach to determine what products/items are purchased together. For example, if the probability of purchasing item B is 5% overall, and the probability of purchasing item B given the customer also purchased item A is 50%, then there is a strong association between items B and A. Co-occurrence of Items table can also be built to study what items are more likely to occur together. Concepts such as Lift=prob(item A and item B)/[prob(item A)*prob(item B)] describes whether item A and item B are more likely purchased together.

However, the traditional approach faces challenges when the number of items or their combinations become large. This is true in the real world. 

Unsupervised machine learning provides a solution to identify the items that tend to be purchased together from a large number of items purchase transaction data. Cluster approach provides a solution to idenitfy which items are correlated closely as oppose to other items that show lower correlations.


# Python code (from Jupyter Notebook)
import numpy as np 
import pandas as pd 
import sklearn as skl
from sklearn.decomposition import PCA
from sklearn.datasets import make_classification
from varclushi import VarClusHi
#from decomposition.var_clus import VarClus
import seaborn as sns
import matplotlib.pyplot as plt

EOB_vec_df=pd.read_sas('Y:/eval/cluster_data_1pct.sas7bdat',format=None, index=None, encoding=None,
                chunksize=None,iterator=False)
                
EOB_vec_df.drop('CLM_NBR', axis=1, inplace=True)
EOB_vec_df.head(3)

## check frequency and correlation amount features
EOB_vec_df.apply(pd.value_counts)
EOB_vec_df.corr(method='pearson')

## Display of correlation matrix graphically.
corr = EOB_vec_df.corr()
fig = plt.figure()
ax = fig.add_subplot(111)
cax = ax.matshow(corr,cmap='coolwarm', vmin=-1, vmax=1)
fig.colorbar(cax)
ticks = np.arange(0,len(EOB_vec_df.columns),1)
ax.set_xticks(ticks)
plt.xticks(rotation=90)
ax.set_yticks(ticks)
ax.set_xticklabels(EOB_vec_df.columns)
ax.set_yticklabels(EOB_vec_df.columns)
plt.show()

## Use correlation as distance to cluster features. Generating what features are highly correlated or not correlated.
## Use unsupervised learning (cluster) to group features and know what features tend to occur together, or weakly correlated.
 
EOB_vc = VarClusHi(EOB_vec_df,maxeigval2=1,maxclus=None)
EOB_vc.varclus()
EOB_vc.info
EOB_vc.rsquare

## Plot correlations on features within the same cluster

corr = df.corr()
fig = plt.figure()
ax = fig.add_subplot(111)
cax = ax.matshow(corr,cmap='coolwarm', vmin=-1, vmax=1)
fig.colorbar(cax)
ticks = np.arange(0,len(df.columns),1)
ax.set_xticks(ticks)
plt.xticks(rotation=90)
ax.set_yticks(ticks)
ax.set_xticklabels(df.columns)
ax.set_yticklabels(df.columns)
plt.show()

## Plot correlations on feature between different clusters

df2=EOB_vec_df[['EOB_00158','EOB_00681','EOB_00066','EOB_00067','EOB_00013','EOB_00651','EOB_00135']]
corr = df2.corr()
fig = plt.figure()
ax = fig.add_subplot(111)
cax = ax.matshow(corr,cmap='coolwarm', vmin=-1, vmax=1)
fig.colorbar(cax)
ticks = np.arange(0,len(df2.columns),1)
ax.set_xticks(ticks)
plt.xticks(rotation=90)
ax.set_yticks(ticks)
ax.set_xticklabels(df2.columns)
ax.set_yticklabels(df2.columns)
plt.show()















    

