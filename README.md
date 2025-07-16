### Main question: 
How can we use multimodal Machine Learing and Artificial Intelligence to find a generalized approach to **quantifying** gender-based price discrimination in clothing companies?
**Skills**: 
- multimodal ML
- computer vision
- NLP
- early & fusion
- webscraping 

# Summary 
My analysis was done on **gymshark**. (The other companies are still in progress.) 
>`gymshark`
### Manual analysis 
`gymshark_scraper.ipynb`
- scraped the original data (contact me for code)
- result: created two information files for mens and womens clothing, respectively: `m_df_scraped_jul_14.csv` and `w_df_scraped_jul_14.csv`

`gymshark_data_cleaning.ipynb`
- performed exploratory data analysis and manual price comparison to confirm my hunch about women's items being priced higher than men's.
- result: 
<img src="https://github.com/user-attachments/assets/49cab888-2ad5-4704-8a46-8a791cdfbd3b" alt="price_comparison_final" width="500"/>

### Automated approaches  
`gymshark_linear_regression_and_RFR.ipynb` 
- ussed lasso regression and random forest regression to automate the above manual results
- "input" was the product description, "output" was the price
- however, this attempt was unsuccessful. the results showed that "womens" clothing label had no effect on price (which contradicts the above result!) 

`gymshark_NLP_clustering.ipynb` 
- shifted my focus to *categorization* rather than direct pricing prediction analysis (to mitigate simpson's paradox) 
- used BERTopic to create clothing categories automatically
- result: clothing categories were odd and didn't make much sense

### Automated multimodal approach 
>`gymshark_with_images` 

`data_scraping.ipynb`
- scraped the images for gymshark (contact me for code)

`clustering.ipynb`
- experimented with early fusion and late fusion k-means clustering to create clothing categories (based on image AND product description)
- cropped out model faces to reduce gender bias in clustering model. example:
<img src="https://github.com/user-attachments/assets/b746705c-171f-4cf4-a1d9-f0c20af79fb5" alt="price_comparison_final" width="200"/>

- **result**: early fusion had the best result with successfully creating cohesive clothing categories irrespective of gender, for hoodies/shirts, bras, pants, outerwear, socks:

<img width="333" alt="cluster_sample_results_1" src="https://github.com/user-attachments/assets/1e0990a3-8902-4180-bb58-6f88948b6a21" />
<img width="333" alt="cluster_sample_results_2" src="https://github.com/user-attachments/assets/714bacc7-46a8-4d6b-9578-cb2125970f56" />




<br>Successfully created an automated approach in quantifying gender-based price discrimination: 
<img width="712" alt="final_results_clean_fixed" src="https://github.com/user-attachments/assets/b9568aac-6a91-408a-81cc-346d0e5220a8" />

### Limitations and discussion 
- My final result isn't as clean as the manual analysis, especially for categories like the hoodies and shirts. However, the clothing categories still make sense and enable us to automate a pricing comparison across gender.
- Cropping out  model faces in photos might not be enough to reduce gender bias since men and women tend to have different physiques as well
- The dataset containing the prices was a different dataset than the one containing all the products analyzed (this was due to issues scraping the pricing data). As a result, some of the products might have been omitted when combining datasets - as we can see with the "mens socks" category.
- There aren't quantitative benchmarks to determine what creates a "cohesive" clothing category, and hence what makes one clothing category organization "better" than another. I had to simply go off of what "looked" the most cohesive. 
- Multimodal approach still led to significantly better results than the other approaches. This is because when I was creating the manual analysis, I was relying heavily on visual data to categorize items.    

# More information  
### Background 
Gender-based price discrimination is [illegal in California](https://oag.ca.gov/ab1287#:~:text=AB%201287%2C%20California's%20Pink%20Tax,girls%20typically%20having%20higher%20prices), but there are still many loopholes that companies may use to charge a higher price to a specific demographic. For example: 
1. Different names: Calling women's sweatpants "joggers" and men's sweatpants "sweatpants", so that they are technically not the "same product" and the company can charge more for "joggers" than "sweatpants".  
2. Material: Making the women's shirts out of cotton and the men's shirt out of polyester to justify a 70% higher price for the women's shirts, even though cotton may only be 20% more expensive than polyester.
3. Style: Making women's shirts a "cropped style" to justify more labor and therefore a higher price, even though cropping the women's shirts might actually make them cheaper to produce since less fabric is used.   

It is not always women who are negatively affected by this - these tools can be used to target any specific demographic, including men.

### Motivations: 
When consumers are comparing womens products versus mens products, they might get a "general vibe" that one demographic's clothing is priced slightly higher than the other. However, direct pricing comparisons are difficult to make due to the factors listed above. Furthermore, oftentimes, consumers don't even think to compare product demographics because they are conveniently separated on every web page ("womens clothing" pages are almost always separated from "mens clothing" pages in the same company). 

### Main question: 
**<mark style = "background: yellow">How can we use Machine Learing and Artificial Intelligence to find a generalized approach to **quantifying** gender-based price discrimination in clothing companies?</mark>** 

**Important note:** This project focuses on the _label assigned by the e-commerce company_ to the clothing. In this project, whenever I refer to "womens" clothing, I am referring specifically to the _label_ that the e-commerce company assigned to the clothing, not implying that this article of clothing may only be worn by those who identify as women. In reality, it is not required for women to shop only womens clothes and for men to shop only mens clothes. Furthermore, gender is complex and goes beyond simple "womens" and "mens" clothing labels. 

### Challenges faced 
Despite collecting an [absurd amount of data](https://www.businessnewsdaily.com/10625-businesses-collecting-data.html) from their customers and site visitors, e-commerce companies make it nearly impossible for a customer to collect even a fraction of their data back. Here were some of the obstacles I noticed when doing this project.
1. Varying HTML tags: In my experience, e-commerce companies will not use certain html tags like "price" and "product" for you to find their information in their site. They often give these HTML tags strange, complex names. This is probably to protect against bots, but also makes it more challenging to run a generalized search across all clothing sites.  
2. Gender separation: Not only do e-commerce sites separate sections by gender, but they also rarely give the same name to the same type of product. For example, mens shorts might be called "Ultra-sport shorts" whereas womens shorts are called "High-cut shorts". Both of these features make it more difficult to run a direct comparison across the two because one is not certain exactly what should be compared. 

### Ethical webscraping 
I performed ethical webscraping during this project by usually not even using any type of crawler but rather, manually scrolling down to the webpage myself, downloading the html page to my computer, and then working from my local machine. When I did use a crawler, I made sure to only send one request before saving the data to my local machine and working from there. 

### Another important note 
All of the results found in this project are not implying that a clothing company deliberately makes clothing a higher price for one gender compared to another. These are the results from my own Natural Language Processing analysis and are merely a reflection of any data that I find.   

Please contact me if you have any questions! Thanks for reading. 
