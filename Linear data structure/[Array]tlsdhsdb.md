



# 배열 



## best-time-to-buy-and-sell-stock



https://leetcode.com/problems/best-time-to-buy-and-sell-stock/submissions/



``` python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0 
        min_price = 10**4
        
        for p in prices :
            min_price = min(min_price,p)
            profit = max(profit,p - min_price)
            
        return profit 
```

![image-20210306000200398](https://user-images.githubusercontent.com/42714724/110945885-980de780-8381-11eb-8773-80e1cd5e3492.png)




### 시간복잡도

`O(n)`



# Daily Temperatures



```python
class Solution:
    def dailyTemperatures(self, T: List[int]) -> List[int]:
        answer = [0 for i in range(len(T))]
        index = []
        
        for i,temp in enumerate(T):
            while index and temp > T[index[-1]]:
                last = index.pop()
                answer[last] = i - last
            index.append(i);
            
        return answer
```

![image](https://user-images.githubusercontent.com/42714724/110946014-becc1e00-8381-11eb-824d-1f4b56545831.png)


인덱스를 이용하는게 포인트다. 넣어줄때에도 가진 인덱스값을 이용하여 해당 위치에 넣어주는 것이 중요하다.



