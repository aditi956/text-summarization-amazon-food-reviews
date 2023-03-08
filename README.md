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

review, and vice - versa for a neutral rating.

![image](https://user-images.githubusercontent.com/94414506/223651878-57308b11-811f-4390-8a21-f546ce83c571.png)

review, and vice - versa for a neutral rating.

Following data pre-processing steps were performed on the reviews in the dataset:
1. All the text was converted into lower case.
2. Stopwords were removed using the stopwords in the English language.
3. All the word contractions that were present in the text were expanded. Example - ‘I’m’ to ‘Iam’.
4. All the special characters, extra whitespaces and links were removed.




