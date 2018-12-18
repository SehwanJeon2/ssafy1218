```python
import random
import requests
from bs4 import BeautifulSoup as bs
# 1~45 까지의 숫자를 가진 numbers라는배열을 만든다.

# python make long array / make number array

# 숫자 배열 방법 1: for를 이용한 반복문

# lotto = []

# for i in range(45):

# lotto.append(i+1)

# print(lotto)

# 숫자 배열 방법 2: list(range())를 이용하기

numbers = list(range(1, 46, 1))
print(numbers)

# numbers에서 숫자 6개를 랜덤으로 뽑는다. (당연히 비복원 추출)

# 랜덤으로 뽑은 숫자들을 lotto에 담고 출력한다.
#random.choice(numbers) 는 1개만 뽑는 것
lotto = random.sample(numbers,6)
#로또 변수에 담겨있는 숫자들을 오름차순으로 정렬하기
```



# 


# 로또 변수에 담겨있는 숫자들을 오름차순으로 정렬하기
```python
lotto = sorted(lotto)
print("이번 주 로또 추천 번호는 {} 입니다." .format(lotto))

#로또 사이트에서 지난 로또 번호 찾기
url = 'https://m.dhlottery.co.kr/common.do?method=main'
response = requests.get(url).text
soup = bs(response, 'html.parser')
#print(soup)
document = soup.select('.prizeresult')[0]
lastnumbers = document.select('span')

ns = []
for number in lastnumbers:
  ns.append(int(number.text))

#print(lastnumbers)
print("지난 주 로또 당첨번호는 {} 입니다." .format(ns))
```





# 지난 주 당첨 숫자 배열을 한번씩 순회하면서
# 내가 뽑아놓은 lotto 배열에서
# 몇개가 맞았는지 카운트 하기
# for와 if를 이용해서 count를 올리는 방법
# 단 반복문이 42번 돌아서 찝찝하다
```for i in lotto:
count = 0
for j in ns:
    if(j==i):
      count=count+1
print("지난 주와 비교하면 {} 개가 일치합니다." . format(count))
```



# 검색을 한 결과 더 짧은 코드
# for num in ns
#   if num in lotto:
#     count = count+1