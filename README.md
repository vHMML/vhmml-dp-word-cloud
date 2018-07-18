# Generate a Word Cloud with vHMML Data

Using the vHMML Data Portal, you can use Reading Room metadata to generate word clouds to create interesting representations of specific collections.

One example, would be to search the Data Portal for only items with the language of Syriac

After exporting the Full Search Data, use SQLIFY to isolate the Title Native Script (The title of an item in the original non-Roman language) and Language ID. 

Looking at the data, because the language is at the part level, we may have manuscripts with multiple languages. However, we would like to isolate the Syriac ones. After loading our data into a Google Sheet, we can use some formulas to trim our data. 

In column A, we have our data. 

In column B, we identify whether there is an 11 in our data (the language id for Syriac) - =if(find("11",A6,1)>0,1,0)

In column C, we find the position or our “,” or comma - =find(",",A6,1)

In column D, we isolate the text of the title native script - =left(A6,C6-1)

In column E, we eliminate rows without data - =if(D6="NULL","",D6)

In column F, we finalize our data - =if(B6=1,E6,"")

With the data in column F, we can feed it to a Word Cloud creator like Jason Davies’ Word Cloud Generator (https://www.jasondavies.com/wordcloud/). Here is our generated word cloud and how it was generated:

We can also use D3.js to create a word cloud on your own webserver. See LINK HERE for the full example (Note, you need a webserver for the example to work). This is based on Varun Agrawal’s Block (http://bl.ocks.org/varunagrawal/e4598d856778fc6733cc03235f6af801). Here is the generated word cloud:
