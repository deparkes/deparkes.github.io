---
layout: post
title: A Machine Learning Workflow
date: 2017-05-12 16:00:36.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
tags:
- analysis
- analytics
- data
- machine learning
author:
  display_name: deparkes
permalink: "/2017/05/12/a-machine-learning-workflow/"
---
Machine learning is an essential part of data science - a field which covers <a href="https://fgiasson.com/blog/index.php/2017/03/10/a-machine-learning-workflow/">a range of activities</a> from data acquisition and cleaning, through to analytics and data visualisation. It can be helpful to think in terms of a <a href="https://www.mckinsey.com/industries/high-tech/our-insights/an-executives-guide-to-machine-learning">machine learning</a> workflow that puts some structure around some of these processes. This post looks at a few existing data science workflows and suggests some other approaches you might want to consider.
There are plenty of data science and machine learning <a href="https://101.datascience.community/tag/workflow/">workflows </a>already out there to draw on. A common starting point is the <a href="https://www.datasciencecentral.com/m/blogpost?id=6448529%3ABlogPost%3A234092">CRISP model</a> which originates in the field of data mining. It can be broken down in to six stages which broadly cover areas of exploration, implementation and deployment:
<ol>
<li>Business understanding</li>
<li>Data understanding</li>
<li>Data preparation</li>
<li>Modelling</li>
<li>Evaluation</li>
<li>Deployment</li>
</ol>
CRISP itself is relatively well established, and is probably already general enough to fit many situations. That said, there are <a href="https://cacm.acm.org/blogs/blog-cacm/169199-data-science-workflow-overview-and-challenges/fulltext">some workflows </a>which attempt to make CRISP more relevant to data science and machine learning. Some of these are quite specialist, such as those focussing on <a href="https://shuaiw.github.io/2016/07/19/data-science-project-workflow.html">data science for Kaggle competitions</a>, or <a href="https://www.nesta.org.uk/blog/9-principles-reforming-public-services-data">using data to change public services</a> which you may also want to look at.
<h1>A Machine Learning Workflow</h1>
The following is my attempt to make sense of different possible approaches to data science and machine learning.
<h2 id="purpose">1. Start with a Purpose</h2>
It's important to try to link you analysis to something in the 'real world' as far as possilbe. Putting this concept first helps avoid going on a '<a href="https://www.futureworkcentre.com/2016/11/hr-analytics-useful-insight-or-data-fishing-trips/">fishing trip</a>' into huge data sets without really knowing why your are doing it and what you hope to achieve.
Starting with a purpose could involve trying to <a href="https://deparkes.co.uk/2016/04/08/analysis-with-impact/">influence a decision</a>, add insight or knowledge to an important area of <a href="https://www.vitae.ac.uk/doing-research/leadership-development-for-principal-investigators-pis/intellectual-leadership/demonstrating-research-impact">academic research</a>, or solve a <a href="https://www.forbes.com/sites/gregsatell/2013/12/03/yes-big-data-can-solve-real-world-problems/#2f0ef06a8896">particular problem</a>. Not understanding the problem or issue can result in wasted time with few good or impactful results.
If you are trying to solve problems or help in a business or organisation a good place to start is <a href="https://deparkes.co.uk/2016/09/16/crunchy-analytics/">Crunchy Questions</a>.
If you are undertaking a data science project as a learning or intellectual exercise it is still worth trying to think about the impact and <a href="https://www.umflint.edu/library/how-select-research-topic">exactly what your are trying to answer</a>. There are many resources available on how to select a good research question such as these from the <a href="https://www.socscidiss.bham.ac.uk/research-question.html">University of Birmingam</a> or <a href="https://libguides.mit.edu/select-topic">MIT</a>.
<h2>2. Get the Data</h2>
Once you've got a good sense of the issue you are going to work on, you need to get your hands on the right data. What exactly this stage means will depend on your project. Some issues that you may encounter include:
<ul>
<li><a href="https://socialtheoryapplied.com/2013/10/29/challenge-accessing-data-phd-journey-far/">Negotiating access/usage rights</a></li>
<li>Finding <a href="https://www.quora.com/Where-can-I-find-large-datasets-open-to-the-public">public data sets</a>
</li>
<li>Overcome <a href="https://www.nesta.org.uk/blog/innovating-open-data-overcoming-challenges">challenges with open data sets</a>
</li>
<li>Purchasing <a href="https://econsultancy.com/blog/67674-what-are-first-second-and-third-party-data/">third party data sets</a>
</li>
</ul>
You may find there is an iterative process between stages one and two as the problem definition becomes clearer, and your / the client's knowledge of the data is also improved.
<h2 id="literature-review">3. Review the Literature</h2>
To <a href="{{site.baseurl}}/2016/03/25/intellectual-protectionism/">avoid re-inventing the wheel</a> you should undertake a literature review. You should already have some sense of the problem area from the time you spent identifying your issue. This stage is an opportunity to develop that knowledge further, and explore what progress has already been made in the area, and whether there are lessons you can learn before you start.
It may seem a rather dry and un-appealing task, but time spent reviewing the current state of the art <a href="https://sites.google.com/site/bikesharekaggle/the-data">will pay dividends</a> in avoiding wasted effort later. <a href="https://shuaiw.github.io/2016/07/19/data-science-project-workflow.html">Some data scientists</a> recommend spending as much as 10 - 20% of the projects time on the literature review.
Your review of the literature could include academic writings, blogs and <a href="https://www.kaggle.com/wiki/PastSolutions">solutions from Kaggle competitions</a> or any other sources of information. You should try to familiarise yourself with domain-specific information relating to the business area, as well problem or question that you are trying to solve or answer. You might find that someone has already published a neat approach to a similar problem, or even that your issue is already solved!
Your literature review doesn't need to be a formal report as such, although <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3715443/">some of the principles</a> of <a href="https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003149">formal scientific literature reviews</a> may be helpful. Plenty of researchers and data scientists have generously published their literature reviews online, so take inspiration from these too. Some examples include <a href="https://dtai.cs.kuleuven.be/events/MLSA16/papers/paper_19.pdf">research papers</a> [pdf], <a href="https://arrow.dit.ie/cgi/viewcontent.cgi?article=1083&amp;context=scschcomdis">Masters theses</a> [pdf], and general <a href="https://cseweb.ucsd.edu/classes/wi17/cse258-a/reports/a058.pdf">project reports</a> [pdf].
Exactly what seems appropriate to you may depend on your project and levels of experience. Some key things you should try to include are:
<ul>
<li>Digging deeper into the problem area</li>
<li>Exploring previous solutions and the current 'state of the art'</li>
<li>Identifying possible approaches and pitfalls</li>
</ul>
<h2 id="define-success">4. Create an Evaluation Framework</h2>
An '<a href="https://datascienceforbusiness.wordpress.com/2016/01/08/the-difa-framework-for-evaluation-data-science-projects/">evaluation framework</a>' will give you some assurance that you have done the right analysis on the right problem and have achieved the right level of performance in your models.
There are a few ways you can approach this. I quite like the <a href="https://becomingadatascientist.wordpress.com/2013/07/10/how-to-quickly-evaluate-a-data-science-project/">description of evaluation</a> in the Becoming a Data Scientist blog which reminds us that getting data science right requires us to <strong>understand the data</strong>, <strong>generate insight</strong>, as well as be technically <strong>well implemented</strong>.
You should be happy: with the answers to questions about the quality, history and suitability of the data; that you will be able to add (testable) insight with your analysis; that your analysis has been correctly implemented (the right analysis for <a href="https://hbr.org/2012/09/are-you-solving-the-right-problem">the right problem</a>).
Understanding how you will measure the success of your modelling can be an important part of establishing an evaluation framework. This can start with defining clear <a href="https://www.leadingagile.com/2014/09/acceptance-criteria/">acceptance criteria</a>, and having a good understanding of your issue. Measuring the success and performance of your models is also likely to come down to <a href="https://www.kaggle.com/wiki/Metrics">metrics </a>for assessing them. It's metrics that give you any indication of whether your model is a suitable approximation of the real world.
There are plenty of lists [<a href="https://www.analyticsvidhya.com/blog/2016/02/7-important-model-evaluation-error-metrics/">1</a>, <a href="https://www.datasciencecentral.com/profiles/blogs/7-important-model-evaluation-error-metrics-everyone-should-know">2</a>, <a href="https://www.analyticsvidhya.com/blog/2016/02/7-important-model-evaluation-error-metrics/">3</a>] of common model evaluation techiques, and SciKit learn also has a <a href="https://scikit-learn.org/stable/modules/classes.html#module-sklearn.metrics">fairly comprehensive list of metrics </a>you may wish to use.
<a href="https://scikit-learn.org/stable/modules/cross_validation.html">Cross validation</a> is also an important step to consider, which helps give some sense about how well your model would perform against an unseen data set. The way this is done in practice is to separate out the initial data set into a '<a href="https://stats.stackexchange.com/questions/19048/what-is-the-difference-between-test-set-and-validation-set">training set</a>' on which the model learns, and a '<a href="https://en.wikipedia.org/wiki/Test_set">test set</a>' which is used to validate the model.
If you working on a competition entry or similar, it may be that your metrics for success are already established. In 'real world' scenarios you may need to work with your client, or explore yourself to figure out sensible ways to <a href="https://www.predictiveanalyticsworld.com/patimes/defining-measures-of-success-for-predictive-models-0608152/5519/">measure the performance of your models</a>.
<h2 id="EDA">5. Explore the Data</h2>
Once you have a sense of how you will assess the success of your analytics you can start to probe and explore your data. <a href="https://en.wikipedia.org/wiki/Exploratory_data_analysis">Exploratory data analysis</a> is the stage where you can really get to grips with your data and start to <a href="https://www.codementor.io/jadianes/data-science-python-r-exploratory-data-analysis-visualization-du107jjms">answer initial questions</a>.
Common goals in EDA include:
<ul>
<li><a href="https://www.learnbymarketing.com/603/variable-importance/">Identify important variables</a></li>
<li><a href="https://en.wikipedia.org/wiki/Anomaly_detection">Detect outliers and anomalies</a></li>
<li><a href="https://www.datasciencecentral.com/profiles/blogs/building-a-predictive-model">Begin to develop models</a></li>
<li><a href="https://docs.newrelic.com/docs/insights/explore-data/data-explorer/event-explorer-query-chart-your-event-data">Explore the data structure</a></li>
<li><a href="https://onlinecourses.science.psu.edu/stat501/node/317">Assess statistical assumptions </a></li>
<li><a href="https://scikit-learn.org/stable/tutorial/machine_learning_map/">Select appropriate techniques</a></li>
</ul>
The techniques used in EDA often involve <a href="https://en.wikipedia.org/wiki/Data_visualization">data visualisation</a> to help identify outliers, trends or patterns that could be of further interest and use later in the workflow. EDA also includes the commonly used <a href="https://en.wikipedia.org/wiki/Five-number_summary">five-number summary</a> of data that can be used to quickly characterise data. Other commonly used techniques include box-plots, histograms, as well as <a href="https://en.wikipedia.org/wiki/Principal_component_analysis">principal component analysis</a>.
EDA, however is more about an approach or way of thinking than any particular tool or technique - delving deeper into the data can reveal phenomena not covered by simply fitting a regression. For <a href="https://en.wikipedia.org/wiki/Exploratory_data_analysis#Example">example</a> simple regression investigating tipping behaviour can hide a range of other activity such as preference for tipping whole-number amounts, gender differences and variance in data. Each one of these avenues could have relevant to the question being studied.
<a href="https://www.itl.nist.gov/div898/handbook/eda/section4/eda4.htm">See some more case study examples of EDA</a>
<a href="https://www.itl.nist.gov/div898/handbook/eda/section1/eda11.htm">Read more about EDA</a>
<h2 id="pre-process">6. Pre-process the Data</h2>
Closely related to exploratory data analysis, is the <a href="https://en.wikipedia.org/wiki/Data_pre-processing">pre-processing</a> of your data itself. This stage is about getting your data ready to solve the problem or issue you identified earlier and helps to avoid the problem of '<a href="https://en.wikipedia.org/wiki/Garbage_in,_garbage_out">Garbage in: garbage out</a>' when  you run your models.
Your EDA may have highlighted issues such has having multiple, separate data sources, incomplete or noisy data. Your data may also not be in the right format to feed into your preferred algorithms. This is another rather unglamourous stage in the workflow, that it will pay dividends to spend some time over. Getting the data pre-processing wrong could at best mean slow running, inefficient analysis or at worst mean spurious results from incorrectly used algorithms with insufficient data.
In theory this can be a simple process of working through standard procedures. You may find things more difficult if you  have many datasets, large amounts of data or many fields to deal with. In these situations a more formal '<a href="https://en.wikipedia.org/wiki/Extract,_transform,_load">ETL</a>' (Extract-Transform-Load) process may be helpful.
Typical tasks during the data pre-processing stage might include:
<ul>
<li>
<strong><a href="https://en.wikipedia.org/wiki/Data_cleansing">Data cleaning</a></strong> - e.g. imputation, smoothing, outlier removal. This is such a common and important task that there are many guides out there to help you which ever tools you use, including SAS [<a href="https://www.ats.ucla.edu/stat/sas/library/nesug99/ss123.pdf">pdf</a>], <a href="https://support.office.com/en-gb/article/Top-ten-ways-to-clean-your-data-2844b620-677c-47a7-ac3e-c2e157d1db19">Excel</a>, <a href="https://data.library.utoronto.ca/cleaning-data-python">Python</a>, and <a href="https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html">R</a>.</li>
<li>
<strong><a href="https://www.ibm.com/analytics/us/en/technology/data-integration/">Data integration</a></strong> - This will be a particular issue if you have data from multiple sources: for example customer data, transaction data, and product data. The goal at this stage is to be able to query the 'data' from one place irrespective of the source. For larger projects there are <a href="https://searchdatamanagement.techtarget.com/feature/Selecting-the-right-data-integration-tool-for-your-needs">tools available</a> to help with data integration.</li>
<li>
<strong><a href="https://en.wikipedia.org/wiki/Data_transformation">Data transformation</a> </strong>- Transformation in this sense refers to operations which will help your analysis run more efficiently, such as normalisation of values, scaling, and aggregation.</li>
<li>
<a href="https://en.wikipedia.org/wiki/Data_reduction"><strong>Data reduction</strong> </a>- This may be more of an issue the more 'big' your data is. Having too many attributes can be a challenge, and <a href="https://www.knime.org/blog/seven-techniques-for-data-dimensionality-reduction">techniques </a>such as principal component analysis, filtering or clustering can help.</li>
<li>
<strong><a href="https://en.wikipedia.org/wiki/Discretization_of_continuous_features">Data discretisation</a> </strong>to convert continuous variables to discrete intervals.</li>
</ul>
Exactly which steps are appropriate will depend on many factors such as the type and quality of your data, the tools you are using, and the algorithms and models you intend to apply.
<h2>7. Engineer Features</h2>
<a href="https://machinelearningmastery.com/discover-feature-engineering-how-to-engineer-features-and-how-to-get-good-at-it/">Feature engineering</a> boils down to selecting the input or ''x' values for your model. In this context a feature is anything that helps you make a prediction with your model. Having the <a href="https://stats.stackexchange.com/questions/18815/increasing-number-of-features-results-in-accuracy-drop-but-prec-recall-increase">right number</a> of <a href="https://en.wikipedia.org/wiki/Feature_(machine_learning)">good features</a> will help improve the the <a href="#define-success">strength of your model</a>, and make you less dependent on picking exactly the right one.
There is no single approach you can take to feature engineering, as the features you will encounter will vary as much as the problems you are working on. Your <a href="#literature-review">literature review</a> and <a href="#eda">EDA </a>may well have identified some likely canditates for good features. Domain knowledge can help, but it <a href="https://www.youtube.com/watch?v=bL4b1sGnILU">isn't always necessary</a> as there are <a href="https://www.researchgate.net/profile/Pedro_Larranaga2/publication/6119033_A_review_of_feature_selection_techniques_in_bioinformatics/links/55b7b5cb08aec0e5f43841e4.pdf">other techniques</a> you can use to <a href="https://www.quora.com/How-do-I-perform-feature-selection">take feature selection</a> such as:
<ul>
<li>
<a href="https://blog.datadive.net/selecting-good-features-part-i-univariate-selection/">Uni-variate feature selection</a> - selects features by determining the significance strength of correlation between the input and output variables.</li>
<li>
<a href="https://blog.datadive.net/selecting-good-features-part-iv-stability-selection-rfe-and-everything-side-by-side/">Recursive feature elimination</a> - starts by fitting all variables to the data, and then removes those with the smallest coefficients until the predictive accuracy of the model is sharply affected.</li>
</ul>
To take feature engineering to the next level you can also do feature creation. An example of this might be important is in predicting house prices. You would expect the land area of the plot to be important in predicting prices, but your data may only have the length and width of your plot. It may not be clear to the model (or you) how the price is linked to these characteristics. Instead you can <em>create</em> a new feature - the land area - from the length multiplied by the width.
This process of transforming and combining existing features is often regarded <a href="https://www.quora.com/What-are-some-best-practices-in-Feature-Engineering">more as as an art than a science</a>. Having a deep understanding of the problem area and the original features themselves can be very beneficial.
<a href="https://www-stat.wharton.upenn.edu/~stine/research/tcnj.pdf">Selecting good features</a> means getting a robust model and reducing the risk of <a href="https://machinelearningmastery.com/overfitting-and-underfitting-with-machine-learning-algorithms/">over fitting</a>, and also makes you less dependent on selecting exactly the right algorithm. The 'added value' of data scientists often comes at the feature engineering stage.
<h2>8. Select, Validate and Tune Your Models</h2>
The type of model or model you ultimately <a href="https://stackoverflow.com/a/30136990">depends </a>on the problem area you are working on and your data. For example, are you trying to <a href="https://www.kdnuggets.com/faq/classification-vs-prediction.html">classify your data or predict trends</a>? Do you have historic data you can use to <a href="https://www.quora.com/What-is-a-training-data-set-test-data-set-in-machine-learning-What-are-the-rules-for-selecting-them">train your model</a>? Your literature search and exploratory data analysis may have given you some ideas, and there is a <a href="https://scikit-learn.org/stable/tutorial/machine_learning_map/">handy guide </a>from sci-kit learn, which may help you work out which models you may wish to consider.
Once you have an idea for the type of model you should be using, you can use a technique called <a href="https://en.wikipedia.org/wiki/Cross-validation_(statistics)">cross validation</a> to <a href="https://robjhyndman.com/hyndsight/crossvalidation/">estimate the predictive abilities of your model.</a> There are <a href="https://en.wikipedia.org/wiki/Model_selection#Criteria_for_model_selection">other techniques</a> you could use, but cross-validation is a common way to check that check that your model is not just a good fit to your training data.
In a simple version of cross validation you would split your sample data into two pots - a training set and a testing set. The training set gives you your model parameters, and your test set give you confidence that they are more widely applicable to just the training set. Cross validation<a href="https://andrewgelman.com/2015/06/02/cross-validation-magic/"> won't guarantee</a> that your model is sensible, but it does help reduce the risk that it is not. Run these <a href="https://stackoverflow.com/a/2598415">validation techniques</a> on different models to check which model or models are most appropriate for your problem.
To take the tuning of your model further you can use '<a href="https://www.quora.com/What-are-hyperparameters-in-machine-learning">hyper-parameter</a>' optimisation. This involves optimising parameters such as the <a href="https://medium.com/data-design/let-me-learn-the-learning-rate-eta-in-xgboost-d9ad6ec78363">learning rate</a> or complexity of the model. Hyperparameters are not learned by the model in the same way that conventional parameters are learned - <a href="https://en.wikipedia.org/wiki/Hyperparameter_optimization">hyperparameter Optimisation</a> generally works by <a href="https://scikit-learn.org/stable/auto_examples/model_selection/randomized_search.html">searching through</a> the hyper-parameter space for one each model to find an optimum solution.
A final stage you can do to improve your machine learning solutions is to use an ensemble of models. By combining the predictions of multiple models it can be possible to make improvements above the predictions of a single one of them. There is a range of <a href="https://scikit-learn.org/stable/modules/ensemble.html">ensemble approaches</a> you could explore, including:
<ul>
<li>
<a href="https://en.wikipedia.org/wiki/Bootstrap_aggregating">Bagging </a>- works by combining the predictions of randomly generated training sets.</li>
<li>
<a href="https://en.wikipedia.org/wiki/Boosting_(machine_learning)">Boosting </a>- similar to bagging, but rather than randomly selected training sets, they are selected depending previous predictions.</li>
<li>
<a href="https://www.quora.com/What-are-examples-of-blending-and-stacking-in-Machine-Learning">Blending and Stacking</a> - The outputs of a first layer of trained models is used to to train the second layer and so on.</li>
</ul>
Ensemble solutions are frequently used in <a href="https://mlwave.com/kaggle-ensembling-guide/">Kaggle competitions</a>.
<h2>9. Finish Up</h2>
Exactly what this looks like will depend on your initial issue, problem or business area. Were you doing some research - in which case publish  your results. Were you enterring a competiation such as Kaggle? In which case submit your entry, and <a href="https://www.kaggle.com/discussion">share your working</a>. If you were supporting a business decision or operational function, you may need to <a href="https://www.techemergence.com/how-to-apply-machine-learning-to-business-problems/">work with the business</a> to make sure your model is implemented correctly, and be prepared to feedback from the business and any new operational data.
