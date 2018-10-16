---
title: "Issues with Unpaywall in Economics"
author: "Lars Vilhuber"
date: "October 15, 2018"
output: 
  html_document: 
    keep_md: yes
    self_contained: no
---



## Unpaywall

[Unpaywall](https://unpaywall.org/) is "an open database of 21,403,865 free scholarly articles" which is construted by "[harvesting] Open Access content from over 50,000 publishers and repositories" ([Unpaywall](https://unpaywall.org/)).

We investigated the usefulness and accuracy of Unpaywall for use in economics, and found some issues. This is not a systematic review!

## RePEc
[RePEc (Research Papers in Economics)](http://repec.org/) is a "collaborative effort of hundreds of volunteers in 99 countries to enhance the dissemination of research in Economics and related sciences" ([RePEc](http://repec.org/)).
[IDEAS](https://ideas.repec.org/) is "the largest bibliographic database dedicated to Economics and available freely on the Internet. Based on RePEc, it indexes over 2,700,000 items of research, including over 2,500,000 that can be downloaded in full text" ([IDEAS](https://ideas.repec.org/) ).

## Our Approach

We picked a few DOIs where we know that reasonable data exists on Google Scholar as well as on [IDEAS/RePEc](https://ideas.repec.org/). We then investigated the available information on Unpaywall.


```r
# select DOIs
dois = c("10.1257/aer.102.3.589","10.1257/mac.20150245","10.1257/aer.p20171020")
unpaywall <- roadoi::oadoi_fetch(dois,email="lars@vilhuber.com")
refs <- rcrossref::cr_cn(dois,format = "text")
```

### Example 1: Hard

|Article:                                                                                                                                                                                              |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Abowd, J. M., & Vilhuber, L. (2012). Did the Housing Price Bubble Clobber Local Labor Market Job and Worker Flows When It Burst? American Economic Review, 102(3), 589–593. doi:10.1257/aer.102.3.589 |
This article in the AER's Papers and Proceedings is found on Unpaywall through CiteSeer:

pmh_id                             url                                                                     
---------------------------------  ------------------------------------------------------------------------
oai:CiteSeerX.psu:10.1.1.232.150   http://www.aeaweb.org/aea/2012conference/program/retrieve.php?pdfid=605 

which points to the conference program website. However, a Google search would also have found the full PDF at https://digitalcommons.ilr.cornell.edu/ldi/2/. As it turns out, the latter, because it is posted AFTER the conference, is actually a better version to use, but that may not be generally the case. 

### Example 2: RePEc has the partial answer

|Article:                                                                                                                                                                                                   |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Haltiwanger, J. C., Hyatt, H. R., Kahn, L. B., & McEntarfer, E. (2018). Cyclical Job Ladders by Firm Size and Firm Wage. American Economic Journal: Macroeconomics, 10(2), 52–85. doi:10.1257/mac.20150245 |
This article in the AER is listed on Unpaywall without an OA option:

doi                    is_oa   journal_is_oa 
---------------------  ------  --------------
10.1257/mac.20150245   FALSE   FALSE         

However, RePEc actually puts this article (https://ideas.repec.org/a/aea/aejmac/v10y2018i2p52-85.html) in relation to the NBER working paper version (https://ideas.repec.org/p/nbr/nberwo/23485.html):

|NBER WP:                                                                                                                           |
|:----------------------------------------------------------------------------------------------------------------------------------|
|Haltiwanger, J., Hyatt, H., Kahn, L., & McEntarfer, E. (2017). Cyclical Job Ladders by Firm Size and Firm Wage. doi:10.3386/w23485 |

Note that while the NBER is typically not OA, it can be if you are "a journalist" or "a resident of nearly any developing country or transition economy." Note that this is not coded anywhere.

### Example 3: RePEc has the entire answer

|Article:                                                                                                                                                                                                            |
|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Decker, R. A., Haltiwanger, J., Jarmin, R. S., & Miranda, J. (2017). Declining Dynamism, Allocative Efficiency, and the Productivity Slowdown. American Economic Review, 107(5), 322–326. doi:10.1257/aer.p20171020 |
This article in the AER is also listed on Unpaywall without an OA option:

doi                     is_oa   journal_is_oa 
----------------------  ------  --------------
10.1257/aer.p20171020   FALSE   FALSE         

However, RePEc actually puts this article (https://ideas.repec.org/a/aea/aecrev/v107y2017i5p322-26.html) in relation with not one, but TWO OA versions: to a [Board of Governors Discussion Paper](https://ideas.repec.org/p/fip/fedgfe/2017-19.html) and a [Center for Economic Studies Working Paper](https://ideas.repec.org/p/cen/wpaper/17-17.html):

![Screenshot of RePEc site](repec_example3.png)

both of which have no download restrictions, and the Board of Governors paper even has a DOI, and thus should be findable within the CrossRef metadata:


|Board of Governors Discussion Paper:                                                                                                                                                                                          |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Decker, R. A., Haltiwanger, J., Jarmin, R. S., … Miranda, J. (2017). Declining Dynamism, Allocative Efficiency, and the Productivity Slowdown. Finance and Economics Discussion Series, 2017(019). doi:10.17016/feds.2017.019 |
However, both are findable, and put in relationship to the AER article, within the RePEc metadata.

## RePEc again
How to obtain RePEc metadata is available at https://ideas.repec.org/getdata.html . 


