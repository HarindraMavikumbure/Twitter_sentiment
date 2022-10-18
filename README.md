# Twitter_sentiment
A study of subject generalizability of fine-grained BERT models 

## Project Description  
Generalizability is the central feature driving current interest in Pretrained BERT models. Pretrained models aim to be generalizable. They are typically trained with a large, general corpus, and finished by feeding in smaller, specialized datasets. 
Typically, a BERT model will be trained with a language, and then further trained to classify features of that language (in our case, levels of positive and negative sentiment). 

When adding data to a model, you run the risk of confounding some existing ability of the model to classify a specific case. For example, if we trained a BERT model to understand a second language, we may expect to see its performance drop when it encounters 
a false cognate, a word that is spelled the same in two different languages and has two different meanings.  

There has been interest in training BERT models with large amounts of twitter data (see: bertweet). Our interest was to see if we could do more with less: to split up trending tweets based on sentiment target, create separate classes for those targets, 
train different models using only data from those classes (e.g., train a model to perform sentiment analysis using only tweets about events), and check how generalizable they are when tested against other categories of sentiment target. If we find that training on a 
category of sentiment target is confounding to a type of sentiment analasys, we may want to omit it when training future models, or to adjust the weight of a model's vote when it is trained on that category and used as a part of an ensemble classifier. 


## Installation Instructions 

	This code was developed to be run from within colab. 
	This direct link will open a copy of "Twitter.ipynb" within colab
	https://colab.research.google.com/github/HarindraMavikumbure/Twitter_sentiment/blob/main/Twitter.ipynb

## Usage instructions 
Run the first cell within colab (press the play button!). This cell contains dependencies that need to be installed, along with !git clone, this will clone the github project into colab's /content/ folder,
allowing you to use the datasets and edit the config file. 

The config file now resides at: 

/content/Twitter_sentiment/config.ini

To navigate here, read about the ini settings, and edit the ini file: 
	Click the folder icon on the left side of the screen 
	Click the drop down arrow on the left of the twitter_sentiment folder we cloned from github in an earlier step 
	Click the drop down arrow on the left side of the src folder to expand its contents 
	Double click the file 'config.ini'. this will open an editing pane on the right side of your browser window 

If you don't see the folder or the ini files in colab's file system after running the first cell in your web browser, try hitting the built-in refresh button (folder icon with arrow circle) near the top of colab's file system GUI.


Within the ini there are comments (lines beginning with #) that explain what changing a value will do. By default, the program is set to quickly make a Naieve Bayes model. Be aware, the BERT and ROBERTA 
models may take a long time to train with colab! Google would prefer you pay them a monthly fee to train your models quickly. If you're just testing the program out for fun or to see its functionality, 
try turning your epochs down to 1. The model won't perform well but you'll see that it's working. 

When the config file is to your liking, run the second cell (contains imports and full code). The specified model will be trained with and tested against the sentiment target datasets you picked out. 

## Method 
Our method is standard. We split the tweets into train, test and dev sets (80, 10, 10). We normalize the tweets for things like contractions and emoji use, tokenize them (with BERT and ROBERTA's built-in tokenizers), and feed them into a pretrained BERT model of our choice (or a Naieve Bayes model if we are in a hurry). 

## Data 
Our data is originally from SemEval 2017 contest involving estimating target sentiment. We rebalanced and repurposed this data for our experiment. 
Our data is fine-grained, we use the standard 5 labels (-2 to 2) to represent strongly negative, negative, neutral, positive, and strongly positive sentiment. 

![image](https://user-images.githubusercontent.com/59939625/196503382-9f3af0da-0156-4907-995c-89bda49826f4.png)

## Full Results:
![image](https://user-images.githubusercontent.com/59939625/196504613-2af5c274-43ff-45e0-81b2-b8d790584246.png)
![image](https://user-images.githubusercontent.com/59939625/196504671-69cddab8-aaee-4c02-9f95-5a89c4dede3a.png)
![image](https://user-images.githubusercontent.com/59939625/196504716-1b8faba0-ebde-4129-9d75-7bfb83ea20fc.png)

## Simplified Results:
![image](https://user-images.githubusercontent.com/59939625/196503881-4429d3ff-4e9f-450d-9cea-2dcbfed80558.png)

This simplification of the results of many runs of the program shows promise, we can see a relevant difference in the performance of these models against each other. We see the group and event target models underperforming in comparison to the individual target model, however, the individual dataset is the largest. Further research is needed to decide whether learning about groups or events is confounding to classifying sentiment about some categories. 

## Future work: 
A larger dataset would allow us to compare our models more effectively. We don't have enough data to have generalizable tests for same-category classification. For example, an event-based model may train on tweets about thanksgiving, and then see tweets about turkey in the test phase. We expect the performance of same-category classification to be slightly positively skewed as a result. A larger dataset would also allow us to see more fine-grained data. Heavy undersampling was needed in order to balance the sentiment of the sets, tweets were generally much more positive about events than they were about groups of people. Many of the extreme values had to be removed to allow for comparison.

Although our research question is motivated by using fewer tweets, we would like to try this experiment with a pretrained model with a large twitter corpus, like bertweet. We would expect to see a performance boost from pretraining with emojis and a more representative volcabulary


## References: 
D. Q. Nguyen, T. Vu, and A. T. Nguyen, “BERTweet: A pre-trained language model for English Tweets,” arXiv:2005.10200 [cs], Oct. 2020, Accessed: May 08, 2021. [Online]. Available: https://arxiv.org/abs/2005.10200
M. Pota, M. Ventura, H. Fujita, and M. Esposito, “Multilingual evaluation of pre-processing for BERT-based sentiment analysis of tweets,” Expert Systems with Applications, vol. 181, p. 115119, Nov. 2021, doi: 10.1016/j.eswa.2021.115119. 
Q. Ismail, R. Obeidat, K. Alissa and E. Al-Sobh, "Sentiment Analysis of COVID-19 Vaccination Responses From Twitter Using Ensemble Learning," 2022 13th International Conference on Information and Communication Systems (ICICS), 2022, pp. 321-327, doi: 10.1109/ICICS55353.2022.9811132
X. Zhou, D. G. Han, and D. Lo, “Assessing generalizability of CodeBERT,” 2021 IEEE International Conference on Software Maintenance and Evolution (ICSME), 2021. 
M. Munikar, S. Shakya and A. Shrestha, "Fine-grained Sentiment Classification using BERT," 2019 Artificial Intelligence for Transforming Business and Society (AITB), 2019, pp. 1-5, doi: 10.1109/AITB48515.2019.8947435.
T. Young, D. Hazarika, S. Poria and E. Cambria, "Recent Trends in Deep Learning Based Natural Language Processing [Review Article]," in IEEE Computational Intelligence Magazine, vol. 13, no. 3, pp. 55-75, Aug. 2018, doi: 10.1109/MCI.2018.2840738.
M. Munikar, S. Shakya and A. Shrestha, "Fine-grained Sentiment Classification using BERT," 2019 Artificial Intelligence for Transforming Business and Society (AITB), 2019, pp. 1-5, doi: 10.1109/AITB48515.2019.8947435.. 

