Q: 
写一个程序求字符串`'abcaacbbba'`字符出现的次数，其结果为`{a: 4, b: 4, c: 2}`.

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
一开始我的解法.复杂度为o2
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
在经过提示后的解法：
```
function unique(arr) {
    let temp = arr.reduce(function(prev, curr) {
        prev[curr] = undefined;
        return prev;
    }, {});

    return Object.keys(temp);
}
```
