## Blog for Digimon Lab

Jack Komaroff
Feingold
Art of Data 2021-2022
E Period
10/20/21

## Lab Questions

**To see my code and the methods to solve all of these questions, please view *digimon.py*. The file will be attached in the assigment page for this lab on Google Classroom**

**1. What is the average speed (Spd) of all Digimon?**

My method *avgSpeed* returns 120.40160642570281. 

**2. Write a function that can count the number of Digimon with a specific attribute. For example, count_digimon("Type", "Vaccine") would return 70.**

My method *countDigimon* will return the number of digimon with the a specific characteristic value. For example, *countDigimon* with parameters *Attribute* and *Fire* will return 33.

**3. The Digimon on your team are restricted by the total amount of Memory that they need. If your team only has 15 Memory, name a team of up to 3 Digimon that has at least 300attack (Atk) in total.**

My method *findDigimonTeam*, will return a dictionary that describes a team of digimon that has a user-set minimum attack power, a user-set maximum digimon per team, and a user-set maximum total memory.

For the restrictions described in the lab instructions (a minimum attack power of 300, a maximum of 3 digimon on a team, and a maximum memory of 15), my method returned the following digimon team:

{'Total Attack Power': 324, 'Total Memory': 9, 'Number of Digimon on Team': 3, 'Teammate #1': {'Digimon': 'Koromon', 'ID': '6', 'Attack Power': 109, 'Memory': 3}, 'Teammate #2': {'Digimon': 'Tsunomon', 'ID': '8', 'Attack Power': 107, 'Memory': 3}, 'Teammate #3': {'Digimon': 'Tsumemon', 'ID': '9', 'Attack Power': 108, 'Memory': 3}}

## References

I did not work with anyone to complete this lab and I did not use any internet sources.

## What Worked

I used *csv.reader()* for 2 questions, but for the counting digimon with certain characteristics, I wanted to use *csv.DictReader()* so that I could utilize the different headers as keys for the dictionary because my user input would include one of those keys. 

I also utilized a few counters in my methods and those helped to keep track of incrementing values.

## What Didn't Work

Initially, I was not able to get my *findDigimonTeam* method to create a new nested dictionary with name Teammate #n. I had to tinker with this until I realized that I was adding a string to an int, and I needed to convert the digimon number to a string in order to add it to the dictionary name. 

## Improvements for Next Lab

Next lab I think I should start with psuedocode instead of jumping straight into the coding process. This would provide a better workflow and allow me to complete the lab more efficiently, instead of just trying different approaches until one ultimately worked. 

## What I Learned

I learned about including more places for user input instead of hard-coding all the inputs to exactly meet the lab specifications. This way the code is more usable to users with a variety of different goals. For example, if there was a special digimon game mode where up to 9 digimon were allowed, the user could easily use my code by simply inputting a 9 instead of a 3 in the *desiredNumDigimon* parameter. This is a very useful aspect in creating method which allows them to be better utilized a wider variety of circumstances. 