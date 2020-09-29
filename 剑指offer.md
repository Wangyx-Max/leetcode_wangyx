# 剑指offer

## 链表题

### 03 从尾到头打印链表

输入一个链表，按链表从尾到头的顺序返回一个ArrayList。

#### 编程细节

* 注意给出函数的返回值的参数，递归函数可以直接用给出的函数，记得返回值要写成全局变量。
* vector可以作为c里面的数组用！（动态数组）；.insert函数可以在任意位置插入数据，必要时可以通过这种方式模拟堆栈；使用迭代器时注意迭代器失效的问题；.erase函数可以删除元素，传入迭代器，一个参数表示删除该元素，两个参数表示删除一个区间；可以用C++自带的reverse函数和sort函数对vector进行反转和排序
* stack取数据时，要用.top函数，.pop函数只负责弹出数据，.size函数可以得到栈大小
* 创建变量（特别是指针）的时候问自己三遍，需不需要初始化？需不需要初始化？
* 递归代码要记得！！调用函数自身！！！记得传参的边界检查

#### 实现思路及代码

* 栈实现

```c++
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector <int> ArrayList;
        stack <int> stck;
        ListNode* p=head;
        while(p!=NULL){
            stck.push(p->val);
            p = p->next;
        }
        
        while(!stck.empty()){
            ArrayList.push_back(stck.top());
            stck.pop();
        }
        return ArrayList;
    }
};
```

* 递归实现

```c++
class Solution {
public:
    vector<int> ArrayList;
    vector<int> printListFromTailToHead(ListNode* head) {
        if(head!=NULL){
            if(head->next!=NULL)
                printListFromTailToHead(head->next);
            ArrayList.push_back(head->val);
        }
        return ArrayList;
    }
};
```

*  使用vector容器在头部进行插入

```c++
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> ArrayList;
        while(head!=NULL){
            ArrayList.insert(ArrayList.begin(),head->val);
            head=head->next;
        }
        return ArrayList;
    }
};
```

* 数组反转

```c++
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> ArrayList;
        while(head!=NULL){
            ArrayList.push_back(head->val);
            head=head->next;
        }
        reverse(ArrayList.begin(),ArrayList.end());
        return ArrayList;
    }
};
```

### 14 链表中倒数第k个结点

输入一个链表，输出该链表中倒数第k个结点。

#### 编程细节

* 边界判定
* .at函数获得

#### 实现思想与代码

* 快慢指针

```c++
class Solution {
public:
    ListNode* FindKthToTail(ListNode* p, unsigned int k) {
        ListNode* pre=p;
        while(k--){
            if(p!=NULL) p = p->next;
            else return nullptr;
        };
        while(p!=NULL){
            p=p->next;
            pre=pre->next;
        }
        return pre;
    }
};
```

* vector实现

```c++
class Solution {
public:
    ListNode* FindKthToTail(ListNode* p, unsigned int k) {
       vector<ListNode*> arr;
        ListNode* head=p;
        while(p!=NULL){
            arr.push_back(p);
            p=p->next;
        }
        if(!arr.size() || !k || arr.size()<k) return NULL;
        else return arr.at(arr.size()-k);
        //return arr[arr.size()-k];
        //[]和.at()的区别是[]不会做边界检查，.at()会检查边界并且可能抛出异常
    }
};
```

* 两次遍历链表实现

```c++
class Solution {
public:
    ListNode* FindKthToTail(ListNode* p, unsigned int k) {
        unsigned int len=0;
        ListNode* pp=p;
        while(p){
            p=p->next;
            len++;
        }
        if(k>len) return NULL;
        unsigned int i=len-k;
        while(i){
            pp=pp->next;
            i--;
        }
        return pp;
    }
};
```

###15 反转链表

输入一个链表，反转链表后，输出新链表的表头。

#### 编程细节

- 声明指针的时候，注意要一个变量一个变量的声明
- 数组从后往前遍历的时候，记得下标-1

####实现思想和代码

* 指针实现

```c++
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {
        ListNode* pre=NULL;
        ListNode* cur=pHead;
        ListNode* tmp;
        if(pHead==NULL || pHead->next == NULL) return pHead;
        while(cur!=NULL){
            tmp=cur->next;
            cur->next=pre;
            pre=cur;
            cur=tmp;
        }
        return pre;
    }
};
```

* stack实现

```c++
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {
        stack<ListNode*> stck;
        stck.push(NULL);
        while(pHead){
            stck.push(pHead);
            pHead=pHead->next;
        }
        pHead=stck.top();
        ListNode* tmp=pHead;
        while(tmp){
            stck.pop();
            tmp->next = stck.top();
            tmp=stck.top();
        }
        return pHead;
    }
};
```

* vector实现

```c++
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {
        vector<ListNode*> arr;
        arr.push_back(NULL);
        while(pHead){
            arr.push_back(pHead);
            pHead=pHead->next;
        }
        for(int i = arr.size();i>1;i--){
            arr[i-1]->next = arr[i-2];
        }
        return arr[arr.size()-1];
    }
};
```

### 16 合并两个或k个有序列表

输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

```C++
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2){
        
    }
};
```

* 实现思想及代码

```c++
class Solution {
public:
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2){
        ListNode *p1=pHead1,*p2=pHead2,*pre=NULL,*tmp;
        while(p1!=NULL && p2!=NULL){
            if(p1->val > p2->val){
                pre->next=p2;
                tmp=p2;
                p2=p2->next;
                tmp->next=p1;
                pre=pre->next;
            }else{
                pre=p1;
                p1=p1->next;
            }
        }
        if(p2!=NULL){
            pre->next=p2;
        }
        return pHead1;
    }
};
```

### 25 复杂链表的复制

#### 编程细节

* 三个循环，三个步骤，不要合并循环
* 头指针不要改，养成不要修改传入参数的习惯！！！

#### 实现思想和代码

```c++
class Solution {
public:
    RandomListNode* Clone(RandomListNode* pHead){
        if(pHead==NULL) return pHead;
        RandomListNode* p=pHead;
        while(p){
            RandomListNode* pCopy=new RandomListNode(p->label);
            pCopy->next = p->next;
            p->next = pCopy;
            p = pCopy->next;
        }
        RandomListNode *pr = pHead;
        while(pr){
            if(pr->random)
                pr->next->random = pr->random->next;
            pr = pr->next->next;
        }
        RandomListNode *ptr=pHead,*result=pHead->next,*ptrCopy=ptr->next;
        while(ptr){
            ptr->next = ptrCopy->next;
            if(ptr->next)
                ptrCopy->next = ptr->next->next;
            ptr=ptr->next;
            ptrCopy=ptrCopy->next;
        }
        return result;
    }
};
```

### 36 两个链表的第一个公共节点

#### 编程细节

- 头指针不要改，养成不要修改传入参数的习惯！！！

#### 实现思想和代码

* 计算diff的算法

```c++
class Solution {
public:
    ListNode* FindFirstCommonNode( ListNode* pHead1, ListNode* pHead2) {
        int len1=0,len2=0,diff;
        ListNode *p1=pHead1,*p2=pHead2;
        while(pHead1){
            pHead1=pHead1->next;
            len1++;
        }
        while(pHead2){
            pHead2=pHead2->next;
            len2++;
        }
        diff = len1>len2?len1-len2:len2-len1;
        if(len1>len2){
            while(diff--){
                p1=p1->next;
            }
        }else{
            while(diff--){
                p2=p2->next;
            }
        }
        while(p1!=p2){
            p1=p1->next;
            p2=p2->next;
        }
        return p1;
    }
};
```

* 时间复杂度为O(a+b+n)的算法

```c++
class Solution {
public:
    ListNode* FindFirstCommonNode( ListNode* pHead1, ListNode* pHead2) {
        ListNode *p1=pHead1,*p2=pHead2;
        while(p1!=p2){
            p1 = (p1==NULL ? pHead2 : p1->next);
            p2 = (p2==NULL ? pHead1 : p2->next);
        }
        return p1;
    }
};
```

### 55 链表中环的入口结点

#### 编程细节

- .count函数可以查找某元素是否在vector中
- 快慢指针实现部分，需要注意边界的处理，首先是while循环应该是检查快指针是不是会越界，再用if指令跳出循环，得到快慢指针相遇的节点。

#### 实现思想和代码

* 快慢指针找到相遇点（证明有环），相遇点和链表起点一起往后走

```c++
class Solution {
public:
    ListNode* EntryNodeOfLoop(ListNode* pHead){
        ListNode *fast=pHead,*slow=pHead;
        while(fast&&fast->next){
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow) break;
        };
        if(!fast || !fast->next) return NULL;
        slow = pHead;
        while(fast!=slow){
            fast = fast->next;
            slow = slow->next;
        }
        return slow;
    }
};
```

* 快慢指针计算环的大小（证明有环），前指针先走n步，找重逢点

```c++
class Solution {
public:
    ListNode* EntryNodeOfLoop(ListNode* pHead){
        ListNode *fast=pHead,*slow=pHead;
        while(fast&&fast->next){
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow) break;
        };
        if(!fast || !fast->next) return NULL;
        fast = fast->next;
        int count=1;
        while(fast!=slow){
            fast = fast->next;
            count++;
        }
        fast=pHead,slow=pHead;
        while(count--){
            fast=fast->next;
        }
        while(fast!=slow){
            fast=fast->next;
            slow=slow->next;
        }
        return slow;
    }
};
```

### 056 删除链表中重复的结点

在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。
例如，链表1->2->3->3->4->4->5 处理后为 1->2->5

#### 实现思想与代码

* 非递归方法

```c++
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead){
        ListNode *p = pHead,*pre,*head = new ListNode(0);
        pre = head;
        pre->next = pHead;
        if(p==NULL) return NULL;
        while(p){
            if(p->next!=NULL && p->next->val == p->val){
                while(p->next!=NULL && p->next->val == p->val)
                    p = p->next;
                pre->next = p->next;
                p = p->next;
            }else{
                pre = pre->next;
                p = p->next;
            }
            
        }
        return head->next;
    }
};
```

## 树

### 04 重建二叉树

```c++
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
        if(vin.size() == 0) return NULL;
        TreeNode *root = new TreeNode(pre[0]);
        vector<int> preLeft,preRight,vinLeft,vinRight;
        int i = 0;
        for(;vin[i] != pre[0];i++){
            vinLeft.push_back(vin[i]);
            preLeft.push_back(pre[i+1]);
        }
        i++;
        for(int j = 0;j<vin.size()-i;j++){
            vinRight.push_back(vin[i+j]);
            preRight.push_back(pre[i+j]);
        }
        root->left = reConstructBinaryTree(preLeft,vinLeft);
        root->right = reConstructBinaryTree(preRight,vinRight);
        return root;
    }
};
```

### 17 树的子结构

```c++
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2){
        bool result  = false;
        TreeNode *p1 = pRoot1,*p2 = pRoot2;
        if(p1 == NULL || p2 == NULL) return false;
        if(p1->val == p2->val){
            result = DoseTree2HasTree1(p1,p2);
        }
        if(result == false) result = DoseTree2HasTree1(p1->left,p2);
        if(result == false) result = DoseTree2HasTree1(p1->right,p2);
        return result;
    }
    bool DoseTree2HasTree1(TreeNode* pRoot1, TreeNode* pRoot2){
        if(pRoot1 == NULL && pRoot2 != NULL) return false;
        if(pRoot2 == NULL) return true;
        if(pRoot1->val != pRoot2->val) return false;
        return DoseTree2HasTree1(pRoot1->left,pRoot2->left) && DoseTree2HasTree1(pRoot1->right,pRoot2->right);
    }
};
```

### 18 二叉树的镜像

```c++
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    void Mirror(TreeNode *pRoot) {
        Change(pRoot);
    }
    TreeNode *Change(TreeNode *pRoot){
        if(pRoot == NULL) return NULL;
        TreeNode *tmp;
        tmp = pRoot->left;
        pRoot->left = Change(pRoot->right);
        pRoot->right = Change(tmp);
        return pRoot;
    }
};
```

### 22 从上往下打印二叉树

从上往下打印出二叉树的每个节点，同层节点从左至右打印。

```c++
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    vector<int> PrintFromTopToBottom(TreeNode* root) {
        
    }
};
```

#### 编程细节

* 队列queue的使用：入队，如例：q.push(x); 将x 接到队列的末端。
  ​				  出队，如例：q.pop(); 弹出队列的第一个元素，注意，并不会返回被弹出元素的值。
  ​				  访问队首元素，如例：q.front()，即最早被压入队列的元素。
  ​				  访问队尾元素，如例：q.back()，即最后被压入队列的元素。
  ​				  判断队列空，如例：q.empty()，当队列空时，返回true。

* 指针访问的时候一定要注意判断是否为空

#### 实现思想及代码

```c++
class Solution {
public:
    vector<int> PrintFromTopToBottom(TreeNode* root) {
        vector<int> arr;
        queue<TreeNode*> que;
        TreeNode *p;
        if(root == NULL) return arr;
        que.push(root);
        while(!que.empty()){
            p = que.front();
            arr.push_back(p->val);
            que.pop();
            if(p->left) que.push(p->left);
            if(p->right) que.push(p->right);
        }
        return arr;
    }
};
```

### 

```c++
class Solution {
public:
    bool VerifySquenceOfBST(vector<int> seq) {
        return seq.empty() ? false : bst(seq,0,seq.size()-1);
    }
    bool bst(vector<int> seq,int begin,int end){
        //if(seq.empty() || begin>end) return false;
        int i=begin,root = seq[end];
        while(seq[i]<root) i++;
        int j = i;
        while(seq[j]>root && j<end) j++;
        if(seq[j]<root) return false;
        bool result = true;
        if(begin<i && result) result = bst(seq,begin,i-1); 
        if(i<end && result) result = bst(seq,i,end-1);
        return result;
    }
};
```



