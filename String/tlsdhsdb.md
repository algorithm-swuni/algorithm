# 문자열



## 펠린드롬

https://leetcode.com/problems/valid-palindrome/

Given a string s, determine if it is a palindrome, *considering only alphanumeric characters and ignoring cases.*

#### **Example 1**

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.

#### **Example 2**

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.

#### **Constraints:**

1 <= s.length <= 2 * 105
s consists only of printable ASCII characters.



## First Code

``` python
def solution(strings) :

    temp = (''.join(list(filter(lambda s: s.isalpha(),strings)))).lower()
    length = len(temp);
    left = temp[:int(length / 2)]
    right = ''

    if len(temp) % 2 is not 0:
        right = temp[length:int(length/2):-1]
    else :
        right = temp[length:int(length/2)-1:-1]

    return True if right == left else False

if __name__ == '__main__':
    string1 = 'A man, a plan, a canal: Panama'
    string2 = 'race a car'

    print(solution(string1))
```

![image-20210225153645819](https://user-images.githubusercontent.com/42714724/109118614-e5d1ff80-7786-11eb-8cfb-24d9954eea47.png)

### problem  resolve

조건 : **영어,숫자** 만 펠린드롬이 된다!

`s.isalpha` = > `s.isalnum` 으로 변경해주면 된다.

`s.isalnum` 은 해당 문자열이 영어 or 숫자인지 체크해주는 함수이다.



### result 

![image-20210225154156968](https://user-images.githubusercontent.com/42714724/109118621-e79bc300-7786-11eb-9ece-e9de22bf68e1.png)



## Final Code 

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
            left = ''
            right = ''
            temp = (''.join(list(filter(lambda s: s.isalnum(),s)))).lower()
            length = len(temp)
            left = temp[:int(length / 2)]

            if len(temp) % 2 is not 0:
                right = temp[length:int(length/2):-1]
            else :
                right = temp[length:int(length/2)-1:-1]
            
            print(f'left:{left}')
            print(f'right:{right}')
            
            return True if right == left else False 
```



## 사용된 개념



### 람다 함수

```python
lambda param : expression

>>> def hap(x, y):
...   return x + y

>>> (lambda x,y : x + y)(10,20)
	30


filter(function,list)

>>> list(filter(lambda x : x < 5 , range(10)))
	[0,1,2,3,4]
```

filter 의 경우 해당 조건에 맞는 경우를 출력하는데 사용.

[람다함수](https://wikidocs.net/64) < 관련 문서



### is  와  == 의 차이

- `is`는 변수가 같은 `Object(객체)`를 가리키면 True
- `==`는 변수가 같은 `Value(값)`을 가지면 True

``` python
>>> a = [1,2,3]
>>> b = a ## a와 b는 같은 리스트 객체를 가리킨다.
>>> c = [1,2,3] ## a,b는 같은 객체를 가리키고 c가 가리키는 리스트와 값이 같지만 c는 다른 객체를 가리키고 있다

>>> a is b
	True    
>>> a is c
	False
    
>>> a == b
	True
>>> a == c
	True
```



[참고자료](https://twpower.github.io/117-difference-between-python-is-and-double-equal)



### 문자열 슬라이싱



![image-20210225155637697](https://user-images.githubusercontent.com/42714724/109118637-e8ccf000-7786-11eb-8b4d-cc0ddcaa02f0.png)

![image-20210225155645866](https://user-images.githubusercontent.com/42714724/109118641-e9fe1d00-7786-11eb-9700-c39e05eab0ca.png)

``` python
>>> mystring[6:]
'world'

>>> mystring[:5]
'hello'

>>> mystring[6:-1]
'worl'

>> mystring[:2:-1]
'leh'
```



### 파이썬의 3항 연산자

```python
# result = when True if condition else when False;
a = 10
b = 20
result = (a-b) if a == b else (a+b)    # 결과는 a+b = 30

## (true) if (conditional) else (false)
```

이러한 형식으로 작성가능하다.



##  Jewels and Stones

https://leetcode.com/problems/jewels-and-stones/

You're given strings `jewels` representing the types of stones that are jewels, and `stones` representing the stones you have. Each character in `stones` is a type of stone you have. You want to know how many of the stones you have are also jewels.

Letters are case sensitive, so `"a"` is considered a different type of stone from `"A"`.



**Example 1**

```
Input: jewels = "aA", stones = "aAAbbbb"
Output: 3
```

**Example 2**

```
Input: jewels = "z", stones = "ZZ"
Output: 0
```

 

**Constraints:**

- `1 <= jewels.length, stones.length <= 50`
- `jewels` and `stones` consist of only English letters.
- All the characters of `jewels` are **unique**.



```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        result = 0
        for j in jewels:
            temp = list(filter(lambda s: s == j,stones))
            result = result + len(temp)
        
        return result
```

## result 

![image](https://user-images.githubusercontent.com/42714724/109118852-347f9980-7787-11eb-8703-2621a4d87464.png)

