# Kew Coding Club - Using APIs
### 2020-01-30

**WELCOME TO THE FIRST KEW CODING CLUB**

## How the session will run

In this first session we will:
1. Run a bit of a questionnaire to find out what people want from the Coding Club
2. Have a bit of an introduction/refresh on how APIs work and how to use them
3. Complete some challenges around accessing data from APIs

## Questionnaire!

This is an **interactive** questionnaire! :scream:

For each question, you can add your own answer to the poll in the grey area below a question by editing the text between the three backticks in your editing window.

For example, if the question is **what is your favourite plant** :evergreen_tree:?

```
********* oak
* banana
*** strawberry
```

If someone has already added your answer, you can add an extra `*` behind it to vote for it.

```
* oak
****** banana
```

And then it will come out looking like a nice bar chart!

### I mainly work in this language

```
****Python
SQL
**R

```

### I am interested in learning more about this language

```
******Python
**R
*SQL
*****bash
```

### I feel confident using these packages

```
*seabourne
plotly
*ape
***ggplot
*requests
**d3 
*****pandas
**dplyr
**numpy
**rCAT
*rredlist
*rgbif
*sklearn
mysql-connector
```

### I feel confident when coding these tasks

```
**dealing with dbs
****plotting
******(tidy)data cleaning
fiddling with phylogentic trees
none of the above
```

### I am struggling with

```
**tidy code
object-relational mapping 
******finding the time to teach myself
*object oriented stuff

```

### I would like to use coding to be able to

```
****build apps
****reproducable research
**data exploration
** save time
*create pipelines
```

### I would like future sessions to focus on

```
*****formatting your code like a pro
**plant name reconciliation

```
## Intro to APIs!

The intro to APIs is in a file [that can be found here](https://github.com/barnabywalker/kew_coding_club/blob/master/docs/sessions/intro_20200130_apis.md).

Any questions? Type them below!

```
Is there an API for IPNI?

```

IPNI API URL format (returns JSON):

https://beta.ipni.org/api/1/[object type]/[id]

https://beta.ipni.org/api/1/n/12345-1

- n for names 
- a for authors
- p for publications

## Challenges!

A template notebook [can be found here](https://github.com/barnabywalker/kew_coding_club/blob/master/challenges/20200130_apis.ipynb). Download it if you want, or just completed the challenges in whatever environment suits you best!

Have a go at the challenges below. 

If you finish a challenge, please offer your help to anyone that hasn't yet finished it! 

If you need help, please don't hesitate to ask someone that has finished the challenge you're stuck on!

All of these challenges involve accessing data from the GBIF API. There are packages that provide wrappers for this API in [python](https://github.com/sckott/pygbif) and [R](https://www.gbif.org/tool/81747/rgbif), but it can help you to learn how APIs work if you try to access the API directly yourself. The documentation for the API can be found here: https://www.gbif.org/developer/summary.

### Challenge 1

Use the GBIF Occurrence API (https://www.gbif.org/developer/occurrence) to get the total number of records held in their database.

Put any code you want to show in backticks below.

```
#baz's solution
```
```
#eduardo's solution
import sys
!{sys.executable} -m pip install pygbif

from pygbif import occurrences as occ
print(occ.count())

#1391094317

or 

import requests

response = requests.get('http://api.gbif.org/v1/occurrence/count')
print(response.text)

#1391094317
```
```
#Heather+Alex+Baz solution
import requests
r= requests.get('http://api.gbif.org/v1/occurrence/count')
r.text
```

```
steve says: 1391094317

```
```
#Berta's solution (Python)
import requests
response = requests.get('http://api.gbif.org/v1/occurrence/search')
if response.status_code == 200:
    json_response = response.json()
    print("total number of records:", json_response["count"])
    # result: 1391094318
```

### Challenge 2

Use the GBIF API to get the total number of occurrence records for *Myrcia decorticans*. 
*hint: you'll need to use the GBIF Species API (https://www.gbif.org/developer/species) to get the species ID first*

Put any code you want to show in backticks below.

```
```

```
Alex Z.

import requests

ParamID={'name':'Myrcia decorticans'}
SppInfo=requests.get('http://api.gbif.org/v1/species/match',params=ParamID).json()
SppKey=SppInfo["speciesKey"]
ParamOcc={'taxonKey':SppKey}
SppOccurrences=requests.get('http://api.gbif.org/v1/occurrence/count/',params=ParamOcc)
print(SppOccurrences.text)
```

```
Eduardo says:

response = requests.get('http://api.gbif.org/v1/occurrence/search?speciesKey=3174041')
jresponse = response.json()
countresponse = jresponse['count']
print(countresponse)

696
```


```
steve says: 696
# challenge 2 - total number of occurrence records for Myrcia decortans. Using rgbif package
nameq <- name_backbone("Myrcia decortans")
nameKey <- nameq$usageKey
nameCount <- occ_count(nameKey)

```
```
# Berta's solution (Python)
import requests

response = requests.get('http://api.gbif.org/v1/species/match?name=myrcia decorticans')
if response.status_code == 200:
    json_response = response.json()
    m_decorticans_key = json_response["speciesKey"]
    print("M.decorticans species key:", json_response["speciesKey"])
elif response.status_code == 404:
    print('Not Found.')

response = requests.get('http://api.gbif.org/v1/occurrence/search?speciesKey='+str(m_decorticans_key)+'')
if response.status_code == 200:
    json_response = response.json()
    print("total occurences M.decorticans:", json_response["count"])
elif response.status_code == 404:
    print('Not Found.')
    
# Results
# M.decorticans species key: 3174041
# total occurences M.decorticans: 696
```

```
HLL+Alex  
import requests
r=requests.get('http://api.gbif.org/v1/species/match?name=Myrcia%20decortican')
k=r.json()['speciesKey']
r=requests.get('http://api.gbif.org/v1/occurrence/count?taxonKey='+str(k))
r.text

```
### Challenge 3

Use the GBIF API to get all occurrence records for *Myrcia decortans* that have coordinates and there are no geospatial issues with those coordinates.

Put any code you want to show in the backticks below.

```
nameq <- name_backbone("Myrcia decortans")
nameKey <- nameq$usageKey
cleanoccs <- occ_data(nameKey, hasGeospatialIssue = F, limit = 200000, hasCoordinate = T)

```

```
Alex Z.

import requests

ParamID={'name':'Myrcia decorticans'}
SppInfo=requests.get('http://api.gbif.org/v1/species/match',params=ParamID).json()
SppKey=SppInfo["speciesKey"]
ParamOcc={'taxonKey':SppKey,'hasCoordinate':True,'hasGeospatialIssue':False}
SppOccurrences=requests.get('http://api.gbif.org/v1/occurrence/search/',params=ParamOcc)
```
