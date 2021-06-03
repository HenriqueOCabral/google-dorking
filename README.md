# Google dorking

## What is dorking?

1- Roleplaying<br/>
2- Any activity generally classified as uncool or dorky<br/>
3- Engaging in any activity for which one might be considered a dork<br/>


## Top 11 Advanced Google Search Commands you should consider start using

* #### “search term” <br/>
Force an exact-match search. Use this to refine results for ambiguous searches, or to exclude synonyms when searching for single words. <br/>

* #### OR <br/>
Search for X or Y. This will return results related to X or Y, or both. Note: The pipe (|) operator can also be used in place of “OR."<br/>

- #### *  <br/>
Acts as a wildcard and will match any word or phrase.<br/>

* #### cache: <br/>
Returns the most recent cached version of a web page (providing the page is indexed, of course). Example: cache:airbnb.com<br/>

* #### filetype: <br/>
Restrict results to those of a certain filetype. E.g., PDF, DOCX, TXT, PPT, etc. Note: The “ext:” operator can also be used—the results are identical.<br/>

* #### site: <br/>
Limit results to those from a specific website. Example: site:airbnb.com.<br/>

* #### inurl | allinurl <br/>
Find pages with a certain word (or words) in the URL. "allinurl" similar to “inurl,” but only results containing all of the specified words in the URL will be returned.  Example: inurl:.pt to especify url from a target country.<br/>

* #### intext: | allintext: <br/>
Find pages containing a certain word (or words) somewhere in the content. "allintext" similar to “intext,” but only results containing all of the specified words somewhere on the page will be returned. Example: intext:children <br/>
 
* #### intitle: | allintitle: <br/>
Find pages with a certain word (or words) in the title. "allintitle" similar to “intitle,” but only results containing all of the specified words in the title tag will be returned. Example: intitle:corona<br/>

* #### inanchor: | allinanchor: <br/>
Find pages that are being linked to with specific anchor text. "allinanchor" similar to “inanchor,” but only results containing all of the specified words in the inbound anchor text will be returned. Example: allinanchor:javascript<br/>

* #### `( )` <br/>
Group multiple terms or search operators to control how the search is executed.<br/>


## How to Google dork - Lazy steps

* Define a target or a vector (domain, sub-domains, specific words, logins, passwords, applications, web technologies etc)
* Build a combo of advanced google search commands to optimize your research
* Gather all the data that fit's your dork
* Repeat all these steps if necessary



## Lazy Steps Example :

* Vector: `cake recipes`
* Combo: `inurl:br filetype:PDF allintext:cake`
* Gather info
* Repeat ?! Nah.

## How am I suposed to use the Advanced Google Search Commands with ease ?!

* You don't have to...
* There's a tool that automates all the process with a couple of bash commands
* Pagodo.py can make your research very easy.
* If you want to go deeper.... 
* Check out their repo `https://github.com/opsdisk/pagodo` to find more advanced stuff 👻👻👻👻

## How to use pagodo.py 
  🐍🐍🐍🐍🐍🐍🐍
## Installing pagodo

```bash
git clone https://github.com/opsdisk/pagodo.git
cd pagodo
virtualenv -p python3 .venv  # If using a virtual environment.
source .venv/bin/activate  # If using a virtual environment.
pip install -r requirements.txt
```

## ghdb_scraper.py

To start off, `pagodo.py` needs a list of all the current Google dorks.  A datetimestamped file with the Google dorks
and the indididual dork category dorks are also provided in the repo.  Fortunately, the entire database can be pulled
back with 1 GET request using `ghdb_scraper.py`.  You can dump all dorks to a file, the individual dork categories to
separate dork files, or the entire json blob if you want more contextual data about the dork.

##### In this example We are going to retrieve all dorks and write them to individual categories:

```bash
python3 ghdb_scraper.py -i
```

Dork categories:

```none
categories = {
    1: "Footholds",
    2: "File Containing Usernames",
    3: "Sensitives Directories",
    4: "Web Server Detection",
    5: "Vulnerable Files",
    6: "Vulnerable Servers",
    7: "Error Messages",
    8: "File Containing Juicy Info",
    9: "File Containing Passwords",
    10: "Sensitive Online Shopping Info",
    11: "Network or Vulnerability Data",
    12: "Pages Containing Login Portals",
    13: "Various Online devices",
    14: "Advisories and Vulnerabilities",
}
```

## pagodo.py

Now that a file with the most recent Google dorks exists, it can be fed into `pagodo.py` using the `-g` switch to start
collecting potentially vulnerable public applications. In this example I've selected the category `dorks/error_messages.dorks`

`-d` command can be used to specify a domain

Performing ~4600 search requests to Google as fast as possible will simply not work.  Google will rightfully detect it
as a bot and block your IP for a set period of time.  In order to make the search queries appear more human, a couple of
enhancements have been made.  A pull request was made and accepted by the maintainer of the Python `google` module to
allow for User-Agent randomization in the Google search queries.  This feature is available in
[1.9.3](https://pypi.python.org/pypi/google) and allows you to randomize the different user agents used for each search.
This emulates the different browsers used in a large corporate environment.

The second enhancement focuses on randomizing the time between search queries.  A minimum delay is specified using the
`-e` option and a jitter factor is used to add time on to the minimum delay number. A list of 50 jitter times is created
and one is randomly appended to the minimum delay time for each Google dork search.

## Let's do the example

* Note that it could take a few days (3 on average) to run so be sure you have the time.

```bash
python3 pagodo.py -d airbnb.com -g dorks/error_messages.dorks -l 50 -s -e 35.0 -j 1.1
```
* At the end of the search pagodo will save a .txt file in its own directory named with `pagodo_results_*****.txt`
