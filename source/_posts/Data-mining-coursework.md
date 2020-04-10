---
title: Data mining coursework
tags: Data mining
categories: Data mining
abbrlink: cf5e19f
date: 2020-03-06 15:57:12
---
> I\'m going to record the errors when I\'m doing my Data Mining coursework here

<!-- more -->
1. reindex() missing 1 required positional argument: 'self'
```python
tweet_df = pd.DataFrame.reindex(index=range(df.shape[0]))
```
This code could help you create a DataFrame filling with 'NaN'.
The new DataFrame tweet_df has one column and the same number of rows as DataFrame df.
The previous code is wrong and it should change to the following code:
```python
tweet_df = pd.DataFrame().reindex(index=range(df.shape[0]))
```
2. in pandas, null means numpy.nan
```python
if pd.isnull(df):
  print('DataFrame df is null')
```
if you want to remove the null character string, you cannot merely use pd.isnull(), you should use:
```python
def drop_rows(tweets):
  for i in range(len(tweets)):
    if tweets[i] == '' or pd.isnull(tweets[i]):
      tweets.drop([i])
  return tweets
```
This code is not really good, the following code is an improvement：
```python
def drop_rows(tweets):
  drop_index = []
  for i in range(len(tweets)):
    if tweets[i] == '' or pd.isnull(tweets[i]):
      drop_index.append(i)

  tweets.drop(drop_index, inplace = True)
  # reset_index这一步很重要，使删除了若干项的不连贯的index重新建立连续的index
  tweets.reset_index(drop=True, inplace=True)
  return tweets
```
3. in some functions in pandas, you should be careful of inplace operator, it may bring you some misunderstanding sometimes.

4. Stemming(词干提取)
Stem (root) is the part of the word to which you add inflectional (changing/deriving) affixes such as (-ed,-ize, -s,-de,mis). So stemming a word or sentence may result in words that are not actual words. Stems are created by removing the suffixes or prefixes used with a word.
 > `Stop words`: `Stop Words` are words which do not contain important significance to be used in Search Queries. Usually, these words are filtered out from search queries because they return a vast amount of unnecessary information. Each programming language will give its own list of stop words to use. Mostly they are words that are commonly used in the English language such as 'as, the, be, are' etc.
 ```python
 import nltk
 nltk.download('stopwords')

 from wordcloud import STOPWORDS

 def stop_words():
   from nltk.corpus import stopwords
   # 179 words
   stop_words_list = stopwords.words('english')
   return stop_words_list

# 179 words
nltk_list = stop_words()
# 190 words
wordcloud_list = list(STOPWORDS)

 ```
 ![stopwords](/images/stopwords.png)
[here](https://www.nltk.org/book/ch02.html)

```python
# 基于Porter词干提取算法
from nltk.stem.porter import PorterStemmer
porter_stemmer = PorterStemmer()
print(porter_stemmer.stem('maximum'))
print(porter_stemmer.stem('prints'))
print(porter_stemmer.stem('printed'))
print(porter_stemmer.stem('printing'))
print(porter_stemmer.stem('this'))
print(porter_stemmer.stem('am'))
print(porter_stemmer.stem('is'))
print(porter_stemmer.stem('are'))
print(porter_stemmer.stem('car\'s'))
print(porter_stemmer.stem('cars\''))
print(porter_stemmer.stem('leaves'))
print('-------------------------------------------')
# 基于Lancaster 词干提取算法
from nltk.stem.lancaster import LancasterStemmer
lancaster_stemmer = LancasterStemmer()
print(lancaster_stemmer.stem('maximum'))
print(lancaster_stemmer.stem('prints'))
print(lancaster_stemmer.stem('printed'))
print(lancaster_stemmer.stem('printing'))
print(lancaster_stemmer.stem('this'))
print(lancaster_stemmer.stem('am'))
print(lancaster_stemmer.stem('is'))
print(lancaster_stemmer.stem('are'))
print(lancaster_stemmer.stem('car\'s'))
print(lancaster_stemmer.stem('cars\''))
print(lancaster_stemmer.stem('leaves'))
print('-------------------------------------------')
# 基于Snowball 词干提取算法
from nltk.stem import SnowballStemmer
snowball_stemmer = SnowballStemmer('english')
print(snowball_stemmer.stem('maximum'))
print(snowball_stemmer.stem('prints'))
print(snowball_stemmer.stem('printed'))
print(snowball_stemmer.stem('printing'))
print(snowball_stemmer.stem('this'))
print(snowball_stemmer.stem('am'))
print(snowball_stemmer.stem('is'))
print(snowball_stemmer.stem('are'))
print(snowball_stemmer.stem('car\'s'))
print(snowball_stemmer.stem('cars\''))
print(snowball_stemmer.stem('leaves'))
```
5. Lemmatisation(词性还原)
```python
import nltk
nltk.download('wordnet')
from nltk import WordNetLemmatizer
lemmatizer = WordNetLemmatizer()
print(lemmatizer.lemmatize('maximum'))
print(lemmatizer.lemmatize('prints'))
print(lemmatizer.lemmatize('printed'))
print(lemmatizer.lemmatize('printing'))
print(lemmatizer.lemmatize('this'))
print(lemmatizer.lemmatize('am'))
print(lemmatizer.lemmatize('is'))
print(lemmatizer.lemmatize('are'))
print(lemmatizer.lemmatize('car\'s'))
print(lemmatizer.lemmatize('cars\''))
print(lemmatizer.lemmatize('leaves'))
```
6. str.replace()的使用误区
此处使用的是pandas.Series.str.replace方法
> 小tip：在路径中去除掉一些特殊意义的字符进行转义，除了可以使用'\\'之外，我们也可以使用r加在所要处理的字符外面，这样就不用专门的去处理引号之中的特殊字符了

```python
word_list = ['user', 'url']
for i in range(len(word_list)):
  df['tweet'] = df['tweet'].str.replace(word_list[i], "")
```
本意是想替换tweets中的所有user，url，只整体替换单词，最后发现只要tweets中出现了这个组合的词都被替换了，比如一个词，原本是username，本无意替换，这里却替换成了name。
最后采用lambda表达式，一行搞定：
```python
df['tweet'] = df['tweet'].apply(lambda x: ' '.join([w for w in x.split() if w not in word_list and len(w)>3]))
```
意思就是把每一条tweets进行遍历（x的作用），每条tweet都根据空格分隔为一个list然后遍历（w），满足条件的留下来（for前面的w），最后每一条tweet通过' '（空格）再连接起来。

7. pandas.DataFrame.merge使用
Merge DataFrame or named Series objects with a database-style join.
以数据库风格的方式合并DataFrame或Series
比如两个csv文件都拥有相同的列名id，现在想根据id合并为一个csv文件（类似Excel的vlookup函数）
```python
outfile = pd.merge(df1, df2, how='inner', left_on='id',right_on='id')
```
表示将df1的id列和df2的id列以inner join的方式进行合并，
```sql
select * from df1 inner join df2
where df1.id = df2.id
```
以上代码过于啰嗦，完全可以用以下代替
```python
outfile = pd.merge(df1, df2, on='id')
```
8. summary

The method I used to create the training data and test data:
- get all the distinct words from different tweets(for example, get offensive words from all the offensive tweets), count and rank them.
- In this case, I get 7 different sets of words(offensive, not offensive, targeted, nottargeted and so on).
- Then, I choose the words that occur more than 10 times(we can modify this threshold), so I get 7 new sets of words.
- After that, I use these 7 new sets of words to filter the original tweets respectively(for example, use new offensive words set to filter the offensive tweets, only keep words in the new offensive words set).
- finally, I get 7 different types of tweets(offensive tweets, notoffensive tweets and so on) and combine them to 3 new tweets sets(subtask_a, subtask_b, subtask_c)

Other data cleaning method I used (maybe they can be mentioned in the presentation)
- Only keep the characters and hash tags
- remove the extra blanks
- lowercase all the words
- remove the stop words and some words that don't make sense.(stop words are from nltk corpus and wordcloud stopwords list)
- replace all the null subtask to NaN
- keep the words longer than 3 words
- word cloud presentation


lemmatizer

- use lemmatizer for the training and test data

stem

- use SnowballStemmer for the training and test data

- words_count

All the words(except the stop words and some words that don't make sense)in the tweets and their counts


Reference:
1. [Pandas API reference](https://pandas.pydata.org/pandas-docs/stable/reference/index.html)
