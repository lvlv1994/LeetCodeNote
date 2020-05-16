---
description: 'https://www.jianshu.com/p/b6ad653fb2e1'
---

# Binary Search

链接里的这个模版很好用，注意左右边界的检查，如果用的是mid = left + \(right - left \) // 2，就要先判断left, 反之，如果是mid = left + \(right - left + 1 \) // 2，就先判断right

```text
def binary_search(inputs,key):
    left,right = 0,len(inputs)-1
    while left <= right:
        mid = (left+right)/2
        if inputs[mid] >= key:
            right = mid -1
        else:
            left = mid + 1
    return left
print(binary_search([1,2,3,4,5],3))
```

```text
   public int binarySearch(List<Integer> list, int key){
           int lo= 0;
           int hi= list.size()-1;
           while(lo<=hi){
               int mid= lo+(hi- lo)/2;
               if(list.get(mid)>=key){
                   hi= mid-1;
               }else{
                   lo= mid+1;
               }
           }
           return lo;
       }
```

