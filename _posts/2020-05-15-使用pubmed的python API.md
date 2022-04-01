---
layout: post
title: "使用pubmed的python API"
date:   2020-05-15
tags: [pubmed]
comments: true
toc: true
author: Songbiao Zhu
---

如何使用python API 来自动化获取pubmed的信息呢？



<!-- more -->

[January 12, 2015](https://marcobonzanini.com/2015/01/12/searching-pubmed-with-python/)[Marco](https://marcobonzanini.com/author/marcobonzanini/)

[source](https://marcobonzanini.com/2015/01/12/searching-pubmed-with-python/)

[PubMed](http://www.ncbi.nlm.nih.gov/pubmed) is a search engine accessing millions of biomedical citations. Users can freely search for biomedical references. For some articles, the access to the full text paper is also open.

This post describes how you can programmatically search the PubMed database with Python, in order to integrate searching or browsing capabilities into your Python application.

There are two main options to consider:

- Accessing the database via their public API
- Using a package that does the above for you, e.g. Biopython

**The Entrez Database a.k.a. the PubMed API**

The PubMed API is called the [Entrez Database](http://www.ncbi.nlm.nih.gov/books/NBK25501/). It’s a web service freely accessible, although there are some guidelines to follow (at the moment of this writing, they recommend not to post more than three requests per second).

There are in total 8 different functions, or e-utilities, which access the database in different ways. Most of the utilities will return XML data, although some of them have the option to return a more convenient JSON format.

In particular, the search API is available at the following URL:

```python
http://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi
```

If we want to search for the term *fever*, the URL we need is for example:

```python
http://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&retmode=json&retmax=20&sort=relevance&term=fever
```

The query string parameters used in this example:

- db=pubmed, to narrow the search down to the pubmed DB only
- retmode=json, to have a JSON string in response and not an XML
- retmax=20, to obtain 20 results
- sort=relevance, the results are sorted by relevance and not by added date which is the default ranking option on pubmed
- term=[your query], the URL-encoded query

This search session will provide a number of PubMed IDs (probably 20) corresponding to the top citations which match our query.

In order to get some more details about these citations, we can use the efetch utility, which takes one or more citation ID as input. At the moment, the efetch utility does not return JSON, so XML is the only option to consider.

Given a list of citation IDs, the fetch operation can be built as follows

```python
http://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&retmode=xml&id=ID1,ID2,...
```

At this point, the response will be an XML to handle with e.g. minidom or other XML library. Please notice that we can query the efetch utility for multiple documents, simply by separating them with a comma.

Overall, it’s relatively easy to create the appropriate request using libraries like urllib.request or, better, [requests](http://docs.python-requests.org/en/latest/). The response can be parsed with the json module, or minidom in case of XML.

An even more convenient way to do the job is to use an existing library that does what we need for us. A good example is [Biopython](http://biopython.org/), a comprehensive package for biological computation in Python.

**Searching PubMed with Biopython**

You can install the Biopython package with pip:

```
sudo pip install biopython
```

The only component we need for searching PubMed is Entrez, which we can import with:

```
from Bio import Entrez
```

We can define a function for performing the search, e.g.

```python
def search(query):
    Entrez.email = 'your.email@example.com'
    handle = Entrez.esearch(db='pubmed', 
                            sort='relevance', 
                            retmax='20',
                            retmode='xml', 
                            term=query)
    results = Entrez.read(handle)
    return results
```

The list of citation IDs will be available as results[‘IdList’].

The next step is to fetch the details for all the retrieved articles via the efetch utility:

```python
def fetch_details(id_list):
    ids = ','.join(id_list)
    Entrez.email = 'your.email@example.com'
    handle = Entrez.efetch(db='pubmed',
                           retmode='xml',
                           id=ids)
    results = Entrez.read(handle)
    return results
```

A full example of search over the term *fever*:

```python
if __name__ == '__main__':
    results = search('fever')
    id_list = results['IdList']
    papers = fetch_details(id_list)
    for i, paper in enumerate(papers):
        print("%d) %s" % (i+1, paper['MedlineCitation']['Article']['ArticleTitle']))
    # Pretty print the first paper in full to observe its structure
    #import json
    #print(json.dumps(papers[0], indent=2, separators=(',', ':')))
```

Notice that the structure of the MedlineCitation dictionaries can get
really convoluted, so we can get familiar with it by doing some pretty-printing.

The reason for declaring your email address is to allow the NCBI to
contact you before blocking your IP, in case you’re violating the guidelines.

The Gist of the full example:

https://gist.github.com/bonzanini/5a4c39e4c02502a8451d

