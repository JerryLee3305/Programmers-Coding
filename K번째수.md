# 문자열 내 마음대로 정렬하기
## Python
### 문제
- 문제 설명
배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면
array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.

1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
2에서 나온 배열의 3번째 숫자는 5입니다.

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

- 제한사항
array의 길이는 1 이상 100 이하입니다.
array의 각 원소는 1 이상 100 이하입니다.
commands의 길이는 1 이상 50 이하입니다.
commands의 각 원소는 길이가 3입니다.

- 입출력 예

- 입출력 예 설명
[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
[1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
[1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.

#### 첫번째 도전 실패
```python
def solution(array, commands):
    answer = []
    for i in commands:
        lis = []
        lis.append(array[i[0]-1:i[1]])
        lis.sort()
        answer.append(lis[i[2]])
        print(answer)
        
    return answer
```
1. commands 내 리스트 하나씩 for문으로 가져오기
2. 리스트 내에서 인덱스를 사용해 array에 있는 숫자들 가져오기
3. 슬라이싱을 사용해서 그 속에 있는 숫자 배열 가져오기
4. 새로운 리스트에 추가한 이후 정렬해주기
5. 정답에 추가해주기

- IndexError: list index out of range
- 리스트의 범위가 아니라고 하니까 인덱스 번호를 다시 한번 조정해보기

#### 두번째 도전 실패
```python
def solution(array, commands):
    answer = []
    for i in commands:
        lis = []
        lis.append(array[i[0]-1:i[1]])
        lis.sort()
        answer.append(lis[i[[2]]])
        print(answer)
        
    return answer
```
- 똑같은 에러가 뜨면서 발생
- for문 안에 print()를 써서 확인해본 결과 lis 내 결과가 [[2,1,3]] 이런 형식으로 들어가져 있음
- 그래서 sort도 진행이 안되었기에 새로운 리스트를 만들지 않고 하나의 변수에 저장해서 하는 것으로 해보기

#### 세번째 도전 실패
```python
def solution(array, commands):
    answer = []
    for i in commands:
        a = array[i[0]-1:i[1]]
        a.sort()
        answer.append(a[i[2]])
    return answer
```
- IndexError: list index out of range
- 이번에도 같은 에러,,,, 다시 print()를 이용해서 하나씩 살펴봐야할듯
#### 네번째 도전 성공
### 성공 코드
```python
def solution(array, commands):
    answer = []
    for i in commands:
        a = array[i[0]-1:i[1]]
        a.sort()
        answer.append(a[i[2]-1])
    return answer
```
- 기본적인 실수를 했다... 리스트 내 숫자를 인덱스 할 때 -1 을 하는 건 기본이였는데 ㅠㅠㅠ

> 프로그래머스 타인 코드
```python
return list(map(lambda x:sorted(array[x[0]-1:x[1]])[x[2]-1], commands))
```
- 한 줄 코드를 좋아하지는 않지만 너무 깔끔하다
- for이 아닌 lambda를 사용해서 내가 쓴 코드를 그대로 사용했다
- sort를 사용하기 위해 변수를 하나 만들었지만 여기서는 sorted를 사용해서 변수 생성 필요 없이 한번에 했다는 점!