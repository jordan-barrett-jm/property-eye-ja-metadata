> To overcome difficulties is to experience the full delight of existence, no matter where the obstacles are encountered.

~ Arthur Schopenhauer


I'm not so sure about the delight bit, but working with patchy, heterogeneous and not-so-error-free real estate listing data has definitely had its obstacles.

**PropertyEyeJA** aims to provide insight into the Jamaican real estate market in an accessible manner, with the overall intention of reducing information asymmetry between would-be buyers and other hopeful market participants and the more experienced agents within the market. 

In short, this platform *should* make it substantially easier for you (assuming the modal interested-but-not-informed user) to glean some insight into an otherwise opaque property market. 

I offer these insights by crawling listing sites, then cleaning, standardizing and aggregating the data. The visualizations shown on this site were determined at my discretion, but they were guided by the aim to provide maximal insight with minimum headache for the viewer. I apologize if I've failed in that effort.


## Not so frequently asked questions

### Is there a charge?
Yes, if you use this site for more than 30 seconds you are obligated to pay me in Internet points. That's right, you'll need to share it with your friends.

### How do you get the data?
Real estate data is pretty abundant, however disorganized. I access it from public listing sources, clean it, and drop it here for your convenience.
Enriching the data might involve adding accessory data sources like poverty statistics, some inference from satellite imagery, and, perhaps , input from _AI_. 

### How reliable is the data?

< Legalese >

> This website and its administrator disclaim any guarantees of complete accuracy regarding the information provided.
> Furthermore, they accept no responsibility or liability for any actions taken based on the use or interpretation of the data presented.
> Users are advised to exercise their own judgment and due diligence when relying on the information available.

< /Legalese >



With that being said, I've eye-balled it and cleaned it and de-duplicated it and in my **gut** says it looks _reasonably_ good (barring sample size issues for granular filters). Obviously, you should verify it ([like with any data source](https://www.global-developments.org/p/how-much-should-we-trust-developing).
One thing I do want to note here is that its listing data, so it's likely slightly biased upwards. 

Assuming that the seller is an economically reasonable agent, a reasonable bet would be that the prices stated are the highest the seller believes they can reasonably get the listing sold for. So, I'd say some slight rounding down would be in order maybe on the order of 2-3% from my investigation.

### On the (in)accuracy of the Price Estimation Model
I spent a few weeks on another project working on the Real Estate price estimation model with the hopes that I could replicate [Zillow's Zestimate accuracy rate](https://www.zillow.com/z/zestimate/) which has a median error rate of around 2.4%. 

The idea was that if I could have a model that predicted valuations with sub-5% error rates I could reliably identify arbitrage opportunities then [some steps in between] and profit.

Unfortunately for me (and perhaps fortunately for you) that was **not** possible for me with my woefully inadequate dataset. Below I've included a snapshot of the median error rate by parish so you can get an idea of how much you can trust the values produced by the model.

Bear in mind that I don't guarantee any level of accuracy and the model is **at best** directionally interesting to look at...for now 🤞

#### Price Estimator Model Accuracy by Parish (As of Dec 2024)

![image](https://github.com/user-attachments/assets/c751e0a5-45cd-495f-aab8-3d9de956d0bc)

### How are the growth statistics calculated?

I've recently refreshed how I go about handling growth calculations to be a lot more conservative. My initial implementation was using some heavy statistical machinery that I think was a bit too much for the scale of data we're handling here. 

I calculate the growth figures by first dividing up the data into quarters, starting from the beginning of 2022. I also find the price per square foot for each listing. This is the building size of the property (not the lot size). I found that price per square foot was the metric most economically sensible to since it normalizes the data across numbers of rooms, and makes it more sensible to compare different property types.

![image](https://github.com/user-attachments/assets/81f524e7-e1e0-45dd-b8c6-0b2d3d6de59d)


I then filter out by property types. I stick with the property types that have the most listings so I don't get wonky growth figures. Those are: houses, apartments, and townhouses. I only show townhouse and apartment growth data for Kingston and St. Andrew because the other regions have such low listing numbers that it makes the figure unreliable and highly unstable.

![image](https://github.com/user-attachments/assets/eaf3daf6-ebbe-4d98-973f-58ddffaf5f26)


For each quarter, I find the median price per square foot across each stratum - house, townhouse, apartment - and the growth rate is defined as the difference in value between current and last quarter in the same time last year divided through by the value in the last quarter. 

![image](https://github.com/user-attachments/assets/f28aeeab-ed04-4602-b4ab-caeadd2beea0)

For illustration, if the price per square foot for an apartment in 2025Q1 is $104 and in 2024Q1 it was $100, then the growth in 2025Q1 would be 4%.

### What team is behind this project?

A team of 1 so far

![391738637-f33675cd-0a7c-49a1-9e75-b55a3fa7c805 (1)](https://github.com/user-attachments/assets/1bf03807-ed9e-4685-a721-21e465c55124)


Quick stats:
* Jordan Barrett
* Data Engineer
* Serial BeautifulSoup enjoyer
* Senior LLM playground user (RIP Davinci-Instruct)
* Graph enthusiast

Web identity:
- [Github](https://github.com/jordan-barrett-jm/)
- [Professional persona](https://www.linkedin.com/in/jordan-barrett-jm/)


### Complaints and Feedback

For all complaints, you can write up a thoughtful, emotive, and heartfelt draft in Google Docs using Times New Roman 12pt font. Double-spaced if you would kindly. You can direct those well-crafted complaints to your recycling bin and can expect an immediate response as your cortisol levels plummet and dopamine releases.

For constructive feedback, which is **welcome** you can email me (Jordan) personally at the email address below:
![image](https://github.com/user-attachments/assets/9aec2850-cd7e-43db-ab43-3f630608f95e)

**NOTE**: You can also send me cool data sources, which I maintain a repository of [here](https://docs.google.com/document/d/e/2PACX-1vTNApip1F4QHeQY3z_1oN5pyCoOZ1K091lt_Rvm0nue1XdAgq6xd81PckYUSbSFePI1x5KvQ_i_s24S/pub)

**NOTE2**: I'm always open to considering collaboration on cool/exciting/challenging data projects. Feel free to reach out.



