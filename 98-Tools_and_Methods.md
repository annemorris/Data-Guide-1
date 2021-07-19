---
layout: page
title: Tools and Methods
---

Tips and steps to get data with the programming language R

---

![](https://images.g2crowd.com/uploads/attachment/file/68288/expirable-direct-uploads_2Fe8193163-4936-4785-bbb5-b760e9eb10b8_2FRStudio_IDE_1.1_Starbucks.png){:width="70%"}


* Add table of contents
{:toc}

<br>

## Using R and RStudio {#R}

![](https://github.com/MPCA-air/air-methods/raw/master/images/tidy_packages.PNG){:width="60%"}

<br>


__Recommended packages__


> Loading data

`readr`     Load data from text files: tab, comma, and other delimited files

`readxl`    Load data from Excel

`RODBC`     Load data from Access and Oracle Dbs such as DELTA / TEMPO

`RPostgresSQL`, `RMySQL`, and `RSQLite`  Connect to SQL databases

`rvest`     Read and scrape content from webpages

`pdftools`  Read PDF documents

`googledrive` Read and write files to your Google Drive

`foreign`   Load data from Minitab and Systat

`R.matlab`  Load data from Matlab

`haven`     Load data from SAS, SPSS, and Stata

<br>


## Microsoft Access {#access}

1. Create a new Access file
2. Add a table 
    - In the 1st column put `name` as the header and add 3 names
    - In the 2nd column put `city` as the header and add 3 cities
3. Add a 2nd table
    - In the 1st column put `name` as the header and include at least one of the same names from the first table
    - Add someone not included in the first table
    - In the 2nd column put `order` and add their donut order
4. Save the file as `donut_orders`

<br>

> Now we can read the data into R:

``` .go
library(RODBC)

# Load the two tables
people <- odbc("donut_orders.accdb", "table_1")

orders <- odbc("donut_orders.accdb", "table_2")

# Join the orders to the first table with `left_join()`
people_orders <- left_join(people, orders)

```
