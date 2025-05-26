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

# Step4
コメントを受けて再度解き直す
```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        char_to_count = defaultdict(int)
        char_to_index = {}
        for index, char in enumerate(s):
            char_to_count[char] += 1
            if char not in char_to_index:
                char_to_index[char] = index
        
        min_index = len(s)
        for char, count in char_to_count.items():
            if count == 1:
                if char_to_index[char] < min_index:
                    min_index = char_to_index[char]
        return min_index if min_index != len(s) else -1
```
char_to_indexに各文字の最初のインデックスを保持して，文字列全体に対するfor文の回数を1回で済むように改変した．
