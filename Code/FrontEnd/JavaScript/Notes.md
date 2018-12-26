# Notes

### async

#### microtask
- Promise 的回调函数不是正常的异步任务，而是微任务（microtask）。它们的区别在于，正常任务追加到下一轮事件循环，微任务追加到本轮事件循环。这意味着，微任务的执行时间一定早于正常任务。
```javascript
setTimeout(function() {
  console.log(1);
}, 0);

new Promise(function (resolve, reject) {
  resolve(2);
}).then(console.log);

console.log(3);
// 3
// 2
// 1
```
#### setTimeout

- setTimeout和setInterval返回的整数值是连续的，也就是说，第二个setTimeout方法返回的整数值，将比第一个的整数值大1。
```javascript
function f() {}
setTimeout(f, 1000) // 10
setTimeout(f, 1000) // 11
setTimeout(f, 1000) // 12
```
上面代码中，连续调用三次setTimeout，返回值都比上一次大了1。

利用这一点，可以写一个函数，取消当前所有的setTimeout定时器。
```javascript
(function() {
  var gid = setInterval(clearAllTimeouts, 0);

  function clearAllTimeouts() {
    var id = setTimeout(function() {}, 0);
    while (id > 0) {
      if (id !== gid) {
        clearTimeout(id);
      }
      id--;
    }
  }
})();
```
上面代码中，先调用setTimeout，得到一个计算器编号，然后把编号比它小的计数器全部取消。

#### debounce

- debounce（防抖动）如果用户连续击键，就会连续触发keydown事件，造成大量的 Ajax 通信。假定两次 Ajax 通信的间隔不得小于2500毫秒。
```javascript
$('textarea').on('keydown', debounce(ajaxAction, 2500));

function debounce(fn, delay){
  var timer = null; // 声明计时器
  return function() {
    var context = this;
    var args = arguments;
    clearTimeout(timer);
    timer = setTimeout(function () {
      fn.apply(context, args);
    }, delay);
  };
}
```

#### setTimeout(f,0)

- setTimeout(f, 0)有几个非常重要的用途。它的一大应用是，可以调整事件的发生顺序。比如，网页开发中，某个事件先发生在子元素，然后冒泡到父元素，即子元素的事件回调函数，会早于父元素的事件回调函数触发。如果，想让父元素的事件回调函数先发生，就要用到setTimeout(f, 0)。

```javascript
// HTML 代码如下
// <input type="button" id="myButton" value="click">

var input = document.getElementById('myButton');

input.onclick = function A() {
  setTimeout(function B() {
    input.value +=' input';
  }, 0)
};

document.body.onclick = function C() {
  input.value += ' body'
};
```

#### with 语句
- with 语句 它的作用是操作同一个对象的多个属性时，提供一些书写的方便。
with (对象) {
  语句;
}
```javascript
// 例一
var obj = {
  p1: 1,
  p2: 2,
};
with (obj) {
  p1 = 4;
  p2 = 5;
}
// 等同于
obj.p1 = 4;
obj.p2 = 5;

// 注意，如果with区块内部有变量的赋值操作，必须是当前对象已经存在的属性，否则会创造一个当前作用域的全局变量。

var obj = {};
with (obj) {
  p1 = 4;
  p2 = 5;
}

obj.p1 // undefined
p1 // 4
```
#### a标签的download

- download 属性
download属性表示当前链接不是用来浏览，而是用来下载的。它的值是一个字符串，表示用户下载得到的文件名。

// HTML 代码如下
// <a id="test" href="foo.jpg">下载</a>
```javascript
var a = document.getElementById('test');
a.download = 'bar.jpg';
```
上面代码中，`<a>`元素是一个图片链接，默认情况下，点击后图片会在当前窗口加载。设置了download属性以后，再点击这个链接，就会下载对话框，询问用户保存位置，而且下载的文件名为bar.jpg

#### bit
- 开关作用
位运算符可以用作设置对象属性的开关。

假定某个对象有四个开关，每个开关都是一个变量。那么，可以设置一个四位的二进制数，它的每个位对应一个开关。
```javascript
var FLAG_A = 1; // 0001
var FLAG_B = 2; // 0010
var FLAG_C = 4; // 0100
var FLAG_D = 8; // 1000
上面代码设置 A、B、C、D 四个开关，每个开关分别占有一个二进制位。

然后，就可以用二进制与运算检验，当前设置是否打开了指定开关。

var flags = 5; // 二进制的0101

if (flags & FLAG_C) {
  // ...
}
// 0101 & 0100 => 0100 => true
```

#### console
- `console.dir`对于输出 DOM 对象非常有用，因为会显示 DOM 对象的所有属性。
- `console.group`分组
- `console.count`计数
- `console.time`和`console.timeEnd`计时

#### BOM

-如果将脚本放在页面底部，就可以完全按照正常的方式写，不需要`DOMContentLoaded`

#### Node
- textContent属性自动忽略当前节点内部的 HTML 标签，返回所有文本内容。

该属性是可读写的，设置该属性的值，会用一个新的文本节点，替换所有原来的子节点。它还有一个好处，就是自动对 HTML 标签转义。这很适合用于用户提供的内容。

`document.getElementById('foo').textContent = '<p>GoodBye!</p>';`
上面代码在插入文本时，会将`<p>`标签解释为文本，而不会当作标签处理。

#### Stdlib

- 如果参数对象有自定义的toJSON方法，那么JSON.stringify会使用这个方法的返回值作为参数，而忽略原对象的其他属性。
```javascript
var user = {
  firstName: '三',
  lastName: '张',

  get fullName(){
    return this.lastName + this.firstName;
  },

  toJSON: function () {
    return {
      name: this.lastName + this.firstName
    };
  }


JSON.stringify(user)
// "{"name":"张三"}"
};
```