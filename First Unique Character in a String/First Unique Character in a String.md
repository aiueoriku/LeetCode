# Step1
何も見ずに解く
```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        for i, char in enumerate(s):
            if char not in s[i+1:] and char not in s[:i]:
                return i
        return -1

```
for文で虱潰しに調べた．もっと良いアルゴリズムが有りそう．

# Step2
他の人の解答を参照
https://github.com/rinost081/LeetCode/pull/14
https://github.com/Satorien/LeetCode/pull/15/

- Counterメソッドを使うと文字の出現回数を辞書のように保持できて便利
- Counterメソッドを持ちいらずに辞書を自分で定義して出現回数を保持するということも出来る

# Step3
他の人の解答を参考に解き直す
```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        char_to_count = Counter(s)
        for i, char in enumerate(s):
            if char_to_count[char] == 1:
                return i
        return -1
```
```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        char_to_count = defaultdict(int)
        for char in s:
            char_to_count[char] += 1
        for i, char in enumerate(s):
            if char_to_count[char]==1:
                return i
        return -1
```
Counterを使うほうが簡潔だし，処理速度も早い．
