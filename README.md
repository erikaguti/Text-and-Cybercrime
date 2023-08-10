# Can we predict cybercrime using text? A preliminary analysis

I set out to create a model to forecast the incidence of cyber attacks using data informed by newspaper articles. 

For cyber attack data I reached out to the owner of [Hackmageddon](https://www.hackmageddon.com/) for the data he uses to report the statistics on his website. And did a lot of data cleaning..

I merged this data with the topics from [conflictforecast.org](https://conflictforecast.org/downloads). A tool that uses LDA on the text of millions of newspaper articles to get the main topics of public discourse every month for every country.

I chose this data because I was curious if hackers would take advantage of times when public discorse was related to certain topics. One could think that perhaps hackers find it opportune to attack a country going through internal turbulence. A proxy for internal turbulence could be when public discorse centers around topics like war or health and emergencies. Or vice versa hackers might find it opportune to attack when a country is going through good times and its companies are failing to prioritze the need for cyber security investments. A proxy for good times could be when public discorse centers around topics such as civilian life or international cooperation.

My final dataset set contains 132 countries and spans from January 2014 to December 2022, making it 14,247 rows long. Each entry had the number of attacks reported in the country that month. To align my dataset with the specifications of the assignment I turn the problem into a binary classification task making each entry correspond to whether there was a cyber attack in the country that month or not. 

My random forest model had a AUC of .75, meaning the model has the capability to distinguish between times where there will be no cyber attack and times there will be a cyber attack with an accuracy of 75%. 

The second part of the assignment was to use the false negatives (FN), false postive (FP), true negative (TN), and true postive rates of the model and implement them into the following decision function. The function is meant to determine at what probability of a cyber attack occuring should the decision maker choose to take intervention measures.

<img width="555" alt="Screenshot 2023-08-10 at 8 41 52 PM" src="https://github.com/erikaguti/Text-and-Cybercrime/assets/57955273/b0e924f2-ecac-4616-a887-be524c0bd4b3">

For this I modeled a scenario where the decision maker is the Chief Security Officer (CSO) of a small to mid-size company seeking approval in increasing their budget for cyber security by 25\%. This forecast will provide complementary support for their proposal, since the model can forecast if there will be cyber attacks in their country of operation. If this is the case, it increases the likelihood that an attack is imminent for the company. 

I also used the following assumptions:

- cyber attack cost on company = 2980000 # the average cost of a cyber attack on a small business
- cost of cyber attack preventative measures = 500000 + 125000 # average cyber security budget of a small business plus a 25% increase
- assured effectiveness of preventative measures = .75

Based on these calculations, the optimal threshold to ask for additional money in the budget is when the risk predicted by the model is just below 30\%

This is a relatively low threshold, but I think its because since the cost of intervention is so low relative to the cost of an attack on the company, the decision maker can afford to have more false positives.


