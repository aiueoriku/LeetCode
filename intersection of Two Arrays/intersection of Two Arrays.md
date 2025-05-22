# Step1
自力で解く
```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        intersection_nums =[]
        for num1 in nums1:
            if num1 not in intersection_nums and num1 in nums2:
                intersection_nums.append(num1)
        return intersection_nums
```
ひとまずfor文で回した．辞書を使えばもっと計算効率上がるかも

# Step2
調べてみる．setという組み込み関数があるらしい
https://qiita.com/KueharX/items/a8cc7831fc430e9340ca
setはuniqueな値を辞書型で返すので，list()で括る
```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        intersected_nums = list(set(nums1) & set(nums2))
        return intersected_nums
```
