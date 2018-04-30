### 从前序与中序遍历序列构造二叉树<h1>
### 描述<h2>
> 根据一棵树的前序遍历与中序遍历构造二叉树。  
> 注意:
你可以假设树中没有重复的元素。

例如，给出
```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```
返回如下的二叉树：
```
    3
   / \
  9  20
    /  \
   15   7
```
### 分析<h4>
- 从前序遍历可以得出根节点
- 用前序遍历来构造，用中序遍历来比较：通过中序遍历
  - 如果当前节值在根节点值左边
    - 如果当前根节点左边为空，把左节点造出来
    - 若不为空，进入左节点
  - 如果当前值造根节点右边
    - 如果当前节点右边为空，把右节点造出来
    - 若不为空，进入右节点
### 代码 ( 468ms )<h5>
```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
static auto x = [](){
    std::ios::sync_with_stdio(false);
    std::cin.tie(NULL);
    return 0;
}();
class Solution {
public:
	TreeNode * buildTree(vector<int>& preorder, vector<int>& inorder) {
		/*vector<int>::iterator current_root_it;
		vector<int>::iterator val_it;*/
		map<int, int> inorder_map;
		for (int i = 0; i < inorder.size(); i++)
			inorder_map[inorder[i]] = i;
		int current_root_it;
		int val_it;
		if (preorder.size() == NULL)return NULL;
		TreeNode* res = new TreeNode(preorder[0]);
		for (int i = 1; i<preorder.size(); i++)
		{
			TreeNode* root = res;
			while (true)
			{
				int current_val = preorder[i];
				int current_root_val = root->val;
				current_root_it = inorder_map.find(current_root_val)->second;
				val_it = inorder_map.find(current_val)->second;
				if (val_it<current_root_it)
				{//当前值在根节点左边
					if (root->left != NULL)
					{//如果左边有值，进入左子树
						root = root->left;
					}
					else
					{//如果左边为空，添加左节点
						root->left = new TreeNode(current_val);
						break;
					}
				}
				else
				{//当前值在根节点右边
					if (root->right != NULL)
					{//如果右边有值，进入右子树
						root = root->right;
					}
					else
					{//如果右边为空，添加右节点
						root->right = new TreeNode(current_val);
						break;
					}
				}
			}
		}
		return res;
	}
};
```    
### 网上16ms的代码<h6>
```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    typedef std::vector<int>::iterator ITER;
   TreeNode* helper(std::vector<int>& preorder,ITER preleft,ITER preright,std::vector<int>& inorder,ITER inleft,ITER inright){
	if (preright >= preleft && inright >= inleft){
		TreeNode* root = new TreeNode(*preleft);
		auto it = std::find(inleft,inright,*preleft);
		int diff = it - inleft;
		root->left = helper(preorder,preleft+1,preleft+diff,inorder,inleft,it-1);
		root->right = helper(preorder,preleft+diff+1,preright,inorder,it+1,inright);
		return root;
	}
	return nullptr;
}
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
      TreeNode* root = nullptr;
	if (preorder.empty() || inorder.empty()) return nullptr;
	root = helper(preorder,preorder.begin(),preorder.end()-1,inorder,inorder.begin(),inorder.end()-1);
	return root;
    }
};
```
