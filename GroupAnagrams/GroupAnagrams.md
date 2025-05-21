# Step1
何も見ずに解く
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        anagrams = []
        str_dict = {}
        for str in strs:
            str_dict[str] = sorted(str)
        print(str_dict)
```
出力
```
{'eat': ['a', 'e', 't'], 'tea': ['a', 'e', 't'], 'tan': ['a', 'n', 't'], 'ate': ['a', 'e', 't'], 'nat': ['a', 'n', 't'], 'bat': ['a', 'b', 't']}
```
辞書のバリューから逆引きしたかったが，文法がわからず断念．
ChatGPTに聞いた結果，str_dict.items()でキーとバリューが取得できる．
listはハッシュに使えないので，予め文字列に変換したほうが良さそう．
また，defaultdictという方法が有効だと感じたのでそれを使うことにする．


# Step2
調べた結果を受けてときなおし
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        anagrams = defaultdict(list)
        for str in strs:
            str_sorted = ''.join(sorted(str))
            anagrams[str_sorted].append(str)
        return list(anagrams.values())
```
defaultdictという文法を使うことで簡潔にかけたが，初期の方針でも書けるようにしたほうが良い気がする．
