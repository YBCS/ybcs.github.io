---
layout: post
comments: true
title:  "A Brief History of Data Leakage in Model Training"
excerpt: "We explore the concept of data leakage in machine learning and cite various sources that discuss this issue in depth."
categories: tech blog
---
### Once upon a time, a model was trained on a dataset, and it performed exceptionally well on the test set. However, when deployed in the real world, it failed miserably. What went wrong? The answer often lies in a phenomenon known as **data leakage**.

<!-- I want to write in sublime text because there is no autocomplte :) -->


You should be suspicious of your model, always.
										- some AI Researcher, probably


Data pre processing can make a lot of difference. Good things, and then leakage. Some manuscripts have "organized" different variations of it. I like this one "quote "

There is no first time ever recorded event of data leakage. It is just a part of model training. So in that respect the title is click baity. However that is not entirely true. In some fields, it is harder to detect data leakage. I prompted my <llm_I_use> and found that it was reported as this. This is actually a snitch story as the author who reported it was complaining about another paper and the reason is they are unable to recreate the performance. If you read some paper, you find.... many such cases.

Today, lets talk about studies with very high dimensional data and in very applied fields like clinical modelling. Why ? because they have high stakes and so studying about it will generalize nicely, or will it ? (what do I even mean here, in this context ?)
In 2016, this team published a paper on guidelines. In 2020, another group of experts published this guideline. 
To summarise the findings of paper 1 
To summarise the <findings>(strike) [advice] of paper 2

Next let's look at this paper which does all of this really well.
it checks all of these boxes

Things we know about how to avoid data leakage are as follows:

Let's go for a test drive. 
How about we first knowingly, convincingly, take a look at an example of.... overfitting.
<llm> do your thing

Do we know if data has overfitted. 

Most guidelines simply have some suggestions. There are no real formula for it. So is it an "art" ?

Now lets try the guidelines:
- reduce the features 
	- how do we know what to pick ?
	- If I just try every known combination after making some problem simplfying decisions and variables, is it still science ? Maybe it is if the results are good ? After all if some unassuming variable turns out to be a good predictor, it may have co-relations, previously unknown. That is a discovery right there. Have there been such before….. Yes plenty … of claims.

- don't ever mix; test and train 
- data is low so lets do some re sampling techniques like nested-CV 
- Lets come up with a strategy to solve for a realistic situation.

## reduce the features 

## The strategy 
### The "situation/setup"
We want to do binary classification. We have only 100 samples to train a model. We have about 50 features. According to this highly cited paper, we should do (.... a long explanation of the technique in the paper)
about 1/3 th samples so about 33 samples. 
How can we choose which to discard?
Let's start with "obvious" techniques.
Look for features which extrapolate to the prediction and drop. (leakage risk)
Look at literature and see which are "shown correlation features". But then again not every problem will have the background literature to make this decision. Lets say our data does not. 
Thankfully there is the concept of "feature extraction". Yeah it does exactly, what it says. 
So we run our model and do just that. But we need to do this inside our nested CV loop. Recall that nested CV is like..... explain 

But here is the question. Every fold might have different features and since data is assumed noisy (what does noisy mean), It is hard to come up with stable features. One strategy here is to simply choose those features which is picked repeatedly more often then others. [this paper backs that … do i understand it ? I hope. ]

There are some feature extraction pipelines which might "look at " entire data. Now why do we want to "extract" more features when we are already trying to get rid of features. Because these features are not some linear combinations of existing features but rather they are different types... say statistical data which tends to look at the entire population... in real settings: genomic data, PCA etc. And in some cases, they are known to have much more predictive power so we cannot ignore them if we have access to them. 

We need to go one step back now. The feature extraction might "leak" data if not done after : train test split. In the case of CV, ... what again ? 




So after all that this is the final pipeline : 







So on the same data lets write some clean and understandable script which is hopefully not wrong. 

Now it does not overfit because now our model is terrible at it. 

Now how do I improve it. 

There is an entire website filled with competitions for the same thing. Kaggle. 

So some few months back (this is actually ages in LLM research years)
People used to bang their head to find something interesting

Now your claude can do this for you 
- So I let my agent try to improvise on my code. I let karpathy's agent prompts do this.

Our script seems to be doing well on all metrics. Data shows that "statistically", it is not overfitting. Again I don't have a formula but....






So to conclude, 
Why am I more confused than when I started ? 




<am I missing anything ? I am trying to think out loud, by writing out my thoughts ; hopefully, I see something and catch some error before I go into real practise. > 


