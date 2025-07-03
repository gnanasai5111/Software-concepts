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

## Postorder Traversal (Iterative)  

- Uses a stack to simulate the recursive postorder traversal (left, right, root).
- Maintains a pointer current to traverse nodes and a temp variable to handle right subtree logic.
- Starts with the root node and goes as far left as possible, pushing nodes onto the stack.
- Once current is null, it checks the right child of the node at the top of the stack.
- If the right child is null, it means both left and right are processed, so the node is popped and added to result.
- After popping, it checks if the node just popped was the right child of the new top. If yes, it means the right subtree was also completed, so it continues popping and adding to the result.
- If the right child exists and is not yet processed, it sets current to that right child to process it next.
- This ensures nodes are only added to the result after both left and right children are handled.

```
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode current = root;
        while (current != null || !stack.isEmpty()) {
            while (current != null) {
                stack.push(current);
                current = current.left;
            }
            TreeNode temp=stack.peek().right;
            if(temp==null){
                temp=stack.pop();
                result.add(temp.val);
                while(!stack.isEmpty() && stack.peek().right==temp){
                    temp=stack.pop();
                    result.add(temp.val);
                }
            }
            else{
                current=temp;
            }
        }
        return result;
    }
}
```

**Time Complexity** - o(N)
**Space Complexity** - o(H)

## Levelorder Traversal (Iterative)  

- This algorithm performs a level-by-level traversal of a binary tree using a queue.
- A result list res is used to store values level by level in the form of nested lists.
- A queue (q) is initialized and the root node is added to start the traversal.
- The loop runs as long as the queue is not empty.
- At each level, the number of nodes currently in the queue is stored in size.
- A temporary list inner is created to hold node values for the current level.
- A for-loop runs size times to process all nodes at the current level.
- Each node is dequeued using poll() and its value is added to inner.
- If the dequeued node has a left child, it is enqueued.
- If it has a right child, it is also enqueued.
- After processing one level, inner is added to the result list res.
- The process repeats for all levels until the queue is empty.
- Finally, the result list res is returned, containing values grouped by levels.

```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res=new ArrayList<>();
        Queue<TreeNode> q=new LinkedList<>();
        if(root==null){
            return res;
        }
        q.add(root);
        while(!q.isEmpty()){
            int size=q.size();
            ArrayList<Integer> inner=new ArrayList<>();
            for(int i=0;i<size;i++){
                TreeNode node=q.poll();
                inner.add(node.val);
                if(node.left!=null){
                    q.add(node.left);
                }
                if(node.right!=null){
                    q.add(node.right);
                }
            }
            if(inner.size()>0){
                res.add(inner);
            }
        }
        return res;
        
    }
}
```

## Levelorder Traversal (Recursive)  

- This approach performs level order traversal using recursion instead of a queue.
- It tracks the current level of the tree during the recursion.
- If the current level does not exist in the result list, it adds a new list for that level.
- It adds the node's value to the list corresponding to the current level.
- It recursively calls the left and right child with level incremented by 1.
- The result list will contain one list per level, with node values in level order.
- The recursion ensures left-to-right order is preserved at each level.
- Efficient for balanced trees, but may risk stack overflow for very deep trees.

```
class Solution {
    public void recursiveLevelOrderTraversal(TreeNode root,List<List<Integer>> res,int level){
        if(root==null){
            return;
        }
        if(level==res.size()){
            res.add(new ArrayList<>());
        }
        res.get(level).add(root.val);
        recursiveLevelOrderTraversal(root.left,res,level+1);
        recursiveLevelOrderTraversal(root.right,res,level+1);

    }
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res=new ArrayList<>();
        recursiveLevelOrderTraversal(root,res,0);
        return res;
        
    }
}
```

**Time Complexity** - o(N)
**Space Complexity** - o(N)
