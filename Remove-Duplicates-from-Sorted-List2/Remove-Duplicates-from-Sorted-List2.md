いつものようにnodeを走査するが、nodeの参照ではなくポインタの繋ぎ変えの方法が分からない
```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node = head
        seen = set()
        while node and node.next:
            if node.val in seen:
                node = node.next
            else:
                seen.add(node.val)
                node = node.next
            
        return node
```
geminiに聞いたところ、ノードの除去は前のノードのnextを次のノードのnextと置き換えれば良いとのこと
```python
prev.next = current.next
```
また、先頭での重複のパターンに対応するために先頭にダミーノードを作ると良いらしい
```python
dummy = ListNode(0, head)
prev = dummy
```
が、これだけだと実装イメージが湧かず。。一旦答えを見て納得し、解き直す。
```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        start_node = ListNode(0, head)  # dummy
        prev_node = start_node
        current_node = head
        while current_node and current_node.next:
            if current_node.val == current_node.next.val:
                while current_node.next and current_node.val == current_node.next.val:
                    current_node = current_node.next
                prev_node.next = current_node.next
            else:
                prev_node = prev_node.next
            current_node = current_node.next
        return start_node.next
```
変数が多くて分かりづらい。が、「自身を含めた重複除去」をするには、消滅しないノード(prev)から操作する必要があるので仕方ないのかな。
