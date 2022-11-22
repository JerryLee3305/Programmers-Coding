# N개의 최소공배수
## Python
### 문제
> 문제 설명

두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

> 제한 사항

1. arr은 길이 1이상, 15이하인 배열입니다.
2. arr의 원소는 100 이하인 자연수입니다.
> 입출력 예

|arr	|result
|---|----
|[2,6,8,14]	|168
|[1,2,3]	|6

### for문으로 풀었을 때 실패!
```python
def solution(arr):
    arr.sort(reverse = True)
    answer = arr[0]
    for i in range(1,len(arr)):
        for j in range(1,len(arr)):
            if arr[i]*j == answer:
                break
            answer += arr[0]
            print(answer)
    return answer
```
- 우선 길이를 지정해주는 것 자체부터 틀린것 같다.
- while을 사용해서 같은 값이 나올 때까지 돌려야하나 싶기도 하다.

### 이중 for문으로 최소공배수 원리 생각하며 성공!
```python
def solution(arr):
    arr.sort(reverse = True)
    answer = arr[0]
    for i in arr:
        for j in range(max(i,answer),i*answer +1):
                if j%i==0 and j%answer ==0:
                    answer = j
                    break
    return answer
```
1. 최대인 것을 먼저 가져온다.
2. 하나씩 비교해가며 최소공배수 원칙을 생각해본다.
3. 두개 중 최대인 값과 둘의 곱까지 for문을 돌려 공배수인지 확인을 하고 정답을 수정한다.
4. 다른 것도 마찬가지로 진행을 하여 정답을 계속적으로 증가시켜준다.