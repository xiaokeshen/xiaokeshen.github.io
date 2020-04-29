# First Unique Number

## Problem
[First Unique Number](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/531/week-4/3313/) from leetcode

## Solution 1 (TLE 16/17 cases passed)

~~~python
# time complexity: 
# init: O(n) where n is the initial lenght of nums
# showFirstUnique: O(1)
# add: O(k) where k is the length of the unique numbers


class FirstUnique:

    def __init__(self, nums: List[int]):
        self.cnt = collections.Counter(nums)
        self.unique = [num for num in nums if self.cnt[num]==1]

    def showFirstUnique(self) -> int:
        if self.unique:return self.unique[0]
        return -1
        

    def add(self, value: int) -> None:
        if value in self.cnt:
            if self.cnt[value] == 1:
                backup = []
                while self.unique:
                    val = self.unique.pop()
                    if val == value:
                        while backup:
                            self.unique.append(backup.pop())
                        break
                    backup.append(val)
        else:
            self.unique.append(value)
        self.cnt[value]+=1

~~~

## Solution 2
~~~python
# time complexity: 
# init: O(n) where n is the initial lenght of nums
# showFirstUnique: O(k) where k is the number of ununique number before the first unique number. The best case  will be O(1) and the worst case will be O(n) where n is unique numbers so far. However, the amortized complexity is faster as if one round we have complexity of O(n), we will popleft all those unqualified numbers, for the next round, we will have less number to consider and we have a very high possibility to reach O(1) next time. The amortized complexity will be something between O(1) and O(n)
# add: O(1)

class FirstUnique:

    def __init__(self, nums: List[int]):
        self.cnt = collections.defaultdict(int)
        self.cnt = collections.Counter(nums)
        self.unique = collections.deque([num for num in nums if self.cnt[num]==1])

    def showFirstUnique(self) -> int:
        # put the dict key into a deque. When checking the first unique number, check from the left, if qualify, return. If not popleft, as this number will not be qualify in the future.
        while self.unique:
            if self.cnt[self.unique[0]]==1:
                return self.unique[0]
            else:
                self.unique.popleft()
        return -1


    def add(self, value: int) -> None:
        if value not in self.cnt:self.unique.append(value)
        self.cnt[value]+=1
~~~

Thanks for reading.
