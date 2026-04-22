# AI Usage Log — NER Assignment

## Overview

AI tools were used throughout this assignment to support technical implementation, debugging, and workflow structuring. All usage complied with course policies. AI was not used for annotation guideline creation, document annotation, interpretation of inter-annotator agreement, or resolving annotation disagreements.

---

## 1. Code Implementation

### Tasks
- spaCy NER Model 1 and Model 2 code implementation  
- Training loop setup (epochs, exporting pre-annotations for batch 3, 80/20 splitting)  
- Data formatting (Label Studio → spaCy format)  
- IAA calculation code (Binary Kappa, BIO Kappa, F1)  
- Evaluation metrics code (precision, recall, F1, per-entity analysis)  
- Deployment of Model 2 into the inference dataset

### How AI Was Used
- Generated initial code structure  
- Provided reusable notebook cells  
- Suggested workflow for pre-annotation export for Model 2 fine-tuning

### My Reflection
Because the sample code provided in class and on GitHub did not immediately implement what I wanted, AI was a great tool for adjusting the parameters. It also helped me separate the parameters for both models, so that the number of epochs could be edited in another cell and then rerun. This became especially helpful after we reviewed it with the professor and decided to use up to 30, rather than 50, epochs for the second custom NER model. 

## 2. Debugging & Error Fixing

### Tasks
- Fixing undefined variables (`nlp2`, missing datasets)  
- Fixing broken training loops  
- Resolving dataset loading issues  
- Debugging rule-based logic (rule-based/regex modeling was ultimately scrapped)

### How AI Was Used
- Suggested fixes for runtime errors  
- Identified missing steps in the pipeline  

### My Reflection
AI fixes consistently worked properly for common troubleshooting issues. That said, I had to constantly verify that the code made sense, and aligned with the specific instructions of the assignment. For example, nlp2 variables weren't working because the AI data had assumed that the two model notebooks would be separate. Or the broken training loop was because it was frozen, and it wasn't listening to my attempts to unfreeze. The attempt the debug the rule-based logic for the fine-tuned second model was not successful, and because I did not have enough of an understanding to understand that technicality, I decided to scrap that initiative. 

## 3. IAA Implementation

### Tasks
- JSON → token-level conversion  
- Binary Cohen’s Kappa  
- BIO-tag Kappa  
- List of disagreement output  

### How AI Was Used
- Generated IAA calculation code  
- Explained which metric to use in submission

### My Reflection
AI explained the multiple different outputs and concepts, allowing me to interpret the instructions to understand the purpose of the IAA code. I originally believed that the raw agreement value would suffice, but asking it to explain how the Kappa code applied, with a simple explanation of the BIO-tagging was helpful. Since JSON file was chosen for the export from Human Signal, the code also transformed from JSON -> CONNL like to help with the calculation. 

## 4. Model Design & Improvements

### Tasks
- Exporting pre-annotations for Batch 3, then applying to existing 220
- Adjusting epochs (30 to 50, then back to 30)
- Best-epoch selection  

### How AI Was Used
- Suggested improvements to the hyperparameters as needed
- Proposed best epoch logic

### My Reflection
After discussion with the professor, we observed that the perceived benefit of utilizing an epoch of 50 for the second model did not lead to an improved NER loss metric. In fact, the 50th epoch did not have the lowest loss, it took longer and was beat by the metric a few epochs before. To improve our modeling, AI developed a method where we could do up to 30 epochs (to match our original Model 1), but specifically keep track of the best result and select the epoch with the lowest NER loss as the best model. This helped us develop the strongest model given the hyperparameters Yarden and I had decided to fine tune. 

## 5. Concept Clarification

### Topics
- NER and spaCy pipeline  
- Precision, Recall, F1 table results (microaverage vs macroaverage) 
- Cohen’s Kappa and BIO score

### How AI Was Used
- Explained concepts  
- Connected theory to implementation  

### My Reflection
Because IAA was entirely new to us, it was difficult to understand and properly interpret the Kohen's Kappa score. Additionally, the code provided by the AI was thorough; however, it included several metrics we were unfamiliar with. AI helped explain and guide us towards the metrics most valuable to this assignment. This is one of the major disadvantages we found of using AI, though. Because AI code is so comprehensive, it doesn't clearly outline or highlight the overall precision, recall, and F1 results that matter most for our comparison. AI could benefit from being more simplistic, as it would drastically help with interpretation.

## 6. Evaluation & Analysis

### Tasks
- Interpreting the scope and size of each model (pretrained ~5k, Model 1 220 docs, Model 2 320 docs)
- Listing out and tracking per-entity performance 
- Confusion matrices for each entity 

### How AI Was Used
- Generated evaluation code  
- Generate confusion matrices for the entities

### My Reflection
AI helped streamline our analysis, especially in the custom NER modeling steps. It allowed us to develop strong per-entity analysis with all metrics for each of our 8 entities and confusion matrices to visualize this analysis. 

## 7. Inference (Step 9)

### Tasks
- Applying model to new dataset  
- Reviewing 20 predictions
- Importing data and dealing with technicalities of hugging face JSON file import

### How AI Was Used
- Implementation of code, and blocks of code for analysis 

### My Reflection
First, selecting and importing the dataset for inference was difficult, especially since Yarden had previously handled data imports, so thankfully, AI provided step-by-step instructions. AI generated code to help us apply the code directly to a sample of 20, where we reused some of the code for cleaning and setup that we had used to setup for the pretrained model. AI created a comprehensive list of the labeling, and even provided us with a tally count as well which helped with the interpretation. Immediately, we identified that the model failed for the new domain of news, especially given

## 8. Human Override of AI:
- Rejected frozen test set suggestion following Hours entity being 0 when using the test data in Model 1
- Adjusted epochs based on loss behavior, adopting a best epochs language and maintaining a max threshold of 30 given computing power
- Applied rule-based/regex logic for Model 2, but ultimately, decided the minimal improvements to the model paired with the need for increased manual work was not worth it
- Ensured file organization, structure of code, and added markdowns to distinguish steps and key portions of the development (such as the area where the 100 export of pre-annotations was necessary) 

## 9. Limitations of AI:
- Incomplete or buggy code  
- Outdated dataset suggestions (for inference)  
- Overconfident recommendations based on epoch hyperparameters, and rule-based regex logic
- Needed manual validation to verify that model could be interpretable, scalable, and deliver the insights we needed. 

## Final Takeaway

Overall, AI was incredibky helpful in this assignment, especially given the technical nature of building custom NER models and dealing with various hyperparameters, stratified splits, and expanded datasets. However, the art of annotating the data, verifying the success of hyperparameter tuning, and analyzing the results of precision, recall and F1 score couldn't be replaced. Overall, AI allowed us to build a custom model quicker, however, the need for domain knowledge, individual interpretation according to our annotation agreement, and testing different hyperparameters according to the results was still needed from a human perspective. 

 To help expand the model first, we would need to expand the human domain through the rule-based/regex modeling especially given that our dataset had very strict entity rules. This would require humans to define it, but I also believe that AI would be very helfpul in listing out all the possible keywords for rule-based NER modeling, rather than manually having to list out all the possibilities. Overall, AI is most helpful for the repetitive nature, and debugging aspects of this assignment. 

 * AI was used to list out the different applications, sections, and use cases that AI was used in this assignment according to chat history. Interpretation of the value of the AI responses, reflections, and human override/AI limitations/final takeway is all human. *