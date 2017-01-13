Q: 
写一个程序求字符串每个字符出现的次数，例如字符串`'abcaacbbba'`, 其结果为`{a: 4, b: 4, c: 2}`.

A: 
```
    var s = 'abcaacbbba';
    s.split('').reduce((prev, curr) => {
        if (prev[curr] === undefined) {
             prev[curr] = 1;
        } else {
            prev[curr] ++;
        }
          
        return prev;
      }, {});
```

Q:
写一个程序 去除一个数组的重复元素例如 将数组`['a', 'b', 'c', 'b', 'a', 'c', 'a']`变为`['a', 'b', 'c']`.

A:
最通用的解法.复杂度为你n(o2)
```
function unique(arr) {
    let contain = false;
    let rt = [];

    for(let i = 0; i<arr.length; i++) {
        contain = false;

        for(let j = 0; j< rt.length; j ++) {
            if(rt[j] === arr[i]) {
                contain = true;
                break;
            }
        }

        if (!contain) {
            rt.push(arr[i]);
        }
    }

    return rt;
}
``` 
改进后的解法：
```
function unique(arr) {
    let temp = arr.reduce(function(prev, curr) {
        prev[curr] = undefined;
        return prev;
    }, {});

    return Object.keys(temp);
}
```

Q: 有一个链表如下：

```
let linkedArray = {
    value: 1,
    next: {
        value: 2,
        next: {
            value: 3,
            next: null
        }
    }
}
```
写一个程序将这个链表反转？

A:
```
function reverse(linkedArray) {
   let cursor = linkedArray;

   cursor.prev = null;
   while(cursor.next) {
       cursor.next.prev = cursor;
       cursor = cursor.next;
   }

   return cursor;
}
```

## 排序算法相关
`swap` 函数：
```
function swap(arr, i, j) {
    var temp = null;
    temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

Q: 冒泡排序算法.
思路： 将数组中的相邻的2个元素进行比较，如果满足对比条件，则交换位置，第一次循环次数为数组的长度，第二次则比第一次少一，以此类推，循环完毕则排序完毕
```
function bubbleSort(arr) {
    for(var i = 0; i < arr.length; i++) {
        for(var j = 0; j < arr.length - i; j++) {
            if (arr[j] > arr[j+1]) {
                swap(arr, j, j+1);
            }
        }
    }

    return arr;
}
```

Q： 快速排序算法
思路： 在数组中找到一个平衡点，使这个平衡点的左边的元素都小于该元素，而右边的元素则都大于该元素，然后从这个平衡点的位置切分成2个数组再进行该过程，直到退出，则排序完成

```
function quickSort(arr) {
    qSort(arr, 0, arr.length - 1);
    return arr;
}

function qSort(arr, low, high) {
 var pivot; 
 if(low < high) {
     pivot = partition(arr, low, high);  
     qSort(arr, low, pivot);
     qSort(arr, pivot+1, high);
 } 
}

function partition(arr, low, high) {
    //假设取low为基准值
    var pivotValue = arr[low];
    while(low<high) {
        //从最右端扫描数组，如果发现右边有一个值比这个基准值小，则交换它与基准值的位置这个时候基准值的位置将变为high
        while(low < high && arr[high] >= pivotValue) {
            high--;
        }
        swap(arr, low, high);
        //交换之后，基准值在数组里面的位置变为high，这个时候在比较这个基准值左边的元素，如果发现左边有元素比它大，则交换位置
        while(low < high && arr[low] <= pivotValue) {
            low++;
        }
        swap(arr, low, high);
    }
    return low;
}
```

Q: 二分查找算法

```
function binarySearch(arr, target) {
    var data;
    var position;
    var bottom=0,top=arr.length-1;  
    while(bottom<=top){  
        position=(bottom+top)>>1;   
        if(data===target)  
            return position;  
        if(data<target)bottom=position+1;  
        else top=position-1;  
    }  

    return -1;
}
```

Q: 简单的Promise的实现

```
function Promise(fn) {
    this.successList = [];
    this.failList = [];
    this.state = 'pending';
    fn(this.resolve, this.reject);
}

Promise.prototype = {
    constructor: Promise,
    resolve: function(value) {
        this.state = 'fulfilled';
        var list = this.successList;
        this.resolveVlue = value;
        var fn = null;
        while(list.length) {
            fn = list.shift();
            if (fn) {
                fn.call(this, this.resolveVlue);
            }
        }
    },
    reject: function(reason) {
        this.state = 'rejected';
        var list =  this.failList;
        this.reason = reason;
        var fn = null;
        while(list.length) {
            fn = list.shift();
            if (fn) {
                fn.call(this, this.reason);
            }
        }
    },
    then: function(successFn, failFn) {
        if(successFn) {
            if(this.state === 'pending') {
                this.successList.push(successFn);
            } else if (this.state === 'fulfilled') {
                successFn.call(this, this.resolveVlue);
            }
        }

        if (failFn) {
            if(this.state === 'pending') {
                this.failList.push(failFn);
            } else if (this.state === 'fulfilled') {
                failFn.call(this, this.reason);
            }
        }
    }
}
```

Q: 从一个字符串里面找出最大的没有重复字符的字符子串，例如:`abcdeafd`, 得到结果 `["abcde", "bcdeaf", "cdeaf", "deaf", "eafd"]` 这个题目当时是没有解出来，经过提示，面试下来之后
依照这个提示做出来的这个算法，虽然当时没有答出来，也算是给自己增加经验吧。

```
 function searchMaxLength(str) {
        var arr = str.split('');
        var startCursor = 0;
        var endCursor = startCursor;
        var strs = [];
        var str = '';
        while(true) {
          if(endCursor < arr.length) {
            if(str.indexOf(arr[endCursor]) === -1) {
                str = str.concat(arr[endCursor]);
                endCursor++;
            } else {
                strs.push(str);
                //reset the string
                str = '';
                startCursor++;
                endCursor =  startCursor;
            }
          } else {
            strs.push(str);
            break;
          }
        }

        return strs;
    }

    var s = 'abcdeafd';
    var ss = searchMaxLength(s);
    console.log(ss);
```