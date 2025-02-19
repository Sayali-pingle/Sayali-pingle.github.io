---
layout: page
title: Analysing Employee Commute Patterns
description: Hierarchical Modeling - Developed Generalized mixed-effects models with time correlated random effects and compared the results using BIC.
img: assets/img/parking.jpg
importance: 1
category: work
related_publications: true
---

Simplistic overview of unlocking commute patterns

🚗 The Question:

How do commute distance, employee location, and weekday patterns impact driving frequency? Can we model this behavior effectively?

🔍 Exploring the Data:

A one-month dataset of 1,154 employees' parking swipe records was analyzed. Each commute day (when an employee used their parking card) was tracked by zip code, distance, and day of the week.

Exploratory Data Analysis (EDA):

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <iframe src="/assets/html/zip_chart.html" title="Interactive Zip Code Chart" class="img-fluid rounded z-depth-1" style="width:100%; height:400px; border:none;"></iframe>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <iframe src="/assets/html/day_chart.html" title="Interactive day Code Chart" class="img-fluid rounded z-depth-1" style="width:100%; height:400px; border:none;"></iframe>
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <iframe src="/assets/html/driv_pat.html" title="Interactive Driving Pattern Chart" class="img-fluid rounded z-depth-1" style="width:100%; height:500px; border:none;"></iframe>
    </div>
</div>
<div class="caption">
    Average number of drives per day for up to 50 randomly sampled employees within each zip code. Standard error bars indicate variability in driving frequency.
</div>

Key Findings:

📌 Commute frequency varies significantly by zip code.<br>
📌 Midweek sees the highest driving rates, weekends the lowest.<br>
📌 Some employees drive more frequently than others, even at similar distances.


📊 Modeling the Commute Patterns
To predict commute frequency, several models were tested:

Linear Regression (lm) – Too simplistic, failed to account for variance.
Mixed-Effects Models (lmer, glmer) – Improved performance by accounting for individual differences.
Generalized Linear Model (glm, Poisson Distribution) – The best model! It balanced accuracy, interpretability, and model fit (lowest BIC).
✅ Key Takeaways
🚀 Spatial and temporal factors play a crucial role in commute behavior.
🚀 A Poisson-based model best captures driving frequency.
🚀 Strategic parking and commute planning could optimize employee transportation.




You can also put regular text between your rows of images, even citations {% cite einstein1950meaning %}.
Say you wanted to write a bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
