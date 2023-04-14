# Customer segmentation from Olist (Brazilian E-commerce)

## Context

Olist wants a customer segmentation for its marketing team in order to identy different customer profils.

## Method

- Data aggregation cleaning and RFM segmentation
- Dimension reduction using T-sne
- Clustering using K-mean
- Stability test using adjusted random score
- group analysis

## Data aggregation cleaning and RFM segmentation

Aggregation of the 9 datasets provided into one with client_id as primary key. <br/><br/>
Outlier detection using Isolation Forest.<br/><br/>
RFM segmentation + feature selection:
- dataset final features: last purchase date(recency), total purchase count (frequency), total purchase amount (monetary), delivery time, mean reviews score, item most purchased, customer state (area), payment type
- dataset size: 8 columns, 37218 rows (customers)

<p align=center>Purchases between oct 2016 and oct 2018</p>

<p align=center><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/repartition_des_donn%C3%A9es_dans_le_temps.png?raw=true"  width="70%" height="70%"></p><br/>

<p align=center>Total purchase amount distribution without outliers</p>
<p align=center><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/analyse_univariee_IFR_total_purchase_amount.png?raw=true" width="100%" height="100%"></p>

## Dimension reduction using T-sne
T-sne (t-distributed stochastic neighbor embedding) is an unsupervised, non-linear technique for data exploration and visualisation.<br/> 
It allows to reduce the dimensions of the data (here from 8 to 2) to be able to visualize it without loosing informations.  

<p align=center>Data visualisation after T-sne reduction</p>
<p align=center><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne.png?raw=true" width="40%" height="40%"></p>

## Clustering using K-mean

K-mean is an unsupervised algorithm that will find clusters with the nearest mean by minimizing cluster variances.<br/>
Results are good for k=4, k=6 or k=7.<br/>

<div>
<p align=center>
<td><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_k_4.png?raw=true" width="30%" height="30%">
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_k_6.png?raw=true" width="30%" height="30%">
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_k_7.png?raw=true" width="30%" height="30%">
</p>
</div><br/>

Validation with Silhouette Coefficient.<br/>
Calculate the mean intra-cluster distance (a) and the mean nearest-cluster distance (b) for each sample. The Silhouette Coefficient for a sample is `(b - a) / max(a, b)`

<div>
<p align=center>
<td><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_sihouette2.png?raw=true" width="30%" height="30%">
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_sihouette6.png?raw=true" width="30%" height="30%">
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_sihouette7.png?raw=true" width="30%" height="30%">
</p>
</div>
The homogeneity of the groups and the value of the coefficient `0.4<x<0.5` confirm the relevance of the clustering.


