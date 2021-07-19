---
layout: page
title: Tools and Methods
---

Tips and steps to get data with the programming language R

---


* Add table of contents
{:toc}

<br>

## Using R and RStudio {#R}

![](https://images.g2crowd.com/uploads/attachment/file/68288/expirable-direct-uploads_2Fe8193163-4936-4785-bbb5-b760e9eb10b8_2FRStudio_IDE_1.1_Starbucks.png){:width="74%"}

<br>

__Recommended packages__
![](https://github.com/MPCA-air/air-methods/raw/master/images/tidy_packages.PNG){:width="53%"}


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

1. Open Access 
1. Create a new `Blank database`
    - Name it `donut_orders.accdb`
3. Select `Click to add` to add 2 new "_short text_" columns 
    - In the 1st column, right click `Field1` and choose "Rename field" and update name to `person` as the header 
          - Add 3 names of hungry people
    - In the 2nd column, rename `Field2` as `city` and add 3 cities
4. Add a 2nd table: Select `Create` from the top menu and click `Table`
    - Add a column named `person` and include at least one of the same names from the first table
          - Include a name of someone not in the first table
    - Add a 2nd column named `donut`
          - Record each person's donut order (eg. **Chocolate Glazed**)
5. Close the file and move to your R project folder

<br>

> ### Now we can read the data into R

```go
library(RODBC)

# Connect to Access file
## Move the Access file to your project folder
access_connect <- odbcConnectAccess2007("donut_orders.accdb")

# Load the two tables
people <- sqlFetch(access_connect, "Table1")

orders <- sqlFetch(access_connect, "Table2")

# Join the orders to the first table with `left_join()`
people_orders <- left_join(people, orders)

```

> ### Did it work? View the joined data.

```go
View(people_orders)
```

<br>

> ### Try using `full_join()`

```go
# Join orders with `full_join()`
people_orders_full <- full_join(people, orders)

View(people_orders_full)
```

> ### What's different?


