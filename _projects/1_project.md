---
layout: page
title: Analysing Employee Commute Patterns
description: Hierarchical Modeling - Developed Generalized mixed-effects models with time correlated random effects and compared the results using BIC.
img: assets/img/parking.jpg
importance: 1
category: work
tags: formatting math
related_publications: false
---

<span style="font-size:27px;"> **🚗 The Question:**<span>

How do commute distance, employee location, and weekday patterns impact driving frequency? Can we model this behavior effectively?

<span style="font-size:27px;"> **🔍 Exploring the Data:**<span>

A one-month dataset of 1,154 employees' parking swipe records was analyzed. Each commute day (when an employee used their parking card) was tracked by zip code, distance, and day of the week.

Exploratory Data Analysis (EDA):

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <iframe src="/assets/html/zip_chart.html" title="Interactive Zip Code Chart" class="img-fluid rounded z-depth-1" style="width:100%; height:400px; border:none;"></iframe>
    </div>
</div>
<div class="caption">
    There seems to be huge difference in count of employees living at different zip codes and should be accounted for in the model if necessary.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <iframe src="/assets/html/day_chart.html" title="Interactive day Code Chart" class="img-fluid rounded z-depth-1" style="width:100%; height:400px; border:none;"></iframe>
    </div>
</div>
<div class="caption">
    Commute Frequency is highest on average mid week with lowest on weekends.
</div>
 
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <iframe src="/assets/html/driv_pat.html" title="Interactive Driving Pattern Chart" class="img-fluid rounded z-depth-1" style="width:100%; height:500px; border:none;"></iframe>
    </div>
</div>
<div class="caption">
    Average number of drives per day for 50 randomly sampled employees within each zip code. Standard error bars indicate variability in driving frequency.
</div>

<span style="font-size:27px;"> **📊 Modeling to predict commute frequency:** <span>

To predict commute frequency, several models were tested:

🤔 **Linear Regression** - Since observations from the same ID are likely to be more similar to each other than observations from different IDs, independence assumption is simply violated.<br>
🤔 **Mixed-Effects Models** – Consider this model: 
`tdrive = day + (1|id)` (ID is now considered a grouping factor)
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/independence.png" title="example image" class="img-fluid rounded z-depth-1" style="height: 400px; object-fit: contain;" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/qq.png" title="example image" class="img-fluid rounded z-depth-1" style="height: 400px; object-fit: contain;" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/const_var.png" title="example image" class="img-fluid rounded z-depth-1" style="height: 150px; object-fit: contain;" %}
    </div>
</div>
<div class="caption">
    Left: Residuals centered around zero without and evident pattern in data. DW-Test confirmed independence, Centre: Hmm.. Looks normal with slight deviation at the ends, Right: Ouch! the model fails assumption of constant variance due to heteroscadasticity
</div>
Count data often exhibit a mean-variance relationship, where the variance increases as the mean increases.This can lead to non-constant variance.

😎 Generalized Linear Mixed Model – Since `total drives` represents count data, both Poisson and Binomial models are potential choices. However, Poisson assumes that the mean and variance are equal, which is often unrealistic in real-world datasets due to overdispersion. Additionally, `total drives to office` has an upper bound (the total possible commute days in a month per employee), making a Binomial model more appropriate than a Poisson model.
Below is the Model Comparision chart:

<table>
<thead>
<tr>
<th>Model Type</th>
<th>Model Formula (R Code)</th>
<th>Degrees of Freedom</th>
<th>BIC</th>
</tr>
</thead>
<tbody>
<tr>
<td>Linear Regression</td>
<td>tdrive~as.factor(day)+ as.factor(id)</td>
<td>1161</td>
<td>33750.41</td>
</tr>
<tr>
<td>Mixed Effect Model</td>
<td>tdrive~ as.factor(day)+(1|id)</td>
<td>9</td>
<td>26603.19</td>
</tr>
<tr>
<td>Poisson Mixed Effect Model</td>
<td>tdrive ~ as.factor(day) + cdist_scaled + (1 | zip/id)</td>
<td>10</td>
<td>23643.00</td>
</tr>
<tr>
<td>Binomial Mixed Effect Model</td>
<td>cbind(tdrive, 30 - tdrive) ~ as.factor(day) + zip + (1 | id)</td>
<td>9</td>
<td>23407.63</td>
</tr>
</tbody>
</table>
<br>

The BIC for Binomial Model is the lowest and hence, this is the best fit model amongst the others. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img src="/assets/img/binomial_res.png" title="Interactive Driving Pattern Chart" class="img-fluid rounded z-depth-1" style="width:100%; height:auto; border:none;">
    </div>
</div>

The residuals still show some heteroscedasticity, but the variance pattern is less structured compared to the Linear Mixed Effect Model.
While the assumption of constant variance is still not perfectly met, this model provides a better fit than the others.

<span style="font-size:27px;"> **✅ Key Takeaways:**<span>

🚀 Commute behavior varies widely, with some employees driving more frequently than others, even at similar distances.<br>
🚀 A Binomial Mixed-Effects Model best predicts commute frequency, outperforming Linear and Poisson models by accounting for individual variability and bounded commute counts.<br>
🚀 Findings can help optimize parking allocation and inform flexible work policies to reduce peak-hour congestion.

**View the Detailed Project:**

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <embed src="/assets/pdf/parking_project.pdf" type="application/pdf" class="img-fluid rounded z-depth-1" style="width:100%; height:600px; border:none;" />
    </div>
</div>
