---
title: Stackoverflow Tag Prediction
layout: post
post-image: "https://cdn.techjuice.pk/wp-content/uploads/2016/10/stackoverflow2.jpg"
description: Predict Tags for given question title and its body
tags:
- EDA
- Machine Learning
- OneVsRest Classifier
- NLP
---

StackOverflow Tag predection is an facebook's hiring challenge in Kaggle 7 years ago.For more information check [this](https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/).They want us to develop a system which can assign tags to a questions in stackoverflow site automatically.

<h2> Introduction </h2>
The Question and answer site like stackoverflow allows users to assign tags manually for their questions in order to make them easier to find.There are some problems in assigning manually that is some users may unable to find a suitable tags for their questions. And other main problem is choice of choosing tags is infinite.To Overcome this kind of problem we need to develop a system which will assign the tags automatically.

	
![image](https://media.makeameme.org/created/lets-get-started-v3u3zd.jpg)
 
 **Contents in this Blog**
 - Problem statement
 - Data overview
 - Data Preprocessing
 - Featurization
 - Feature Engineering
 - Converting tags for Multilabel problem 
 - Building the Model
 - Results and Observations
 
 <h3>Problem Statemet</h3>
 The task is to predict the tags (a.k.a. keywords, topics, summaries), given only the question text and its title. The dataset contains content from disparate stack exchange sites, containing a mix of both technical and non-technical questions.Read full statemnt on [kaggle](https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/)
 
 <h3>Data Overview<h3>
 All of the data is in 2 files train.csv and test.csv
 
 **train.csv**
 
 		 Number of Rows : 6034195
		 Number of Columns : 4
		 Size of train set : 6.7GB
		 Duplicates: yes
		 NUll values : Yes
		 Columns:
		 	 Id - A unique Identifier for each post or question
			 Title - title for a question (it was plain text)
			 Body - Body of a question (It contains html tags, code segemnts , some descrtiption)
 			 Tags - tags are seperated with space
			 
let get an instance of a dataset . I mean datapoint

**Title**:
	``` MVC4 StyleBundle not resolving images ```
	
**Body**:
	<p>My question is similar to this:</p>

	<blockquote>
	  <p><a href="http://stackoverflow.com/questions/9780099/asp-net-mvc-4-minification-background-images">ASP.NET MVC 4 Minification &amp; Background 	Images</a></p>
	</blockquote>

	<p>Except that I want to stick with MVC's own bundling if I can. I'm having a brain crash trying to figure out what the correct pattern is for specifying style bundles such that standalone css and image sets such as jQuery UI work.</p>

	<p>I have a typical MVC site structure with <code>/Content/css/</code> which contains my base CSS such as <code>styles.css</code>. Within that css folder I also have subfolders such as <code>/jquery-ui</code> which contains its CSS file plus an <code>/images</code> folder. Image paths in the jQuery UI CSS are relative to that folder and I don't want to mess with them.</p>

	<p>As I understand it, when I specify a <code>StyleBundle</code> I need to specify a virtual path which does not also match a real content path, because (assuming I'm ignoring routes to Content) IIS would then try to resolve that path as a physical file. So I'm specifying:</p>

	<pre><code>bundles.Add( 
    new StyleBundle("~/Content/styles/jquery-ui")
        .Include("~/Content/css/jquery-ui/*.css"));
	</code></pre>

	<p>rendered using:</p>

	<p><code>@Styles.Render("~/Content/styles/jquery-ui")</code></p>

	<p>I can see the request going out to:</p>

	<p><code>http://localhost/MySite/Content/styles/jquery-ui?v=nL_6HPFtzoqrts9nwrtjq0VQFYnhMjY5EopXsK8cxmg1</code></p>

	<p>This is returning the correct minified CSS response. 
But then the browser sends a request for a relatively linked image as:</p>

	<p><code>http://localhost/MySite/Content/styles/images/ui-bg_highlight-soft_100_eeeeee_1x100.png</code></p>

	<p>Which is a <code>404</code>.</p>

	<p>I understand that the last part of my URL <code>jquery-ui</code> is an extensionless URL, a handler for my bundle, so I can see why the relative request for the image is simply <code>/styles/images/</code>. </p>

	<p>So my question is <strong>what is the correct way</strong> of handling this situation? </p>

**Tags** : 
	css jquery-ui asp.net-mvc-4 bundle asp.net-optimization
	
