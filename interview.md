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

# 3

```
function funcGenerator(count) {
  var funcs = [];

  for(var i=0; i < count; i++) {
    funcs.push(function() {
        console.log(i)
    });
  }

  return funcs;
}

funcGenerator(5)[3]();
```


# 4
```
class Person {
  constructor(name, age sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
  }

  bindClick() {
    console.log(this.name);
    console.log(this.age);
    console.log(this.sex);
  }
}

in one page

I have want to bind a click to on button
such as
var person = new Person('test', '24', 'male');
<button onclick = person.bindClick>Click Me</button>


Question:
1. If user click that button, what will happen?
2. If there are something wrong, how to fix it?
```

# 5
```
function doSomething() {
  console.log(1);
  return Promise.resolve(1);
}

function doSomethingElse() {
  console.log(2);
  return 2;
}

doSomething().then(function() {
  return doSomethingElse()
}).then(function() {
  console.log(arguments);
});

doSomething().then(function() {
   doSomethingElse()
}).then(function() {
  console.log(arguments);
});

doSomething().then(doSomethingElse()).then(function() {
  console.log(arguments);
});

doSomething().then(doSomethingElse).then(function() {
  console.log(arguments);
});

```
