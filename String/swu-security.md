# Palindrome

## Problem

#### Given a string s, determine if it is a palindrome, considering only alphanumeric charters and ignoring cases.

### Example 1:

Input: s ="A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.

### Example 2:

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.

### Constraints

1 <= s.length <= 2 * 105
s consists only of printable ASCII characters.

### <u>First Code</u>

```python
# 유효한 펠린드롬
# 펠린드롬이란 앞으로 뒤로해도 같은 문자열
# 대소문자 상관 없음
# 문장부호 제외

def palindrome(s: str) -> bool:
    string = ""
    for char in s:
        if char.isalpha():
            string += char.lower()
    if string == string[::-1]:
        print("string: %s, reverse: %s" % (string, string[::-1]))
        return True
    else:
        print("string: %s, reverse: %s" % (string, string[::-1]))
        return False

if __name__ == '__main__':
    # Example 1:
    s1 = "A man, a plan, a canal: Panama" # True
    print(palindrome(s1))
    # Example 2:
    s2 = "race a car"                     # False
    print(palindrome(s2))
```

### <u>Result</u>

![image-20210225174411664](C:\Users\happy\AppData\Roaming\Typora\typora-user-images\image-20210225174411664.png)

### <u>Error Correction</u>

```python
def palindrome(s: str) -> bool:
    string = ""
    for char in s:
        if char.isalnum():
            string += char.lower()
    if string == string[::-1]:
        print("string: %s, reverse: %s" % (string, string[::-1]))
        return True
    else:
        print("string: %s, reverse: %s" % (string, string[::-1]))
        return False

if __name__ == '__main__':
    # Example 1:
    s1 = "A man, a plan, a canal: Panama" # True
    print(palindrome(s1))
    # Example 2:
    s2 = "race a car"                     # False
    print(palindrome(s2))
```

### <u>Result</u>

![image-20210225180340853](C:\Users\happy\AppData\Roaming\Typora\typora-user-images\image-20210225180340853.png)



### <u>Big O </u>

for문에서 주어진 문자열 길이만큼 반복되므로 시간 복잡도는 **O(n)**



# Jewels And Stones

## Problem

You're given strings J representing the types of stones that are jewels, and S representing the stones you have. Each character in S is a type of stone you have. You want to know how many of the stones you have are also jewels.

The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A".

## Example

Input: J = "aA", S = "aAAbbbb"

Output: 3

### <u>Code</u>

```python
def numJewelsInStones(jewels: str, stones: str) -> int:
    result = 0
    for jewel in jewels:
        result += stones.count(jewel)
    return result
```

### <u>Result</u>

![image-20210226145944144](C:\Users\happy\AppData\Roaming\Typora\typora-user-images\image-20210226145944144.png)

### <u>Big O</u>

for문에서 주어진 jewels 리스트의 요소 개수만큼 반복하므로 시간복잡도는 **O(n)**

