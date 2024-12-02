> The purpose of a system is what it does
> ~ some guy

Completely ignoring the above quote, I'll start off with what the _intention_ is for PropertyEyeJA before I get into what it **is**.

PropertyEyeJA aims to provide insight into the Jamaican real estate market in an accessible (mostly) manner, attempting to provide some amount of information symmetry among market participants.

In short, this platform/web app/data source **should** make it wayyyy easier for you to glean some insight into an otherwise opaque (IMO) market. 


## Not so frequently asked questions

### What is PropertyEyeJA?
It's a fun project that I will try to tinker with and iteratively improve

### Do I have to pay you?
Well, first I don't think we've been acquainted and I'm not entirely sure if this is **valuable** to you. So, first how about you try to use it and then we can talk about compensation a bit later on. For now, you can pay me by making the usage numbers go up.

### How do you get the data?
The same way that you do! Real estate data is, thankfully, pretty abundant however disorganized. I access it from public listing sources, clean it, and drop it here for your convenience.
Enriching the data might involve adding accessory data sources like povery data, some inference from satellite imagery, and, of course, input from _AI_. 

### How reliable is the data?
<Legalese>This website or its maintainer in no way guarantees complete accuracy and accepts zero responsibility for any actions that you choose to undertake after consuming that data</Legalese>
With that being said, I've eye-balled it and cleaned it and de-duplicated it and in my **gut** it looks good. Obviously, you should verify it (like with any data source).

### On the accuracy of the Price Estimation Model
I spent a few weeks on another projecting working on the Real Estate price estimation model with the hopes that I could replicate [Zillow's Zestimate accuracy rate](https://www.zillow.com/z/zestimate/) which has a median error rate of around 2.4%. 

The idea was that if I could have a model that predicted valuations with sub-5% error rates I could reliably identify arbitrage opportunities then [some steps in between] and profit.

Unfortunately for me (and perhaps fortunately for you) that was **not** possible for me with my woefully inadequate dataset. Below I've included a snapshot of the median error rate by parish so you can get an idea of how much you can trust the values produced by the model.

Bear in mind that I don't guarantee any level of accuracy and the model is **at best** directionally interesting to look at...for now 🤞

#### Price Estimator Model Accuracy by Parish

| Parish           | Median Error Rate | Test Sample Size |
|------------------|-------------------|------------------|
| Clarendon        | 17.72%            | 96               |
| Hanover          | 17.88%            | 22               |
| Kingston & St. Andrew | 10.46%      | 614              |
| Manchester       | 18.06%            | 156              |
| Portland         | 38.07%            | 15               |
| St. Ann          | 11.24%            | 205              |
| St. Catherine    | 15.20%            | 283              |
| St. Elizabeth    | 20.40%            | 67               |
| St. James        | 23.79%            | 143              |
| St. Mary         | 10.27%            | 79               |
| St. Thomas       | 20.88%            | 21               |
| Trelawny         | 9.69%             | 40               |
| Westmoreland     | 19.54%            | 62               |


### Which team is behind this project?

A team of 1 so far

<img src="https://github.com/user-attachments/assets/f33675cd-0a7c-49a1-9e75-b55a3fa7c805" alt="Jordan Barrett, moi" width="280">

Quick stats:
* Jordan Barrett
* Data Engineer
* Serial BeautifulSoup enjoyer
* Senior LLM playground user (RIP Davinci-Instruct)
* Graph enthusiast

Web identity:
- https://github.com/jordan-barrett-jm/
- https://www.linkedin.com/in/jordan-barrett-jm/


### Complaints and Feedback

For all complaints, you can write up a thoughtful, emotive, and heartfelt draft in Google Docs using Times New Roman 12pt font. Double-spaced if you would kindly. You can direct those well-crafted complaints to your recycling bin and can expect an immediate response as seratonin is released and your stress levels fall.

For constructive feedback, which is **welcome** you can email me (Jordan) personally at the email address below:
![image](https://github.com/user-attachments/assets/9aec2850-cd7e-43db-ab43-3f630608f95e)

**NOTE**: You can also send me cool data sources, which I maintain a repository of [here](https://docs.google.com/document/d/e/2PACX-1vTNApip1F4QHeQY3z_1oN5pyCoOZ1K091lt_Rvm0nue1XdAgq6xd81PckYUSbSFePI1x5KvQ_i_s24S/pub)

**NOTE2**: I'm always open to considering collaboration on cool/exciting/challenge data projects. Feel free to reach out.



