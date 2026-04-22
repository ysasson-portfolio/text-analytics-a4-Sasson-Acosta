# Assignment 4: Named Entity Recognition

By: Yarden Sasson and Brandon Acosta

ysasson@lion.lmu.edu

bacosta3@lion.lmu.edu





## Overview

This assignment revolves around building models that can help identify the entities within certain texts relating to restaurants, food, and more relevant topics in the food industry. We look at the Spacy Pre-Trained Model as well as a custom trained Spacy model. Once we custom trained the model, we were able to fine tune it by running different parameters and correcting the predictions made by the model before reintroducing it and running it again. Based on the performance of the three models, we will compare the overall performances. 



### Dataset

- **Name:** MIT Restaurant

- **Source:** https://huggingface.co/datasets/tner/mit\_restaurant

- **Size:** 6,900 rows

- **Domain:** Restaurants, Food, Searches, Amenities



### Entity Types

- **Restaurant Name:** Names of Restaurants specifically

- **Price:** Words that relate the pricing of food or a restaurant

- **Hours:** Words relating to the hours of a restaurant or times they are ordering food. 

- **Location:** Words that can describe where the restaurant is or identify relative locations

- **Dish:** Words describing specific food items. 

- **Amenity:** Words that are related to things that a restaurant can offer to make the experience more enjoyable.

- **Rating:** Words that describe the positive, negative, or neutral feelings associated with the food or experiences at a restaurant.

- **Cuisine:** Words that relate to categories of food that encompass many dishes. 





### Files

- `notebooks/Studio Lab Code.ipynb` - Code to convert .json files into files that can import into HumanSignal

- `notebooks/spacy\_model\_pretrain.ipynb` - Running all of the training data through the pre-trained spacy model

- `notebooks/custom\_ner\_models.ipynb` - Training, Testing, Fine Tuning, and Re-Testing the custom spacy models using our own annotations and samples from the dataset

- `notebooks/iaa\_batch1.ipynb` - IAA Calculations for the first batch of annotations Brandon and Yarden both did separately

- `notebooks/iaa\_batch2.ipynb` - IAA Calculations for the second batch of annotations Brandon and Yarden both did separately

- `docs/AI\_usage\_log.md` - AI interaction documentation

- `docs/reflection.md` - Lessons learned

- `models` - Folder contains the models for each of the groups


### Launch Jupyter

jupyter notebook notebooks/ Change the paths wherever necessary to run the files run the notebooks



## Methods

### Pre-Trained Spacy Model

We applied a pre-trained spacy model (en\_core\_web\_sm) to the unannotated dataset in order to see how the model performs with only its default settings. The model did not perform well initially because of the specificity within the domain of the dataset. After classifying the custom entity tags to the match the ones from the default model, the model performed a bit better, but not by much



### Annotation Process

The annotation process was done in multiple batches as specified in the assignment:

- **Batch 1:** Both Annotators annotated the same 20 documents separately and reviewed them together.

- **Batch 2:** 100 documents each from the same dataset while reviewing an overlap of 20%.

- **Batch 3:** Reviewing and correcting the output of 100 documents that the model predicted and putting them back into the model. 

Throughout the annotation process the guidelines were consistently updated depending on the rules that appeared within the text data. 



### Custom Model Training (Model 1)



For this model, we took the 220 documents from batches 1 and 2 from the annotation process and split it into an 80/20 train-test split. After training the model on 80% of these documents, we input the test values to see how the model performs based on the training methods. 



### Custom Model Training (Model 2)



After correcting the outputs that were pre-annotated by the model, we added these to the initial training set that was used in model 1 and re-trained the model. We then put in a new set of test documents to see how well the model performed after being corrected by humans. 





## Results

### IAA Scores

- Batch 1 Binary Cohen’s Kappa Score: 0.9712

- Batch 1 BIO-tag Cohen’s Kappa Score: 0.9422 

- Batch 2 Binary Cohen’s Kappa Score: 0.9485 

- Batch 2 BIO-tag Cohen’s Kappa Score: 0.9345 



This statistic refers to how two alike two different people are when it comes to annotating a text including the entities tagged and the length of the entities. Based on these results for batch 1, Yarden and Brandon agreed that something was an entity 97.12% of the time, while agreeing on the exact boundary and labels for each specific entity 94.22% of the time. For the second batch, they agreed that something was an entity 94.85% of the time, while agreeing on the exact boundary and labels for each specific entity 93.45% of the time. The primary score that was used for this particular situation was the Binary Cohen’s Kappa Score because it is more forgiving and is not as specific as the BIO-tag Cohen’s Kappa Score. This shows that Brandon and Yarden agreed more in the beginning of the process and these cases where there was disagreement allowed them to discuss and make the necessary edits to the annotation guidelines. Throughout the second batch of annotations there were more unique situations when it came to the annotations and it raised many questions about how we need to refine the guidelines for the process. 



### Spacy Pre-Trained Model (Baseline)

- Model Used: en_core_web_sm

- Precision: 0.5163

- Recall: 0.1022

- F1 Score: 0.1706 



Using the Spacy Pre-Trained Model, “en_core_web_sm” on the reviews of the model did not achieve the optimal performance results that we would expect from a model like this. First, Spacy has its own particular set of elements while the “Restaurants MIT” dataset has custom tags that are more relevant to the overall topic of the reviews. In this case, the model needed the tags from the restaurant dataset to be standardized to match the tags from the spacy model. If the tags are not standardized, the performance statistics would have been either 0.0000 or something very close to that. This is because these metrics measure whether the prediction matches the outcome and the prediction in the case (from the spacy model) would not match the tags from the restaurant data. Even when the data was standardized, it still performed very poorly with an F1 score of 0.1706. This is because the spacy data is a very general dataset while the restaurant dataset that was being used is very specific in terms of topics being discussed. This helped us support our conclusion that the pre-trained models do not support tasks that involve domain specific entities. 



### Custom NER Model Using Spacy (Model 1)

- Precision: 0.6196

- Recall: 0.6000

- F1 Score: 0.6096 



When this model was trained, it was trained using the annotations from the first batch of 220 annotations done by Brandon and Yarden using an 80/20 stratified split. This model performed significantly better than expected on the first try. Most of the entities had a decent F1 score. The worst performing entities were Restaurant\_Name (0.5000), Dish (0.3333), and Hours (0.0000). Looking at the Training Loss curve, there was a significant drop in the beginning and the rate of loss slowed down as more epochs were processed. This model shows that the lowest NER loss happened at 26 epochs. This means we could have stopped the process earlier and prevented unnecessary computation. The custom NER model was able to accurately identify whether something is an entity 61.96% of the time, while it correctly identifies all entities 60% of the time.  



### Custom NER Model 2 (Expanded Data + 50 epochs)



- Precision: 0.5865

- Recall: 0.5865

- F1 Score: 0.5865



While the F1 score was only slightly worse, we consider this to be the better performing model. The first model had a higher F1 score along with a higher score for precision and recall. The reason we felt that this model was better is because the F1 scores across all entities were more balanced while the first model had an entity (Hours) with a F1 score of zero which does not make sense for an entity recognition model. This model is still accurately identifying positive instances of entities and is correct about it approximately 58.65% of the time. The entity that had the most confusion is Location and Restaurant Name. These two entities were confused for each other because they both can be used interchangeably. For example, “I would like to eat at McDonalds” could refer to the restaurant McDonalds or a specific McDonalds location. This is generally confusing because the capitalization rule can apply to it and be categorized as both locations and restaurant names. As we ran more epochs, we noticed that the lowest training loss was actually at 28 epochs instead of the 30 we originally tested in the first model. We decided to stop at 28 epochs because it was the best NER loss and to keep going would cost computational power and could lead to a higher NER loss. 



### Per-Entity Analysis



- **Pre-Trained Spacy Model:** Per-Entity Analysis in this case is not an optimal analysis to perform. The Pre-Trained Spacy Model has a set of entities that are considered very high-level entities and can encompass a wider range of entities within the category. Unlike the default spacy model, the Restaurant MIT dataset is a very domain oriented set of texts. In order to make sure that we were able to get the correct analysis, the dataset came with its own set of entity classification options. These options are very specific to the food and restaurant domain including elements such as the restaurant name, cuisine of the restaurant, ratings of the food or experience, amenities that the restaurant provides, and more. Since both sets of tags are completely different (maybe with the exception of location), the performance metrics of this model could be extremely low. The first time we ran the model and tried to compare it without modification, there was an F1 Score of 0.000 which means that the model did not perform well at all making no correct predictions whatsoever. After creating a dictionary to try and standardize the tags with each other, the model’s F1 Score increased to 0.1706. While this is an improvement from the first attempt at this model, it is not as good as a specialized model dedicated to this domain would perform. This is because multiple entities from the default set could be put under the same umbrella as one of those from the custom set. An example of this can include Hours belonging to Date and Time, Restaurant Name belonging to ORG and FAC, Location belonging to LOC and GPE, etc. With this range, the model may not select the right entity. 





| Entity           | Precision Model 1| Recall Model 1 | F1 Score Model 1 | Precision Model 2| Recall Model 2 | F1 Score Model 2 |
|------------------|------------------|----------------|------------------|------------------|----------------|------------------|
| Price            | 1.0000           | 0.6667         | 0.8000           | 0.8333           | 1.0000         | 0.9091           |
| Amenity          | 0.7826           | 0.6429         | 0.7059           | 0.5625           | 0.6207         | 0.5902           |
| Cuisine          | 0.6250           | 0.7692         | 0.6897           | 0.8667           | 0.7647         | 0.8125           |
| Rating           | 0.5556           | 0.7143         | 0.6250           | 0.6364           | 0.7778         | 0.7000           |
| Location         | 0.6667           | 0.5833         | 0.6222           | 0.5806           | 0.5455         | 0.5625           |
| Restaurant Name  | 0.4286           | 0.6000         | 0.5000           | 0.4000           | 0.3333         | 0.3636           |
| Dish             | 0.4000           | 0.2857         | 0.3333           | 0.3571           | 0.4167         | 0.3846           |
| Hours            | 0.0000           | 0.0000         | 0.0000           | 0.6667           | 0.6000         | 0.6316           |



From the first model, we can see that most elements perform very well except for the restaurant name, dish, and hours. This is why we decided to make sure to highlight the cases where these three elements existed and were corrected in the third batch of annotations. Setting these as ground truths helped the next model to learn from these mistakes. Although the next model has a lower F1 Score, it is a little bit lower but all of the entities have a F1 score that is more balanced than before. 



## Insights and Recommendations



Based on the results of all 3 models that were run, we recommend that the second custom NER model should be deployed. This model was the one that had high performance in general and more specifically had better performance across more entities individually. Looking at the text and the application of text outside the domain, we found that domain specific entities require more intensive training and it is very difficult to generalize that training to other areas.  We also noticed that the more we trained the model with aligned text annotation the better it performed. Alignment within the annotation guidelines is crucial to the overall success of the model. We recommend that the model be updated as new annotation cases appear within texts and update the annotation guidelines as we go. With a more aligned strategy and set of guidelines for the annotations, there is no way that the model will not continue to improve. We would recommend that this model should be deployed in order to help restaurants or food delivery services understand what consumers are looking for when it comes to the food and delivery experiences. Another recommendation is for brands to use this model in order to help optimize their position in search engine results. They could use the results in order to tag certain keywords that will match the most popular entities or highlight entities that best match their overall brand. 

 

## Results from Inference on a New Dataset



We applied the second Custom NER Model onto 20 sentences from the CoNLL -2003 news dataset to evaluate whether our model and entities can be generalized and perform well with datasets in other domains. Based on the results and the poor performance of the model, we came up with the following conclusions:

- Interpretation of any numerical values were considered to be hours because the model has learned to associate numbers with restaurant hours in the original dataset.

- When words are capitalized, the model interprets them mostly as restaurant names or locations. This is because the model assumes that capitalization is associated with proper nouns (names, locations, countries, cities, etc.). 

- Words like “Indian” or “Crude” can be interpreted as a cuisine, even though it is possible for one word to have multiple definitions depending on the context. 

- It is very difficult for a model that is trained to perform domain specific tasks to be generalized and perform well in other domains. This model was trained specifically for texts involving the food or restaurant industry.


## Conclusion


This project has highlighted the importance that the annotation process and quality hold when it comes to the NER process. While it is important to start with a quality dataset, the annotation guidelines and annotated samples are the true bedrock for each NER model that we decide to build. They determine the way that the models handle any words that contain multiple entities, noisy text that could affect the models ability to interpret the text, and recognizing entities without any additional information. Here are some things that we learned throughout this project:

It is important to consistently edit the annotation guidelines based on any new cases that we can find within the texts that we are planning to test or train with the model.

- The more we are able to annotate and re-train the model, the better the model will perform across all entities and in general.

- Many changes in the current state of language can drastically affect the way the models process information. Slang, idioms, and words that change with context can drastically affect the way that the model processes information.

- Pre-trained models are not always transferable to datasets that are focused on a specific domain. Entities may not match and will be miscategorized very often.

- Model performance is based on the dataset that is used to train the model and the annotations along with it. 



Adding custom entities and training the model already improved the F1 score we got in the pretrained model by 0.4. This was not a different model, it was just based on the overall data used to train the model and the annotation guidelines. These are the overall main contributors for a successful task involving NER. 



