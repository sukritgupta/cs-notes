# Merge Sort

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;
void merge(int i, int j, int k, int l , vector<int>& nums){
  vector<int> sorted;
  sorted.reserve(l-i+1); 
  int startIndex = i;
  while(i<=j && k<=l){
    if(nums[i]<nums[k]){
      sorted.push_back(nums[i]);
      i++;
    }else{
      sorted.push_back(nums[k]);
      k++;
    }
  }
  while(i<=j){
    sorted.push_back(nums[i]);
      i++;
  }
  while(k <= l){
    sorted.push_back(nums[k]);
      k++;
  }
  copy(sorted.begin(), sorted.end(), nums.begin()+startIndex);
}


void mergeSort(vector<int>& nums, int i, int j){
  if(i>=j){
    return;
  }
  int mid = i + (j-i)/2; //prevents overflow
  mergeSort(nums, i, mid);
  mergeSort(nums, mid+1, j);
  merge(i, mid, mid+1, j , nums);
}

int main(){
  vector<int> nums= {9,8,7,6,5,4,3,1};
  int i=0, j=nums.size()-1;
  mergeSort(nums, i, j);
 
  for(auto num:nums){cout<<num<<endl;}
  
}
