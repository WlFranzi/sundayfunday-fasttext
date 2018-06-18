Kafka feat IBM Watson


	•	downloaded parallel corpora for the English and German books here: http://farkastranslations.com/bilingual_books.php
	⁃	great data as each English sentence is exactly translated into a German sentence
	•	took English sentence by sentence and pinged Watsons tone analyzer API(https://tone-analyzer-demo.ng.bluemix.net/). Find some python code her(https://bruceelgort.com/2016/06/07/using-ibm-watson-tone-analyzer-with-python/) This gave me up to 7 labels for my sentences: joy, fear, anger, sadness, analytical, confident, tentative
	⁃	I just assumed that the corresponding German sentence have the same labels
	•	Now, used Fasttext (speedy Gonzales classifier as its a hierarchical classifier) from Facebook AI research for text classification. Fasttext basically automates training, predicting and evaluation of your model. I trained a model on my German and one on my English data. 
	•	the documentation is not verbose but describes in simple steps how to prep the data and train model on training set. https://github.com/facebookresearch/fastText 
	⁃	testing e.g. for my repo: `$ ./fastText-master/fasttext test resources/english/model_englishbooks.bin resources/english/englishbooks.valid`
	⁃	N	4673
	⁃	P@1	0.671
	⁃	R@1	0.406
	⁃	Number of examples: 4673
	⁃	not great, but hey.. without any single inch of preprocessing and tuning - not too bad.
	⁃	predicting run: `$./fastText-master/fasttext predict-prob resources/german/model_german12books.bin - 5`
	⁃	will enable you to type your sentences and receive a percentage prediction of first 5 labels
	⁃	German example:
	⁃	froh zu sein bedarf es wenig und wer froh ist ist ein koenig
	⁃	__label__Joy 0.419923 __label__Analytical 0.18635 __label__Confident 0.14924 __label__Sadness 0.105466 __label__Tentative 0.094536
