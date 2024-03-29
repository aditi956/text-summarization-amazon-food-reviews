# Text summarization of Kaggle Amazon fine food reviews

In this project, I have implemented extractive and abstractive summarization techniques  to generate the summary of the reviews and compare
the performances.The data consisted of the reviews of amazon fine foods. The models  I implemented are discussed in the following sections with the results.

## Dataset
The amazon fine food reviews dataset[1] consists of around 500,000 reviews. It covers reviews for more
than 10 years, from October 1999 till October 2012. The dataset also includes information of the product
and users like product rating, number of users who found the review helpful. There are a total of 70,000
products and 250,000 users for whom the reviews are captured. The data also has a column for summary
which contains the summary of the review text, helpful for performing supervised text summarisation.

## Methodology and Results
The entire methodology has been divided into low, medium and high risk tasks, depending on the
complexity of the operations. The workflow explaining the steps to execute for implementation of the
algorithms is shown in the figure below : 

![image](https://user-images.githubusercontent.com/94414506/223651292-da03ed1a-d23d-46e2-973e-ee9d9cb9cf99.png)

![image](https://user-images.githubusercontent.com/94414506/223651322-4314d627-9d90-4dd8-b5a1-0f034b07a349.png)

### Low Risk Task
I could get an insight into the reviews dataset by exploring the various aspects listed below:

1. Distribution of summary text length values show that most of the summaries have text length
between 13 and 30 characters.

![image](https://user-images.githubusercontent.com/94414506/223651690-a96e359b-0414-465a-93bc-3a0d242e8514.png)


2. Distribution of review text length values show that most of the review texts have text length
between 179 and 527 characters.

![image](https://user-images.githubusercontent.com/94414506/223651727-87c200c2-22a5-405d-a6a6-b14ebec5ad9d.png)


3. Plotting review text length with the number of users who found the review helpful shows that
users find the review helpful as the details on product increase.

![image](https://user-images.githubusercontent.com/94414506/223651796-4b5961a4-efef-4526-816d-457602c6b5cb.png)

4. Plotting the product ratings with the number of punctuations and words in a review show that
an extreme rating of 1 or 5 corresponds to a review with more punctuations and less detailed
review, and vice - versa for a neutral rating.

![image](https://user-images.githubusercontent.com/94414506/223651841-be69d840-f0cc-4618-9904-4d965398077c.png)

![image](https://user-images.githubusercontent.com/94414506/223651878-57308b11-811f-4390-8a21-f546ce83c571.png)


Following data pre-processing steps were performed on the reviews in the dataset:
1. All the text was converted into lower case.
2. Stopwords were removed using the stopwords in the English language.
3. All the word contractions that were present in the text were expanded. Example - ‘I’m’ to ‘Iam’.
4. All the special characters, extra whitespaces and links were removed.


The 
#### Extractive Text Summarization 
uses a scoring function for the purpose of picking up the most
important sections of the text by creating an intermediate representation. The most important information
in the text can be identified by various methods. I implemented the following two methods

1) Frequency Based  
2) Graph Based 

#### Observation :  
The run time was very high for the graph based algorithm. So the data was subsampled before
implementing both techniques. The performance of both the methods was measured by computing the
BLEU score obtained by comparing the summary generated by these algorithms with the summary given
in the dataset. The BLEU score obtained was very low on average for both the methodologies, the reason
being that the summaries generated used sentences from the reviews but the summary in the data had
new sentences. Below are the snapshots of the summaries from both methodologies, which suggest that
the generated summaries make sense. 

![image](https://user-images.githubusercontent.com/94414506/223652433-c9edcadd-d167-4174-87ce-f6dcd676b0e3.png)

  Summary generated (‘gen_summary’) by extractive summarization TF-IDF method
  
![image](https://user-images.githubusercontent.com/94414506/223652450-f19d0972-32d6-4480-9c85-6b92621e1281.png)

     Summary generated (‘gen_summary’) by extractive summarization Page Rank method (Top 3 important sentences)
     
     
### Medium Risk Task
Abstractive Text Summarization algorithms create new phrases and sentences to generate the
summary. I implemented the Seq2Seq model using LSTM for encoder and decoder architecture to
perform abstractive summarisation. In this problem, the length of the input and output sequences was
different for the encoder-decoder.

### High Risk Task
It is very difficult to remember the long sequence into fixed length sequence and it is observed that BLEU
score decreases as the length of the sequence increases and therefore to overcome this attention model
comes into the picture. Attention model takes care of this by focusing more on the target sequence that
could be part of the target sequence. Attention mechanism uses the bidirectional RNN which in contrast to
unidirectional RNN processes the sequence from first word to end word while in bidirectional it occurs in
forward and reverse direction. The context vector is the weighted sum of outputs from the encoder.
I tried building a custom attention layer, but were not successful completely in doing that.

### Conclusion
After performing both the extractive and the abstractive summarisation, I could infer that extractive
summarisation will be more efficient but would have less accuracy as it heavily depends upon the model
and it might take a significant amount of time to process even with small amounts of data. For the
abstractive summariser, after performing 10 epochs of 1024 batch size we received the validation loss of
1.7440 which could be considered good for this less number as for the large number of epochs, it was not
possible for us to train due to the memory issue and slow computation. After trying on colab with the GPU,
it was taking around 6 hours for each epoch and due to the time limit being exceeded we trained on the
whole data set with a small number of epochs.Train and test loss
decreases with each epoch and still the plateau has not been reached and there is still scope for better
performance. For the attention mechanism, which was a high risk phase, the custom attention model was
not working correctly on our dataset, in case of the attention model, accuracy and performance of the
model could have been much better as it takes bidirectional RNN into consideration.


### References
[1] https://www.kaggle.com/snap/amazon-fine-food-reviews/code

[2] https://medium.com/luisfredgs/automatic-text-summarization-with-machine-learning-an-overview-68ded5717a25

[3] https://colab.research.google.com/github/ziadloo/attention_keras/blob/master/examples/colab/LSTM.ipynb

[4] https://www.tensorflow.org/api_docs/python/tf/keras/backend/rnn

[5] https://www.itm-conferences.org/articles/itmconf/pdf/2021/05/itmconf_icacc2021_03023.pdf
