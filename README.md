# Text-Classification Using CNN

## Data ¶
1. Data comprises total of 20 types of documents(Text files) and total 18828 documents(text files).
2. You can download data from this link (https://drive.google.com/open?id=1rxD15nyeIPIAZ-J2VYPrDRZI66-T
BWvM), in that you will get documents.rar folder.
If you unzip that, you will get total of 18828 documnets. document name is defined as'ClassLabel_Docume
ntNumberInThatLabel'.
so from document name, you can extract the label for that document.
4. Problem is to classify all the documents into any one of the class.

## Preprocessing

useful links: http://www.pyregex.com/ (http://www.pyregex.com/)

1. Find all emails in the document and then get the text after the "@". and then split those texts by
'.'
after that remove the words whose length is less than or equal to 2 and also remove'com' word and then
combine those words by space.
In one doc, if we have 2 or more mails, get all.
Eg:[test@dm1.d.com, test2@dm2.dm3.com]-->[dm1.d.com, dm3.dm4.com]-->[dm1,d,com,dm2,dm3,com]-->[dm1,dm2,
dm3]-->"dm1 dm2 dm3"
append all those into one list/array.

2. Replace all the emails by space in the original text

3. Get subject of the text i.e. get the total lines where "Subject:" occur and remove
the word which are before the ":" remove the newlines, tabs, punctuations, any special chars.
Eg: if we have sentance like "Subject: Re: Gospel Dating @ \r\r\n" --> You have to get "Gospel Dating"
Save all this data into another list/array.

4. After you store it in the list, Replace those sentances in original text by space.

5. Delete all the sentances where sentence starts with "Write to:" or "From:".

6. Delete all the tags like "< anyword >"

7. Delete all the data which are present in the brackets.
In many text data, we observed that, they maintained the explanation of sentence
or translation of sentence to another language in brackets so remove all those.
Eg: "AAIC-The course that gets you HIRED(AAIC - Der Kurs, der Sie anstellt)" --> "AAIC-The course that
gets you HIRED"

8. Remove all the newlines('\n'), tabs('\t'), "-", "\".

9. Remove all the words which ends with ":".
Eg: "Anyword:"

10. Decontractions, replace words like below to full words.
please check the donors choose preprocessing for this
Eg: can't -> can not, 's -> is, i've -> i have, i'm -> i am, you're -> you are, i'll --> i will
There is no order to do point 6 to 10. but you have to get final output correctly

11. Do chunking on the text you have after above preprocessing.
Text chunking, also referred to as shallow parsing, is a task that
follows Part-Of-Speech Tagging and that adds more structure to the sentence.
So it combines the some phrases, named entities into single word.
So after that combine all those phrases/named entities by separating "_".
And remove the phrases/named entities if that is a "Person".
You can use nltk.ne_chunk to get these.
Below we have given one example. please go through it. 

> i am living in the New York --> [('i', 'NN'), ('am', 'VBP'), ('living', 'VBG'), ('in', 'IN'), ('the', 'DT'), T
ree('GPE', [('New', 'NNP'), ('York', 'NNP')])]
--------------------------------------------------
> My name is Srikanth Varma --> [('My', 'PRP$'), ('name', 'NN'), ('is', 'VBZ'), Tree('PERSON', [('Srikanth', 'NN
P'), ('Varma', 'NNP')])]

12. Replace all the digits with space i.e delete all the digits.

13. After doing above points, we observed there might be few word's like
 "_word_" (i.e starting and ending with the _), "_word" (i.e starting with the _),
 "word_" (i.e ending with the _) remove the _ from these type of words.

14. We also observed some words like "OneLetter_word"- eg: d_berlin,
"TwoLetters_word" - eg: dr_berlin , in these words we remove the "OneLetter_" (d_berlin ==> berlin) and
"TwoLetters_" (de_berlin ==> berlin). i.e remove the words
which are length less than or equal to 2 after spliiting those words by "_".

15. Convert all the words into lower case and lowe case
and remove the words which are greater than or equal to 15 or less than or equal to 2.

16. replace all the words except "A-Za-z_" with space.

17. Now You got Preprocessed Text, email, subject. create a dataframe with those.

## Model Architecture

![multi_input_and_output_model](https://user-images.githubusercontent.com/58303643/185766710-6a2a3fc3-d8fe-4e09-a58e-9936b6c333ea.png)

### Accuracy Plot

![text_cnn_acc_plot](https://user-images.githubusercontent.com/58303643/185766715-d51a55a8-5634-4046-818a-8a0861c3e9f1.png)













