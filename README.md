# IPFS-Arxiv
IPFS-Arxiv is hosted via the interplanetary file system protocol. It is a decentralized collection of the newest 1000 machine learning papers from arxiv. Since the site isn't dynamic, I have to manually upload the new papers every now and then. We will see how long I can keep this up ;)  
Important: All papers are actually uploaded and stored in a decentralized fashion!

https://gateway.ipfs.io/ipfs/QmVxheJqLSqJ4VTw2LYwe3UbDYLYhq1RWb3ie43yGYTr8y (ipns link follows)

# Siraj - IPFS challenge
I have created this site because of two reasons, my primary goal was to create something for IPFS because I think it is amazing and may very well be the future of the internet. And the second reason why I created this particular project at this time is Sirajes IPFS challenge. So Siraj, this is my official submission. (https://www.youtube.com/watch?v=BA2rHlbB5i0)


# Description
The project consists of two parts. The first part is a webscraper written in python. It requests machine learning paper search results via the arxiv API. And the second one is the website itself, it reads in the json index generated by the webscraper and displays the results. It also links to the papers contained in the "pdfs" folder.

# Webscraper
The webscraper uses the arxiv API to send a search query in this format:<br/>
```
http://export.arxiv.org/api/query?search_query=[query]&start=[start_index]&max_results=[result_count]
```
the query is in the machine learning case "machine%20learning", start_index is a zero based offset index from which paper to start and result_count the amount of results that should be returned.

API results are in xml format so the next step is to parse them and add the new titles,ids and summaries (these is all the tags we are using) to the index.json file. There we save all the information but not without checking for doubles so no redundant entries are being written to the index after a potential restart. Then all pdfs of the non redundant entries are downloaded and saved to the "pdfs/" folder.
PDF request url:<br/>
```
http://arxiv.org/pdf/[paper_id].pdf
```
Yah, paper_id is just the id of the paper!
All the code is in arxiv_scraper.py

# Website
The website reads the index.json file generated by the webscraper and creates the website entries from it. The site consists of index.html the main html file, ipfs_arxiv.js creates the entries from json and handles next/prev page management, jquery is completely pointless and pdfs/ contains all the machine learning paper pdfs.
On a side note because of chromes cross-domain protection security I couldn't load the index.json directly so I just put a "var index_json = [index.json content];" around it and added it as a javascript.
<br/><br/>
<img src='images/ipfs_arxiv_website.jpg'/>
