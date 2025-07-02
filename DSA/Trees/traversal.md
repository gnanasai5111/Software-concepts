## Binary Tree Traversal - Recursive (Java)

This note includes implementations of all three **depth-first traversals**:

*  Inorder (Left → Root → Right)
*  Preorder (Root → Left → Right)
*  Postorder (Left → Right → Root)


## TreeNode Class

```
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode() {}
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
```

## Inorder Traversal (Recursive)

**Order**: Left → Root → Right

```
class Solution {
    public void inorderRecursiveTraversal(TreeNode root, List<Integer> res) {
        if (root == null) return;
        inorderRecursiveTraversal(root.left, res);
        res.add(root.val);
        inorderRecursiveTraversal(root.right, res);
    }

    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inorderRecursiveTraversal(root, res);
        return res;
    }
}
```

## Preorder Traversal (Recursive)

**Order**: Root → Left → Right

```
class Solution {
    public void preorderRecursiveTraversal(TreeNode root, List<Integer> res) {
        if (root == null) return;
        res.add(root.val);
        preorderRecursiveTraversal(root.left, res);
        preorderRecursiveTraversal(root.right, res);
    }

    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        preorderRecursiveTraversal(root, res);
        return res;
    }
}
```

## Postorder Traversal (Recursive)

**Order**: Left → Right → Root

```
class Solution {
    public void postorderRecursiveTraversal(TreeNode root, List<Integer> res) {
        if (root == null) return;
        postorderRecursiveTraversal(root.left, res);
        postorderRecursiveTraversal(root.right, res);
        res.add(root.val);
    }

    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        postorderRecursiveTraversal(root, res);
        return res;
    }
}
```
