# Introduction 
### Inspiration for this project 
I had been looking for non-expensive, womens athlesiure clothes when a friend suggested going to a certain website (let's call it Website A). He told me that all the shorts on Website A were "cheap". I was mildly surprised, as I was certain I had looked on Website A before and the shorts had been expensive. Regardless, as per his recommendation, I visited the site again, and was not surprised that indeed, all the womens shorts were still expensive. Then, out of curiousity, I visited the mens site. To my surprise (and mild outrage), the mens shorts were being sold at a lower value. However, I was only able to obtain this impression by scrolling through many of the products and creating an estimate in my head. I needed numbers and statistics to back up my impression. Hence, this project was born. 

### Goals
- Analyze clothing data from 3-5 e-commerce athlesiure websites to see if adding a "womens" label leads to a higher price for the same type of product compared to "mens". 
- Use natural language processing tools to associate product descriptions with prices.
- Use natural language processing to compare similar products that might have a different name. 
- Raise awareness about gender disparities in pricing, and provide tools to enable others to run their own analyses.

### Important note 
This project focuses on the _label assigned by the e-commerce company_ to the clothing. In this project, whenever I refer to "womens" clothing, I am referring specifically to the _label_ that the e-commerce company assigned to the clothing, not implying that this article of clothing may only be worn by those who identify as women. In reality, it is not required for women to shop only womens clothes and for men to shop only mens clothes. Furthermore, gender is complex and goes beyond simple "womens" and "mens" clothing labels. 

### Challenges faced 
Despite collecting an [absurd amount of data](https://www.businessnewsdaily.com/10625-businesses-collecting-data.html) from their customers and site visitors, e-commerce companies make it nearly impossible for a customer to collect even a fraction of their data back. Here were some of the obstacles I noticed when doing this project.
1. Varying HTML tags: In my experience, e-commerce companies will not use certain html tags like "price" and "product" for you to find their information in their site. They often give these HTML tags strange, complex names. This is probably to protect against bots, but also makes it more challenging to run a generalized search across all clothing sites.  
2. Gender separation: Not only do e-commerce sites separate sections by gender, but they also rarely give the same name to the same type of product. For example, mens shorts might be called "Ultra-sport shorts" whereas womens shorts are called "High-cut shorts". Both of these features make it more difficult to run a direct comparison across the two because one is not certain exactly what should be compared. (This is where natural language processing comes into play!)

### The argument of different products 
A common argument for pricing disparity between gender is that one clothing item may be of higher quality than another. For example, on a certain site, men's shorts are made of cotton and women's shorts are made of polyester, hence it is fair for a site to price men's shorts higher. Or, women's clothing requires a more complicated sort of cut than men's clothes, hence requiring  a higher price. My rebuttal to this argument is: that's not a choice by the consumer. When I am shopping on an e-commerce website, if my only option is a more expensive, cotton short, then I am still being required to pay a higher price for a certain product against my preferences.  

### Ethical webscraping 
I performed ethical webscraping during this project by usually not even using any type of crawler but rather, manually scrolling down to the webpage myself, downloading the html page to my computer, and then working from my local machine. When I did use a crawler, I made sure to only send one request before saving the data to my local machine and working from there. 

### Another important note 
All of the results found in this project are not implying that a clothing company deliberately makes clothing a higher price for one gender compared to another. These are the results from my own Natural Language Processing analysis and are merely a reflection of any data that I find.   

## Athlesiure companies 

### Choosing athlesiure brands 
To choose athlesiure brands, I looked at the largest clothing companies by market cap from [this website](https://companiesmarketcap.com/clothing/largest-clothing-companies-by-market-cap/). I ended up going with these three: 
1. Nike
2. Lululemon
3. Gymshark 

# Machine learning

### Initial statistical analysis 
I began with the gymshark data because the product descriptions were simpler to work with, with only ~30 unique words in the set of all product descriptions for womens and mens clothing, respectively. I created thirteen clothing categories (tanks, sweaters, etc) and placed items into categories based on which words were in the product description. Then, when comparing comparable categories between mens clothing and womens clothing, I found that indeed, womens clothing was priced higher in every category. 

Limitations of this approach: this approach is time-consuming and depends on my own interpretation of clothing categories, which can be subjective. 

### Converting language data into numerical data  
The product descriptions of Lululemon and Nike were a bit more complex, so I wanted to run some sort of algorithm that could not only predict the price based on clothing labels, but also tell me which words in the product description influenced the price in which way. Immediately, I thought of Lasso, which was the model I used in my internship over the summer. Lasso is great for feature selection because it gives you the coefficients of each feature which tell you how the coefficient influences the outcome. However, to use Lasso, I had to create a feature matrix with numerical input. I thought of the Bag of Words method, since order does not matter in this project but rather the word alone (we are trying to find the most influential one). So, I created a feature matrix as such: 
**rows**: each row corresponds to the "sample", i.e. the product description of one product. 
**columns** each column represented one word in the set of all words in the product descriptions. 
If the product description contained a word, then I put "1" in the column that represented that word. Otherwise, I put 0. 
Then, I added a "womens" column and placed "1" in all the product descriptions that came from the womens page. 
**output** the output column was just the price corresponding to that product. 

### Models 
As mentioned earlier, I ran Lasso because I liked its coefficients feature that tells you which feature is most influential and in which way. However, pricing models are rarely linear. I then learned about SHAP values, which can be paired with neural net models such as Random Forest Regressor and can tell you which features influenced the output variable in each iteration of the model. 

The rest is still in progress... 
