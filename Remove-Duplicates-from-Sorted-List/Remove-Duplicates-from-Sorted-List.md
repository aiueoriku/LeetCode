# Step1
current_nodeを走査する方針は思いついたが、
次の要素を除去するロジックの書き方がわからない。
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current_node = head
        while current_node is not None:
            if current_node.value == current_node.next.value:
                # 次の要素を除去
        return head
```

geminiにヒントを貰う。


次の要素の除去 = nodeの参照先を次の次にする。とのこと
```python
 current_node.next = current_node.next.next
```

修正するもまだエラーが出る
```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current_node = head
        while current_node is not None:
            if current_node.val == current_node.next.val:
                # 次の次のノードを参照
                current_node.next = current_node.next.next
            else:
                current_node = current_node.next
        return head
```

```
AttributeError: 'NoneType' object has no attribute 'val'
                           ^^^^^^^^^^^^^^^^^^^^^
    if current_node.val == current_node.next.val:
Line 10 in deleteDuplicates (Solution.py)
          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    ret = Solution().deleteDuplicates(param_1)
Line 43 in _driver (Solution.py)
    _driver()
Line 58 in <module> (Solution.py)
```

current_nodeがNoneTypeになっているようだ。

geminiに再度確認したところ、current_node.nextがnot Noneであることもwhile loopの条件に加える必要とのこと。

```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current_node = head
        while current_node is not None and current_node.next is not None:
            if current_node.val == current_node.next.val:
                # 次の次のノードを参照
                current_node.next = current_node.next.next
            else:
                current_node = current_node.next
        return head
```
パスできた。

