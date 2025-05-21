# Step 1
まずは愚直に実行

```python

class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                if nums[i]+nums[j]==target:
                    return [i,j]
                    break
```
実行時間は2271ms



# Step 2
PRや公式解答を参照．
解答を見るとhashmapという手法を発見．dictを用いることで高速に探索出来るらしい．
keyの操作に慣れていないので，デバッグしつつ実装
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hashmap = {}
        for i in range(len(nums)):
            hashmap[nums[i]] = i
        print(nums) # [2, 7, 11, 15]
        print(hashmap) # {15: 3, 2: 0, 11: 2, 7: 1}
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap and hashmap[complement] != i: # dict[key]=value
                return [i, hashmap[complement]]
        return []
```
実行時間は158ms．計算量を減らすことが出来た．

# Step 3
何も見ないで実装
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hashmap = {}
        for i in range(len(nums)):
            hashmap[nums[i]] = i
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap and hashmap[complement]!=i:
                return [i, hashmap[complement]]
        return []
```
実行時間は5ms同じコードなのに実行時間が違う．他に見るべき指標があるかも．

# Step 4
いただいたアドバイスを元に実装
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_to_index = {}
        for i in range (len(nums)):
            complement = target - nums[i]
            if complement in num_to_index and num_to_index[complement]!=i:
                return [i, num_to_index[complement]]
            num_to_index[nums[i]] = i
        return []
```
辞書の名前をnum_to_indexに変更して意味を分かりやすくした．
for文を1つにまとめた．

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_to_index = {}
        for i, num in enumerate(nums):
            complement = target - num
            if complement in num_to_index and num_to_index[complement]!=i:
                return [num_to_index[complement], i]
            num_to_index[num] = i
        return []
```
enumerateでも書いてみた．個人的にはこちらのほうが好みかも．
