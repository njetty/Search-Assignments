# ILS-Z534: Search
## Assignment 1

### Running Instructions:
Both question 1 and Question 2 are written as seperate maven projects in order to have the dependencies easily created.

*Running Generate Index*
```sh
# GO to the project root folder
cd GenerateIndex
# Build the package
mvn package
# Run the program
mvn exec:java -Dexec.args="/home/njetty/CORPUS_LOCATION /home/njetty/INDEX_LOCATION"
```

*Running Index Comparison*
```sh
# GO to the project root folder
cd IndexComparison
# Build the package
mvn package
# Run the program
mvn exec:java -Dexec.args="/home/njetty/CORPUS_LOCATION /home/njetty/INDEX_LOCATION"
```

### Task 1:
##### How many documents are there in this corpus?
There are a total of 84474 documents in the given corpus. Below is the output for the GenerateIndex.java

```sh
Total number of documents in the corpus:84474
Number of documents containing the term "new" forfield "TEXT": 38604
Number of occurences of "new" in the field "TEXT": 83642
Size of the vocabulary for this field: 233384
Number of documents that have at least one term for this field: 84456
Number of tokens for this field: 26649680
Number of postings for this field: 18049815
```

##### Why different fields are treated with different kinds of java class? i.e., StringField and TextField are used for different fields in this example, why?
Lucene indexes are composed of atomic documents. Each document is divided into named fields which either have content that can be searched or data that can retrieved. Before storing data into a field, it is important to determine which field type best fits the nature of the content being indexed.

It is also best practice to avoid retrieving large amounts of data from the index itself. The Search Lucene Content module indexes most data using the UnStored field type. When searches match content in these fields, only the matching node ID is retrieved from the index, and the search results are populated with data from the database.

Below are the different field types available in Lucene:
1)	Un Stored
2)	Keyword
3)	TextField
4)	StringField
5)	Binary Field
6)	Unindexed Field.

Different fields are Indexed based on the data available, in order to reduce cost and improve the performance of the system.

##### Differences between TextField and StringField:
"TextField" is a sequence of terms that has been tokenized. Punctuation and spacing is ignored for a "TextField". Text tends to be lowercased, stemmed. Synonyms and even stop words are removed. This helps in saving storage space and supports queries based on keywords there by improving the ranking accuracy when processing large texts. In Text Fields preprocessing text will be done before index is built

"StringField" is a single term. "StringField"s are literal character strings where all punctuation, spacing, and case are preserved. For example all unique values like phone numbers, unique IDs will be stored as string field in lucene. "StringField" is useful for facets and filter queries.

For the given example "DOCID" is given as "StringField" because it is unique for the given document, whereas rest of the fields are declared as Text fields to improve the performance and searching.

### Task 2:
Comparing the Analyzers

|      Analyzer     | Tokenization applied? | How many tokens are  there for this field? | Stemming applied? | Stop Words removed? | How many terms  are there in the  dictionary? |
|:-----------------:|:---------------------:|:------------------------------------------:|:-----------------:|:-------------------:|:---------------------------------------------:|
|  Keyword analyzer |           NO          |                    84474                   |         NO        |          NO         |                     84061                     |
|  Simple Analyzer  |          YES          |                  37330144                  |         NO        |          NO         |                     169981                    |
|   Stop Analyzer   |          YES          |                  26216475                  |         NO        |         YES         |                     169948                    |
| Standard Analyzer |          YES          |                  26649680                  |         NO        |         YES         |                     233384                    |

