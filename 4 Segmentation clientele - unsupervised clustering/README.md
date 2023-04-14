# Customer segmentation from Olist (Brazilian E-commerce)

## Context

Olist wants a customer segmentation for its marketing team in order to identy different customer profils.

## Method

- Data aggregation and cleaning.
- RFM segmentation for feature selection 
- Dimension reduction using T-sne
- Clustering using K-mean
- Stability test using adjusted random score
- group analysis

## Data aggregation and cleaning

Aggregation of the 9 datasets provided into one with client_id as primary key. <br/><br/>
Creation of new features => first purchase date, last purchase date, delivery time, min purchase amount, max purchase amount, total purchase amount, count review score, mean review score, item most purchased. <br/><br/>
Outier detection using Isolation Forest.<br/><br/>

<p align=center>Purchases between oct 2016 and oct 2018</p>

<p align=center><img src="https://github.com/AlexandreLarget/data_scientist_projects/blob/master/4%20Segmentation%20clientele%20-%20unsupervised%20clustering/Images/repartition_des_donn%C3%A9es_dans_le_temps.png?raw=true"  width="70%" height="70%" align=center></p>


