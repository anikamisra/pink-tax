### Main question: 
How can we use multimodal Machine Learing and Artificial Intelligence to find a generalized approach to **quantifying** gender-based price discrimination in clothing companies?

**Skills used**: 
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
