# DATA 512: Human Centered Data Science

## Homework Assignment 2: Considering Bias in Data

## Goal

The goal of this assignment is to explore the concept of bias in data using Wikipedia articles. This assignment will consider articles on political figures from different countries. For this assignment, you will combine a dataset of Wikipedia articles with a dataset of country populations, and use a machine learning service called ORES to estimate the quality of each article.

You are expected to perform an analysis of how the coverage of politicians on Wikipedia and the quality of articles about politicians varies among countries. Your analysis will consist of a series of tables that show:

1. The countries with the greatest and least coverage of politicians on Wikipedia compared to their population.
2. The countries with the highest and lowest proportion of high quality articles about politicians.
3. A ranking of geographic regions by articles-per-person and proportion of high quality articles.

## Source data licenses

The source data is distributed under the Creative [Commons Attribution-ShareAlike 3.0 Unported License](https://creativecommons.org/licenses/by-sa/3.0/) which states:

1. You are free to:
   - **Share** — copy and redistribute the material in any medium or format
   - **Adapt** — remix, transform, and build upon the material for any purpose, even commercially
2. Under the following terms:
   - **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made. You may do so in any reasonable manner, but not in any way that suggests the licensor endorses you or your use
   - **ShareAlike** - If you remix, transform, or build upon the material, you must distribute your contributions under the same license as the original
3. Additionally, you may not apply legal terms or technological measures that legally restrict others from doing anything the license permits.

## References to API

[MediaWiki API Documentation](https://www.mediawiki.org/wiki/API:Info)
[ORES API Documentation](https://www.mediawiki.org/wiki/ORES)

## Outputs

The `HW2.ipynb` notebook documents the data acquisition and analysis procedure for this assignment. The following two files are outputs produced:

- `wp_countries-no_match.txt`: List of countries that have either missing article information or missing population information (check step 3 of notebook).
- `wp_politicians_by_country.csv`: A CSV file that contains the stored results of fetching data from the 2 APIs listed above. The table below describes the columns

   |Name|Data type| Description|
   |---|---|---|
   |`country`|`string`|Name of country politician is associated with|
   |`region`|`string`|Region that the country belongs to|
   |`population`|`float`|Population (in millions)|
   |`article_title`|`string`|Title of politician's Wikipedia article|
   |`revision_id`|`int`|Latest revision ID for the article fetched from the MediaWiki API|
   |`article_quality`|`string`|Predicted article quality by ORES|

## Known Issues and Special Considerations

1. There is some amount of data duplication - Politicians are listed under multiple countries
2. There are some articles for which the data could not be fetched. These incidents are logged in the `errors.log` file
3. The data will differ slightly based on the time at which the code is run. This assignment ran the data pull on **October 11, 2022 at 4:23 PM** ([link to commit](https://github.com/hbaghar/data-512-homework_2/commit/de65c1fdc375e7c85423875619040042d07f6ca3))
4. Out of the countries that did not have a match, one of them is "Korean"

## Research Implications

1. What biases did you expect to find in the data (before you started working with it), and why?

   I expected to find biases that indicated that article coverage and quality would be lower from developing and underdeveloped countries. This is because the proportion of population from these countries that would have Wikipedia contributors would likely be less due to lower rates of internet access and literacy among the population.

2. What (potential) sources of bias did you discover in the course of your data processing and analysis?

   This analysis suffers from the following potential sources of bias:
   1. *Selection bias:* On looking at the list of countries with missing data many developed countries are not a part of the dataset that was formed by scraping Wikipedia such as US, Canada, UK and Australia. This means that we havev not accounted for a potentially huge part of Wikipedia.
   2. *Lack of coverage of developing countries:*
      - Section 5.2 shows that per capita coverage of politicians is very poor for a lot of developing countries. While it is no surprise that India and China are in the top 10 (since they have much larger populations than other countries) countries like Mexico, Romania, Sri Lanka, Vietnam, Egypt and Ethiopia are clearly underrepresented
      - When viewed by region in section 5.5, we see that there is a clear divide with European regions having higher coverage than Asian and African regions
      - In section 5.4 when we see coverage of high quality articles based on ORES predictions, most of the countries that score 0 are developing or underdeveloped. If we assume that the model is fair and makes these predictions only on article structure and not based on country of origin, it shows us that there is under-representation of high-quality articles from developing and underdeveloped countries on Wikipedia. This finding is consistent with our initial hypothesis in point 1

3. What might your results suggest about (English) Wikipedia as a data source?

   As discussed above in the third point, Wikipedia does not seem to have many high-quality articles or great per-capita coverage for many developing and underdeveloped countries based on this sample of articles we have analyzed

4. What might your results suggest about the internet and global society in general?

   It seems to reinforce the idea that the internet is dominated by the West, which likely has more contributors per capita and access to resources that facilitate better participation on forums like Wikipedia

5. How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?

   More data is more often than not better. A researcher can add articles from the countries that are listed as missing in the `wp_countries-no_match.txt` file to improve the representation of countries in the sample. We can also try to extend this analysis to different categories of articles by country and region to see if these biases are consistent. Additionally, it might also be valuable to study the breakdown of Wikipedia contributors by country if possible. Knowing this can also help us understand if there is a possibility that there are biases embedded within the articles themselves. If more contributors are from the West, popular narratives from the West are likely to be dominant voices on the internet.
