---
layout: post
title: Digimon Lab
subtitle: Reading Files and CSVs
cover-img: /assets/img/Digimon_Adventure_2020_episode_6.jpg
tags: [labs, python]
author: Jack Komaroff
---
**By Jack Komaroff**

## My Code
The following is my *digimon.py* file which contains the methods that I used to answer the lab questions.

```py
import csv

#this method inputs the csv file and will find the average speed of all digimon by iterating through the csv
#each line it will the current speed to a total speed counter and add 1 to the total digimon counter
#then it returns the average
def avgSpeed(filePath):
    numDigimon=0
    speedDigimon=0
    with open(filePath, "r") as file:
        data = csv.reader(file)
        next(data)
        for i in data:
            i[12]=int(i[12])
            #turns data into ints so we can average
            numDigimon+=1
            speedDigimon+=i[12]
    return (speedDigimon/numDigimon)



#this method will input a csv file, an characteristic of a digimon, and a value for that characteristic
#it will then return how many digimon in the csv have that characteristic with that specific value
def countDigimon(filePath,characteristic,value):
    counter=0
    with open(filePath, "r") as file:
        data = csv.DictReader(file)
        for i in data:
            if i[characteristic]==value:
                counter+=1
            #if the row has a characteristic value equal to the desired characteristic value, then add 1 to counter
    return counter


#this method will input a csv file, a desired number of digimon on the team, a desired attack total, and a desired memory total
#it will find a team that meets those specifications and return the team roster (with team info) as a dictionary
def findDigimonTeam(filePath, desiredNumDigimon, desiredAttackTotal, desiredMemoryTotal):
    myTeam={"Total Attack Power":{},"Total Memory":{}, "Number of Digimon on Team":{}}
    #if the user inputted more than 3 digimon desired, we need to set it to 3 because 3 digimon is the maximum number per team
    if desiredNumDigimon>3:
        desiredNumDigimon=3
    numDigimon=0
    totalAttackPower=0
    totalMemoryUsed=0
    atkPerDigimon=desiredAttackTotal/desiredNumDigimon
    memPerDigimom=desiredMemoryTotal/desiredNumDigimon
    with open(filePath, "r") as file:
        data = csv.reader(file)
        next(data)
        for i in data:
            #make our data ints
            i[9]=int(i[9])
            i[5]=int(i[5])
            #if the specific digimon has sufficient attack power, not too much memory, and we haven't filled a team roster yet
            if (i[9] >= atkPerDigimon) and (i[5]<=memPerDigimom) and (numDigimon<=(desiredNumDigimon-1)):
                numDigimon+=1
                totalAttackPower+=i[9]
                totalMemoryUsed+=i[5]
                myTeam["Teammate #"+str(numDigimon)]={"Digimon": i[1], "ID": i[0], "Attack Power":i[9], "Memory":i[5]}
                #add this digimon to our team roster and include the specific info for that digimon in our table
        myTeam["Total Attack Power"]=totalAttackPower
        myTeam["Total Memory"]=totalMemoryUsed
        myTeam["Number of Digimon on Team"]=numDigimon
    return myTeam

print(avgSpeed("Datasets/digimon.csv"))
#how many digimon have a type of vaccine type
print(countDigimon("Datasets/digimon.csv","Type","Vaccine"))
#how many digimon have a attribute of Fire
print(countDigimon("Datasets/digimon.csv","Attribute","Fire"))
#I have set the parameters to be 3 digimon, 300 minimum attack power, and 15 maximum memory (the lab specifications), but we could change these parameters depending on the situation
print(findDigimonTeam("Datasets/digimon.csv",3,300,15))
```
## Lab Questions

**1. What is the average speed (Spd) of all Digimon?**

My method *avgSpeed()* returns 120.40160642570281. 

This method iterates through every digimon and adds that digimon's speed to a total. 
At the end, we divide this total by the number of digimon counted to get the average speed. 

This is the basis for how I found the total speed of every digimon and found how many digimon were counted:
```py
for i in data:
            i[12]=int(i[12])
            #turns data into ints so we can average
            numDigimon+=1
            speedDigimon+=i[12]
    return (speedDigimon/numDigimon)
```
**2. Write a function that can count the number of Digimon with a specific attribute. For example, count_digimon("Type", "Vaccine") would return 70.**

My method *countDigimon()* will return the number of digimon with the a specific characteristic value. For example, *countDigimon()* with parameters *Attribute* and *Fire* will return 33. I employed the following code to check if a certain digimon had the desired specific characteristic:

```py
for i in data:
            if i[characteristic]==value:
                counter+=1
```

**3. The Digimon on your team are restricted by the total amount of Memory that they need. If your team only has 15 Memory, name a team of up to 3 Digimon that has at least 300 attack (Atk) in total.**

My method *findDigimonTeam()*, will return a dictionary that describes a team of digimon that has a user-set minimum attack power, a user-set maximum digimon per team, and a user-set maximum total memory.

After properly storing our inputs, we can use the following code to assemble our digimon team and add it to the dictionary:
```py
for i in data:
    #make our data ints
    i[9]=int(i[9])
    i[5]=int(i[5])
    #if the specific digimon has sufficient attack power, not too much memory, and we haven't filled a team roster yet
    if (i[9] >= atkPerDigimon) and (i[5]<=memPerDigimom) and (numDigimon<=(desiredNumDigimon-1)):
        numDigimon+=1
        totalAttackPower+=i[9]
        totalMemoryUsed+=i[5]
        myTeam["Teammate #"+str(numDigimon)]={"Digimon": i[1], "ID": i[0], "Attack Power":i[9], "Memory":i[5]}
```
For the restrictions described in the lab instructions (a minimum attack power of 300, a maximum of 3 digimon on a team, and a maximum memory of 15), my method returned the following digimon team:
```py
{'Total Attack Power': 324, 'Total Memory': 9, 'Number of Digimon on Team': 3, 'Teammate #1': {'Digimon': 'Koromon', 'ID': '6', 'Attack Power': 109, 'Memory': 3}, 'Teammate #2': {'Digimon': 'Tsunomon', 'ID': '8', 'Attack Power': 107, 'Memory': 3}, 'Teammate #3': {'Digimon': 'Tsumemon', 'ID': '9', 'Attack Power': 108, 'Memory': 3}}
```

Obviously there are dozens of other acceptable team rosters, the above roster is just one combination that fulfills the lab requirements.

## References

I did not work with anyone to complete this lab and I did not use any internet sources.

## What Worked

I used *csv.reader()* for 2 questions, but for the counting digimon with certain characteristics, I wanted to use *csv.DictReader()* so that I could utilize the different headers as keys for the dictionary because my user input would include one of those keys. 

I also utilized a few counters in my methods and those helped to keep track of incrementing values.

## What Didn't Work

Initially, I was not able to get my *findDigimonTeam()* method to create a new nested dictionary with name Teammate #n. I had to tinker with this until I realized that I was adding a string to an int, and I needed to convert the digimon number to a string in order to add it to the dictionary name. 

## Improvements for Next Lab

Next lab I think I should start with psuedocode instead of jumping straight into the coding process. This would provide a better workflow and allow me to complete the lab more efficiently, instead of just trying different approaches until one ultimately worked. 

## What I Learned

I learned about including more places for user input instead of hard-coding all the inputs to exactly meet the lab specifications. This way the code is more usable to users with a variety of different goals. For example, if there was a special digimon game mode where up to 9 digimon were allowed, the user could easily use my code by simply inputting a 9 instead of a 3 in the *desiredNumDigimon* parameter. This is a very useful aspect in creating method which allows them to be better utilized a wider variety of circumstances. 

Additionally, I learned about practical applications of reading CSVs. The same methods in *digimon.py* could be easily applied to sorting foods (based on calories, size, price, etc.) or even ranking stock choices (based on share price, analyst rankings, company debt, etc.)