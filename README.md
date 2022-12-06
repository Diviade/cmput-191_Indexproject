# The Beats Index
# Creation of Index Table and Results: 
The index creation occured in 7 stages
## Stage 1: Getting the Data
To begin my index project, I scraped the "https://themacindex.com/variants/MHA22/beats-pro?currency=USD" site which displayed the price of beats headphones for 34 countries around the world. It included the list price, price with refunds as well as the price in the country's local currency. 

I then used my scrape_table function which converts result set created by the beautiful soup function to into the table format.

## Stage 2: Getting the Prices (CAD) - Cleaning Pt.1
In my first step of cleaning the data retrived from the web, I had to retrieve the price of beats in each country and convert that to Canadian dollars. However, this was easier said than done as the dataset I had to work with was far from analyzable. In the table created from the scraped data, the values all lumped together during the scraping process making the cleaning process much more difficult. This meant getting the price in Canadian dollars would be a journey 
- To start I had to get the price in US dollars (this was the currency my scraped data used) which were the first 3 numerical value in my lumped price Data. 
- In my analysis from visually looking at my values, I figured out that the data values with > 15 characters could all be grouped together and analyzed, which conversly meant data values < 15 characters could also be grouped together and analyzed.
- I then used the split method on my 2 groups of data and was able to obtain the prices in US dollars.
- Hoever, my job wasn't done as I had to convert to Canadian dollars. Thankfully this was the easy part as with a quick google search I was able to find the current exchange rate and used this to get my prices in Canadian dollars  

The prices were then added to begin building my beats index table

## Stage 3: Dealing with taxes - Cleaning Pt.2
The next step I took was retrieving and factoring in the tax vaues Into my calculations. 
- To begin I retrieve the tax data which was lumped with the country values. 
- Since not all the values in the column were formated, I first visually found similarilities which were the length of characters in the values
- I then once again used the split method to isolate the tax values.
- This worked for all the values except for switzerland, which I handled as it's own seperate case. 
- I had to return all the tax values as integers to be able to multiply them into the prices

After I was done with retrieving the tax values, the next step was multiplying them in. Thankfully this was one of the easier steps and I was able to do some simple arthethic in order to get the price of the products with the taxes factored in.

The tax prices were then added into my beats index table 

## Stage 4: Getting the Country Name - Cleaning Pt.3
This involved me cleaning the country name column. 
- This step involved me simply using split to find the country name which worked for most of the values.
- For the values that it did not work for (due to differing value lenght), I simply used string matching followed by split to get the country name 

I then added the cleaned country value to my beats index table

## Stage 5: Getting the currency code 
This was probably my hardest step. My first attempt had me try to retrieve the currency symbol from the price column of the original scraped table. However after a couple hours of futily trying (due to, too many difference value cases to account for), I decided the best strategy would be to import the currency code from the web and use string matching to retrieve the currency code for each country
- First I scraped the site "https://www.countries-ofthe-world.com/world-currencies.html" to retrive the result set which I then converted into a table using my scrape_table function.
- After sorting my table in alphabetically (done in a previous step), I used string matching to match the name of the country from my index table to the name of the country from my currency code table.
- This was followed by using the number index of the matched country to find that country's currency code. 
- For the countries which were not matched (due to the currency code table using a different name), I used the name used by the currency code table and the index of that value to find the currency code. 
- This procedure provided me with the currency code for each of my countries.

The currency code was then added to the beats index table

## Stage 6: Getting the local prices
After the lessons learned from the previous step of trying to retrieve the currency code, I decided to go with the safe route and once again used data scraping on the site "https://www.theglobaleconomy.com/rankings/Dollar_exchange_rate/" to get the country's exchange rate and convert my prices in CAD to the price in that country. 
- After creating my exchange rate table I once again used string matching to match the countries in my beats index table and got the exchnage ate value through this. 
- Worth noting is that the exhange rate I got from the table was the exchange rate as compared to USD.
- This meant I had to first divide the exchange rate in USD by the exchange rate from USD - CAD. 
- I was then able to multiply the exchange rate by the CAD price and get the local prices.

The local prices were then added to the beats index table

## Stage 7: Getting the price difference
This was an easy step as all I had to do was subtract the beats price for each country to the CAD price.

The difference was then added to the beats Index Table

I concluded this first part of my assignment by creating a bar graph with the price difference


# External Factor Analysis: 
The external factor I chose was the inflation rate per each country in my analysis. Exchange rate is {}

The analysis of the external factor occured in x stages

## Stage 1: Retriveing and applying the external factor values to the beats index table






