import requests
import time
from bs4 import BeautifulSoup as bs
import json

# 1. 내가 원하는 정보를 얻을 수 있는 주소를 url 변수에 담는다
url = 'http://webtoon.daum.net/data/pc/webtoon/list_serialized/thu?timeStamp=1545117148822'


# 2. 해당 url에 요청을 보내 응답을 받아 저장한다.
response = requests.get(url).text
print(type(response))
#soup = bs(response, 'json')


# 3. 구글신에게 python으로 어떻게 json을 피싱(딕셔너리 형으로 변환)하는지
#    물어보고 파싱한다. (변환한다)
document = json.loads(response)
print(type(document))


# 4. 내가 원하는 데이터를 꺼내서 조합한다.
data = document["data"]
toons = []
for toon in data:
  print(toon["title"])
  print(toon["pcThumbnailImage"]["url"])
  print("http://webtoon.daum.net/webtoon/view/{}".format(toon["nickname"]))

# 오 힘드렀다