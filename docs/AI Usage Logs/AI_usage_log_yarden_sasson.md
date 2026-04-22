# AI Usage Log – Assignment 4 (NER)
**Course:** BSAN 6200 – Text Mining and Social Media Analytics  
**Students:** Yarden Sasson & Brandon Acosta  

---

## Entry 1: File Path Error Debugging

**AI use category:** Debugging / Environment Setup  

**What task were you trying to do?**  
Load the dataset file into a Jupyter Notebook using Python.

**What prompt did you use?**  
“What does this error mean?” (Unicode escape error with file path)

**What did AI suggest?**  
The AI explained that Python was interpreting backslashes (`\`) in the file path as escape characters. It suggested three fixes:
- Use a raw string (`r"..."`)
- Replace `\` with `/`
- Escape backslashes (`\\`)

**What did you modify?**  
I changed my file path to use a raw string (`r"..."`).

**Why did you modify it?**  
This was the simplest and cleanest solution for handling Windows file paths. I also modified this in order to be able to import the data necessary for this code to work. 

**What did you learn?**  
I learned that various operating systems have different ways that the Python environments process file paths. Some use forward slashes while some use backslashes. There are different ways to interpret the code and I need to make sure that I use the one that works with my operating system. Python code can be used to Python interprets backslashes as escape sequences, which can cause errors when loading files. Using raw strings prevents this issue because it allows me to paste the path the way that it is and not make any adjustments.

**Any AI errors found?**  
There were no errors found as the solution immediately fixed the problem.

---

## Entry 2: JSONDecodeError (Dataset Format)

**AI use category:** Debugging / Data Handling  

**What task were you trying to do?**  
Load the dataset using `json.load()`.

**What prompt did you use?**  
“What does this error mean?” (JSONDecodeError: Extra data)

**What did AI suggest?**  
The AI identified that the dataset was in JSON Lines (JSONL) format rather than a standard JSON array. It suggested reading the file line-by-line using `json.loads(line)`.

**What did you modify?**  
I changed my data loading code to:

tasks = [json.loads(line) for line in f]

**Why did you modify it?**  
Because the dataset contained multiple JSON objects on separate lines instead of a single list. I also modified the code because I have never worked with JSON files within a dataset and we needed to work with the JSON files because that is how the dataset is formatted. 

**What did you learn?**  
JSONL files must be read line-by-line, while `json.load()` only works for a single JSON object or array. I learned that JSON files are not as straightforward as importing a .csv file. This file was imported as one list with many different elements while a csv is a single dataframe with several rows or columns that are easily accessible without having to format the table differently. 

**Any AI errors found?**  
No.

---

## Entry 3: Understanding Missing NER Output

**AI use category:** Conceptual Understanding / NLP  

**What task were you trying to do?**  
Understand why spaCy was not detecting entities in my dataset.

**What prompt did you use?**  
“Why aren't there any outputs for the entities?”

**What did AI suggest?**  
The AI explained that the default spaCy model is trained on general-purpose entities (e.g., PERSON, ORG), while my dataset uses domain-specific labels (e.g., Cuisine, Restaurant_Name).

**What did you modify?**  
I did not change code immediately, but adjusted my expectations and analysis.

**Why did you modify it?**  
To understand that the issue was not code-related but model-related. I did not change the code because I learned that the code I used was trying to calculate TP,TN, FP, and FN, it was looking for a direct comparison. The only way this code would work is if I found a dataset that used more of the same entity tags within the analysis.

**What did you learn?**  
Pretrained models do not perform well on domain-specific tasks without fine-tuning. I did not change the code because I learned that the code I used was trying to calculate TP,TN, FP, and FN, it was looking for a direct comparison. This is why custom entity and NER tasks are not as successful with the default spacy tags. 

**Any AI errors found?**  
No.

---

## Entry 4: Clarifying Error Analysis Objective

**AI use category:** Conceptual Guidance / Clarification of Instructions 

**What task were you trying to do?**  
Understand what should be compared for error analysis.

**What prompt did you use?**  
“What am I comparing?”

**What did AI suggest?**  
The AI clarified that I should compare:
- Model predictions (`doc.ents`)  
- Ground truth labels (dataset annotations)  

It also defined:
- True Positives  
- False Positives  
- False Negatives  
- Wrong Labels  

**What did you modify?**  
I structured my evaluation approach around comparing predicted vs. actual entities. I did not fix the code immediately because I needed to figure out how to compare the elements that do not have the same labels (or entities in this case).  

**Why did you modify it?**  
To align with assignment requirements. I tried to modify it in order to fit the task but had some issues. 

**What did you learn?**  
NER evaluation requires comparing predicted entities to labeled ground truth data. I also learned how to pull the entities from the list when it came to the analysis from the NLP package. 

**Any AI errors found?**  
No.

---

## Entry 5: Building Error Analysis Code

**AI use category:** Code Generation / Implementation  

**What task were you trying to do?**  
Generate code to compute TP, FP, FN, and evaluation metrics.

**What prompt did you use?**  
“Give me the code to generate error analysis”

**What did AI suggest?**  
The AI provided:
- Functions to convert token labels into spans  
- Functions to extract spaCy predictions  
- Logic for TP, FP, FN, and wrong labels  
- Precision, Recall, and F1 calculations  

**What did you modify?**  
I integrated the code into my notebook and adjusted file paths and variable names.

**Why did you modify it?**  
To ensure compatibility with my existing notebook structure. This was the optimal way to start building my error analysis code and start to measure the performance of the pre-trained model. 

**What did you learn?**  
How to convert token-level BIO tags into span-based entities and evaluate NER performance. I also learned here that the error analysis relied on the entity labels from the pre-trained model and the custom entities we created had to be exactly the same. This resulted in a F1 score of 0.00000 because the entity tags were different as we were trying to compare them. This is where I realized that I needed to change my approach if I wanted to make any kind of analysis of the performance of the pre-trained model.

**Any AI errors found?**  
Minor adjustments were needed to match my variable names, but no major errors.

---

## Entry 6: Label Standardization

**AI use category:** Model Evaluation Strategy  

**What task were you trying to do?**  
Improve evaluation by aligning spaCy labels with dataset labels.

**What prompt did you use?**  
“Give me a way to standardize the labels”

**What did AI suggest?**  
The AI created a mapping dictionary:

```python
SPACY_TO_RESTAURANT = {
    "ORG": "Restaurant_Name",
    "GPE": "Location",
    "NORP": "Cuisine"
}

It also suggested modifying the evaluation pipeline to apply this mapping before comparison.

**What did you modify?**  
I implemented the mapping into my evaluation code and adjusted how predictions were processed.

**Why did you modify it?**  
To avoid an F1 score of zero and allow partial alignment between the two label systems.

**What did you learn?**  
Differences in label schemas can significantly affect evaluation metrics, and mapping can help provide a more meaningful baseline.

**Any AI errors found?**  
The mapping introduced some inaccuracies (e.g., incorrect assumptions about entity types), but this was expected and accounted for in analysis.

---

## Entry 7: Attempt to Increase Pre-Trained F1 Score

**AI use category:** Conceptual Explanation/Attempt to Improve Model Results 

**What task were you trying to do?**  
Understand whether my F1 score (0.1706) was reasonable.

**What prompt did you use?**  
“Could the standardized labeling be affecting this?”

**What did AI suggest?**  
The AI explained that:
- Label mapping introduces noise  
- Domain mismatch leads to high false negatives  
- Low F1 scores are expected for pretrained models on specialized datasets  

**What did you modify?**  
I incorporated this reasoning into my results and discussion section. There was no reason to modify any of the code to attempt to get a higher F1 score because of the fact that the entities that we are comparing along with the dataset are so different that it does not make sense that we would have a higher performing model right at the beginning.  

**Why did you modify it?**  
To properly justify the model’s performance in the report. I modified it because it provided a conceptual explanation about pre-trained models on domain focused datasets that will not perform well no matter what because of the specificity within the domain. 

**What did you learn?**  
Low evaluation metrics do not necessarily indicate failure but can reflect model-domain mismatch. I learned that pre-trained models within a domain specific dataset will usually have a F1 score between 0.1-0.4 because of the lack of domain specific elements within the default pre-trained model. 

**Any AI errors found?**  
No.

---

## Entry 8: Markdown Table Formatting

**AI use category:** Documentation / Formatting  

**What task were you trying to do?**  
Fix tables not rendering correctly on GitHub.

**What prompt did you use?**  
“Why is it showing up like this after I commit it to GitHub?”

**What did AI suggest?**  
The AI identified formatting issues and provided a properly structured Markdown table with correct alignment and column formatting.

**What did you modify?**  
I replaced my original table with the corrected version.

**Why did you modify it?**  
To ensure proper rendering on GitHub.

**What did you learn?**  
Markdown tables require strict formatting rules, including consistent column counts and proper separators. I also learned that the columns have to be identical to each other otherwise GitHub will not display the table properly.

**Any AI errors found?**  
AI made a mistake when it made the first table because it had one more dash mark within the separators which caused problems the first time it produced the table. 

---

## Entry 9: README Table Creation

**AI use category:** Documentation / Content Generation  

**What task were you trying to do?**  
Convert raw table data into Markdown format for the README.

**What prompt did you use?**  
“Make the tables in markdown and add it to the file”

**What did AI suggest?**  
The AI generated:
- A formatted performance comparison table  
- A structured work division table  

**What did you modify?**  
I inserted the tables into my README and adjusted minor formatting.

**Why did you modify it?**  
To improve readability and presentation of results.

**What did you learn?**  
Proper formatting significantly improves clarity and professionalism in documentation. I also learned that the columns have to be identical to each other otherwise GitHub will not display the table properly.


**Any AI errors found?**  
AI made a mistake when it made the first table because it had one more dash mark within the separators which caused problems the first time it produced the table. 

---

## Entry 10: AI Usage Log Creation

**AI use category:** Documentation / Reflection  

**What task were you trying to do?**  
Create a complete AI usage log for the assignment.

**What prompt did you use?**  
“Please review the full conversation and create an AI usage log…”

**What did AI suggest?**  
The AI compiled structured entries summarizing:
- Tasks performed  
- AI suggestions  
- Modifications made  
- Lessons learned  

**What did you modify?**  
I reviewed the entries and ensured they accurately reflected my work. I modified some of the responses in order to put more detail and be able to explain more of the reasoning behind my thought process. 

**Why did you modify it?**  
To ensure the log was honest, accurate, and aligned with assignment expectations. I modified some of the responses in order to put more detail and be able to explain more of the reasoning behind my thought process. This was also done in order to make sure that everything was correct. 

**What did you learn?**  
How to document AI usage transparently and professionally for academic work. I also learned that AI is not 100% right as it misclassified some of the prompts. 

**Any AI errors found?**  
One of the topics was listed as an interpretation explanation, but it was more of a concept explanation in order to see if there is a way to improve the results of the model. 