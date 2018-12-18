import requests
import time
from bs4 import BeautifulSoup as bs

today = time.strftime("%a").lower()
print(today)
# 1. 네이버 웹툰을 가져올 수 있는 주소(url)를 파악하고 url 변수에 저장한다.
naver_url = 'https://comic.naver.com/webtoon/weekdayList.nhn?week=tue'


# 2. 해당 주소로 요청을 보내 정보를 가져온다.
response = requests.get(naver_url).text


# 3. 받은 정보를 bs를 이용해 검색하기 좋게 만든다.
soup = bs(response, 'html.parser')
# print(soup)


# 4. 네이버 웹툰 페이지로 가서, 내가 조아하는 정보가 어디에 있는지 파악한다.
# 오늘자 업데이트 된 웹툰들의 각각 리스트 페이지 +
# 웹툰의 제목 + 해당 웹툰의 썸네일
toons = []
li = soup.select('.img_list li')
#print(li)
for item in li:
  toon = {
​    "title": item.select('dt a')[0].text,
​    "url":  item.select('dt a')[0]["href"],
​    "img_url":  item.select('.thumb img')[0]["src"]
  }
  toons.append(toon)
  print(toon)
#내가 처음에 .dt 로 접근 못한 이유가 여러가지를 select 해서 배열이 됨
#그래서 항상 [0]같은게 붙어야 했다.


# 5. 3번에서 저장한 문서를 이용해 4번에서 파악한 위치를 뽑아낸다.

# 6. 출력한다.





#document = soup.select('.thumb')
#first_link = document.select('<a title="여신강림" href="/webtoon/list.nhn?titleId=703846&amp;weekday=tue">여신강림</a>')
#print(document)