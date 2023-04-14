# Customer segmentation from Olist (Brazilian E-commerce)

## Context

Olist wants a customer segmentation for its marketing team in order to identy different customer profils.

## Method

- [Data aggregation cleaning and RFM segmentation](#1)
- [Dimension reduction using T-sne](#2)
- [Clustering using K-mean](#3)
- [Stability test (model and time)](#4)
- [group analysis](#5)

## Data aggregation cleaning and RFM segmentation<a class='anchor' id='1'></a>

Aggregation of the 9 datasets provided into one with client_id as primary key. <br/><br/>
Outlier detection using Isolation Forest.<br/><br/>
RFM segmentation + feature selection:
- dataset final features: last purchase date(recency), total purchase count (frequency), total purchase amount (monetary), delivery time, mean reviews score, item most purchased, customer state (area), payment type

<p align=center>Purchases between oct 2016 and oct 2018</p>

<p align=center><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/repartition_des_donn%C3%A9es_dans_le_temps.png?raw=true"  width="60%" height="60%"></p><br/>

<p align=center>Total purchase amount distribution without outliers</p>
<p align=center><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/analyse_univariee_IFR_total_purchase_amount.png?raw=true" width="100%" height="100%"></p><br/>

- **final dataset size: 8 columns, 460,547 rows (customers)**
<p align=center><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/df_if2_head_short.png?raw=true" width="100%" height="100%"></p>

We will split the dataframe in 2: 

- the data from 2017 will be used to elaborate and train a model
- the data from 2018 will be used to test the reliability and robustness of the model


## Dimension reduction using T-sne<a class='anchor' id='2'></a>

T-sne (t-distributed stochastic neighbor embedding) is an unsupervised, non-linear technique for data exploration and visualisation.<br/> 
It allows to reduce the dimensions of the data (here from 8 to 2) to be able to visualize it without loosing informations.  

<p align=center>Data visualisation after T-sne reduction</p>
<p align=center><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne.png?raw=true" width="40%" height="40%"></p>

## Clustering using K-mean<a class='anchor' id='3'></a>

K-mean is an unsupervised algorithm that will find clusters with the nearest mean by minimizing cluster variances.<br/>
Results are good for k=4, k=6 or k=7.<br/>

<div>
<p align=center>
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_k_4.png?raw=true" width="30%" height="30%">
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_k_6.png?raw=true" width="30%" height="30%">
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_k_7.png?raw=true" width="30%" height="30%">
</p>
</div><br/>

Validation with Silhouette Coefficient.<br/>
Calculate the mean intra-cluster distance (a) and the mean nearest-cluster distance (b) for each sample. The Silhouette Coefficient for a sample is `(b - a) / max(a, b)`

<div>
<p align=center>
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_sihouette2.png?raw=true" width="30%" height="30%">
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_sihouette6.png?raw=true" width="30%" height="30%">
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_sihouette7.png?raw=true" width="30%" height="30%">
</p>
</div>
The homogeneity of the groups and the value of the coefficient 0.3 &lt; x &lt; 0.4 confirm the relevance of the clustering.

## Stability test model and time<a class='anchor' id='4'></a>

To ensure the relevance of the model, we will test both its reliability by initializing the clusters centroids randomly and its robustness over time.

#### Model reliability

Loop with `method random` for centroids initiation to see if the model finds the same clusters.<br/><br/>
Iterations 1 to 6<br/><br/>
Visual results:
<div>
<p align=center>
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_iteration_0.png?raw=true" width="30%" height="30%">
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_iteration_1.png?raw=true" width="30%" height="30%">
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_iteration_2.png?raw=true" width="30%" height="30%">
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_iteration_3.png?raw=true" width="30%" height="30%">
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_iteration_4.png?raw=true" width="30%" height="30%">
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_iteration_5.png?raw=true" width="30%" height="30%">
</p>
</div>
<br/>

Numerical results, an iteration `n` in compared with `n-1`
<div>
<p align=center>
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_heatmap_-1.png?raw=true" width="30%" height="30%">
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_heatmap_0.png?raw=true" width="30%" height="30%">
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_heatmap_1.png?raw=true" width="30%" height="30%">
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_heatmap_2.png?raw=true" width="30%" height="30%">
  <img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_heatmap_3.png?raw=true" width="30%" height="30%">
</p>
</div>
<br/>

#### Model robustness

Use of the ARI (adjust random index).<br/>
The Rand Index computes a similarity measure between two clusterings by considering all pairs of samples and counting pairs that are assigned in the same or different clusters in the predicted and true clusterings.

<p align=center>
<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/tsne_kmean_stabilite_temp.png?raw=true" width="50%" height="50%">
</p><br/>
After 5 month, the ARI of the model collapses and then come back to an high index. It show the robustness of the model through time.<br/>
A way to improve the model would be to retrain it with the data from 2017 and 2018 together and test it with the data of 2019 when available.

## Group analysis<a class='anchor' id='5'></a>

Quick analysis of the clusters found by the model (more details in the ppt presentation).

#### Group 0: One time customer

- Little amount, pay by cash
_ Mostly from Sao Paulo

- One time customer


<img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/polar0.png?raw=true" width="30%" height="30%">
</th>
<th>

- Little amount, pay by cash
- Mostly from Sao Paulo

</th>
</tr>
</div>

