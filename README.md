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



作者： 陈不不

邮箱：2833844911@qq.com

### 欢迎加入星球哦

``星球连接https://t.zsxq.com/06bIUvBEM``
