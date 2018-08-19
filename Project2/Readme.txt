
Introduction
—————————————
The project involves generation of a unigram model by the parsing New York times articles given in SGML tags.


Approach
—————————

1. PROCESSLING FILES IN DIRECTORY
The code has Project2.py instantiates the class UnigramLanguageModel and collects the text from every XML file provided in the directory /corpora/LDC/LDC02T31/nyt/2000. The class makes a method call to Process File which handles the collection of text and conversion to lowercase. The text is also split by using space as a delimiter to store in a staging dictionary. The key is the splitted pattern and the value is the frequency. This is not the final frequency. Words before cleaning along with their counts are included in the dictionary. An example is provided below - {Francisco:1000, Fransisco*123:2000, Fransisco:3000, Fransisco1:4000}.

2. CLEANING OF FILES

The cleaning operation contains 2 steps
- Removal of SGML tags
- Removal of unnecessary characters other than {a-z,A-Z,’}

Removal of SGML tags:

The code iterates through the keys found in  staging dictionary calls the method 'ReadAndCleanData' where the data is stripped of white spaces(Carriage returns, trailing spaces and line feeds). The cleaned word is then passed to the method CollectTags which is used to collect the tags seen in words into a dictionary using a regex '</?[A-Z_]*>'. The tags dictionary is used so as to avoid costly regex operations. The method 'IsTag' is used to find out if an incoming new word in the list is a SGML tag.

Removal of uncessary charecters other than {a-z,A-Z,’}:

The method FilterUnwantedCharecter is used to remove unwanted charecters. The regex '[^A-Za-z\']' is used to identify unwanted characters.

3. VALID WORD COUNTS:
Post the cleaning operation, valid words are names are collected using the method 'SplitFileCollectWords'. Four regexes are used to collect valid words
"[A-Za-z]{1}\'?[A-Za-z]{1,}s'"
"[A-Za-z]{1}\'?[A-Za-z]{1,}'s"
"[A-Za-z]'?[A-Za-z]{1,}"
"[A-Za-z]+"

The following examples of words are collected as valid words

Ex: O'conner  - Considered O'conner
    James's - Considerd James's
    Government'' - Considerd Government 
    
    
4. AGGREGATING WORD COUNTS:

Cleaned words are reaggregated to form correct counts. Taking the previous example, the following words from staging  {Francisco:1000, Fransisco*123:2000, Fransisco:3000, Fransisco1:4000} are cleaned to form the key 'Fransisco' and hence the individual counts are reaggregated to form the final count of the cleaned key: 1000+2000+3000+4000 = 10000. The method 'RecordWordCounts' collects the word counts into a dictionary unigram_count.

5. RECORD WORD COUNTS

Word counts are provided as the output to the console by iterating through the items of the dictionary. Each word and count are seperated by a TAB character.




 


