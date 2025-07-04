## Binary Tree Paths

- Given the root of a binary tree, return all root-to-leaf paths in any order.
- A leaf is a node with no children.

```
Example 1:

Input: root = [1,2,3,null,5]
Output: ["1->2->5","1->3"]

Example 2:

Input: root = [1]
Output: ["1"]
```
**Constraints** :
- The number of nodes in the tree is in the range [1, 100].
- -100 <= Node.val <= 100

## Recursion (string Builder):

- Uses depth-first search (DFS) to find all root-to-leaf paths in a binary tree
- Reuses a single StringBuilder to efficiently build path strings without creating new ones
- Appends the current node’s value to the StringBuilder during traversal
- Checks if a node is a leaf (both left and right children are null) and adds the built path to the result list
- Adds "->" only when the node has children to continue the path
- Saves the current length of the StringBuilder before exploring children to allow clean backtracking
- After visiting both children, resets the StringBuilder to the previous length using setLength()
- Ensures that each path in the result list is correctly formed without extra arrows or partial values

```
class Solution {
    public void findAllTreePaths(TreeNode root, List<String> res,StringBuilder sb){
        if(root==null){
            return;
        }
        int len = sb.length();
        sb.append(root.val);
        if(root.left==null && root.right==null){
            res.add(sb.toString());
        }
        else{
            sb.append("->");
            findAllTreePaths(root.left,res,sb);
            findAllTreePaths(root.right,res,sb);
        }
        sb.setLength(len);
        
    }
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res=new ArrayList<>();
        findAllTreePaths(root,res,new StringBuilder());
        return res;
    }
}
```

**Time Complexity** - o(N)
**Space Complexity** - O(H)


## Recursion (string):

- Uses depth-first search (DFS) to explore all root-to-leaf paths in the binary tree
- Builds the path as a string by appending the current node’s value using string concatenation
- Appends "->" only if the current node has children (i.e., not a leaf)
- When a leaf node is reached, the complete path string is added to the result list
- Passes the curr string by value (since strings are immutable in Java), so no manual backtracking is required
- No use of StringBuilder, extra classes, or data structures — clean and readable logic
- Simpler to understand and implement, suitable for beginner to intermediate level
- Slightly less memory efficient than StringBuilder approach due to creation of new string objects at each recursion


```
class Solution {
    public void findAllTreePaths(TreeNode root, List<String> res,String curr){
        if(root==null){
            return;
        }
        curr=curr+root.val;
        if(root.left==null && root.right==null){
            res.add(curr);
        }
        else{
            curr=curr+"->";
            findAllTreePaths(root.left,res,curr);
            findAllTreePaths(root.right,res,curr);
        }    
    }
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res=new ArrayList<>();
        findAllTreePaths(root,res,"");
        return res;
    }
}
```

**Time Complexity** - o(N)
**Space Complexity** - O(H)

## Iterative (two stacks)

- Uses iterative DFS with two stacks: one for TreeNode and one for path strings
- Starts by pushing the root node and its value as a string into the respective stacks
- For each node popped from the stack, the current path string is also popped
- If the current node is a leaf node (both left and right children are null), the path is added to the result list
- If the node has a right child, it is pushed onto the stack with the updated path (path + "->" + right.val)
- If the node has a left child, it is pushed similarly with the updated path
- The order of pushing right first ensures that the left subtree is processed before the right, maintaining pre-order traversal
- No need for backtracking or custom data structures like Pair or StringBuilder
- String concatenation is used to build paths; acceptable here due to limited depth in most binary trees
- Handles edge cases like empty tree (root == null) safely at the beginning

```
class Solution {
  
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res=new ArrayList<>();
       if (root == null) return res;
        Stack<TreeNode> stack = new Stack<>();
        Stack<String> paths = new Stack<>();
        stack.push(root);
        paths.push(String.valueOf(root.val));
        while(!stack.isEmpty()){
            TreeNode node=stack.pop();
            String path = paths.pop();
            if(node.left==null && node.right==null){
                res.add(path);
            }
            if (node.right != null) {
                stack.push(node.right);
                paths.push(path + "->" + node.right.val);
            }

            if (node.left != null) {
                stack.push(node.left);
                paths.push(path + "->" + node.left.val);
            }
        }
        return res;
    }
}
```

**Time Complexity** - o(N)
**Space Complexity** - O(H)


## Iterative (one stacks)

- Implements iterative DFS using a custom Pair class to store each node and its associated path string
- The Pair class holds two fields: TreeNode node and String path
- The path is built incrementally by appending "->" and the child node’s value during traversal
- A Stack<Pair> is used to simulate recursion, ensuring controlled depth and iterative logic
- The initial pair (root, root.val) is pushed onto the stack
- For each popped pair, if the node is a leaf, the full path is added to the result list
- Right child is pushed first to ensure left subtree is processed first (pre-order behavior)
- Custom Pair class allows bundling TreeNode and String together cleanly without using additional data structures
- Handles edge case where root is null at the very beginning
- Avoids recursion, making it suitable for very deep binary trees where stack overflow is a concern

```
class Pair{
    TreeNode node;
    String path;
    public Pair(TreeNode node,String path){
        this.node=node;
        this.path=path;
    }

}
class Solution { 
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res=new ArrayList<>();
       if (root == null) return res;
        Stack<Pair> stack = new Stack<>();
        stack.push(new Pair(root,String.valueOf(root.val)));
        while(!stack.isEmpty()){
            Pair p=stack.pop();
            TreeNode node=p.node;
            String path = p.path;;
            if(node.left==null && node.right==null){
                res.add(path);
            }
            if (node.right != null) {
                stack.push(new Pair(node.right,path + "->" + node.right.val));
            }

            if (node.left != null) {
                stack.push(new Pair(node.left,path + "->" + node.left.val));
            }
        }
        return res;
    }
}
```

**Time Complexity** - o(N)
**Space Complexity** - O(H)
