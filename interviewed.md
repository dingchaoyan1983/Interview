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
      
