# [从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

```java
class Solution {
    HashMap<Integer, Integer> map = new HashMap<>();
    int[] preorder;

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        return build(0, 0, preorder.length - 1);
    }

    // 根节点前序遍历对应的索引pre_root、中序遍历左边界in_left、中序遍历右边界in_right
    private TreeNode build(int pre_root, int in_left, int in_right) {
        if (in_left > in_right) {
            return null;
        }
        TreeNode root = new TreeNode(preorder[pre_root]);
        //根节点中序遍历对应的索引
        int index = map.get(preorder[pre_root]);
        root.left = build(pre_root + 1, in_left, index - 1);
        //根节点索引 + 左子树长度 + 1
        root.right = build(pre_root + index - in_left + 1, index + 1, in_right);
        return root;
    } 
}
```

