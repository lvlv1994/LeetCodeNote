# maxSumWithK

这个算法还是挺有名的，就是首先sumArray记录了以index为结尾的最长的sum，然后求一个k的和每次更新这个和，在和当前最大值与之前求到的这个sumArray的最大值的和相加求最值，这个sumArray就很强

```text
def maxSumWithK(a, k):    sumArray = [0 for i in range(len(a))]    sumArray[0] = a[0]    currMax = a[0]    for i in range(1,len(a)):        currMax = max(a[i],currMax+a[i])        sumArray[i] = currMax    sum_k = 0    for i in range(k):        sum_k += a[i]    result = sum_k    for i in range(k,len(a)):        sum_k = sum_k + a[i] - a[i-k]        result = max(result,sum_k)        result = max(result,sum_k+sumArray[i-k])    return resultprint(maxSumWithK([1,2,3,-1,3],2))
```

