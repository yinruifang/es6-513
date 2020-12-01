## 1.let const var
const 定义常量 ，不可以重新赋值
var let区别：let 有块级作用域

## 2.解构
将数据或对象中的值在转为单一的变量的形式  ，一般这种写法更简单，可以少写代码
## 3.模板字符串
``  可以换行写、变量的添加方式 ${变量名} ，写法更简洁不需要字符串连接，性能更好
## 4.函数参数默认值
在函数调用时，给参数默认值，保证不报错
```
function animal( name = "狗"){
	var nn = name.trim();
	console.log(nn);	
}
```

## 5.扩展运算符 ...
1.可以将set  、map数据格式转为数组或对象
2.可以进行数组连接
3.和解构一起使用
4.可以替代apply方法
5.可以和 generator一起使用

## 6.箭头函数
作用：保留this的指向，vue的项目中经常出现；（如果 this指向出现问题了，一定记得使用 箭头函数）
## 7.类和类的继承
```
class
class  类名  extends 父类{
	//子类中想要使用 this
	constructor(arg) {
		super();//如果子类里面想要使用this，必须在this使用前面调用 super
		//原因是：子类没有自己的this指向，必须使用 super函数来继承父类的this指向
	    this.type = 'dog';
	}
	
}

```
## 8.set  map
set 作用  去重
map key值可以是多样化的
## 9.es6之后的新特性
1.指数运算 **
2.数组方法 includes 是否存在该元素
3.Object.values 获取到对象中的所有 值  Object.keys 获取到对象中的所有 键
4.padStart  可以使用*补足字符串不足的位数，在字符串前补足   //padEnd     可以使用*补足字符串不足的位数，在字符串后补足
//5.trimStart 前面去空格 trimEnd 后面去空格


## 10.异步回调地狱问题的解决
*****
1. promise 解决了异步回调的地狱问题
```
function getData(){
	return new Promise((resolve,reject)=>{
		//异步操作
		resolve('返回成功');
	})
}
getData().then(function(){
	//成功的回调
},function(){
	//失败的回调
})


new Promise((resolve,reject)=>{
	//返回成功或者失败
}).then(function(){
	//接收的成功的回调
},function(){
	//接收的失败的回调
})


promise怎样解决地狱回调问题：
1.当调用多个数据并返回的结果是需要有序是，就会回调中嵌着回调,所谓的回调地狱.
2.promise 创建了一个promise 对象，将未来返回的正确或者错误的结果，作为他的参数，
就不会出现回调中嵌套回调的情况，只需要写 .then()的链式写法就可以了

.then(function(){
	
}).then(function(){
	
})
...

多个异步操作，需要转同步时，可以使用  promise.all()，缺点：如果有一个失败了，后面的都不执行
解决方法是：promise.allSettled()
//promise 有三种状态 ：成功（resolve） ，失败(reject) ，进行中（pending）
//缺点：
//首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。//其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。//第三，当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

```

2.async  await  异步转同步的写法，一种语法糖
```
async  await 调用的函数一定是返回promise对象的
async function task(){
				console.log('start...');
				await zhunbei();
				await chao();
				await dun();
				await tiaoliao();
				await eat();
				console.log('end!');
			}
```

3.generator 1,迭代器，2，地狱回调 （语法比较难）
generator 使用在 react中的 redux-saga     dva 或者 umi
```
function * he(){
	yield "hello";
	yield "hi";
	yield 45;
	return ;
}

var h = he();
console.log(h.next());//{done:false,value:'hello'}
console.log(h.next());//
console.log(h.next());//
console.log(h.next());//{done:true,value:undefined}  done:true 表示迭代结束了c
```
Promise是基础，Generator和async/await串连多个Promise的同步执行，也就是把Promise的异步特性变为同步，编程更爽。
当然Generator的yield也可以跟非Promise类型的对象，对于Generator更可以理解为迭代器。而async/await则是多个Promise同步执行的简单方法。
			