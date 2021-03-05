# Array
## Array 배열
- 데이터를 나열하고, 각 데이터를 인덱스를 대응하도록 구성한 선형 데이터구조
- python 에서는 List 타입이 배열 기능을 제공
## 배열을 쓰는 이유
- 같은 종류의 데이터를 효율적으로 관리
- 같은 종류의 데이터를 순차적으로 저장
- 장점 : 빠른 접근 가능 => 첫 데이터의 위치에서 상대적인 위치로 접근 가능 (index), 시간 복잡도 O(1)
- 단점 : 데이터 추가/삭제의 어려움
## 시간복잡도
* 삽입/삭제
  - 배열의 맨 앞에 삽입/삭제하는 경우: O(n)
  - 배열의 맨 뒤에 삽입/삭제하는 경우: O(1)
  - 배열의 중간에 삽입/삭제하는 경우: O(n)
* 탐색 - O(1)
## Best Time to Buy and Sell Stock
## Problem
### You are given an array prices where prices[i] is the price of a given stock on the ith day.
### You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
### Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.
## Example 1:
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
## Example 2:
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
## Constraints
- 1 <= prices.length <= 105
- 0 <= prices[i] <= 104

## <u>First Code</u>
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) <= 1:
            return 0
        maximum = 0
        for i in range(len(prices)-1):
            for compare in range(i+1,len(prices)):
                if prices[i]+maximum < prices[compare]:
                    maximum = prices[compare] - prices[i]
         
        return maximum
```
## Result
![image](https://user-images.githubusercontent.com/66547492/110101034-71323d00-7de6-11eb-9899-0d9649863c6a.png)
- 이중 for문을 사용하여 Time Limit Exceeded 발생
- 시간 복잡도는 O(n²)
## <u>Change Code</u>
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) <= 1:
            return 0
        maximum = 0
        minimum = prices[0]
        for i in range(1,len(prices)):
            if prices[i] < minimum:
                minimum = prices[i]
            elif minimum + maximum < prices[i]:
                maximum = prices[i] - minimum
        return maximum

```
## Result
![image](https://user-images.githubusercontent.com/66547492/110101160-94f58300-7de6-11eb-98ea-168043e65760.png)
- 기존의 이중 for문을 사용하던 코드에서 단일 for문만 사용하도록 수정
- for문은 하나이므로 시간복잡도는 O(n)


## Daily Temperatures
## Problem
### Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.
### For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].
### Note: The length of temperatures will be in the range [1, 30000]. Each temperature will be an integer in the range [30, 100].
### <u>Code</u>
```python
class Solution:
    def dailyTemperatures(self, T: List[int]) -> List[int]:
        today = 0
        result = [0 for i in range(len(T))]
        for today in range(len(T)):
            for cnt in range(1, len(T)-today):
                if T[today] < T[today+cnt]:
                    result[today] = cnt
                    break

        return result
```
### Result
![image](https://user-images.githubusercontent.com/66547492/110104855-059e9e80-7deb-11eb-9067-e0349bddbd40.png)
- 이중 for문 사용으로 인해 Time Limit Exceeded 발생
- 시간복잡도는 O(n²)
