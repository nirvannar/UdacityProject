# UdacityProject
My first Udacity Project based on CRISP-DM
# Table of Contents

* [Installation](#Installation)
* [Project Motivation](#Project-Motivation)
* [File Descriptions](#File-Descriptions)
* [Results](#Results)
* [Licensing, Authors, and Acknowledgements](#Licensing,-Authors,-and-Acknowledgements)


## Installation <a name="Installation"></a>
The code should run with no issues using Python versions 3.8.8 using Jupyter Notebook server version 6.3.0.  Numpy, Pandas, matplotlib.pyplot, math, seaborn, wordcount, Datapane and Folium libraries were used

```python
pip install -U datapane
```

## Project Motivation <a name="Project-Motivation"></a>
For this project, I was interestested in using Smithsonian Institution data from the Global Volcanism Program entitled Volcanoes of the World 4.10.1, downloaded on 24 Jul 2021 at 11:16 AM	to use characteristcs of Holocene volcanoes for the purpose of Volcano tourism.  It will allow the traveller to use a combination of analyses to pick the locations for leisure travel purposes.  
The .csv file was analysed using Jupyter Notebook.  It had 1398 rows of data and 4 columns of quantitative variables.  The total columns were 14 with 2 containing blanks.  The colums of data "Dominant Rock Type" and "Tectonic Setting" conatined blanks.  However these were not used to obtain results and are excluded from any analysis.  

Data understanding – What data do we have / need? Is it clean?
Data preparation – How do we organize the data for modeling?
Modeling – What modeling techniques should we apply?
Evaluation – Which model best meets the business objectives?
Deployment – How do stakeholders access the results?



**_The following questions were required to be answered from the data._**
 
*Which is the highest Volcano in the world?  
Which country has the most volcanoes?
What is the most common volcano type?  
Which year had the most eruptions  2021 July YTD, and which were they?  
Which is the closest volcano to OR Tambo Airport in Johannesburg, South Africa?  
Which are the active volcanoes within 3000km radius of OR Tambo Airport in Johannesburg, South Africa?*



## File Descriptions  <a name="File-Descriptions"></a>
There is one notebook available here to showcase work related to the above questions. 

The notebook is exploratory in searching through the data pertaining to the questions showcased by the notebook title. Markdown cells were used to assist in walking through the thought process for individual steps.



## Results <a name="Results"></a>

[A Medium blog](https://medium.com/@nirvannsramp/intrepid-explosive-voyages-77f23e47e24e?source=friends_link&sk=b97c94187c9f435b0b955aa12acc408d) was created using the results. 

## Licensing, Authors, and Acknowledgements<a name="Licensing,-Authors,-and-Acknowledgements"></a>
The data was downloaded from the Smithsonian Institution Global Volcanism Program. Stack Overflow, Kaggle, Medium and Github were consulted for syntax references.  
The Volcano marker used in the Folium map was created by Joris Hoogendoorn from the Noun Project
