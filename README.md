# Closed-domain Question Answering on AIP dataset

# Introduction

The goal of this project is to help Air Traffic Controllers retrieve information swiftly from a corpus consisting of ATC manuals.

# Documentation

## Code Organization

The code is set up into several main directories:

- [**data**](https://github.com/TanJiaTing/AIP/tree/master/data): contains the corpus and train/test questions
  - [**cleaned_text**](https://github.com/TanJiaTing/AIP/tree/master/data/cleaned_text): contains the cleaned corpus in .txt format
  - [**pdf**](https://github.com/TanJiaTing/AIP/tree/master/data/pdf): contains the raw pdf file used to train the model
  - [**questions**](https://github.com/TanJiaTing/AIP/tree/master/data/questions): contains the training data in SQUAD format, as well as a human-readable csv format
  - [**results.csv**](https://github.com/TanJiaTing/AIP/blob/master/data/results.csv): contains the results and prediction scores from each model
- [**models**](https://github.com/TanJiaTing/AIP/tree/master/models): contains the models used to generate predictions
- [**notebooks**](https://github.com/TanJiaTing/AIP/tree/master/notebooks): contains the codes stored in Jupyter Notebooks

## Data Processing
I converted the AIP manual into a .txt file by parsing it with [**tika**](https://tika.apache.org/1.6/api/org/apache/tika/parser/Parser.html), while cleaning the data by removing symbols such as (~,^,\*) List items were concatenated onto the same line, with whitespaces removed.
I then extracted 40 questions from this passage using [**cdQA-annotator**](https://github.com/cdqa-suite/cdQA-annotator) in SQuAD format as follows:
```
{"version":"v2.0"
  "data":[{"title":"AIP",
            "paragraphs":[{"qas":[{"question":"When is the deadline for agents of non-scheduled flights to submit their slot requests?",
                                   "id":"questionID1",
                                   "answers":[{"answer_start:180,
                                               "text":"no later than 24 hours prior to the operation of the flight"}]},
                                  {"question":"Who should operators of commercial flights submit their slot requests to?",
                                   "id":"questionID2",
                                   "answers":[{"answer_start":116,
                                               "text":"Changi Slot Coordinator"}]}],
                                   "context":"Operators or agents of non-scheduled, commercial and non-commercial flights shall submit their slot requests to the 
                                              Changi Slot Coordinator no earlier than 7 calendar days and but no later than 24 hours prior to the operation of the
                                              flight, for which the slot will be utilized"}]}]}
```
