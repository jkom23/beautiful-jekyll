---
layout: post
title: Animal Crossing API Lab
subtitle: Get 10 Bells If You Read My Lab
cover-img: /assets/img/animalCross.jpg
tags: [labs, python, API, data]
author: Jack Komaroff
---
**By Jack Komaroff**

## My Code

The following is my *animalcrossing.py* file which contains the methods that I used to answer the lab questions.

```py
from pip._vendor import requests
import csv
BASE_URL="https://hm-cs.herokuapp.com"
ENDPOINT="/sockOptions"
API_KEY = "ArtOfDataKEY123"
#payload setup and imports



def generateCSV():
    #make API requests and generate a CSV
    n=0
    payload= {'key': API_KEY, 'idx': n}
    with open("Datasets/animalCrossing.csv", "w") as file1:
        response = requests.get(BASE_URL+ENDPOINT,params=payload)
        response_text=response.text[1:]
        while response.ok:
            #while no API request errors, continue to change payload and get new socks items
            file1.write(response_text+"\n")
            n+=1

            payload= {'key': API_KEY, 'idx': n}
            #change our payload as we iterate through the API until we get errors and no more socks are left
            response = requests.get(BASE_URL+ENDPOINT,params=payload)
            response_text=response.text
            #turn this get object into a text object that we write to our csv


def sockTypeVariations():
    with open("Datasets/animalCrossing.csv", "r") as file2:
        data = list(csv.reader(file2))[1:]
        sockOptions={}
        #open the generated csv and make a table that will store the sock types
        for i in data:
            if i[0] not in sockOptions.keys():
                sockOptions[i[0]]=1
            else:
                sockOptions[i[0]]+=1
        #iterate through the csv, if the sock type isnt in the csv then add its type to the csv
        #if the sock type is in the csv then add 1 to that sock type value

        mostNumVariations = max(sockOptions.values())
        sockTypeWithMostVariations = []
        #find the largest value in the csv, the sock type with those values have the most possible variations
        #we will make a new list that has all of these sock types

        for keys in sockOptions:
            if sockOptions.get(keys)==mostNumVariations:
                sockTypeWithMostVariations.append(keys)
        #iterate through the sock types, if their value is the same as the max variation value, then add it to our special list
        #if not, then it doesnt have the most variations and doesnt go in the special list
    print(sockTypeWithMostVariations)


def sockColorOptions():
    with open("Datasets/animalCrossing.csv", "r") as file3:
        data = csv.reader(file3)
        colorOptions = {}
        next(data)
    #iterate through the generated csv and check for all the sock colors
    #if the sock color1 isnt in our color options dictionary then we add it, if it is there then increase our count of that color by 1
        for i in data:
            if i[5] not in colorOptions.keys():
                colorOptions[i[5]] = 1
            else:
                colorOptions[i[5]] += 1
    #repeat this process for color 2
            if i[6] not in colorOptions.keys():
                colorOptions[i[6]] = 1
            else:
                colorOptions[i[6]] += 1
    #if color 1 and color 2 are the same then remove one instance of it so we dont double count
            if i[5] == i[6]:
                colorOptions[i[6]] -=1 

        print(colorOptions)


generateCSV()
sockTypeVariations()
sockColorOptions()

#these functions give us our answers
```
## Discuss how you used the API to obtain the dataset.

For API requests, we need a few basic pieces of information (BASE_URL, API_KEY, ENDPOINT, and payload. With that, we can send requests to the API and receive data. This data (which is sent as an object) can be converted into text for us to add to a csv. To do this, we change our index value (starting at 0) in our payload and make requests until the server gives us an error (which we can tell with response.ok). So, every interaction we increase our index by 1 (with a local variable n) and this will get us the next sock in the API (this continues until we get an error because we have indexed through all socks on the server). After the API returns a data object using our get() method, we can turn response into response.text, which is a readable format and allows us to use the write() method and add that sock (and its characteristics) to the csv. Now we have a csv that has stored the entire line of sock characteristics (because we converted the get object into text) for each sock they are on individual lines (because we did +”\n”). 

## Which sock has the most variations? If there is more than one answer, then list all of them.

['argyle crew socks', 'color-blocked socks', 'frilly knee-high socks', 'holey tights', 'kiddie socks', 'mixed-tweed socks', 'no-show socks', 'semi-opaque socks', 'semi-opaque tights', 'sequin leggings', 'simple-accent socks', 'striped socks', 'striped tights', 'tube socks', 'ultra no-show socks', 'vivid leggings', 'vivid socks', 'vivid tights']

To determine the number of variations for sock types, I opened up the csv that I just generated using the API and I made a new dictionary. I iterated through this csv with csv.reader(file) because this is a defined dataset (as opposed to an API on the internet). We can iterate line by line to see if the sock type is already in our sock options dictionary. If it is not, which we can check with i[0] not in sockOptions.keys(), then we should add it in and set the value to be 1. If it is already in our dictionary, then increase the value of that key by 1. After doing this for the entire csv, we can see which key has the highest value. This represents the maximum possible variations for any sock type (because multiple sock types might have the largest possible variation value). We can then check through the sockOptions dictionary and if any sock types reach this max value (sockOptions.get(keys)==mostNumVariations), then we add that key to a special list of all socks with the maximum number of variations. This list is the answer to the question.

## How many socks of each color are there? If a sock has two different colors, it should be counted in both. However, if a sock has the same Color1 and Color2, make sure you don’t double count it!

{'Pink': 41, 'Red': 39, 'Green': 50, 'Light blue': 33, 'Orange': 27, 'Purple': 37, 'Blue': 47, 'Yellow': 33, 'Beige': 15, 'White': 85, 'Black': 59, 'Brown': 11, 'Gray': 31, 'Colorful': 14}

For sock color, we repeat a similar process of iterating through a csv and adding keys and values to a new dictionary. We then return a dictionary that has these values and this communicates the prevalence of certain colors as sock options. The only detail is that we need to account for color1 being the same as color2 (which would cause double counting because that sock is just one solid color, not two separate colors). We can get around this by checking if i[5] == i[6] and if so reduce that color counter by 1. 

## Discuss your process of how you worked on this lab. Include details such as who you worked with, what methods you tried, what worked or didn’t work, what could have gone better, and what you learned during this lab. Focus more on the programming side of the lab! Feel free to attach images, screenshots, pseudocode, etc to elaborate on your response.
 
At first this lab confused me because I wasn’t sure how to utilize the API to get the requests. Thankfully the csv part of the lab was simple enough because it was very similar to the penguin lab. Once I figured out the API part with Feingold’s help, I was on my way to properly cloth myself in socks for my trip to my Animal Crossing island! 

There was some initial difficulty with response.json() versus response.text, but once I got that sorted out I could begin to write data that I received from the API into a csv. I also had experimented with making a Sock class, but realized that this was unnecessary because I could just get all of the information and tweak my csv code to only utilize sock name, color1, and color2.  The maximum number of variations was probably the hardest idea conceptually and I worked with Mikail on that to figure out how a variable like that would work. Once created, it allows us to simply see which sock types have that max variation value and include only those sock types in the desired list that we output. 

During this lab, I was able to refine my understanding of APIs (and csvs) and advance the skills I had learned with the pokemon practice and the penguin lab. In a practical manner, I now understand how long it takes servers to respond to API requests. This was mildly annoying at first when it took two whole minutes to see if my code worked, but I now understand that is a part of how APIs work (especially on group server sites like herokuapp). Finally, I learned that we can use response.ok for more than just error messages. It can be a theoretical ‘final index’ for us to use in our while loop. This is different than with pokemon practice when we stopped when we finished all the pokemon listed in the messy data csv. 

Thanks for reading!