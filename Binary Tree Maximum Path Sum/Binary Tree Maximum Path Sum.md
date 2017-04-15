
https://leetcode.com/problems/binary-tree-maximum-path-sum/#/description

```
Given a binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

For example:
Given the below binary tree,

       1
      / \
     2   3
Return 6.
```


```
public class TreeNode {
    public var val: Int
    public var left: TreeNode?
    public var right: TreeNode?
    public init(_ val: Int) {
        self.val = val
        self.left = self.right
    }
}

class Solution {
    func maxPathSum(_ root: TreeNode?) -> Int {
        return _maxPathSum(root).1
    }
    
    private func _maxPathSum(_ root: TreeNode?) -> (Int, Int) {
        if let root = root {
            let left = _maxPathSum(root.left)
            let right = _maxPathSum(root.right)
            
            return (max(max(0, left.0), max(0, right.0)) + root.val, max(max(max(0, left.0) + max(0, right.0) + root.val, left.1), right.1))
        }
        return (Int.min, Int.min)
    }
}
```
