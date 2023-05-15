typescript
会检查类型变化，可以避免类型错误
检查变量值的类型，可以显示出标记出代码中的意外行为，降低发生错误的可能性
类型注解：
let age:number = 18;
注意  ：number  就是类型注解
作用  为变量添加类型约束

常用基础类型概述：
分为两类：js已有的+ts新增
 js 已有的
原始类型：numbe/ string / boolean/ null / undefined / symbol
对象类型（包括，数组，对象，函数等）
ts新增的
联合类型、自定义类型（类型别名）、接口、元组、字面量类型、枚举、void 、 any 等
数组类型： 
//两种写法
let num: number[] = [1,2,3,5];
let num2: Array<number> =  [1,2,3,5];
//既有number 又有 string 
//有小括号表示既可以是string 又可以是number
//没有小括号表示，arr既可以是string类型，又可以number类型
let arr:(number | string)[] = [1,2,"sdjknf",5]

//解释：  |(竖线)在ts中叫做联合类型

类型别名:
//类型别名
type CoustomArray = (number | string)[];
let arr1:CoustomArray = [1,2,'as'];
let arr2:CoustomArray = [1,2,'sdfs',5,6];

函数类型

//关明生 管理之道，胜利之光，喜悦之光。
let myAdd: (x: number, y: number) => number =
    function(x: number, y: number): number { return x + y; };
    //关明生的诡异的方式会议  128
可选参数  ?:类型   
对象类型
let person:{
    name:string;
    age:number;
    //  sayHi():void   //两种写法
    sayHi()=> void
    greet(name:string,age:number):void}={
        name:"藏三"，
        age:18,
        sayHi(){},
        greet(name,age){
                    
        }
    }
    
接口（interface）
// 使用interface关键字来声明，每一行只有一个属性类型，属性后边没有分号
//优点：可以复用
interface Iperson{
    name:string
    age:number
    sayHi():void
}

let person:Iperson = {
    name:"Z行含"，
    age:18,
    sayHi(){}
}

interface 和 type(类型别名)对比
//相同点：都可以给对象指定类型
//不同：接口，只能为对象指定类型   ，    类型别名，不仅可以给对象指定，实际上可以给任意类型指定别名
interface Iperson{
    name:string 
    age:number 
    sayHi():void
}

type Iperson = {
    name:string 
    age:number 
    sayHi():void
}

type NumStr = number | string
 接口   如果两个接口之间有相同的属性或方法，可以将公共的属性或方法抽离出来，通过继承来实现复用
interface Point2D {x:number; y: number}
interface Point3D extends Point2D {z: number}
//使用关键字 extends（继承）实现了接口point3D继承Point2D


元组（Tuple）   
元组是另一种类型的数组，它确切知道包含多少个元素，以及特定索引对应的类型
let postion: [number,number] = [39.2545 , 45.7256]
类型推论：
在ts中，有些地方并没有明确指出类型，ts的类型推论会帮助提供类型
发生类型推论的常见场景：1声明变量并初始化，2.决定函数返回值时
类型断言
有时候你会比ts更加明确一个值的类型，这个时候需要类型断言
这个类型太宽泛不具体，，无法操作href等a标签特有的属性或方法，这时就用类型断言指定更加具体的类型
const alink = document.getElementById('link') 
这个时候无法去操作a标签的特有属性href ,
const alink = document.getElementById('link') as HTMLAnchorElement
使用as关键字实现类型断言
关键字as后跟一个具体的类型（HTMLAnchorElement 是 HTMLElement的子类型），这样就可以访问到a标签的属性和方法了

字面量类型：
let str1 = "hollo wor"   //  string 类型
const str2 = "hollo wor"    // hollo wor  类型

const str3:hollo wor = "hollo wor"
let str4:15 = "hollo 15   

使用模式： 字面量类型配合联合类型一起使用
使用场景： 用来表示一组明确的可选值列表
比如：在贪吃蛇游戏中，游戏方向上下左右中的任意一个
function changeDirection(direction:'up' | 'down' | 'left' | 'right') {
    console.log(direction)
}
changeDirection("up")

解释： direction 只能是up/down/left/right 中的任意一个
优势：相比于string类型，使用字面量更加精确，严谨
枚举
定义一组命名常量，他描述一个值，该值可以是这些命名常量中的一个
枚举类型都是有值的，如果没值，默认初始值为0递增，也可以自己设置，数字，字符串..
枚举不仅用作类型，还提供值
enum Direction {
    Up,
    Down,
    Left,
    Right
}
function changeDirection(direction:Direction){
    console.log(direction)
}
changeDirection(Direction.Up)

成员设置初始值
enum Direction {
    Up=2,
    Down=16,
    Left=8,
    Right=24
}

any 
不推荐使用，     其他隐式具有any类型的情况： 1.声明变量不提供类型也没有初始值 ，   2. 函数参数不加类型

typeof
ts也提供了typeof操作符，可以再类型上下文中引用变量或属性的类型（类型查询）,无法查询其他形式的类型（如函数调用的类型）
let p = {x: 1, y:2}
function formatpoint(point:{x:number,y:number}){}
formatpoint(p)

function  formatpoint(point:typeof p){}


高级类型
重点学习
class 类
类型兼容性
交叉类型
泛型和 keyof
索引签名类型和 索引查询类型
映射类型

class 
基本使用
class Person{
    age: number,
    name:"zhansan"
}
const p: Person
const p = new Person()
ts中，不仅提供了class语法的功能，也作为一种类型存在


class Person{
    age:number
    gender:string
    constructor(age:number,gender:string){
        this.age = age
        this.gender = gender
    }
}
const p = new Person(18,"男")


实例方法
clss POint{
    x:1
    y=2
    scale(n:number):void{
            this.x *= n
            this.y *= n
    }
}
const p = new Point()
p.scale(10)  //放大十倍

类的继承
类继承的两种方式：1.extends(继承父类)  2. implements(实现接口)
//第一种
class Animal{
    move(){
        console.log("父类")    
    }
}
class Dog extends Animal{
    back(){
        console.log("子类")    
    }
}
const d = new Dog()
d.move()


//实现接口
interface Singale{
    sing():void
}
class Person implement Singale{
    sing(){
        console.log("接口唱诵")    
    }
}
类成员可见性
可以使用ts来控制class的方法或属性对于class外的代码是否可见
可见性修饰符包括：1.public(公有的) 2.protected(受保护的) 3.private(私有的) 4 . readonly（只读，只修饰属性，不修饰方法，readonly修饰的属性需带着类型，不然设置的值会变为字面量属性）
class Animal{
    public move(){
        console.log("父类")    
    }
}
class Dog extends Animal{
    back(){
        console.log("子类")    
    }
}

类型兼容性
类和接口之间也存在兼容性
类型多的可以赋值给少的（包含于白被包含的关系）
函数之间兼容性比较复杂，需要考虑参数个数，参数类型，返回值类型，
参数个数（）参数多的兼容参数少的（参数少的可以赋值给多的）
参数类型   相同位置的参数类型要相同（原始类型）或兼容（对象类型）

交叉类型
功能类似于接口继承（extends）,用于组合多个类型为一个类型（常用于对象类型）
interface Person {name:string}
interface Contack {phone:string}
type PersonDetail = Person & Contack
let obj: PersonDetail = {
    name: 'jack',
    phone: '1234569'
}

泛型
泛型可以在保证类型安全的情况下，让函数等多种类型一起工作，从而实现复用，常用于：函数，接口，class中
需求：创建一个id函数，传入什么数据就返回该数据本身（也就是说，参数和返回值类型相同）
function id<Type>>(vlaue:Type):Type{ return value}

泛型约束
默认情况下，泛型函数的类型变量Type可以代表多个类型，这导致无法访问任何属性，比如id('a') 调用这个函数时获取参数的长度，就需要为泛型添加泛型约束,收缩类型
function id<Type[]>>(value:Type[]):Type[]{ 
    value.length
    return value
}


interface Ilenth {
    lenth: number
}

function id<Type extends Ilength>>(vlaue:Type[]):Type[]{
    value.length
    return value
}
id('sdnfsf')


泛型工具类型：（内置的，简化ts中的常见操作，都是基于泛型来实现）--------partial<Type>----readonly<Type>-------pick<Type,Keys>----Record<Keys,Type>----
partial<Type>: 用来构建（创造）一个类型，将Type的所有属性设置为可选
interface Props {
    id:string
    children:number[]
}
type PartialProps = Partial<Props>

Readonly<Type>用来构造一个类型，将Type的所有类型设置Readonly只读
interface Props {
    id: string
    children:[]
}
type ReadonlyProps = Readonly<Props>

let props: ReadonlyProps = {id:'1', children:[]}
props.id = '2'   //报错，readonly属性里边的都是只读属性，不能重新赋值

Pick<Type,Keys>: 从Type中选择一组属性来构造新类型
interface Props {
    id：string
    title:string
    children:number[]
}
type PickProps = Pick<Props,'id' | 'title'>
Record<Keys,Type>: 构建一个对象类型，属性建为Keys，属性类型为Type
type RecordeObj = Record<'a' | 'b' | 'c' | 'd' , string[]>

let obj:RecordObj = {
    a: ['1'],
    b: ['2'],
    c: ['3'],
    d: ['4']
}

索引签名类型
使用场景： 当无妨确定对象中有那些属性（或者说对象中可以出现任意多个属性），此时，就用到索引签名类型了
//对象中建的名就是string类型
interface AnyObject {                                       //   let obj: AnyObject = {
    [key: string] : number                                  //       a: 1,         
}                                                           //       b: 2,                 
                                                            //    }
在js中，数组是一类特殊的对象，特殊在数组的键（索引）是数值类型
interface MyArray<T> {
    [n: number]: T
}
let arr = MyArray<number> = [1,3,5,7]
映射类型
基于旧的类型创建新的类型（对象类型），减少重复，提升开发效率
type PropKeys = 'x' | 'y' | 'z'
type Type1 = { x: number; y: number; z: number}
//这样写没问题，但xyz重复，类型也相同
type PropKeys = 'x' | 'y' | 'z'
type Type1 = {[Key in PropKeys] : number}


类型声明文件
ts中有两种文件类型：1.    .ts文件   2.     .d.ts文件
.ts文件：既包含类型信息又可以执行代码，可以被编译成.js文件，然后执行代码，用途：编写程序代码的地方
.d.ts文件： 只包含类型信息的类型声明文件，不会生成.js文件，仅用于提供类型信息，用途： 为js提供类型信息
总结：.ts是implementation(代码实现文件)；.d.ts是declaration(类型声明文件)。

类型声明文件的使用说明： 1.库自带的类型声明文件，2.由DefinitelyTyped文件名





