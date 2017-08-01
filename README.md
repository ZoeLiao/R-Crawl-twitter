# R_Crawl_twitter

```{r}
library(devtools)
library(twitteR)
require(stringr)
library(dplyr)

#create account 創建帳號 
Consumer_key<- "your key"
Consumer_secret <- "your secret"
access_token <- "your access_token"
access_token_secret <- "your access_token_secret"
setup_twitter_oauth(Consumer_key,Consumer_secret,access_token,access_token_secret)

#search hashtag and date 可查詢hashtag＆日期 
data<-searchTwitter("#TaoyuanAirport#Christmas",n = 300, since="2016-12-09")

#create a table 製做成表格 
data
df <- do.call("rbind", lapply(data, as.data.frame))
df
df$text<-strsplit(as.character(df$text), "https") 
df$text<-gsub(pattern="://",replacement="https://",df$text)
df$text
output<-data.frame(df$screenName,df$text,df$created)
output
names(output)<-c("username","hashtag","time")
write.csv(output,file="twitter20170103yes.csv")

```
