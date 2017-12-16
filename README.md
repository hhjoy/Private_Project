# Personal Project   
---------------------------  
## Description  
### 1. 데이터 수집.  
> * package : selenium, requests, BeautifulSoup, etc.  
> 
> 1. 일별로 카테고리별 랭킹에 따라 뉴스를 크롤링.  
>> * 네이버, 다음.  
>> * 뉴스는 본문,  신문사, 랭킹순위, 카테고리, 날짜, 사이트, 댓글수, 크롤링한 댓글수, (다음의 경우, 키워드 정보까지).  
>>
>> 다음.  
>> 
>> | category | date | link | press | rank | title | mainText | keywords | number of comments |  real comment | site |  
>> |:------------|:------:|:-----:|:-------:|:------:|:----:|:-------------:|:-----------:|:-----------------------:|:---------------:|------:|
>> | category | date|link | press | rank | title | mainText | keyword | number of comments |  real comment | site |  
>> 
>> 네이버.    
>> 
>> | category | date | link | press | rank | title | mainText | number of comments |  real comment | site |  
>> |:------------|:------:|:-----:|:-------:|:------:|:----:|:-------------:|:----------------------------:|:--------------------:|------:|
>> | category | date | link | press | rank | title | mainText | number of comments |  real comment | site |  
>
> 2. 해당 뉴스에 대한 전체 댓글 내용과 각 댓글의 공감/비공감 수.  
>>   
>> 댓글.  
>> 
>> | category | date | link | comment | 공감 | 비공감 | site |  
>> |:------------|:------:|:-----:|:------------:|:-----:|:---------:|-----:|  
>> | category | date | link | comment | 공감 | 비공감 | site |  
>>  
> 3.  2시간마다 해당 시간대의 newstopic에 대한 순위를 카테고리별로 수집함.  
> * 이모티콘으로만 구성된 댓글은 배제함.
>>  
>> 뉴스토픽.  
>> 
>> | date | time | site | category | rank | topic |  
>> |:-------|:------:|:-----:|:-----------:|:------:|--------:| 
>> | date | time | site | category | rank | topic |    
>>   

### 2. 데이터베이스 구축 (2017 12월 16일 15시 20분 기준).  
> 크롤링을 통해 데이터를 저장할 데이터 베이스를 구축.  
> mongoDB.  
> * DB 구축.  
>> * news - Daum : 2172.  
>> * news - Naver : 3601.  
>> * comments : 3468082.  
>> * newsTopic : 3600.  

### 3. 웹 구축. 
> Flask를 이용하여 Amazone Web Service(AWS)에 웹 구축 (예정). 

### 4. 키워드 분석. 
> package : konlpy, customized-konlpy, etc. 
> customized-konlpy의 경우, corpus를 추가할 수 있어, 공공 데이터포털의 뉴스빅데이터 분석 정보 파일([빅카인즈](https://www.kinds.or.kr/) )을 이용하여 명사만을 추출하여 추가함.  
>  * 목표 : 네이버와 다음에서 각 카테고리별로 하루동안 많이 본 뉴스들에 대하여 키워드 분석을 진행하고 두 사이트별로 카테고리에 따른 키워드의 분포, 그리고 키워드의 빈도, 그리고 공통된 키워드와 차이가 있는 키워드를 분석할 수 있다.  
> * 뉴스 본문의 키워드 추출 (빈도수)  
>> * 다음의 경우, 키워드가 제시되어 있는 것도 있고 없는 것도 있음, 추가 코드로 만들어진 키워드와의 차이를 비교할 수 있음.  
>> 문제점. 
>>>  뉴스 본문의 키워드를 konlpy의 Twitter, mecab 그리고 ETRI에서 제공하는 [공공 인공지는 오픈 API DATA 서비스](http://aiopen.etri.re.kr/)를 이용하여 주요 키워드를 추출해보고자 하였으나, 다음에서 보여주는 키워드와 기사를 읽어보고 대략적으로 파악한 키워드와는 차이를 보임.  

### 5. 감정 분석  
> * 추출된 키워드에 대하여 뉴스 내용이 긍정적인지 부정적인지 분석. 
> * 추출된 키워드에 대하여 언론사가 어떠한 뉘앙스로 서술을 하는지 알려진대로 조선일보는 진보진영에 비판적이고 보수진영에 긍정적인지, 경제쪽 신문은 기업들을 옹호하는지, 한겨례와 경향은 진보진 영에 긍정적이고 보수진영에 비판적인지에 대하여 분석을 해보고자 함.  
> * 뉴스의 댓글들에 대하여 감정 분석. 
>> * 뉴스 본문에서 추출된 키워드에 대하여 뉴스 본문에서부터 얻는 감정 분석 정보와 해당 뉴스의 댓글에서 얻을 수 있는 전체적인 감정에 대하여 분석을 하고자 함.  
> naver movie sentiment, 공공 데이터포털의 뉴스빅데이터 분석 정보 파일([빅카인즈](https://www.kinds.or.kr/) )중 주제에 따라 감정분석과, 긍정문장, 부정문장을 가지고 있는 문서가 존재하여 이를 이용하고자 함. 
>  * 공공 데이터포털의 뉴스빅데이터 분석 정보 파일
>> 긍정 문장 : 156291  
>> 긍정 단어 : 632330  
>> 부정 문장 : 161297  
>> 부정 단어 :  1617233  
> * naver movie sentiment analysis   
>> 20만건  

### 6. 추가분석  
> * 유사한 키워드를 가지고 있는 뉴스들에 대하여 본문을 분석하고 신문사별 긍부정 분석. 
> * 네이버와 다음의 댓글 성향이 얼마나 다른지에 대하여 분석을 해보고자 함.  
> * 신문사, 키워드 등의 정보를 이용하여 분류  
> * 신문사, 키워드 등의 정보를 이용하여 클러스터링  
> * 시각화 작업  
>> * 키워드 사이의 연관성을 보여주는 그래프를 보여줄 수 있다.  
---------------------------  
### * 참고
* [konlpy](konlpy.org)
* [customized konlpy](https://github.com/lovit/customized_konlpy)
* [datascienceschool](https://datascienceschool.net/)
* [공공데이터포탈](https://www.data.go.kr/)
> [데이터셋](https://www.data.go.kr/dataset/15012945/fileData.do)
* [빅카인즈](https://www.kinds.or.kr/)
---------------------------  