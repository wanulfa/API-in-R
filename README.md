# API-in-R

##API in R

Fist, I have to install the jsonlite package. There are two way to do this, by clicking the install in packages menu or by doing this code:

```{r}
install.packages('jsonlite')
```

Then, I have to put it into my library:

```{r}
library('jsonlite')
```

Then, I put my object into R. This time, I am doing with the postcode:

```{r}
url <- "http://api.postcodes.io/postcodes/b422su"
```

To load the data from url, I need to run the function. 

```{r}
jsoneg <- fromJSON(url)
```
If I want to see what inside the jsoneg, I use

```{r}
jsoneg[['status']]
```

Now, I have the data in my environment. That is better to open the url so I konw what is it there, what kind of data I can grab. What function I have. In this case, I have some function like result, code, and ccg. So I can type

```{r}
jsoneg[['result']][['codes']][['ccg']]
```
So, to get the constituency, I need:
```{r}
jsoneg[['result']][['parliamentary_constituency']]
```

#Creating a loop

To use this on multiple postcodes, I have to create a loop and need a list of postcodes:

```{r}
postcodes <- c("B422SU","BL23QQ","B735XJ")
```

Now, I have the lists of postcodes in my values.

A loop uses 'for', followed by a reference to the list in parentheses, followed by what we want to happen for each item. 

```{r}
for (i in postcodes){
  print(i)
  }
```

At this moment, i is just printed-but we can do something more useful with it. How? add it to the postcode URL will be so useful. 

```{r}
paste("http://api.postcodes.io/postcodes/","B422SU")
```

This combines the two strings in parentheses, into one.

```{r}
postcode <- "BL23QQ"
paste("http://api.postcodes.io/postcodes/",postcode)
```

To erase the space between them:

```{r}
paste("http://api.postcodes.io/postcodes/","B422SU", sep="")
```

Put them into the loop

```{r}
for (i in postcodes){
  print(paste("http://api.postcodes.io/postcodes/",i, sep=""))
}
```
See! we have 3 url now. Let grab the JSON from each url:

```{r}
for (i in postcodes){
  #store the full url in an object
  url <- paste("http://api.postcodes.io/postcodes/",i, sep="")
  #grab the JSON
  jsoneg <- fromJSON(url)
  #drill down into one branch and print the value
  print(jsoneg[['result']][['parliamentary_constituency']])
}
```
