### nodeV8 的使用 （去除了node的vm所有检测点,且可调试） 

版本18.2.0

```javascript
// 导入关键包
const cbb = require("cbb");

// 启动并执行v8, 并把node中的console导入了
var d = cbb.cbbnative.startv8("cyData.console.log(!new function(){eval(\"this.a=1\")}().a)",{console:console})

console.log(d)
```

vm2 检测点

``console.log(!new function(){eval("this.a=1")}().a)``

vm检测点

``console.log(this.constructor.constructor('return process.env')())``

``"a = {}; a['b'] = ()=>{}; this.__proto__ = a; console.log(this.hasOwnProperty('b'))"``


上面检测点都可过


## 新加功能

1.强行执行异步
```javascript
const cbb = require("cbb")

setTimeout(()=>{
    console.log(1)
},0)

// 强制执行一轮循环
cbb.cbbnative.cbbasyncone()
console.log(2)
// 输出
// 1
// 2

```

2.把普通函数变native函数

```javascript
const cbb = require("cbb")
a ={}
b = function (){
    console.log("is b");
}
//                      需要保存在什么对象  需要native化的函数   别名   是否删除多余属性   length的长度    是否为不可枚举
cbb.cbbnative.setNative(a,               b,                'isb', false,           0,            1);

console.log(a.isb.toString())
// 输出 function isb() { [native code] }

```

3.document.all解决
```javascript
const cbb = require("cbb")
a = {};
cbb.cbbnative.undfObject(a);
document_all = new a.ldObj();
console.log(typeof document_all);
// 输出 undefined
```

4.强制删除
```javascript
const cbb = require("cbb")
d = {"a":function (){}}
cbb.cbbnative.delete(d,"a");
console.log(d.a);
// 输出 undefined

```



作者： 陈不不

邮箱：2833844911@qq.com

### 欢迎加入星球哦

``星球连接https://t.zsxq.com/06bIUvBEM``
