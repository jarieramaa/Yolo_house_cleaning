# Properties data from ImmoWeb

## Files

There are three files for data: 

1. housing_data.df    -- Contains a Pandas DataFrame, shape : (14625, 112)
2. housing_data.csv.  -- Same data in CSV format
3. investigate_file_with_panda.py

You can find files 1 and 2 from './data' -folder. File #3 can be found under 'scraping code' -folder.

The file 'housing_data.df' contains a Pandas DataFrame in a binary folder and it can be read with the module "investigate_file_with_panda.py". It's just an example how you can have access to this binary file. 

I didn't drop any rows or columns. You can decide what columns you want to use and what rows should be dropped. It easy to do in Pandas DataFrame anyway.

## Fresh
I like my coffee and data fresh. I recreated the data this weekend. Compared to previous version, I added 'Price HTML' column (it will be explained below). 

Previously we had some 'null ads', because the ad was removed during the runs (Selenium and Beautiful Soup). This time I ran both programs during the same day. Both Selenium and Beautiful Soup worked without any errors. 

## Properties

### ImmoWeb ID and url
The url to ad and 'ImmoWeb ID' are included to every row. Please, use these when you see something susbicious.

### The property price information
There are three columns for price information:
1. Price 
2. Price_SR
3. Price HTML

The reason for several price-columns is that the price information in the ImmoWeb site is free text field and it can contain almost anything. 
Sometimes there is a one price. Other times there are two different prices, hence 'Price_sr'. Please, see the example below. There are even few (4) properties without any price information. 

'Price HTML' is a small slice of html information that contains the price information. You may use this field, if you want to create more specific calculation for the price. 

![Sometimes there is a price range](./data/pictures/price_example_1.png)
### 1 square meter terrace or garden
Tim raised a question, because rather many terrace/garden had 1square meter area. That is how the are is reported in the ImmoWeb site. It's not a scraping error. Please, check the link to the ad. I guess that they didn't have the actual information when creating the ad. 
![1 square meter terrace and garden](./data/pictures/garden.png)

## Duplicates
With Duplicates it't not straight forward. You can easily run : *'drop_duplicates(subset=["Immoweb ID"])'* and get clean data, but you have to consider why there are duplicates in the first place. The reason is that the same house or apartment might be listed to several sub property types. Please, see the picture below:

![Same apartment has different sub-types](./data/pictures/duplicates.png)
Which one of these is correct, or are they all correct?

[PENTHOUSE](https://www.immoweb.be/en/classified/new-real-estate-project-apartments/for-sale/hasselt/3500/6981865?searchId=61feb44398555)

[GROUND_FLOOR](https://www.immoweb.be/en/classified/new-real-estate-project-apartments/for-sale/hasselt/3500/6981865?searchId=61ff66ba7bbf3)

[FLAT_STUDIO](https://www.immoweb.be/en/classified/new-real-estate-project-apartments/for-sale/hasselt/3500/6981865?searchId=61feb551241a4)

As you can see they are all correct. However, all of these would be filtered out for different reasons (variable price) and they are not valid samples when considering ML modeling. 

This is the reason, I didn't filter out duplicates. Perhaps it's better to filter the data another way first and check what are the remaining duplicates (if any).






 




