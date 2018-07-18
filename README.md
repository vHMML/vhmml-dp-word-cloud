# Generate a Word Cloud with vHMML Data

Using the vHMML Data Portal, you can use Reading Room metadata to generate word clouds to create interesting representations of specific collections.

One example, would be to search the Data Portal for only items with the language of Syriac

![alt text](https://github.com/vHMML/vhmml-dp-word-cloud/blob/master/img/wc_language_1.PNG "filter language")

After exporting the Full Search Data, we can use SQLIFY to isolate the Title Native Script (The title of an item in the original non-Roman language) and Language ID. 

![alt text](https://github.com/vHMML/vhmml-dp-word-cloud/blob/master/img/wc_sqyilfy_2.PNG "SQLIFY")

Looking at the data, because the language is at the part level, we may have manuscripts with multiple languages. However, we would like to isolate just the Syriac ones. After loading our data into a Google Sheet, we can use formulas to clean our data. 

![alt text](https://github.com/vHMML/vhmml-dp-word-cloud/blob/master/img/wc_gs_3.PNG "Google Sheet")

In column A, we have our data. 

In column B, we identify whether there is an "11" in our data (the language id for Syriac): ```=if(find("11",A6,1)>0,1,0)```

In column C, we find the position of the “,” (comma): ```=find(",",A6,1)```

In column D, we isolate the text of the title native script: ```=left(A6,C6-1)```

In column E, we eliminate rows without data: ```=if(D6="NULL","",D6)```

In column F, we finalize our data: ```=if(B6=1,E6,"")```

With the data in column F, we can create a word cloud using Jason Davies’ Word Cloud Generator (https://www.jasondavies.com/wordcloud/):

![alt text](https://github.com/vHMML/vhmml-dp-word-cloud/blob/master/img/wc_jd_wcg_5.PNG "Word Cloud Generator")

# D3.js and Word Clouds

We can also use D3.js to create a word cloud on your own webserver. See [the full example](https://github.com/vHMML/vhmml-dp-word-cloud/tree/master/example) (Note, you need a webserver for the example to work). This is based on Varun Agrawal’s Block (http://bl.ocks.org/varunagrawal/e4598d856778fc6733cc03235f6af801). Here is the generated word cloud:

![alt text](https://github.com/vHMML/vhmml-dp-word-cloud/blob/master/img/wordcloud_syriac_localhost.PNG "D3.js Word Cloud")

