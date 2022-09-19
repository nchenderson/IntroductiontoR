# (PART) Importing and Organizing Data {-}

# Reading Data Files into R {#fileinput}


* All of the files storing data that we will read into **R** will be assumed to be **text files**.

* **Text files**

  + Files with human readable characters such as letters, numbers, special characters (e.g., .red[", ', ?]), typically composed of multiple lines.
  
  + Can represent different characters by text encodings 
  
  + There are many types of text files, e.g.,
      
      -R files (.R)
      
      -html files (.html) / cascading style sheet (.css)
      
      -text files (.txt)
    

## Downloading a file locally

* Need to download a file to your local computer

* To test out reading in datasets into **R** that you have stored locally on your computer, we will first download the **gapminder** dataset.

* When you download a file, make sure you know
which **folder** it is in and that you can find the file path for the downloaded file.
   

* To load the **gapminder** dataset into **R**, you can use the **read.csv** function.

* Before running `read.csv`, it is often **convenient** to first set the **working directory** in **R** first using `setwd`
   + This allows you to load in all the files from the folder containing your data files without typing in the full file path name every time
   
   + For example, if the **gapminder** data was stored in a folder with path **"~/IntrotoR/Data**, we could first type

```r
setwd("~/IntrotoR/Data")
```

* After running `setwd`, we can now load in the **gapminder** dataset (stored as `gapminder_full.csv` on my computer) using `read.csv`

```r
fname <- "gapminder_full.csv"
gapminder <- read.csv(fname)
```



---


* To import a .csv file (or any other text file) in **Rstudio**, you can also click on the **Import Dataset** button on the top right panel.

* This lets you view how the data would appear before it is loaded into **R**.

---


* The **read.table()** function is the more general function 
for reading in rectangular data stored in text files.
   + You can read in other types of text files: e.g., **.tsv**, **.txt**

* **read.table()** can do the same thing as **read.csv()**. The main difference is that the default settings of **read.csv()** are setup to handle .csv files nicely.

* For example, we could read in the **gapminder** data with **read.table()** using:

```r
df <- read.table(fname, header=TRUE, sep=",") # Set header=TRUE
head(df)
```

```
##       country year population continent life_exp  gdp_cap
## 1 Afghanistan 1952    8425333      Asia   28.801 779.4453
## 2 Afghanistan 1957    9240934      Asia   30.332 820.8530
## 3 Afghanistan 1962   10267083      Asia   31.997 853.1007
## 4 Afghanistan 1967   11537966      Asia   34.020 836.1971
## 5 Afghanistan 1972   13079460      Asia   36.088 739.9811
## 6 Afghanistan 1977   14880372      Asia   38.438 786.1134
```

---

* You can look at the **first few rows** of a loaded data frame using `head`:


```r
dim(gapminder) # 1704 observations, 6 variables
```

```
## [1] 1704    6
```

```r
head(gapminder, 8)  ## look at first 8 rows
```

```
##       country year population continent life_exp  gdp_cap
## 1 Afghanistan 1952    8425333      Asia   28.801 779.4453
## 2 Afghanistan 1957    9240934      Asia   30.332 820.8530
## 3 Afghanistan 1962   10267083      Asia   31.997 853.1007
## 4 Afghanistan 1967   11537966      Asia   34.020 836.1971
## 5 Afghanistan 1972   13079460      Asia   36.088 739.9811
## 6 Afghanistan 1977   14880372      Asia   38.438 786.1134
## 7 Afghanistan 1982   12881816      Asia   39.854 978.0114
## 8 Afghanistan 1987   13867957      Asia   40.822 852.3959
```

```r
gapminder$country[1:5] # note that country is a factor
```

```
## [1] "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan"
```

---

* Looking at the **structure** of the data frame using `str()`


```r
str( gapminder )
```

```
## 'data.frame':	1704 obs. of  6 variables:
##  $ country   : chr  "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
##  $ year      : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
##  $ population: int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
##  $ continent : chr  "Asia" "Asia" "Asia" "Asia" ...
##  $ life_exp  : num  28.8 30.3 32 34 36.1 ...
##  $ gdp_cap   : num  779 821 853 836 740 ...
```

---

* Reading strings as **non-factors**: 


```r
gapminder_nofac <- read.csv(fname, stringsAsFactors = FALSE) 
head(gapminder_nofac)
```

```
##       country year population continent life_exp  gdp_cap
## 1 Afghanistan 1952    8425333      Asia   28.801 779.4453
## 2 Afghanistan 1957    9240934      Asia   30.332 820.8530
## 3 Afghanistan 1962   10267083      Asia   31.997 853.1007
## 4 Afghanistan 1967   11537966      Asia   34.020 836.1971
## 5 Afghanistan 1972   13079460      Asia   36.088 739.9811
## 6 Afghanistan 1977   14880372      Asia   38.438 786.1134
```

```r
gapminder_nofac$country[1:5] # No more "levels"
```

```
## [1] "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan"
```

---

* You can **skip** lines when you read in a text file.
    + This is useful if you don't want to read
in the "header" line of the .csv file: 

```r
df <- read.table(fname, header=FALSE, sep=",",skip=1) 
head(df)
```

```
##            V1   V2       V3   V4     V5       V6
## 1 Afghanistan 1952  8425333 Asia 28.801 779.4453
## 2 Afghanistan 1957  9240934 Asia 30.332 820.8530
## 3 Afghanistan 1962 10267083 Asia 31.997 853.1007
## 4 Afghanistan 1967 11537966 Asia 34.020 836.1971
## 5 Afghanistan 1972 13079460 Asia 36.088 739.9811
## 6 Afghanistan 1977 14880372 Asia 38.438 786.1134
```

* Or, skip the header and the first two rows of the .csv file

```r
df <- read.table(fname, header=FALSE, sep=",",skip=3) 
head(df)
```

```
##            V1   V2       V3   V4     V5       V6
## 1 Afghanistan 1962 10267083 Asia 31.997 853.1007
## 2 Afghanistan 1967 11537966 Asia 34.020 836.1971
## 3 Afghanistan 1972 13079460 Asia 36.088 739.9811
## 4 Afghanistan 1977 14880372 Asia 38.438 786.1134
## 5 Afghanistan 1982 12881816 Asia 39.854 978.0114
## 6 Afghanistan 1987 13867957 Asia 40.822 852.3959
```


## Opening a remote file using read.table()

* You can read in a dataset directly from a URL:

```r
# Read in ignoring the fact that there is a header line
urlname <- paste("https://web.stanford.edu/~hastie/",
                 "ElemStatLearn/datasets/bone.data", sep="")
bone_dat <- read.table(urlname)
head(bone_dat, 4)
```

```
##      V1    V2     V3          V4
## 1 idnum   age gender      spnbmd
## 2     1  11.7   male  0.01808067
## 3     1  12.7   male  0.06010929
## 4     1 13.75   male 0.005857545
```


```r
# Set header=TRUE to read in top line as the variable names
bone_dat2 <- read.table(urlname, header=TRUE)
head(bone_dat2, 4)
```

```
##   idnum   age gender      spnbmd
## 1     1 11.70   male 0.018080670
## 2     1 12.70   male 0.060109290
## 3     1 13.75   male 0.005857545
## 4     2 13.25   male 0.010263930
```


