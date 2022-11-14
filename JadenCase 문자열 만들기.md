# JadenCase 문자열 만들기
## Python
### 문제
> 문제 설명

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)

문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

> 제한 조건
1. s는 길이 1 이상 200 이하인 문자열입니다.
2. s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
3. 숫자는 단어의 첫 문자로만 나옵니다.
4. 숫자로만 이루어진 단어는 없습니다.
5. 공백문자가 연속해서 나올 수 있습니다.

> 입출력 예

|s	|return
|-|-
|"3people unFollowed me"|	"3people Unfollowed Me"
|"for the last week"	|"For The Last Week"

### 예제 성공 문제 런타임 에러 실패!
```python
def solution(s):
    answer = ''
    s = list(s.lower().split(' '))
    for i in s:
        answer += i[0].upper()
        answer += i[1:] + ' '
    return answer[:-1]
```
1. 먼저 띄어쓰기를 없애고 소문자로 모두 변환한 이후에 리스트에 저장을 해준다.
2. 한 단어씩 가져오면서 맨 앞의 단어를 대문자로 변경해준다.
3. 이때 숫자에 upper문을 사용해도 에러가 나지 않는다.
4. 그 이후의 단어들을 정답칸에 넣는다.
5. 띄어쓰기를 해준 다음 마지막에도 띄어쓰기가 존재하기 때문에 맨 마지막의 띄어쓰기만 없애고 출력한다.
- 내 생각엔 for문을 사용하였기에 런타임 에러가 발생한 듯 하다

### 첫 문자를 대문자로 만드는 capitalize()를 사용해도 실패!
```python
def solution(s):
    answer = ''
    for i in s.lower().split():
        answer += i.capitalize() + ' '
    return answer[:-1]
```
1. 소문자로 만든 후 단어를 분리시킨다.
2. 단어를 하나씩 가져오면서 첫 문자를 대문자로 만들고 뒤에 공백을 제거해준다.
- 무엇이 문제일까..... 하나씩 해봐야 할듯!

### 하나씩 하니까 성공!!
```python
def solution(s):
    s = s.split(" ")
    for i in range(len(s)):
        s[i] = s[i][:1].upper() + s[i][1:].lower()
    return ' '.join(s)
```
1. 먼저 공백을 기준으로 단어를 나눠준다.
2. 인덱스를 기준으로 첫 문자를 대문자로 나머지 문자를 소문자로 설정한 후 저장
3. 사이에 공백이 필요하기 때문에 join을 이용하여 묶어주기
