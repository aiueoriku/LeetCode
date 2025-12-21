# step1
Linked List Cycle1と同様、current_nodeを走査する方針で行う。
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current_node = head
        visited = set()

        while current_node:
            print(f"current_node: {current_node}")
            if current_node in visited:
                return current_node
            elif current_node.val == -1:
                return null
            else:
                current_node = current_node.next
```
無限ループに陥る。

geminiにヒントを求めたところ、visitedにcurrent_nodeをaddし忘れていると指摘された。
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current_node = head
        visited = set()

        while current_node:
            if current_node in visited:
                return current_node
            elif current_node.val == -1:
                return null
            else:
                visited.add(current_node)
                current_node = current_node.next
```
が、headに-1が含まれる場合に誤った答えになってしまう。

ここで、elifの条件分岐はcurrent_node.valではなくcurrent_node自体が-1かどうかを確認する必要があることに気づく。さらに、noneではなくNoneに変更
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current_node = head
        visited = set()

        while current_node:
            if current_node in visited:
                return current_node
            elif current_node == -1:
                return None
            else:
                visited.add(current_node)
                current_node = current_node.next
```

パスできた

