<!--
author:yuansir
date:2023/8/12 晚上11点
 -->
## typeScript学习笔记
# 一、ts引入相关知识
1. TypeScript是什么？
以javascript为基础构建的语言，是一个javascript的超集，可以在任何支持javascript的平台执行，并扩展了javascript（添加了类型），ts不能直接被js解析器直接执行。
2. typescript增加了什么？
类型、支持es的新特性，强大的开发工具，添加es不具备的新特性，丰富的配置选项。
3. ts环境搭建
下载并安装node.js，全局安装typescript（npm i -g typescript）,创建ts文件，使用tsc对文件进行编译执行。
# 二、基本类型
1. 特点：
通过类型声明可以指定变量的类型；
自动类型判断（即变量的声明和赋值是同时进行的）；
函数的参数，及返回值都要添加类型；
声明变量如果不指定类型，ts解析器会自动判断变量为any类型；
unknown类型的变量不能直接赋值给其他变量，要做个if判断；
2. 类型
number,string,boolean,any,void,object,array,never；
字面量，unknown,tuple,enum
3. object 和{}区别,函数声明方式
```javaScript

// {} 可以在属性名后边加上？ 表示是可选的
let a:{name:string,age?:number,obj?:object}
a= {
  name:'sdad',
  age:21,
  obj:{
    dada:12
  }
}
//利用[propName:string]:any 表示任意属性
let c:{ name:string,[propName:string]:any}
c={
  name:'2132',
  age:12,
  phone:'213213'
}
//设置函数结构的类型声明

let fn:(a:number,b:number)=>number;
fn=function(a1:number,a2:number):number{
  return 10;
}
```
4. 数组、元组、枚举

```javaScript
 // 数组
 let num:number[];
 num=[1,2,3,4]
 let str:string[];
 str=['1','2','3'];
 let arr:Array<number>;
 arr=[23,2];
 //元组（固定长度的数组）
 let h:[string,number,string];
 h=['saed',2,'32']
//枚举
enum Gender{
    male=0,
    female=1
}
let i:{name:string,gender:Gender};
i={
    name:'121',
    gender:0
}
//类型别名
```
5. 编译选项
tsconfig.json文件
include,exclude,compilerOptions,
```javaScript
// tsc 文件名.ts -W
```
6. 类
抽象类，抽象方法，继承，super,构造函数和this
```javaScript
//直接定义的属性是实例属性，需要通过对象的实例去访问
//使用static开头的属性是静态属性（类属性），可以直接通过类来访问。

```
7. 接口
接口是可以重复声明的，而type不能重复声明一个对象；
接口中所有属性都不能有实际的值，只定义对象结构，接口中所有方法都是抽象方法。
```javaScript

//定义一个对象的类型
type myType={
    name:string,
    [prototype:string]:string
}
const obj:myType={
    name:'123',
    age:23
}
//接口
interface myType{
    name:string,
    sayHello():void;
}
//通过类实现接口(使类满足接口的要求)
class Myclass implements myType{
  name:string;
  constructor(name:string){
    this.name=name;
  }
  sayhello(){
    console.log('sad');
  }
}
```
8. 属性的封装
原因：属性是在对象中设置的，属性的值可以被任意的修改，这会导致对象中的数据变得非常不安全。
解决方法：ts中支持
public 默认值，可以在任意地方被访问
private: 私有属性，只能在类内部被访问，可以通过在类中添加方法使得私有属性被外部访问 如setter,getter方法（属性的存取器）
protected:受保护的属性，只能在当前类和当前类的子类中使用

```javaScript
class B{
  private _name:string;
  constructor(name:string){
    this._name=name;
  }
  get name(){
    return this._name;
  }
  set name(name:string){
    this._name=name;
  }
}
class A extends B{

}

```
9. 泛型
在定义函数或者类时，如果遇到类型不明确的就可以使用泛型。
```javaScript
function fn<T>(A:T):T{
  return a;
}

let result=fn(a:10);
let result1=fn<String>(a:'sanguo');

interface Inter{
  length:number;
}
class fn2<T extends Inter>(a:T):number{
  return a.length;
}

class myclass<T>{
  name:T;
  constructor(name:T){
    this.name=name;
  }
}
const mc=new myclass<string>(name:'孙悟空');
```
