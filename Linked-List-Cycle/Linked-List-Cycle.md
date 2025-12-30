# Linked Listの定義を先に勉強する
https://qiita.com/tsudaryo1715/items/12c4848028716ab015bb
## Linked List(連結リスト)
- データ＋ポインタ（次のデータへの参照）
- 配列のような大きなメモリの確保が不要(必要な要素分だけでOK)
- 要素の追加、除去に強い。ポインタのアドレスを変更するだけ。o(1)

### Singly Linked List(単方向リンクリスト)
- 次のリストを指すポインターが片方のみ
- 要素へのアクセスが苦手。先頭から愚直にみる必要。o(n)
### Doubly Linked List(双方向リンクリスト)
- ポインタが前後にある
- 検索や移動がより柔軟(後ろからも辿れる)
- 前後のポインタのせいで単方向リンクリストよりメモリを食う

### 配列
- メモリアドレス1,2,3,4...と連続している
- 要素へのアクセスが高速（上記のメモリアドレスを指定するだけ）
- 要素の追加、除去は苦手。要素をずらす作業が伴う。平均o(n)

# Step1
posってなんだ？headってなんだ？
headがpythonのリストと同じ形をしているのが混乱を招いていそう。
geminiと格闘。下記の理解で腹落ち。
```text
headはLinkedList
head = [3,2,0,-4]などと整数の値が見えているが、これらはデータ。裏で各データに対応するアドレスが存在する

head.valで2,0,-4などデータを取り出せる
head.nextは次のアドレスを指定するポインタ
head.next.valで次のアドレスの値を取り出せる
```
回答を見て、実装
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        
        visited = set()

        current_address = head

        while current_address is not None:

            # すでにアクセスしたアドレスの場合ループなのでTrueを返す
            if current_address in visited:
                return True

            visited.add(current_address)
            current_address = current_address.next
        
        # NoneになればCycleを抜けたことになるのでFalseを返す
        return False
```

# Step2
変数名を修正
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        visited = set()
        current_node = head
        while current_node is not None:
            if current_node in visited:
                return True
            
            visited.add(current_node)
            current_node = current_node.next
            
        return False
```
