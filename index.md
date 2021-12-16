---
title: An unfortunate data story
cover-img: "assets/img/Title.png"
---

## An unfortunate data story

We started this project with the goal of finding patterns between language use and speaker attributes based on the analysis of millions of quotes in the [Quotebank](https://dlab.epfl.ch/people/west/pub/Vaucher-Spitz-Catasta-West_WSDM-21.pdf) dataset. Our goal was to answer questions such as:

* How does your socio-cultural background, such as nationality, gender, or religion, affect the way you speak?
* Are people who speak about the past usually older?
* Are people who speak with a more positive sentiment usually young?

However, we could not find sufficient patterns between speakers and the way they talk to accurately describe the speaker’s attributes based on a given quote. Nevertheless, we are happy with our findings. To live in a less predictable world, in which we cannot tell exactly who a person is simply by looking at the language features of their quotes, is certainly much more fun. Please follow us on this journey, in which we find out what we can (or maybe more appropriately cannot) say about someone based on their language usage.

## What data is our story based on?

We were given a gigantic amount of data: quotes extracted from newspapers from 2015 to 2020, tens of millions of rows to work with. But that is great, the bigger the data, the more trust-worthy the study. After some intense pre-processing and filtering -- you can read more about it in [this](https://github.com/epfl-ada/ada-2021-project-r-o-c-k/blob/main/Milestone%202/preprocessing_notebook.ipynb) Notebook. We eventually ended up working with exactly 47 779 271 quotes, shared between 451 041 different unique speakers. For the sake of the study, filtering has been performed in order to keep speakers that were born between 1928 and 2016, as it would not make much sense to study the speech of an ancient Roman emperor or a young baby barely able to talk in our contemporary context. For this analysis, six different speaker features were kept: year of birth, gender, occupation, academic degree, and nationality. 

We created features for the millions of quotes available, as well as looked at the speaker attributes for all of the quotes. To cope with limited computing resources, we use a sample of the data to form this data story. However, an early plot from our project, showing the distribution of speaker attributes for all of the 47 779 271 quotes we treated, can be found on this [link](https://github.com/ohallstrom/data-story/blob/master/assets/img/AllQuotesDistribFinal.png).

Anyways, images speak louder than words so below are the distributions of the speaker attributes for all of the quotes in our sample: 

## TODO: ADD RAPH's PLOT

Even though we cannot be certain, it seems like the speakers are dominated by North Americans, Christians and Males...

To show the lexical features that this Data Story is based on, we have used a quote by the R.O.C.K team’s spiritual leader Dwayne Johnson, also known as The Rock. For each quote in Quotebank, the features seen in the following image were generated. 

![alt text](./assets/img/Features.png)
# TODO: Correct typos in image
# TODO: Accept Oskar's proposition

If you did the math, you might had expected a higher verb ratio for the given quote. The reason for that is that we don't include modal auxiliaries when counting the verbs, so 'can' is not counted. Also, you might would have expected the superlative ratio to be the highest adjective ratio. But the ratios for adjectives are, due to our pos-tagging on single words, are only identifying single word comparative adjectives and superlatives. Whenever an adjective is constructed with a more or most in front of it, it is still counted as an ordinal adjective. That is why we do not include these ratios in our further analysis. Please refer to our [README](https://github.com/epfl-ada/ada-2021-project-r-o-c-k/blob/main/README.md) for a more in depth description of the features.

## What does our data look like?

Here is a sneak peak on how the lexical features are mapped to speaker attributes. The boxplots shown are just a fraction of all combinations of lexical features and speaker attributes. We only show one boxplot per lexical feature here, but you can explore as much as you want to satisfy your “data hunger” with [this](https://github.com/epfl-ada/ada-2021-project-r-o-c-k/blob/main/feature_exploration.ipynb) Notebook.

# TODO: increase readability of labels?

![alt text](./assets/img/Plots-01.png)

## Heat maps and distributions

In order to identify the major differences between the language usage of different types of speakers, the statistical Mann-Whitney-U-test is applied on the dataset. With this test, the distribution of a particular lexical feature for different speaker attributes are compared. The U-test outputs a p-value which represents the probability of observing these differences in the samples given that they both come from the same underlying distribution. Given the large number of possible U-tests per cell, two different scoring metrics are used:

## TODO: Formula formatting problem

$Score_{med} = \frac{1}{\med_{P_{i}}}$

$Score_{max} = \frac{1}{\max_{P_{i}}}$

![alt text](./assets/img/Grid-01.png)

As seen from the figures above, it seems that some cells embed significant differences in their distribution. These cells exhibit a high score value either in terms of median or in terms of maximum observed p-value. Large differences are observed from both the median and maximum grid. For instance in [Occupation,Pronoun_per_word], [Gender,Self_Ratio], [Gender,Union_Ratio] … We might be discovering something huge in terms of socio-cultural and language research -- An ADAventurer’s dream coming true. But wait a second, why is the median score so low? Does it mean that only specific pairs within a speaker attribute are different?

We can now look more closely at the most significant and least significant differences by plotting their distributions. We provide you with the top 4 pairs of distributions with the most significant difference, as well as the top 2 pairs of distributions with the least significant difference. Specific feature/attribute distribution can be found in [this](https://github.com/epfl-ada/ada-2021-project-r-o-c-k/blob/main/feature_exploration.ipynb) Notebook.
## TODO: Don't we need to add the plots such as self_ratio for artists and politicians in the notebook above
## TODO: Title below implies that a pair can be stat. significant. Isn't it the difference that is significant?
## Distribution of statistically significant pairs

Significant differences can be seen between various lexical features and date of birth and occupation, shown below. The following can be said: First, speakers born in the 90s seem to use more pronouns than those from the 50s. Second, differences are observed between Politicians and other occupations such as Arts and Sports. Politicians speak more about “us” as a group than artists. And for the ones who only mention themselves in the quotes, it is more likely that they are an artist than a politician -- Well, that’s obvious and quite intuitive! Can we get to the juicy part?

![alt text](./assets/img/Significant_dist_01.png)
<br/><br/>
<br/><br/>
![alt text](./assets/img/Quotes.png)
## TODO: Ralph add his comment

Apart from the pairings with high significance rankings, we can also see interesting relationships in pairings with lower rankings. Looking at the nationality, one can notice a significant difference in the distributions of pronouns and the number of words used between North America and Asia. 

We know you probably went all the way to the bottom of this hoping to find something about gender biases -- quite a hot topic. But you’ll probably not find what you are looking for.  

![alt text](./assets/img/Gender_dist_new.png)

Men and women are kind of similar from a talking point of view. The distribution in terms of sentiment, pronouns, and reference to the “self” show a lot of overlap. Other lexical features / speaker attributes combinations show similar insignificant differences.

## What now?

Should we just call it a day and stop here? Based on the previous observations we have demonstrated some interesting differences in the distributions of feature/attribute pairs, as well as many similarities between some speaker attributes. Would that be enough to achieve our goals of predicting a person’s attributes given a sentence? There’s only one way to find out.

## Model Fitting, Clustering and PCA
## TODO: tables, plots + shord discussion of results?

We did tree-based feature selection and then dimensionality reduction using PCA to see if we could cluster different lexical features and to see if different people speak differently. The features found were [',_per_sentence' 'sign_per_token' 'approx_word_count' 'token_count'
 'adj_per_word' 'verb_per_word' 'base_ratio' 'pres_ratio' 'past_ratio'
 'pronoun_per_word' 'sentiment']. With 6 principle components explaining over 80% of the variance, we could not see any clusters by grouping the main PC’s in 2D. 

![alt text](./assets/img/pca_gender.png)

The overlap between the gender’s lexical features makes it impossible to visualize clusters in 2 dimensions. As shown above, the clusters for males and females cannot be separated. This was the case for all speaker features. We decided to investigate clusters in higher dimensions. When clustering in 6 dimensions using six principal components of lexical features, the distributions per cluster were very similar for all the clusters with sufficient data points to draw any conclusions. We therefore tried clustering in the unprojected space, using the 6 lexical features for which the U-test gave the most significant differences, however without any notable improvement. Consequently, this method does not seem to help for the task of classifying the speaker based on the lexical features of its quote. The distributions of speaker attributes within the resulting clusters of the last clustering can be seen in the plot below. The silhouette score is 0.48.

![alt text](./assets/img/clustering.png)

Since the original goal was to predict things about a person based on the way they speak, we also trained Gradient Boosting Regressors on the data. As expected from our previous work, the trained models only had R^2 scores between -0.003 and 0.03 which means they are very inaccurate. The lexical features don’t seem to be an accurate predictor of speaker attributes.

## Discussion

The main findings came from the statistical analysis with the U-test, which underlines how some lexical features are not distributed the same ways amongst different groups within speaker attributes. The most relevant differences were found for the usage of pronouns per word between people born in the 50s compared to people born in the 90s, the union ratio between artists and politicians, and the pronouns per word between politicians and athletes. 

Even if these findings are interesting, they have to be very carefully handled. Despite the fact that indeed, people might have different ways of speaking depending on their occupations, it also seems very biased to assert that politicians casually use more ‘union’ pronouns compared to artists. People in both professions mainly are public figures, so their quotes are usually not said in an informal context. Politicians represent the people and are therefore more likely to speak using union pronouns, whereas artists are mainly asked to talk about themselves and their work, which highly encourages them to use ‘self’ pronouns.

Differences computed between different continents are quite interesting too, but we must keep in mind that there are many biases when making speech analysis between people with different origins: if the quote was originally in a different language than English, then differences might be observed because of the translation or because of intrinsic differences between languages. Even if the quote was originally in English, the speaker’s mother tongue may not be English. In addition, punctuation within the quote depends on the person who documented the quote.

Despite initially encouraging findings, it seems that the distributions overlap greatly so we cannot  see clear clusters based on the lexical and speaker features that we selected. This could be due to many reasons, including undesired features of the raw data. For example, there are more quotes than speakers, which means certain individuals are over-represented in the dataset. Furthermore, Quotebank may not alway be attributing quotes to the correct speaker.

## Conclusion

When starting this project, we all had great hopes of coming up with incredible conclusions, we dreamt that our work would be a bomb in the psycho-sociologist world. Unfortunately, no groundbreaking discovery could be done, putting a deadly end to our hopes of fame and sociologist careers. While we did not find what we were looking for, we found something even better, which is that we live in a mult-faceted world with complex actors, in which people cannot guess who we are simply by listening to us talk. How boring and simple would life be if people sharing a bunch of similar socio-cultural features talked in the exact same way?  How boring and simple would life be if people sharing a bunch of similar socio-cultural features talked in the exact same way?
