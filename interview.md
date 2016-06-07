# 1:

```
var obj = {
  a: 1,
  b: () => console.log(this.a),
  c: function() { console.log(this.a) }
}

obj.b();
obj.c();
```

# 2:
```
function arrayPrint1(array) {
  array.forEach(function(item) {
    window.setTimeout(function() {
      console.log(item);
    }, 0);
  });
}

arrayPrint1([1, 2, 3, 4, 5]);
```

```
function arrayPrint2(array) {
  for(var i = 0; i < array.length; i++) {
    window.setTimeout(function() {
      console.log(array[i]);
    }, 0);
  }
}

arrayPrint2([1, 2, 3, 4, 5]);
```
