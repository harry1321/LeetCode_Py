# **138. Copy List with Random Pointer**

https://leetcode.com/problems/copy-list-with-random-pointer/description/

# Description

A linked list of length `n` is given such that each node **contains an additional random pointer**, which could point to any node in the list, or `null`.

Construct a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly `n` **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.

For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x` and `y` in the copied list, `x.random --> y`.

Return *the head of the copied linked list*.

## Example

![](https://assets.leetcode.com/uploads/2019/12/18/e1.png)

# Note

**UMPIRE Method:**

> **Understand**
> 
> - Ask clarifying questions and use examples to understand what the interviewer wants out of this problem.
> - Choose a “happy path” test input, different than the one provided, and a few edge case inputs.
> - Verify that you and the interviewer are aligned on the expected inputs and outputs.

現在有一個linked list，其中的node包含一個random指標，可能會指向list中的任意一個node或者是None。現在要執行一個deep copy，建立一個新的linked list，其中所有的節點不會指向原有的list中的節點。兩個list需要完全獨立。

- (edge case)input的linked list中node數一定大於0嗎?
    - 不一定，有可能沒有任何node
- 節點的值有可能相同嗎?
    - 有可能
- node.random是一個指標還是linked list中的順序指標，像是list中的index?
    - It is a pointer.

> **Match**
> 
> - See if this problem matches a problem category (e.g. Strings/Arrays) and strategies or patterns within the category

因為要執行deep copy，在複製node.next和node.random需要記憶新的節點的記憶體位置。這樣的過程需要儲存、存取、查找，所以hash map是一個相當實用的資料結構。

> **Plan**
> 
> - Sketch visualizations and write pseudocode.
> - Walk through a high level implementation with an existing diagram.

因為next和random是指標，又需要做deep copy，所以應該先建立出新的linked list所有的node，然後再次歷遍，找出正確指向的新node。

應該改用hash map，不但加快查詢效率，也能利用非數值的key去查找random node。

![Copy List with Random Pointer.png](/pics/Copy_List_with_Random_Pointer.png)

1. 考慮到edge case，如果linked list為空，則直接回傳空值。
2. 建立一個新的linked list，先複製node的數值。並利用hash map儲存這些節點，其中key是舊的指標，value是新的node。
3. 再次歷遍舊的linked list，這次利用舊的pointer作為key查詢hash map中新節點的記憶體位子。將新的記憶體位子指派給新的節點。
4. 回傳hash map初始節點的記憶體位子

> **Implement**
> 
> - Implement the solution (make sure to know what level of detail the interviewer wants).
- See Solution below.

> **Review**
> 
> - Re-check that your algorithm solves the problem by running through important examples.
> - Go through it as if you are debugging it, assuming there is a bug.

> **Evaluate**
> 
> - Finish by giving space and run-time complexity.
> - Discuss any pros and cons of the solution.
- 時間複雜度：`O(n)`
- 空間複雜度：`O(n)`
    - 使用hash map紀錄n個節點

# Solution

```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head:
            return None
        
        tmp = head
        # store node index
        new_nodes = collections.defaultdict(lambda: Node(0))

        tmp = head
        while tmp:
            new_nodes[tmp].val = tmp.val
            new_nodes[tmp].next = new_nodes[tmp.next] if tmp.next else None
            new_nodes[tmp].random = new_nodes[tmp.random] if tmp.random else None
            tmp = tmp.next
        
        return new_nodes[head]
```