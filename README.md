## 刷题



### 二分搜索

https://leetcode-cn.com/problems/binary-search/



# 暴力
class Solution {
public:
    int search(vector<int>& nums, int target) {
        
        for(int i=0;i<nums.size();i++){
            if(nums[i]==target) return i;
        }
        return -1;
    }
};
                                        
# 暴力优化
                                        
class Solution {
public:
    int search(vector<int>& nums, int target) {        
        for(int i=0;i<nums.size();i++){
            if(nums[i]==target) return i;
            if(nums[i]>target) return -1;
        }
        return -1;
    }
};

                                        
# 二分
  
  class Solution {
public:
    int search(vector<int>& nums, int target) {    
        int left=0;int right=nums.size()-1;    
        int mid;
        while(left<=right){
            mid=left+(right-left)/2;
            if(nums[mid]<target){
                left=mid+1;
            }
            else if(nums[mid]>target){
                right=mid-1;
            }
            else if(nums[mid]==target){
                return mid;
            }
        }
        return -1;
    }
};
  
  ##  要注意mid=起点+长度
    
    
    ###  双指针
    https://leetcode-cn.com/problems/remove-element/submissions/
    
    class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
       int slow=0;
       for(int i=0;i<nums.size();i++){
           if(nums[i]!=val)
           nums[slow++]=nums[i];
       } 
       return slow;
    }
};
                                       
 #slow统计有效数字，i扫一遍
