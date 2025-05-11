> The purpose of a system is what it does

~ Stafford Beer


Completely ignoring that [elegant dictum from Mr Beer](https://en.wikipedia.org/wiki/The_purpose_of_a_system_is_what_it_does), I'll start off with what the _intention_ is for PropertyEyeJA before I get into what it **is**.

PropertyEyeJA aims to provide insight into the Jamaican real estate market in an accessible (mostly) manner, attempting to provide some amount of information symmetry among market participants.

In short, this platform/web app/data source **should** make it wayyyy easier for you to glean some insight into an otherwise opaque (IMO) market. 


## Not so frequently asked questions

### What is PropertyEyeJA?
It's a fun project that I will try to tinker with and iteratively improve

### Do I have to pay you?
Well, first I don't think we've been acquainted and I'm not entirely sure if this is **valuable** to you. So, first how about you try to use it and then we can talk about compensation a bit later on? For now, you can pay me by making the usage numbers go up.

### How do you get the data?
The same way that you do! Real estate data is, thankfully, pretty abundant however disorganized. I access it from public listing sources, clean it, and drop it here for your convenience.
Enriching the data might involve adding accessory data sources like povery data, some inference from satellite imagery, and, of course, input from _AI_. 

### How reliable is the data?

< Legalese >

> This website and its administrator disclaim any guarantees of complete accuracy regarding the information provided.
> Furthermore, they accept no responsibility or liability for any actions taken based on the use or interpretation of the data presented.
> Users are advised to exercise their own judgment and due diligence when relying on the information available.

< /Legalese >



With that being said, I've eye-balled it and cleaned it and de-duplicated it and in my **gut** says it looks _reasonably_ good (barring sample size issues for granular filters). Obviously, you should verify it ([like with any data source](https://www.global-developments.org/p/how-much-should-we-trust-developing).

### On the (in)accuracy of the Price Estimation Model
I spent a few weeks on another projecting working on the Real Estate price estimation model with the hopes that I could replicate [Zillow's Zestimate accuracy rate](https://www.zillow.com/z/zestimate/) which has a median error rate of around 2.4%. 

The idea was that if I could have a model that predicted valuations with sub-5% error rates I could reliably identify arbitrage opportunities then [some steps in between] and profit.

Unfortunately for me (and perhaps fortunately for you) that was **not** possible for me with my woefully inadequate dataset. Below I've included a snapshot of the median error rate by parish so you can get an idea of how much you can trust the values produced by the model.

Bear in mind that I don't guarantee any level of accuracy and the model is **at best** directionally interesting to look at...for now 🤞

#### Price Estimator Model Accuracy by Parish (As of Dec 2024)

![image](https://github.com/user-attachments/assets/c751e0a5-45cd-495f-aab8-3d9de956d0bc)

### How is the price index constructed?

#### Background

First, I'll start with the background on _why_ a price index was even required. Jamaica's real estate market is fairly small (in terms of volume of sales/listings) but with a large degree of diversity among the unique properties - # of bedrooms, the community it's located in, the square footage of the land its on. On a month-by-month basis there is considerable variation in the composition of the properties listed. I'll provide an example for illustration:

![image](https://github.com/user-attachments/assets/df4c5c29-01e9-46c2-bc7d-53052475d3c1)


This is somewhat exaggerated but not that far from observations I've made in the live data. The mix of properties varies over time, which has an impact on the average price across time periods. The result is that attempting to interpret how much the value has appreciated period-over-period becomes error-prone, as apples-to-apples comparisons become pretty much impossible. 

If you take the median prices at face value (haha) in the example I provided, you'd be forced to interpret home values as increasing almost 30% from Jan 2025 to Apr 2025. This would obviously be incorrect as the increase is largely attributable to there being more luxury properties listed in the latter period. 

Constructing a price index fixes the issue of variation in property mix across time. It allows an analyst to perform true apples-to-apples comparison across periods to identify how prices independent of quality have trended.

#### Implementation

The implementation for the price index was inspired by the following papers:

- [A Hedonic Residential Real Estate Index for Jamaica (R Brian Langrin - Bank of Jamaica)](https://boj.org.jm/uploads/pdf/papers_pamphlets/papers_pamphlets_A_Hedonic_Residential_Real_Estate_Index_for_Jamaica_A_Pilot_Study_of_the_Kingston_&_St._Andrew_Region.pdf)
- [How to better measure hedonic residential property price indexes (Mick Silver - IMF)](https://www.imf.org/external/pubs/ft/wp/2016/wp16213.pdf)

Specifically, my implementation resembles the characteristics approach described in the latter paper. In very simple terms (how I best understand things) I constructed the index in the below method:

1) Built a hedonic regression model for property listings over the past 3 years, incorporating home characteristic factors like bedrooms, bathrooms, square footage, etc. and the quarter it was listed in.
2) Defined a common basket of properties as the set of properties sold in the first quarter.
3) Predicted the value of the homes in that common basket for each successive period using the hedonic regression model.
4) Calculated the ratio between the average predicted value of the properties in each period and the value of those properties and multiplied it by 100.

The final calculation would be the index value for each period (quarter).

Now, I'll attempt a slightly more formal definition using the aid of an LLM:

We start by defining our hedonic regression model as the below
![image](https://github.com/user-attachments/assets/7a7d1661-64f3-4b5c-842a-887eea724103)


Fixed attributes are defined as bedrooms, bathrooms, parish, property type and square footage while segments are created for the pricing tier, parish (for the market model) and property type. 
These segments are made to interact with the time dummy variable as I observed them to vary significantly through time.

The reference basket is then derived from the first period and the average predicted price is calculated using our model.

![image](https://github.com/user-attachments/assets/e83dd31d-d5ba-4f54-828e-3e8e27e3f105)

We then use the same reference basket to calculate the average predicted price in quarter t

![image](https://github.com/user-attachments/assets/0314ea11-13fd-4908-969c-d2b3723aaefc)

Finally, the index for quarter t is found by calculating the ratio of average predicted prices through the ratio between the average predicted prices in quarter 0 and quarter t

![image](https://github.com/user-attachments/assets/730ef5fb-48c4-4233-bd91-1a8b1184f102)

If you have ideas on improvements I could make to this approach please do reach out but I'm OK enough with this method in that I don't feel like shutting down the whole web app every time I look at the chart. By that metric, this change represents considerable performance gains.


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



