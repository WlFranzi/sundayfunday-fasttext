Kafka feat IBM Watson

### I took 7 English books and their German translation and pinged Watson's tone analyzer API 

``` As an example result after training my models, I got the top emotional predictions for my sentences:

"froh zu sein bedarf es wenig und wer froh ist ist ein Koenig"

--> Joy 0.419923, Analytical 0.18635, Confident 0.14924

*which means, "to be happy takes little and who is happy is a king"*

```

Steps to take to build your own model with fasttext:

1. downloaded parallel corpora for the English and German books here: http://farkastranslations.com/bilingual_books.php

this is great data set, as each English sentence is exactly translated into a German sentence


2. take every english sentence and ping Watsons tone analyzer API(https://tone-analyzer-demo.ng.bluemix.net/). Here is a handy  python script for that (https://bruceelgort.com/2016/06/07/using-ibm-watson-tone-analyzer-with-python/) 

This will give you up to 7 labels for each sentences: joy, fear, anger, sadness, analytical, confident, tentative. 

Take the corresponding German sentence and apply the same emotion labels to it.

3. used Fasttext (a hierarchical classifier) from Facebook AI research for text classification. Fasttext basically automates training, predicting and evaluation of your model. You can train a model on the German and one on the English books. Here the documentation: https://github.com/facebookresearch/fastText 

for example my simply trained model gives me:
`$ ./fastText-master/fasttext test resources/english/model_englishbooks.bin resources/english/englishbooks.valid`
N	4673
P@1	0.671
R@1	0.406

It is not great, but without any single inch of preprocessing and tuning it's not too bad.

if you want to run a prediction, run: `$./fastText-master/fasttext predict-prob resources/german/model_german12books.bin - 5`
this will open a dialog and you can type sentences and receive a percentage prediction for the first 5 labels
