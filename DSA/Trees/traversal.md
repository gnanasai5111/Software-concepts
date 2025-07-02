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

## Inorder Traversal (Iterative)

- The code performs an iterative inorder traversal of a binary tree using a stack.
- It starts by initializing an empty list (res) to store the result and a stack (s) to keep track of the tree nodes.
- The traversal begins with the curr pointer at the root.
- The first inner while loop moves as far left as possible, pushing each node onto the stack. This simulates the recursive call stack in a typical inorder traversal.
- When it reaches a null left child, it pops the last node from the stack (which has no unvisited left children).
- The popped node's value is added to the result list (this is the "node" part of left → node → right).
- The traversal then moves to the right subtree by setting curr = pop.right.
- This process repeats until both the stack is empty and curr is null.
- The result list res ends up containing the node values in inorder sequence (left → root → right).
  
```
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();
    TreeNode current = root;

    while (current != null || !stack.isEmpty()) {
        while (current != null) {
            stack.push(current);
            current = current.left;
        }

        TreeNode node = stack.pop();
        result.add(node.val);
        current = node.right;
    }

    return result;
}
```

## Preorder Traversal (Iterative)

- The code performs an iterative preorder traversal of a binary tree using a stack.
- An empty list res is initialized to store the final traversal result.
- A stack is used to mimic the call stack of recursive traversal.
- If the root is null, the function immediately returns the empty result list.
- The root node is pushed onto the stack to start the traversal.
- The loop runs while the stack is not empty.
- In each iteration, a node is popped from the stack.
- The node’s value is added to the result list.
- The right child is pushed onto the stack if it exists.
- The left child is then pushed onto the stack if it exists.
- Pushing right before left ensures the left child is processed first due to the LIFO nature of the stack.
- This results in visiting nodes in the correct preorder sequence: root → left → right.
- Once the stack is empty, all nodes have been visited and the result list is returned.
  
```
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res=new ArrayList<>();
        Stack<TreeNode> stack=new Stack<>();
        if(root==null){
            return res;
        }
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node=stack.pop();
            res.add(node.val);
            if(node.right!=null){
                stack.push(node.right);
            }
            if(node.left!=null){
                stack.push(node.left);
            }
        }
        return res;
    }
}
```
