
# CVPR papers pretty html

This is a set of scripts for creating nice preview page (see here: http://www.colinlea.com/guides/cvpr2013 ) for all papers published at CVPR. I hope these scripts can be useful to others to create similar pages for other conferences. They show how one can manipulate PDFs, extract image thumbnails, analyze word frequencies, do AJAX requests to load abstracts, etc.

#### Installation

0. Clone this repository `git clone https://github.com/colincsl/cvpr2013papers.git`

1. Make sure you have the following libraries [System: ghostscript, imagemagick; Python: httplib2, beautifulsoup]

On OSX:
brew install ghostscript
brew install imagemagick
pip install httplib2
pip install beautifulsoup


2. Download CVPR papers using download_cvpr.py $year. The papers are download to papers{year}/

3. Run `pdftowordcloud.py` (to generate top words for each paper. Output saved in topwords.p as pickle)

4. Run `pdftothumbs.py` (to generate tiny thumbnails for all papers. Outputs saved in thumbs/ folder)

5. Run `scrape_cvpr2013.py` (to generate paperid, title, authors list by scraping NIPS .html page)

6. Run `makecorpus.py` (to create allpapers_{year}.txt file that has all papers one per row)

7. Run `python lda.py -f allpapers.txt -k 7 --alpha=0.5 --beta=0.5 -i 100` . This will generate a pickle file called `ldaphi.p` that contains the LDA word distribution matrix. Thanks to this [nice LDA code](https://github.com/shuyo/iir/blob/master/lda/lda.py) by shuyo! It requires nltk library and numpy. In this example we are using 7 categories. You would need to change the `website_template.html` file a bit if you wanted to try different number of categories.

8. Finally, run `generatenicelda.py` (to create the nipsnice.html page)

Optional(for visualized LDA result). 

9.  Run genLDA.py $year ${number of topic} to make specific LDA result. This outputs dictionary(*.dict), corpus(*.mm) and model(*.model) files.(gensim is required)

10. Run genpapers.py $year ${number of topic} to make visualized LDA model (pyLDAvis is required). an HTML file is output.

#### Licence

WTFPL licence
