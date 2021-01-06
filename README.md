# Edmunds--Statistical-Analysis--Python-R
# Edmunds is one of America’s renowned automobile information resource where customers can obtain information deals associated with used as well as new cars. 
# To analyses the enormous amount of data generated from their website. Car reviews for more than forty brands from its website is analyzed and visualized using various models including the sentimental analysis, 
# text classification and topic modelling have been performed. The primary goal of this project is to help the customer select the right brand, based on the real time opinion of thousands of customers, 
# all information concerning the car be it the vehicle’s make, model, the capacity and the review data is considered. The reviews data is analyzed and used for building a customer friendly dashboard that gives away all the information about cars and the customer satisfaction levels through a few clicks.

# Code

import nltk.corpus
nltk.download ('stopwords')
from nltk.corpus import stopwords
import string
from wordcloud import WordCloud
import matplotlib.pyploy as plt
import pandas as pd
from nltk.stem import *
from textblob import TextBlob

# Toincrease the width of the output screen
desired_width = 320
pd.set_option ('display.width',desired_width)
pd.set_option('display.max_columns',12)

# Reda the dataset
car_data = pd.read_csv(r' path')
# create an another column with same data (Reviews)
car_data ['Normalize_review'] = car_data['Review']

# Remove noise from the data

car_data ['Normalize_review']= car_data ['Normalize_review']. str.repace('[^a-zA-Z]', ' ')

# Remove the stopwords
stop = stopwords.words('english')
car_data ['Normalize_review']= car_data ['Normalize_review'].apply(lambda x: ' ' .join([word for word in x.split() if word not in (stop) and len(word)>3]))
car_data['New_norm_review']= car_data ['Normalize_review']

# Tokenize the data
Tokenized_car_Reviews = car_data ['Normalize_review'].apply(lambda x: x.split())

# Lematize the tokens
Lemmatizer= WordNetLemmatizer()
Tokenized_car_Review = Tokenized_car_Reviews.apply(lambda x: [Lemmatizer.lemmatize(i) for i in x])
car_data ['Lemmatized_data'] = Tokenized_car_review

# Merge all the lemmatized tokens

for i in range(len(Tokenized_car_Reviews)):
         Tokenized_car_Review[i] = ' ' .join(Tokenized_car_Review[i])
car_data[Normalize_review']= Tokenized_car_Review


# Generate word cloud
Total_words= ' '.join([text for text in car_data['Normaize_review']])
wordcloud = WordCloud(width=1000, height= 600, random_state= 110).generate(Total_words)
plt.figure(figsize = (15,8))
plt.imshow(wordcloud,interpolation='bilinear')
plt.axis('off')
plt.show()


# Perform sentimental analysis and store the data in diff columns
car_data = car_data.assign(Polarity='', Subjectivity='')

for j, car_reviews_new in enumerate(car_data.Normalize_review):
      textblob = TextBlob(carreviews_new)
      car_data.Polarity[j]= textblob.polarity
      car_data.Subjectivity[j]= textblob.subjectivity


# Print the output
print(car_data)

# Save the data to a CSV file
car_data.to_csv(r'path')






