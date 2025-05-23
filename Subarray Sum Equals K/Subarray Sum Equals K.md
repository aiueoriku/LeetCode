# Step1
何も見ないで解く
```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        num_subarrays = 0
        for steps in range(len(nums)):
            for i in range(len(nums)-steps):
                print(f"nums[i:i+steps+1]:{nums[i:i+steps+1]}")
                if sum(nums[i:i+steps+1]) == k:
                    num_subarrays += 1
        return num_subarrays
```
まずは総当たりでSubarrayを求めることを試みた．テストケースは突破したが，Submitの際，Output Limit Exceededとなってしまう．

# Step2
他の人の解答を見る．
https://github.com/rinost081/LeetCode/pull/15/

- 累積和がキーワードぽい．今の総和-累積和をすることで1回のfor文で事足りる．
- 累積和を保持するためにHashmapを使うのが良さそう

# Step3
他の人の解答を参考に解き直し
```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        subarray_count = 0
        current_sum = 0
        prefix_sum = defaultdict(int)
        prefix_sum[0] = 1
        for num in nums:
            current_sum += num
            complement = current_sum - k
            if complement in prefix_sum:
                subarray_count += prefix_sum[complement]
            prefix_sum[current_sum] += 1
        return subarray_count
```
prefix_sum[0]=1を書かないと，例えばnums=[1,2,3], k=1で最初の要素がヒットするときに対応出来ないというポイントがある．(prefix_sum[complement]=0となってしまう)
