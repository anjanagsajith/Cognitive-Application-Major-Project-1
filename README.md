# Cognitive-Application-Major-Project-1
# -*- coding: utf-8 -*-
"""Iris major project 1.ipynb
Automatically generated by Colaboratory.
Original file is located at
    https://colab.research.google.com/drive/1ykONZ_U0VvCdxF76lb4DkrLQReeNYr-A
**MAJOR PROJECT - 1 (COGNITIVE
APPLICATION)**
IRIS FLOWER CLASSIFICATION
This is one of the most famous machine learning projects with Iris Flowers being the simplest
machine learning datasets in classification literature. The dataset has numeric attributes and
ML beginners need to figure out how to load and handle data. The iris dataset is small which
easily fits into the memory and does not require any special transformations or scaling, to
begin with.
The goal of this machine learning project is to classify the flowers into among the three species – virginica,
setosa, or versicolor based on length and width of petals and sepals.
Importing the required libraries
"""

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

"""Importing the dataset and printint first values we can also use df tail to print last few values"""

df = pd.read_csv('iris.csv')
df.head()

"""checking the discription of data"""

df.describe()

"""checking which data type is used for which values"""

df.info()

"""From the above data we can se that width and length are of type float64 and sprcies is of object
**displaing no. of samples on each class**
"""

df['Species'].value_counts()

"""preprocesssing the data and
check for null values
"""

df.isnull().sum()

"""**plotting **
Sepal.Length    
Sepal.Width     
Petal.Length    
Petal.Width
"""

df['Sepal.Length'].hist()
df['Sepal.Width'].hist()

df['Petal.Width'].hist()

df['Petal.Length'].hist()

"""plotting sepal length and width using scatterplot"""

colors = ['red', 'orange', 'blue']
species = ['virginica','versicolor','setosa']
for i in range(3):
    x = df[df['Species'] == species[i]]
    plt.scatter(x['Sepal.Length'], x['Sepal.Width'], c = colors[i], label=species[i])
plt.xlabel("Sepal Length")
plt.ylabel("Sepal Width")
plt.legend()

"""similarly plotting petal length and petal width"""

for i in range(3):
    x = df[df['Species'] == species[i]]
    plt.scatter(x['Petal.Length'], x['Petal.Width'], c = colors[i], label=species[i])
plt.xlabel("Petal Length")
plt.ylabel("Petal Width")
plt.legend()

for i in range(3):
    x = df[df['Species'] == species[i]]
    plt.scatter(x['Sepal.Length'], x['Petal.Length'], c = colors[i], label=species[i])
plt.xlabel("Sepal Length")
plt.ylabel("Petal Length")
plt.legend()

for i in range(3):
    x = df[df['Species'] == species[i]]
    plt.scatter(x['Sepal.Width'], x['Petal.Width'], c = colors[i], label=species[i])
plt.xlabel("Sepal Width")
plt.ylabel("Petal Width")
plt.legend()

"""**Training the model**"""

from sklearn.model_selection import train_test_split
# train - 70
# test - 30
X = df.drop(columns=['Species'])
Y = df['Species']
x_train, x_test, y_train, y_test = train_test_split(X, Y, test_size=0.30)

"""**Using logistic regression**"""

from sklearn.linear_model import LogisticRegression
model = LogisticRegression()

model.fit(x_train, y_train)

print("Accuracy: ",model.score(x_test, y_test) )

"""**using decision tree**"""

from sklearn.tree import DecisionTreeClassifier
model = DecisionTreeClassifier()

model.fit(x_train, y_train)

print("Accuracy: ",model.score(x_test, y_test) * 100)

"""**Using K nearest neighbour**"""

from sklearn.neighbors import KNeighborsClassifier
model = KNeighborsClassifier()

model.fit(x_train, y_train)

print("Accuracy: ",model.score(x_test, y_test) * 100)

"""**Hence we have sucessfully classified using 3 methods....**"""
