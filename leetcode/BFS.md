# BFS框架总结
## 关键词：在图中找到起点start到终点target的最近距离。
BFS基本可以用的场景有，路径最近距离，替换单词的最少次数等等。  
关键知识点：要用到队列。  
框架：  
- 如果没有root，返回0，-1，false等特殊条件；
- 把原始root加入到队列中；
- 只要队列不为空，开始下列循环；
- （测量下q的长度，用于接下来的for循环）；
- 弹出队列的头部元素node；
- 判断是否到达终点，返回对应的要求。
- 将node的child加入队列‘
- （判断node的child是否已经走过，一般来说在二叉树中不需要这一步）。
- 增加步数

#### LC111.二叉树最小深度
这道题是一道很经典的可以用BFS的题目，最小深度的话，就相当于顶点到节点的最小距离。这里判断终点为节点没有左右子树。一旦存在子树就加入到队列。  
时间复杂度：O(n)  
空间复杂度：O(n)  
```python
def minDepth(root):
    from collections import deque
    if not root: return 0
    q = deque([root,1])
    while q:
        node, depth = q.popleft()
        if not node.left and node.right:
            return depth
        if node.left:
            q.append([root.left. depth+1])
        if node.right:
            q.append([root.right, depth+1])
    return 0
```
#### LC429.N叉树的层次遍历
已经提出来层次遍历了，所以这道题是非常典型的用BFS的题目。完全可以套用BFS的框架来进行默写。  
因为要层次遍历，所以在q循环中用一个level来存储每层的节点，其中循环size是为了把这层的节点存起来，并且把所有节点的子节点放到q中。for循环结束后，将level加到res中，最后q为空之后输入res。
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        from collections import deque
        res = []
        q = deque([root])
        while q:
            level = []
            size = len(q)
            for _ in range(size):
                node = q.popleft()
                if not node: continue
                level.append(node.val)
                for child in node.children:
                    q.append(child)
            if level:
                res.append(level)
        return res
```